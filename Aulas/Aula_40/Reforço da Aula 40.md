# Reforço da Aula 40 — Despacho e escalonamento

## Políticas
FIFO atende por ordem de chegada. Prioridade atende primeiro pedidos importantes. Aging aumenta a prioridade de quem espera. Deadline tenta limitar o tempo de espera.

## Métricas
Throughput mede dados por tempo; latência mede tempo de cada pedido; justiça mede oportunidade de atendimento. Melhorar uma pode piorar outra.

## Exemplo
Uma política de prioridade estrita pode deixar um pedido comum esperando indefinidamente. Aging aumenta sua prioridade ao longo do tempo e reduz starvation.

## Perguntas
1. Qual a diferença entre despacho e escalonamento?
2. O que é starvation?
3. Como aging ajuda?
4. Por que throughput alto pode coexistir com latência ruim?
5. Por que medir a carga real antes de otimizar?
