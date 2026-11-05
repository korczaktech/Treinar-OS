# Reforço da Aula 38 — Ordenação de requisições

## Três ordens
Submissão é a ordem em que o kernel envia comandos. Execução é a ordem em que o dispositivo os processa. Persistência é a ordem em que os resultados se tornam duráveis.

## Exemplo
Dados de um bloco precisam estar persistidos antes de um metadado apontar para ele. Se o metadado persistir primeiro, uma queda pode deixar uma referência para conteúdo incompleto.

## Dependências
Represente operações como nós e dependências como setas. Só reordene operações independentes. Barreiras e flushes estabelecem fronteiras segundo o contrato.

## Perguntas
1. Por que a ordem de submissão não basta?
2. O que pode ocorrer se metadados persistirem primeiro?
3. Como representar uma dependência?
4. O que uma barreira estabelece?
5. Qual a diferença entre execução e persistência?
