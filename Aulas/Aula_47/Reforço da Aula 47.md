# Reforço da Aula 47 — Snapshots em nível de bloco

## 1. Ideia principal

Snapshot preserva uma visão anterior do volume. Copy-on-write guarda a versão antiga antes de sobrescrever o bloco.

## 2. Cuidados que não podem ser esquecidos

Snapshot não é necessariamente backup. Gerencie espaço, mapas e referências e defina o que ocorre quando a reserva acaba.

## 3. Ligação com o ZenithOS

A implementação deve separar política, validação e acesso ao dispositivo. O gerenciador de volumes oferece uma abstração consistente, enquanto drivers executam operações específicas e comunicam falhas reais.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
