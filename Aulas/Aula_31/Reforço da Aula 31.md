# Reforço da Aula 31 — Integridade e recuperação de tabelas de partição

## 1. Ideia principal

GPT oferece cópias principal e backup e CRCs para diagnóstico. Uma cópia válida pode estar desatualizada.

## 2. Cuidados que não podem ser esquecidos

CRC não autentica. Diagnóstico deve preceder reparo; preserve imagem e não invente entradas quando a evidência for insuficiente.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
