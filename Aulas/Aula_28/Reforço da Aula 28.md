# Reforço da Aula 28 — Montagem e desmontagem de volumes

## 1. Ideia principal

Montagem associa um sistema de arquivos a um ponto da árvore após validar metadados. Desmontagem coordena referências, operações e dados pendentes.

## 2. Cuidados que não podem ser esquecidos

Não remover estruturas enquanto houver referências ativas. Forçar desmontagem não garante persistência de gravações.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
