int led1=9;
int led2=11;
int led3=13;

long tempoinicial=0;

// Dado que o usuário deve declarar:

float potencia = 0.15; //potência do aparelho em KWH
float tempoligado = 1500; // tempo do aparelho ligado durante o mês (em milisegundos) - Num dispositivo final o tempo constaria em horas, mas para uma exibição não seria interessante o público esperar por horas para ver o dispositivo funcionar, por isso, ele está rodando com o tempo em milisegundos.
float valorkwh = 0.56;  // valor pago no kWH

// Valor pago:

float valorpago; // valor máximo que o usuário pagará pelo tipo de uso que faz do aparelho


float limitador1=50; //valor limite, em reais, sair da zona ver e ir para a zona amarela
float limitador2=100; //valor limite, em reais, para sair da zona amarela e ir para a zona vermelha


float valor; // valor instantâneo pago pelo usuário

//Condições iniciais do programa
void setup() {

pinMode(led1,OUTPUT); //Declara led1 como porta de saída de sinal
pinMode(led2, OUTPUT);//Declara led2 como porta de saída de sinal
pinMode(led3, OUTPUT);//Declara led3 como porta de saída de sinal
Serial.begin(9600);//inicia o monitor serial para que possa exibir os valores que o usuário pagará.
}

void loop() {
tempoinicial = millis();                              //atribuo o tempo (em milissegundos) que o arduino está ligado na variável tempoinicial

valorpago=potencia*tempoligado*valorkwh;

valor=potencia*tempoinicial*valorkwh;


controle(); //função que ajuda o usuário no controle da conta de energia acionando os sinais luminosos.
 
 Serial.print("Valor limite ="); // imprime no monitor serial o valor limite
    Serial.println(valorpago);
Serial.print("Valor atual  ="); // imprime no monitor serial o valor istatâneo gasto com o aparelho
    Serial.println(valor);    
}

void controle(){
 if (valor<limitador1) {  //verifica se o limitador1 foi atingido, e se não, acende o led1
 digitalWrite(led1,HIGH);
 }
 else {
   
if (valor >= limitador1 && valor< limitador2) { //verifica se o limitador1 foi atingido e se sim, acende o led2
   
   digitalWrite(led1,HIGH);
   delay (500);
   digitalWrite(led2,HIGH);
}
else {if(valor >=limitador2 ){ //verifica se o limitado3 foi atingido e se sim, acende o led3 e o faz piscar
  digitalWrite(led2,HIGH);
   delay (500);
   digitalWrite(led3,HIGH); 
   delay(500);
   digitalWrite(led3,LOW);
   delay(500);
   digitalWrite(led3,HIGH);
   delay(500);
   digitalWrite(led3,LOW);
   delay(500);
   digitalWrite(led3,HIGH);

   }
  }}
}
