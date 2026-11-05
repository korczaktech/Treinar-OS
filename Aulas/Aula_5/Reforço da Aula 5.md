# Reforço da Aula 5 — Alinhamento e Requisitos de Transferência

## 1. Imagine uma régua de endereços

Cada número representa um endereço de byte. Para alinhamento de 4, as fronteiras são 0, 4, 8, 12, 16... Para alinhamento de 8, são 0, 8, 16, 24, 32...

A fronteira depende da regra exigida.

## 2. Encontre a próxima fronteira

Endereço 10, alinhamento 8: o próximo múltiplo de 8 é 16. Endereço 16, alinhamento 8: o próprio 16 já serve.

Se o endereço não estiver alinhado, pode ser necessário deixar bytes vazios antes do dado. Esse espaço é padding.

## 3. Três tamanhos diferentes

- Alinhamento: onde o dado começa.
- Tamanho do setor: quantos bytes correspondem a um LBA.
- Tamanho de transferência: quantos bytes serão movimentados.

Um buffer de 4096 bytes pode começar em endereço alinhado a 8 e receber dados de vários setores. São propriedades independentes.

## 4. Política do ZenithOS

O ZenithOS usa 8 bytes como política inicial para determinadas estruturas. Isso não quer dizer que todo hardware exija 8 bytes nem que toda leitura tenha tamanho múltiplo de 8. Requisitos específicos do mecanismo de transferência continuam valendo.

## 5. Alinhamento e limites

Uma região pode ter um endereço inicial alinhado, mas não possuir espaço suficiente para a estrutura. Primeiro verifique a fronteira; depois, a capacidade disponível. Uma condição não substitui a outra.

## 6. Perguntas de fixação

1. O endereço 24 está alinhado a 8 bytes?
2. Qual é o próximo endereço alinhado a 8 a partir de 19?
3. O que é padding?
4. Por que tamanho de setor e alinhamento não são sinônimos?
5. Um endereço alinhado pode estar fora da região reservada?
6. Por que requisitos de DMA ou de uma interface não devem ser presumidos?

Refaça os exemplos com números próprios até conseguir explicar cada resultado.
