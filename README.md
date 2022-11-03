- [Introdução](#Introducao)
- [Hardware e Esquemas Elétricos]()
  - [ESP32]()
  - [ATMega328P](#clone-your-fork)

# Braço Robótico
#### Desenvolvimento de um braço robótico para pegar objetos em ponto A e levar a ponto B

Esse braço robótico, desenvolvido pela segunda turma do curso de Sistemas Embarcados da Fatec de Jundiai, foi apresentado como um desafio à classe, sendo uma continuação do projeto da sala anterior, uma esteira seletora.

O dispositivo em questão foi adquirido no mercado e compõe-se basicamente de uma estrutura em acrílico para a parte mecânica e uma outra eletromecânica relativa aos quatro servomotores (base, altura, avanço e garra). O seu único objetivo é ilustrar, de forma bastante prática, o funcionamento de um equipamento em escala industrial, com nível de complexidade muito próximo no tocante à sua funcionalidade.


imagem | Figura 5 do documento
![Figura 5 do documento](/imgs/20221030_141908.jpg "git")


Para o desenvolvimento do braço, foram necessários dois microcontroladores, o NodeMCU ESP32 e o ATMega328P (microcontrolador do Arduino UNO) utilizando o prototocolo de comunicação I²C entre eles, utilizando a linguagem C++ para os microcontroladores, e HTML, JavaScript e CSS para interface de controle do robô. 

# Hardware e Esquemas Elétricos
Como mencionado anteriormente, o projeto usa quatro servomotores. O modelo utilizado foi o MICRO SERVO TOWERPRO 9G SG90 que possui 3 fios, sendo eles para alimentação (fio vermelho), GND (fio marrom) e para PWM (fio laranja). Pode ser alimentado com tensões entre 3,0 à 7,2V. No nosso projeto, utilizamos uma fonte externa, juntamente ao ATMega328P, que envia os sinais PWM para operar os motores.

#### ATMega328P:

imagem | pinout ATMega328P

O microcontrolador ATMega328P é o microcontrolador presente no Arduino UNO. Porém, no nosso projeto, utilizamos somente o ATMega. Mas, o arduino também pode ser utilizado no lugar dele.

O positivo da fonte deve ser conectado aos cabos vermelho dos servos e o negativo aos cabos marrons dos servos e ao negativo do ATMega328P.

No ATMega328p/Arduino:
- No pino 11(porta digital 6 do arduino): o PWM do servo da garra;
- No pino 15(porta digital 9 do arduino): o PWM do servo da base;
- No pino 16(porta digital 10 do arduino): o PWM do servo da ângulo do braço;
- No pino 17(porta digital 11 do arduino): o PWM do servo da avanço do braço;
- No pino 8 ou 22(qualquer GND do Arduino): jumper com o negativo da fonte externa, e no negativo do ESP32;
- No pino 28(porta analógica A5 do arduino): o SCL do I²C;
- No pino 27(porta analógica A4 do arduino): o SDA do I²C;

#### ESP32:

imagem | pinout esp32

No ESP32, as ligações são feitas da seguinte forma:
- No Pino 22: SCL do I²C;
- No Pino 21: SDA do I²C;
- No GND: conectado ao GND do ATMega328P(pino 8 ou 22).

