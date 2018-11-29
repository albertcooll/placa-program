# placa-program
es per el meu treball del TDR 

#include <Servo.h> 
Servo girar;
int vel = 0;
 
const int LED = 13; // aqui és la alimentació de la placa 
const int BTPWR = 12; //nidea crec que no hi ha res
const int LEDMTR = 8; //led esta al 7
const int BRU = 7; //brunzidor esta al 7

const int tonos[] = {261, 277, 297, 311, 330, 349};
const int countTonos =10;

char nombreBT[10] = "Pastiller";
char velocidad = '4'; //9600
char pin [5] = "1234";
char valor;

void setup() {
  // put your setup code here, to run once:
  girar.attach(9);
  
  pinMode(LED, OUTPUT);
  pinMode(BTPWR, OUTPUT);
  pinMode(LEDMTR,OUTPUT);

  digitalWrite(LED, LOW);
  digitalWrite(BTPWR, HIGH);
  digitalWrite(LEDMTR, LOW); //aqui es el pin on ha d anar conectat el servo

  Serial.begin(9600);

  Serial.print ("AT");
  delay(100);

  Serial.print("AT+NAME PASTILLER");
  Serial.print(nombreBT);
  delay(100);

  Serial.print("AT+BAUD");
  Serial.print(velocidad);
  delay(100);

  Serial.print("AT+PIN");
  Serial.print(pin);
  delay(100);

 digitalWrite(LED,HIGH);


}

void loop(){

  // put your main code here, to run repeatedly:

    valor=Serial.read();
  if (valor=='A'){
  
    for(int i=0; i<2; i++)
    {
    vel = 180;
    girar.write(vel);
    delay(1500);
    
    digitalWrite(LEDMTR,HIGH);
    delay(20000);
    digitalWrite(LEDMTR,LOW);
    }

    for(int iTono = 0; iTono < countTonos; iTono++)
     {
      tone(BRU, tonos[iTono]);
      delay(1000);
     }
      noTone (BRU);
  }
  }
