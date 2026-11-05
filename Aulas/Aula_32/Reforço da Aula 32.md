# Reforço da Aula 32 — Discos removíveis e detecção de hot-plug

## 1. Ideia principal

Hot-plug permite conexão e remoção durante a execução. Remoção exige bloquear novas operações e tratar requisições pendentes.

## 2. Cuidados que não podem ser esquecidos

Use estado e geração de conexão para invalidar referências antigas. Remoção pode interromper gravações e deixar dados não persistidos.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
