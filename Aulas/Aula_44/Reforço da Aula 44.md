# Reforço da Aula 44 — Níveis RAID e tolerância a falhas

## 1. Ideia principal

RAID 0 distribui sem redundância; RAID 1 espelha; RAID 5 usa paridade simples; RAID 6 dupla; RAID 10 combina espelhamento e distribuição.

## 2. Cuidados que não podem ser esquecidos

Capacidade e tolerância dependem do nível e da posição das falhas. RAID não protege contra exclusão acidental.

## 3. Ligação com o ZenithOS

A implementação deve separar política, validação e acesso ao dispositivo. O gerenciador de volumes oferece uma abstração consistente, enquanto drivers executam operações específicas e comunicam falhas reais.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
