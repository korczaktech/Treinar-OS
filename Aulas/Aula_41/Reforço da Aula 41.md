# Reforço da Aula 41 — Diagnóstico de desempenho de armazenamento

## 1. Ideia principal

Latência mede duração; throughput mede volume por tempo; IOPS mede operações por segundo. Percentis mostram picos que a média esconde.

## 2. Cuidados que não podem ser esquecidos

Declare carga, duração, cache, sincronização e padrão de acesso. Benchmarks de escrita podem sobrescrever dados; métrica isolada não revela o gargalo.

## 3. Ligação com o ZenithOS

A implementação deve separar política, validação e acesso ao dispositivo. O gerenciador de volumes oferece uma abstração consistente, enquanto drivers executam operações específicas e comunicam falhas reais.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
