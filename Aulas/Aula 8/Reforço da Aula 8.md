# Reforço da Aula 8 — Fluxo de leitura e escrita de blocos

## Leitura e gravação têm direções opostas
- Leitura: dispositivo para buffer de memória.
- Gravação: buffer de memória para dispositivo.

## Exemplo resolvido
Uma operação transfere 4 blocos lógicos de 512 bytes. A transferência é 4 × 512 = 2.048 bytes. O buffer precisa comportar pelo menos 2.048 bytes. Um buffer de 2.047 bytes é insuficiente.

## O que uma requisição descreve?
Dispositivo, LBA inicial, quantidade, direção, buffer e capacidade do buffer. Sem esses dados, a camada não consegue validar corretamente o pedido.

## Estados
Criada, validada, em execução e concluída. Também pode falhar. A validação não garante que o hardware responderá com sucesso.

## Perguntas de fixação
1. Qual é a direção dos dados em uma leitura?
2. Qual é a direção dos dados em uma gravação?
3. Quantos bytes são transferidos em 5 blocos de 4.096 bytes?
4. Por que um buffer pequeno deve ser rejeitado antes da execução?
5. O que significa uma operação parcialmente concluída?
