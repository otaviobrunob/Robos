# ICEI / CIÊNCIA DA COMPUTAÇÃO - CAMPUS POÇOS DE CALDAS  
## REGISTRO E MONITORAMENTO DAS PRÁTICAS DE EXTENSÃO

**Disciplina: Seminários III / Turno: Manhã**

**Comunidade atendida:** Centro Municipal de Ensino Especializado Dr. Tarso de Coimbra  
**Data/hora da oficina:** 02/07/2025 - 15:00  
**Grupo:** Otávio Bruno, Luis Bordin, Angelo Henrique.
---

## 🧠 ATIVIDADE PROPOSTA
**Apresentação de braço robótico com Arduino**

---

## 🎯 OBJETIVO DA ATIVIDADE
Estimular o interesse dos alunos pela tecnologia e pela robótica, por meio da demonstração prática de um braço mecânico funcional. A atividade visa despertar a curiosidade e introduzir conceitos básicos de automação e programação de forma lúdica e acessível.

---

## 🛠️ RECURSOS UTILIZADOS
● Arduino UNO
● Servo motores
● Protoboard e jumpers
● Fonte de energia
● Notebook com IDE Arduino
● Projetor
● Papel e lápis para anotações.

---

## 📚 DESENVOLVIMENTO
1. A equipe monta o braço robótico previamente, programado para realizar movimentos simples como pegar e soltar objetos.
2. Durante a oficina, os alunos observam a montagem e o funcionamento do braço em tempo real, com explicações sobre cada componente e suas funções.
3. É promovida uma breve interação onde os alunos podem sugerir movimentos e observar o código responsável por isso.

---

## ✅ RESULTADOS (AVANÇOS E DIFICULDADES)
Resultado ainda a ser realizado.

---

## 📷 FOTOS
| Braço Mecânico         | Foto 2 - Alunos na Apresentação |
|------------------------|-------------------------------|
| ![Imagem 1](fotos/braço.jpg) | ![Imagem 2](fotos/turma.jpg) |

---

## 📎 MATERIAL DESENVOLVIDO
> *● Código-fonte do Arduino utilizado*

#define potGarra        0           // porta A0 Joystick esquerda POT X
#define potBase         1           // porta A1 Joystick esquerda POT Y 
#define potAltura       2           // porta A2 Joystick direita  POT X
#define potProfundidade 3           // porta A3 Joystick direita  POT Y 

int atraso = 20;                    // atraso de 20 milisegundos

int valorGarra ;
int valorBase ;
int valorAltura ;
int valorProfundidade;

int valorGarraFinal ;
int valorBaseFinal ;
int valorAlturaFinal ;
int valorProfundidadeFinal;

#include <Servo.h>                    // Biblioteca Servo 

Servo myservoBase;                    // Objeto servo para controlar a base
Servo myservoGarra;                   // Objeto servo para controlar a garra
Servo myservoAltura;                  // Objeto servo para controlar a altura do braço
Servo myservoProfundidade;            // Objeto servo para profundidade a altura do braço

void setup()
{
  myservoBase.attach(9);              //Associa cada objeto a um pino pwm
  myservoGarra.attach(10);
  myservoAltura.attach(11);
  myservoProfundidade.attach(6);

  Serial.begin(9600);                 // console serial 9600 Bps
  valorBaseFinal = 90;                // valores usados para o controle dos servomotores 
  valorAlturaFinal = 90;
  valorProfundidadeFinal = 90;
}

void leituraJoysticks ()
{
  valorGarra = map(analogRead(potGarra), 10, 1000, 179, 0);                        // leitura do Joystick POT Garra
  Serial.print(" Valor Garra ="); Serial.println(valorGarra);                      // print Valor Garra  

  valorBase = map(analogRead(potBase), 10, 1000, 0, 179);                          // leitura do Joystick POT Base
  Serial.print(" Valor Base ="); Serial.println(valorBaseFinal);                   // print Valor Base

  valorAltura = map(analogRead(potAltura), 10, 1000, 0, 179);                      // leitura do Joystick POT Altura
  Serial.print(" Valor Altura ="); Serial.println(valorAlturaFinal);               // print Valor Altura 

  valorProfundidade = map(analogRead(potProfundidade), 10, 1000, 0, 179);          // leitura do Joystick POT Profundidade
  Serial.print(" Valor Profundidade ="); Serial.println(valorProfundidadeFinal);   // print Valor Profundidade

  Serial.println(); Serial.println();                                              // salta duas linhas 
}

void loop()
{
  leituraJoysticks ();                                                             // leitura dos POTs dos Joysticks 

  myservoGarra.write(valorGarra);                                                  // comando PWM para o servomotor Garra 

  if (valorBase > 95)                                                              // se Valor do POT Base > 95
  {
    valorBaseFinal = valorBaseFinal + 1;                                           // incrementa Valor Base 
    if (valorBaseFinal > 180) valorBaseFinal = 180;                                // limita Valor Base máximo até 180 
    delay (atraso);                                                                // atraso
  }
  if (valorBase < 80)                                                              // se Valor do POT Base < 80 
  {
    valorBaseFinal = valorBaseFinal - 1;                                           // decrementa Valor Base
    if (valorBaseFinal < 0) valorBaseFinal = 0;                                    // limita Valor Base mínimo até 0 
    delay (atraso);                                                                // atraso
  }
  myservoBase.write(valorBaseFinal);                                               // comando PWM para o servomotor Base

  if (valorAltura > 95)                                                            // se Valor do POT Altura > 95
  {
    valorAlturaFinal = valorAlturaFinal + 1;                                       // incrementa Valor Altura
    if (valorAlturaFinal > 160) valorAlturaFinal = 160;                            // limita Valor Base máximo até 160 
    delay (atraso);                                                                // atraso 
  }
  if (valorAltura < 80)                                                            // se Valor do POT Altura < 80 
  {
    valorAlturaFinal = valorAlturaFinal - 1;                                       // decrementa Valor Altura
    if (valorAlturaFinal < 30) valorAlturaFinal = 30;                              // limita Valor Base mínimo até 30 
    delay (atraso);                                                                // atraso
  }
  myservoAltura.write(valorAlturaFinal);                                           // comando PWM para o servomotor Altura

  if (valorProfundidade > 95)                                                      // se Valor do POT Profundidade > 95
  {
    valorProfundidadeFinal = valorProfundidadeFinal + 1;                           // incrementa Valor Profundidade
    if (valorProfundidadeFinal > 150) valorProfundidadeFinal = 150;                // limita Valor Base máximo até 150 
    delay (atraso);                                                                // atraso
  }
  if (valorProfundidade < 80)                                                      // se Valor do POT Profundiade < 80 
  {
    valorProfundidadeFinal = valorProfundidadeFinal - 1;                           // decrementa Valor Profundidade
    if (valorProfundidadeFinal < 30) valorProfundidadeFinal = 30;                  // limita Valor Base Profundidade até 30 
    delay (atraso);                                                                // atraso 
  }
  myservoProfundidade.write(valorProfundidadeFinal);                               // comando PWM para o servomotor Profundidade 

}

