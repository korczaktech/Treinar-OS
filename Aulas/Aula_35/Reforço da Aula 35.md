# Reforço da Aula 35 — Operações de leitura e escrita em múltiplos blocos

## 1. Ideia principal

Uma operação agrupa LBAs consecutivos. Limites de protocolo, controlador e buffer podem exigir dividir uma solicitação.

## 2. Cuidados que não podem ser esquecidos

Valide capacidade, multiplicações e buffer. O resultado precisa representar conclusão parcial e erros.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
