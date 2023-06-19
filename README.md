# home-broker
This project is a smaller test for a home broker
Este projeto é uma simulação de um Home Broker

## Schedule
- Entencer o projeto prático
- Tecnologias que serão utilizadas
- Ordem do desenvolvimento
- Entendimento do microserviço de "Bolsa"
- Início do microserviço de "bolsa"

# Projeto

- Desenvolvimento de uma plataforma como Home Broker:
- Sistema da Bolsa(Simular uma B3- Dar Match de ofertas d compra e venda de ações)
- Home Broker - Onde as ofertas serão submetidas, além dos indicadores em tempo real

# Dinâmica do projeto

Um usuário
Front - Home Broker (React/Next.js)
Backend -  (Nest.js)
Fila  - Apache Kafka
Bolsa (backend b3) - Golang

----------------
SSE - Tempo Real ( Server Sent Event)

# Tecnologias
 - Docker
 - Linguagem Go
 - Next.js
 - Nest.js
 - Apache Kafka

 # Complexidades do Microserviço de "Bolsa"
 - Simulador da bolsa possui um algoritmo ligeiramente complexo para fazer o match das ordens de compra e venda.
 - simulador deve ser performático
 - Precisará trabalhar com as operações "in memory"
 - Principais alocações precisarão ficar na heap e não na stack

 # Filas de ordem de Compra e Ordem de Venda
 Um local onde serão colocadas todas as ordens de compra e de venda
 
 # microserviço Bolsa
 - Cada vez que uma ordem de compra e venda dão "match", geraremos uma transação.
 - Essa transação será publiada no Apache Kafka no formato JSON
 - Não utilizaremos banco de dados por conta de tempo e simplificação
 - Sim, se o processo morrer, perderemos transações(lembrando estamos simplificando)

 # Microserviço de "Bolsa" - Channels
 - Linguagem Go trabalha com "channels" para fazer comunicação entre threads
 - Todas as ordens de compra e venda serão eniadas a um único channel para poderem ser registradas no "livro" de compra/venda
 - Quando um "match" ocorre, uma "transaction" é gerada e enviada a um channel de output que será lido pelo Apache Kafka
