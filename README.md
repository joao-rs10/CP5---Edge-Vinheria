Projeto "Vinheria" - Prova de Conceito IoT com FIWARE
1. Integrantes:

Erick Gabriel Ferreira dos Santos

João Vitor Reis Silva

Victor Henry Melchior Camara

2. Resumo do Projeto: 

Este projeto consiste em uma Prova de Conceito (PoC) para a disciplina de Internet das Coisas. O objetivo é validar uma arquitetura IoT completa, demonstrando a coleta de dados de múltiplos sensores através de um microcontrolador ESP32 e a comunicação em tempo real com uma plataforma em nuvem (IoT Cloud FIWARE).

A solução simula o monitoramento ambiental de uma "Vinheria", enviando dados de temperatura, umidade, luminosidade e risco de alagamento.

3. Detalhes da Implementação
3.1. Arquitetura da Solução
A arquitetura é composta por duas partes principais:

Simulador de Dispositivo (Wokwi): Um ESP32 simulado no Wokwi coleta dados de quatro sensores distintos.

Plataforma IoT (FIWARE): Uma instância pública do FIWARE (Orion Context Broker) recebe, armazena e disponibiliza esses dados.

3.2. Simulador (Wokwi)
Microcontrolador: ESP32.

Ambiente: O projeto foi desenvolvido e simulado na plataforma Wokwi, utilizando a rede Wokwi-GUEST para conectividade.

Sensores Utilizados:

DHT22: Para medição de Temperatura (°C) e Umidade (%).

LDR (Fotoresistor): Para medição de Luminosidade (valor analógico "raw").

HC-SR04 (Sensor Ultrassônico): Para medir a distância, simulando um medidor de nível de "Alagamento" (em cm).

3.3. Plataforma IoT (FIWARE)
Para esta PoC, utilizamos a plataforma pública disponibilizada, conforme as instruções:

IP Público (Broker): 9.234.138.146

Portas: 1883 (MQTT) e 1026 (HTTP - Orion)

Device ID: lamp003

Tópico MQTT: iot/lamp003/attrs

3.4. Comunicação
O ESP32 envia os dados coletados para a plataforma FIWARE usando dois métodos simultaneamente para garantir a entrega:

MQTT: Publicação dos dados no tópico iot/lamp003/attrs. Este é o método primário para telemetria IoT.

HTTP PATCH: Envio de uma requisição PATCH para a API do Orion Context Broker (http://9.234.138.146:1026/v2/entities/lamp003/attrs). Isso atualiza diretamente a entidade no broker.

O payload enviado segue o padrão NGSI-v2 (FIWARE), como no exemplo abaixo:

JSON

{
  "temperatura": { "value": 25.50, "type": "Float" },
  "umidade": { "value": 60.10, "type": "Float" },
  "luminosidade": { "value": 850, "type": "Integer" },
  "alagamento": { "value": 150.20, "type": "Float" }
}


4. Resultados da Prova de Conceito (PoC)

Link do Wokwi: https://wokwi.com/projects/445655100070148097
