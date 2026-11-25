# Objetivo

Criar uma rede distribuida e descentralizada de envios de bytes segmentado com recompensa.

# Agentes

- O Orquestrador
- Cliente
- Trabalhador

# Cenário

Um client quer o buffer de uma música e pede ao orquestrador

Vários trabalhadores estão disponíveis com catálogos próprios

O orquestrador publica o pedido do cliente, e vários trabalhadores diz que tem essa música.

O orquestrador conhece a reputação de cada trabalhador, e escolhe o melhor entre eles, e diz ao cliente qual URL o stream pode ser ouvido.

# Recompensa

O cliente compra 100 de saldo.

O orquestrador recompensa o trabalhador pelo trabalho, mas precisa de uma prova que ele fez o serviço.

Então quando o trabalhador envia o segmento de bytes para o cliente, ele envia também o comprovante para o orquestrador.
Quando o cliente recebe o segmento, ele envia o comprovante para o orquestrador.

O orquestrador valida que ambos comprovantes são válidos, e desconta dos créditos do cliente. E posteriormente, paga ao trabalhador.

# Regras

Para o lado do cliente, o trabalhador precisa de pelo menos entregar X bytes (ou 30 segundos de música), para que sua entrega completa seja válida.

Para o lado do trabalhador, ele é recompensado independente se o cliente ouviu 30 segundos, 2 minutos, ou 1 hora.

Um exemplo prático, uma música de 10min, que foi ouvida por 8min, os 8 serão pagos. Se nos primeiros 30seg, percebeu que é cover, ou má qualidade, então a conexão é fechada, e não é cobrado ao cliente, nem pago ao trabalhador.

# Penalização

O trabalhador pode entregar a música com qualidade, e rápido, mas mesmo assim, o cliente pode escolher não ouvir esse trabalhador. Ele não será penalizado por isso, mas se houver frequencia, estatisticamente, ele será penalizado pela quantidade de rejeição de seu trabalho.

# Burlas

Não podemos permitir que:

- O Cliente dizer que só recebeu 1 segmentos, e falhou, enquanto continua ouvindo.
- O Cliente receba mais do que pagou.
- O trabalhador dizer que continua enviando, enquanto o Cliente perdeu a conexão, ou encerrou pela qualidade.
- O trabalhador peça mais do que entregou.

# Provas de transação

As transações precisam ser reconhecidas e fácilmente auditadas utilizando Contrato Besu. Então registramos o lote de comprovantes utilizando uma árvore merkle, e nós QBFT (Istanbul Byzantine Fault Tolerance) para verificação.

