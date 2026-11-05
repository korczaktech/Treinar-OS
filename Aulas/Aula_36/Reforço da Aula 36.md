# Reforço da Aula 36 — Leitura e escrita parcial de blocos

## 1. Ideia principal

A interface de blocos costuma operar em setores completos. Alterar poucos bytes pode exigir leitura-modificação-escrita.

## 2. Cuidados que não podem ser esquecidos

Operações concorrentes no mesmo setor precisam de sincronização para não perder atualizações.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
