# Reforço da Aula 33 — Capacidades e características anunciadas por dispositivos

## 1. Ideia principal

Dispositivos anunciam capacidade, tamanho de bloco, limites de transferência e recursos opcionais. O kernel normaliza esses dados.

## 2. Cuidados que não podem ser esquecidos

Desconhecido não significa suportado. Valide os campos e trate falhas mesmo quando o recurso foi anunciado.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
