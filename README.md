# Sensor PPA EndStopHouseGarage
Exemplo de uso de sensor de Fim de Curso em portão com Arduino.


A conexão do sensor tipo PPA é bem simples. Ligamos o sensor usando o modelo de Pull-Down de forma semelhante ao botão tátil (Push Button). Quando seguramos um ímã pelo sensor, os terminais do mesmo serão fechados e a chave deixa passar o sinal ativando o evento configurado no Arduino. 
O exemplo é acionar um led, mas podemos ativar qualquer dispositivo, acender uma luz, ativar um alarme.

Para isso precisamos dos seguintes componentes:

+ Uma protoboard 
+ Um sensor do tipo PPA 
+ Um Arduino ou Esp
+ Fiospara conexão
+ Um led 
+ Dois resistores de 1k 

Montamos o seguinte esquema na protoboard.
<div align="center">
  <img src="https://user-images.githubusercontent.com/46107950/170777415-3b223caa-990a-4288-b40d-d99cc64c8402.png" />
</div>
<br/> 

Com o esquema montado na Protoboard, passamos o seguinte Sketch para o Arduino:


~~~
/*  
*
* By JDev - https://github.com/JulianoDaniel
* 
*/

#define endR 10 
#define led  13
 
unsigned long timeEndR = 0;

void setup() {
  Serial.begin(9600);

  pinMode(led, OUTPUT);
  digitalWrite(led, LOW);  

  pinMode(endR, INPUT);
  digitalWrite(endR, LOW); 
  
  Serial.println(" Programa iniciado! ");

}

void loop() {
    if((millis() - timeEndR) >= 300){
      if(digitalRead(endR)){ 
        Serial.println(" Chave 1 ligada! "); 
        digitalWrite(led, HIGH);
      }else{
        Serial.println(" Chave 1 desligada! "); 
        digitalWrite(led, LOW);
      }

    timeEndR = millis();  
    }
}

~~~

Se a intenção for, por exemplo, deixar um led ligado apenas passando o ímã pelo sensor, 
como também ocorre em caso de desejar montar um modelo de alarme,
podemos trocar o loop pelo código abaixo, não esqueça de declarar a variável "int estatoSensor".

~~~
if((millis() - timeEndR) >= 1000){
      if(digitalRead(endR)){ 
        estadosensor = !estadoSensor; 
      }
      
      if(estadoSensor){
        Serial.println(" Chave 1 ligada! "); 
        digitalWrite(led, HIGH);
      }else{
        Serial.println(" Chave 1 desligada! "); 
        digitalWrite(led, LOW);
      }

    timeEndR = millis();  
}
~~~
  


