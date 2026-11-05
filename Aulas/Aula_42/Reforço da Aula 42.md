# Reforço da Aula 42 — Dispositivos compostos e encadeamento de volumes

## 1. Ideia principal

Um dispositivo composto encaminha operações a dispositivos inferiores e traduz endereços entre camadas.

## 2. Cuidados que não podem ser esquecidos

Valide cada faixa, divida pedidos em fronteiras e impeça ciclos no grafo. Remoções e falhas inferiores precisam propagar estado.

## 3. Ligação com o ZenithOS

A implementação deve separar política, validação e acesso ao dispositivo. O gerenciador de volumes oferece uma abstração consistente, enquanto drivers executam operações específicas e comunicam falhas reais.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
