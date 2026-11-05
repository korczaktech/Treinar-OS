# Reforço da Aula 8 — Particionamento e Mapa do Disco

## 1. Uma divisão no mesmo dispositivo

Um dispositivo com 1000 blocos pode ter uma partição de 0 a 199 e outra de 200 a 999. São regiões do mesmo dispositivo, não dois discos físicos.

## 2. Início e quantidade

Uma partição que começa em 200 e possui 300 blocos é [200, 500). Contém 200 até 499. O 500 é o limite exclusivo.

## 3. Cabe ou ultrapassa?

Dispositivo: 1000 blocos.

Início 800, quantidade 200: termina no limite 1000 e cabe. Início 800, quantidade 201: ultrapassa e deve ser rejeitada.

## 4. Adjacência e sobreposição

[100, 200) e [200, 300) são adjacentes. [100, 200) e [199, 300) se sobrepõem porque compartilham o bloco 199.

## 5. Mapa não é conteúdo

A tabela responde onde começam e terminam as regiões. O sistema de arquivos responde quais diretórios e arquivos existem. GPT organiza partições, não arquivos.

## 6. Perguntas de fixação

1. Uma partição começa em 900 e possui 100 blocos em um dispositivo de 1000. Cabe?
2. Qual é o limite exclusivo de uma partição que começa em 20 e possui 10 blocos?
3. [10, 20) e [20, 30) se sobrepõem?
4. [10, 20) e [19, 30) se sobrepõem?
5. GPT organiza arquivos ou partições?
6. Uma partição vazia deixa de ser uma partição?
