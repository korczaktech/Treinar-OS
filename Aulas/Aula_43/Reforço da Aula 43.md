# Reforço da Aula 43 — Volumes distribuídos e espelhados

## 1. Ideia principal

Distribuição divide dados entre membros; espelhamento mantém cópias. Capacidade, paralelismo e tolerância variam conforme a estratégia.

## 2. Cuidados que não podem ser esquecidos

Redundância não substitui backup. Defina quando gravação é concluída e como detectar divergência entre cópias.

## 3. Ligação com o ZenithOS

A implementação deve separar política, validação e acesso ao dispositivo. O gerenciador de volumes oferece uma abstração consistente, enquanto drivers executam operações específicas e comunicam falhas reais.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
