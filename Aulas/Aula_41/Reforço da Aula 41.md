# Reforço da Aula 41 — Diagnóstico de desempenho

## Métricas
- Latência: duração de uma operação.
- Throughput: dados por unidade de tempo.
- IOPS: operações por segundo.
- p50/p95/p99: percentis da distribuição de latência.

## Exemplo
1.000 MiB em 10 segundos correspondem a 100 MiB/s. Isso não informa sozinho a latência p99 nem identifica o gargalo.

## Testes comparáveis
Registre tamanho de bloco, padrão sequencial/aleatório, concorrência, profundidade da fila, aquecimento, cache e sincronização. Altere uma variável por vez.

## Perguntas
1. Como latência difere de throughput?
2. O que IOPS mede?
3. Por que p99 é útil?
4. Quais condições precisam ser documentadas em um benchmark?
5. Quais camadas podem causar um gargalo?
