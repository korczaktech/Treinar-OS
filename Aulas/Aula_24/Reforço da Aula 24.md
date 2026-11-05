# Reforço da Aula 24 — Compatibilidade e leitura de tabelas MBR

## 1. Ideia principal

MBR clássico possui quatro entradas primárias. Partições estendidas usam EBRs encadeados para descrever partições lógicas.

## 2. Cuidados que não podem ser esquecidos

Detecte ciclos, endereços repetidos e regiões fora da partição estendida. O MBR protetor GPT não é uma tabela MBR convencional.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
