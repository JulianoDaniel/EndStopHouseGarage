# Sensor PPA EndStopHouseGarage
Exemplo de uso de sensor de Fim de Curso em portão com Arduino.


A conexão do sensor tipo PPA é bem simples. Ligamos o sensor usando o modelo de Pull-Down de forma semelhante ao botão tátil (Push Button). Quando seguramos um ímã próximo ao sensor, os terminais do mesmo se fecham e a chave deixa passar o sinal para o pino configurado como entrada no Arduino.

O exemplo é acionar um led, mas podemos ativar qualquer dispositivo, acender uma luz, ativar um alarme.

Componentes:

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

Com o esquema montado na Protoboard, grave o Sketch ppa.ino para o Arduino.

Se a intenção for deixar um led ligado apenas passando o ímã pelo sensor,<br> 
podemos trocar o loop pelo código abaixo e declarar a variável "int estadoSensor" alterando<br>
o estado "ligado/desligado" da chave.

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

<br><hr>
<div align="left">
  <img src="https://licensebuttons.net/l/zero/1.0/80x15.png" />
</div>
<br/> 

