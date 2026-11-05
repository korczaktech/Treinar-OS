# Reforço da Aula 26 — Volumes, regiões reservadas e limites de uso

## 1. Ideia principal

Disco é o dispositivo; partição é uma região descrita; volume é uma unidade lógica oferecida ao sistema. Reservas não podem ser entregues ao sistema de arquivos.

## 2. Cuidados que não podem ser esquecidos

Valide faixa do volume antes de converter LBA relativo em absoluto. Exclua regiões reservadas da capacidade utilizável.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
