# Reforço da Aula 37 — Atomicidade e limites de operações

## 1. Ideia principal

Atomicidade é indivisibilidade segundo um contrato; durabilidade é persistência. Uma não implica automaticamente a outra.

## 2. Cuidados que não podem ser esquecidos

Conheça limites e condições anunciados pelo dispositivo. Journal e copy-on-write ajudam quando hardware não oferece atomicidade ampla.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
