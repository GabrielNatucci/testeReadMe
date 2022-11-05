- [Introdução](#braço-robótico)
- [Hardware e Esquemas Elétricos](#hardware-e-esquemas-elétricos)
  - [ATMega328P](#atmega328P)
  - [ESP32](#esp32)
- [Software](#software)
- [Aplicação Web para configuração do Robô](#aplicação-web-para-configuração-do-robô)
- [Sistema Supervisório](#sistema-supervisório)

# Braço Robótico
#### Desenvolvimento de um braço robótico para pegar objetos em ponto A e levar a ponto B

Esse braço robótico, desenvolvido pela segunda turma do curso de Sistemas Embarcados da Fatec de Jundiai, foi apresentado como um desafio à classe, sendo uma continuação do projeto da sala anterior, uma esteira seletora.

O dispositivo em questão foi adquirido no mercado e compõe-se basicamente de uma estrutura em acrílico para a parte mecânica e uma outra eletromecânica relativa aos quatro servomotores (base, altura, avanço e garra). O seu único objetivo é ilustrar, de forma bastante prática, o funcionamento de um equipamento em escala industrial, com nível de complexidade muito próximo no tocante à sua funcionalidade.

<img src="/imgs/Imagem do braço.png" alt="Braço Robótico" style="height:auto; width:100%;"/>

Para o desenvolvimento do braço, foram necessários dois microcontroladores, o NodeMCU ESP32 e o ATMega328P (microcontrolador do Arduino UNO) utilizando o prototocolo de comunicação I²C entre eles, utilizando a linguagem C++ para os microcontroladores, e HTML, JavaScript e CSS para interface de controle do robô. 

# Hardware e Esquemas Elétricos

Como mencionado anteriormente, o projeto usa quatro servomotores. O modelo utilizado foi o MICRO SERVO TOWERPRO 9G SG90 que possui 3 fios, sendo eles para alimentação (fio vermelho), GND (fio marrom) e para PWM (fio laranja). Pode ser alimentado com tensões entre 3,0 à 7,2V. No nosso projeto, utilizamos uma fonte externa, juntamente ao ATMega328P, que envia os sinais PWM para operar os motores.

#### ATMega328P ou Arduino:

<img src="/Esquemas Elétricos/Pinout ATMega328P.png" alt="PinoutATMega328p" style="height:auto; width:100%;"/>

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

No nosso projeto, o esquema elétrico é o seguinte:
<img src="/Esquemas Elétricos/Placa de controle robô ATMega328p.jpeg" alt="PinoutATMega328p" style="height:auto; width:100%;"/>

#### ESP32:

<img src="/Esquemas Elétricos/ESP32-pinout.jpg" alt="PinoutATMega328p" style="height:auto; width:100%;"/>

No ESP32, as ligações são feitas da seguinte forma:
- No Pino 22: SCL do I²C;
- No Pino 21: SDA do I²C;
- No GND: conectado ao GND do ATMega328P(pino 8 ou 22).

# Software

#### ATMega328P ou Arduino:

Se o código for ser usado em um arduino, não tem segredo. Basta acessar a diretório *"/codigos/Arduino"* e lá se encontrará o arquivo para subir nele. Para ele não é necessário instalar nenhuma biblioteca externa as padrões do Arduino.

Senão, será necessário instalar o *breadboard-avr* atráves do seguinte link:
- [BreadBoard-avr](https://www.arduino.cc/en/uploads/Tutorial/breadboard-1-6-x.zip_gl=1*1w4n6f*_ga*MTIwMzQ0MTc0NC4xNjYzMjU1NTQ3*_ga_NEXN8H46L5*MTY2NzY4NDI0Ni4xNi4wLjE2Njc2ODQyNDYuMC4wLjA.)

#### ESP32:

Para o código funcionar corretamente, são necessárias três bibliotecas que não são instaladas ao configurar o *board manager* do ESP32.

Primeiramente, para instalar o *board manager* do ESP32, siga as intruções do seguinte repositório:
- [esp32-arduino](https://github.com/iotechbugs/esp32-arduino)

Além disso, são necessárias as bibliotecas:
- [AsyncTCP](https://github.com/me-no-dev/AsyncTCP)
- [ESPAsyncWebServer](https://github.com/me-no-dev/ESPAsyncWebServer)
- WebSocketsServer(essa é instalável pelo próprio gerenciador de bibliotecas do Arduino, e pode ser encontrada com o seguinte nome: **WebSockets** by **Markus Sattler**)

Depois disso, para o processo de configuração inicial do ESP32, é necessário um plugin(esp32-fs), que permite que se suba arquivos à memória flash do ESP32, que nesse projeto são necessários para o funcionamento da interface *Web*.
-[esp32-fs](https://github.com/me-no-dev/arduino-esp32fs-plugin)

Depois de tudo isso, deve se apertar o botão *ESP32 Sketch Data Upload*, em "ferramentas". Após isso, para se conectar ao servidor web criado pelo ESP, basta se conectar ao seu WIFI, que podem ter nome e senhas alterados no próprio código(nas linhas 9 e 10). Depois disso, basta escrever *192.168.4.1* no seu navegador de escolha e assim a seguinte página deve se carregar:

<img src="/imgs/Tela de Login.png" alt="Tela de login" style="height:auto; width:100%;"/>

Nesse projeto, apesar de implementarmos a página de login, ela não foi configurada para ser acessada com determinada senha e id. Sendo assim, basta preencher os campos com qualquer coisa que o site deixará vocẽ prosseguir à tela que está no item abaixo.

#### Aplicação Web para configuração do Robô

A fim de se aproximar de uma aplicação real da indústria, além da facilitar a configuração do braço robótico, foi desenvolvido uma aplicação Web, se utilizando das linguagens como HTML, CSS e JavaScript para a criação de um site para configuração dos movimentos que o dispositivo irá realizar para transporte da peça do ponto A ao B. 

Dessa maneira o operador responsável pelo manuseio do braço poderá escolher os ângulos de movimentação da base, avanço, altura e garra do braço, para os respectivos passos que o dispositivo irá fazer em cada posição, tendo a função de escolha do número de passos máximos que serão configurados. Uma vez configurado os movimentos, o braço pode entrar em modo automático. 

Vale ressaltar que para que haja a configuração efetiva entre o operador para o braço, o microcontrolador ESP32 é o responsável pela comunicação entre a aplicação web e os dados que serão passados para o braço robótico, por apresentar wifi integrado, pode criar um *Acess Point* e lidar com com conexões de uma forma relativamente parecida com o que um servidor faria.

<img src="/imgs/Tela de configuração.png" alt="Tela de configuração do braço" style="height:auto; width:100%;"/>

# Sistema Supervisório

Todas as funções que estiverem ocorrendo no momento de configuração ou quando o braço estiver em operação automática, serão posssíveis de viazualizar a partir de um sistema supervisório, que é responsável pelo monitoramento em tempo real. A transmissão de dados ocorre pelo protocolo de comunicação RS232, através da porta serial do ESP32.

<Imagem tela supervisório>