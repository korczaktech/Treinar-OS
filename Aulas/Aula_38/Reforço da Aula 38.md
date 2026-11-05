# Reforço da Aula 38 — Ordenação de requisições de armazenamento

## 1. Ideia principal

Filas podem reordenar pedidos independentes, mas dependências e barreiras precisam preservar a consistência.

## 2. Cuidados que não podem ser esquecidos

Ordem de submissão não garante ordem persistente. Flush e barreiras dependem do contrato real do dispositivo.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
