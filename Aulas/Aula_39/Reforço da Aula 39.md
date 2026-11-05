# Reforço da Aula 39 — Agrupamento e divisão de requisições de I/O

## 1. Ideia principal

Agrupamento combina pedidos contíguos e compatíveis. Divisão adapta uma operação a limites de transferência.

## 2. Cuidados que não podem ser esquecidos

Preserve ordem, prioridades, dependências e offsets de buffer. A soma dos segmentos deve corresponder à requisição original.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
