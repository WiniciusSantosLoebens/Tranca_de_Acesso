🔐 Tranca Remota com Registro de Acesso – IoT

Projeto acadêmico desenvolvido para a disciplina de Internet das Coisas (IoT), com o objetivo de implementar um sistema de controle de acesso remoto utilizando ESP32, comunicação MQTT e registro de eventos em tempo real.

📌 Sobre o Projeto

O projeto consiste no desenvolvimento de uma tranca eletrônica controlada remotamente, utilizando um microcontrolador ESP32 conectado à rede Wi-Fi.

A proposta busca oferecer uma alternativa de baixo custo para controle de acesso em ambientes compartilhados, como escritórios e pequenas empresas, reduzindo a dependência de chaves físicas e permitindo o acompanhamento dos registros de acesso.

Inicialmente, o projeto foi idealizado para utilizar cartões ou tags RFID cadastrados como identificadores de acesso. Entretanto, para a apresentação em ambiente de simulação, o sistema foi adaptado para funcionar por meio de comandos remotos enviados pelo protocolo MQTT.

O sistema permite:

Abertura e fechamento remoto da tranca.

Comunicação sem fio por Wi-Fi.

Envio e recebimento de comandos utilizando MQTT.

Identificação da chave responsável pela solicitação.

Registro de data e horário dos acessos.

Indicação visual do estado da tranca por LEDs.

Acionamento de um servomotor para simular a abertura e o fechamento da porta.

🏗️ Arquitetura do Sistema

O projeto está organizado em quatro camadas principais:

1. Camada de Percepção e Atuação

ESP32 DevKit V1.

Servomotor Micro SG90.

LEDs indicadores verde e vermelho.

2. Camada de Conectividade

Rede Wi-Fi.

Comunicação baseada em TCP/IP.

Protocolo MQTT.

3. Camada de Servidor

Broker MQTT público HiveMQ.

Endereço: broker.hivemq.com.

Responsável por intermediar a comunicação entre os dispositivos.

4. Camada de Aplicação

Cliente MQTT ou dashboard.

Envio de comandos de abertura e fechamento.

Acompanhamento dos registros de acesso.

🔌 Hardware Utilizado

Componente

Modelo / Especificação

Função

Microcontrolador

ESP32 DevKit V1

Processamento e conexão Wi-Fi

Servomotor

Micro SG90 (5V)

Simulação da tranca

LED Verde

LED difuso

Indicação de acesso autorizado

LED Vermelho

LED difuso

Indicação de porta fechada ou acesso negado

Resistores

220 Ω

Proteção dos LEDs

📍 Tabela de Pinos

Componente

Pino ESP32

Função

Servomotor (Sinal)

GPIO 13

Controle PWM

Servomotor (VCC)

5V / VIN

Alimentação

Servomotor (GND)

GND

Terra

LED Verde

GPIO 2

Sinalização de porta aberta

LED Vermelho

GPIO 4

Sinalização de porta fechada

💻 Tecnologias e Bibliotecas

O desenvolvimento foi realizado em C++, utilizando a IDE Arduino e o simulador Wokwi.

Tecnologias

C++

ESP32

Arduino IDE

Wokwi

Wi-Fi

MQTT

JSON

NTP

Bibliotecas utilizadas

Biblioteca

Finalidade

WiFi.h

Conexão com a rede Wi-Fi

PubSubClient.h

Comunicação MQTT

ESP32Servo.h

Controle do servomotor

ArduinoJson.h

Manipulação de mensagens JSON

NTPClient.h

Sincronização de horário

WiFiUdp.h

Comunicação UDP para sincronização NTP

📡 Comunicação MQTT

O protocolo MQTT foi escolhido por ser leve, eficiente e adequado para dispositivos IoT.

O sistema utiliza os seguintes tópicos:

Tópico de comandos:

fag/iot/porta/comando

Exemplo de mensagem para abrir a porta:

{
  "comando": "ABRIR",
  "chave": "10012"
}

Tópico de status:

fag/iot/porta/status

Exemplo de resposta publicada pela ESP32:

{
  "dispositivo": "esp32_porta_lateral",
  "estado_porta": "ABERTA",
  "origem_acao": "COMANDO_REMOTO_JSON",
  "chave_identificacao": "10012",
  "horario": "20:30:15"
}

Dessa forma, cada comando recebido pode gerar uma atualização de status, permitindo acompanhar as operações realizadas pelo sistema.

⚙️ Funcionamento do Sistema

O funcionamento ocorre seguindo as seguintes etapas:

A ESP32 inicia e realiza a conexão com a rede Wi-Fi.

O dispositivo estabelece conexão com o broker MQTT.

O operador envia um comando pelo cliente MQTT.

A ESP32 recebe a mensagem por meio do tópico de comandos.

O sistema interpreta o conteúdo JSON e identifica o comando solicitado.

O servomotor realiza o movimento de abertura ou fechamento.

Os LEDs indicam visualmente o estado da tranca.

A ESP32 publica uma mensagem de status contendo a identificação da chave e o horário da operação.

🧪 Testes e Validação

Os testes foram realizados no ambiente de simulação Wokwi, integrado a clientes MQTT externos.

Durante o desenvolvimento, foram identificados e corrigidos alguns problemas:

1. Falta de dependências na compilação

Foi identificado um erro relacionado à ausência da biblioteca PubSubClient.h.

Solução: inclusão do arquivo libraries.txt com as dependências necessárias para o funcionamento do projeto.

2. Erro de sintaxe no código

Foi identificado um espaço indevido na chamada do método client.connected().

Solução: correção da chamada do método, permitindo a verificação adequada da conexão MQTT.

Após as correções, foram realizados testes de comunicação, recebimento de comandos e acionamento do servomotor.

🎯 Objetivos Alcançados

Implementação de comunicação Wi-Fi com ESP32.

Integração com broker MQTT.

Recebimento e interpretação de comandos remotos.

Acionamento de servomotor.

Sinalização visual por LEDs.

Estruturação de mensagens JSON.

Registro de informações de acesso com identificação e horário.

📚 Aprendizados

O desenvolvimento proporcionou conhecimentos práticos sobre:

Arquitetura de Internet das Coisas (IoT).

Programação de microcontroladores com C++.

Comunicação entre dispositivos utilizando MQTT.

Integração entre hardware e software.

Manipulação de dados no formato JSON.

Sincronização de horário utilizando NTP.

Simulação e validação de circuitos eletrônicos.

🤖 Uso de Inteligência Artificial

Ferramentas de Inteligência Artificial foram utilizadas como apoio durante o desenvolvimento, principalmente na estruturação inicial de rotinas de código, integração de bibliotecas e revisão textual do relatório.

Todo o código foi analisado, ajustado e testado pelos integrantes do grupo, buscando garantir a compreensão do funcionamento e da lógica implementada.

🚀 Conclusão

O projeto demonstrou a possibilidade de desenvolver uma solução de controle de acesso remoto utilizando componentes de baixo custo e tecnologias de comunicação IoT.

A integração entre ESP32, Wi-Fi e MQTT permitiu implementar o recebimento de comandos, o acionamento de uma tranca simulada e o envio de informações de status.

Além dos resultados técnicos, o trabalho contribuiu para o aprendizado prático sobre sistemas embarcados, comunicação de rede, eletrônica e desenvolvimento de software.
