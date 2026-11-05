# Reforço da Aula 48 — Clonagem e duplicação de volumes

## Três operações diferentes
- Cópia de arquivos: interpreta arquivos e diretórios.
- Cópia bruta: transfere blocos no escopo definido.
- Clone lógico: pode compartilhar blocos e copiar sob alteração.

## Exemplo
Uma origem de 10.000 blocos não cabe integralmente em um destino de 8.000 blocos. A cópia bruta integral deve ser rejeitada. Antes de copiar uma origem ativa, coordene as gravações ou use snapshot.

## Identificadores
Clones podem duplicar UUIDs e GUIDs. Se origem e clone forem conectados juntos, o sistema precisa evitar ambiguidade.

## Perguntas
1. Qual a diferença entre cópia bruta e cópia de arquivos?
2. Por que uma origem ativa pode gerar clone inconsistente?
3. Por que identificadores precisam ser tratados?
4. Quando o destino pode ser publicado?
5. Como snapshot ajuda a criar uma cópia consistente?
