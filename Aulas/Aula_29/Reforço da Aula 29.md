# Reforço da Aula 29 — Metadados e estruturas de armazenamento

## 1. Ideia principal

Metadados descrevem organização, atributos, alocação e estado. Estruturas persistentes precisam de formato binário especificado.

## 2. Cuidados que não podem ser esquecidos

Não grave diretamente structs nativas com padding e ponteiros. Defina versão, endianness, tamanho e serialização.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
