# Dillinger
## The Last Markdown Editor, Ever

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Dillinger is a cloud-enabled, mobile-ready, offline-storage compatible,
AngularJS-powered HTML5 Markdown editor.

- Type some Markdown on the left
- See HTML in the right
- ✨Magic ✨

## Features

- Import a HTML file and watch it magically convert to Markdown
- Drag and drop images (requires your Dropbox account be linked)
- Import and save files from GitHub, Dropbox, Google Drive and One Drive
- Drag and drop markdown and HTML files into Dillinger
- Export documents as Markdown, HTML and PDF

Markd…
# Braço Robótico
### Desenvolvimento de um braço robótico para pegar objetos em ponto A e levar a ponto B

Esse braço robótico, desenvolvido pela segunda turma do curso de Sistemas Embarcados da Fatec de Jundiai, foi apresentado como um desafio à classe, sendo uma continuação do projeto da sala anterior, uma esteira seletora.

O dispositivo em questão foi adquirido no mercado e compõe-se basicamente de uma estrutura em acrílico para a parte mecânica e uma outra eletromecânica relativa aos quatro servomotores (base, altura, avanço e garra). O seu único objetivo é ilustrar, de forma bastante prática, o funcionamento de um equipamento em escala industrial, com nível de complexidade muito próximo no tocante à sua funcionalidade.


imagem | Figura 5 do documento


Para o desenvolvimento do braço, foram necessários dois microcontroladores, o NodeMCU ESP32 e o ATMega328P (microcontrolador do Arduino UNO) utilizando o prototocolo de comunicação I²C entre eles, utilizando a linguagem C++ para os microcontroladores, e HTML, JavaScript e CSS para interface de controle do robô. 

# Hardware | Esquemas Elétricos
Como mencionado anteriormente, o projeto usa quatro servomotores. O modelo utilizado foi o MICRO SERVO TOWERPRO 9G SG90 que possui 3 fios, sendo eles para alimentação (fio vermelho), GND (fio marrom) e para comunicação serial (fio laranja). Pode ser alimentado com tensões entre 3,0 à 7,2V. No nosso projeto, está sendo utilizada uma fonte externa, juntamente ao ATMega328P, que envia os sinais PWM para operar os motores.

### ESP32:

imagem | pinout esp32

No ESP32, as ligações são feitas da seguinte forma:
- No Pino 22: SCL do I²C;
- No Pino 21: SDA do I²C;
- No GND: conectar ao GND do ATMega328P(pino 8 ou 22).

### ATMega328P:

imagem | pinout ATMega328P

No ATMega328p:
- No Pino 22: SCL do I²C;
- No Pino 21: SDA do I²C;
- No GND: conectar ao GND do ATMega328P(pino 8 ou 22).
