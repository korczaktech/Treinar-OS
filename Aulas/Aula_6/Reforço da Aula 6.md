# Reforço da Aula 6 — Geometria lógica e organização de blocos

## 1. Modelo que o sistema enxerga
O sistema operacional recebe uma sequência de LBAs. Cada endereço identifica uma unidade lógica; o tamanho dessa unidade informa quantos bytes são transferidos.

## 2. CHS versus LBA
CHS descreve cilindro, cabeça e setor. LBA usa um número linear. Em sistemas atuais, o driver e o controlador cuidam das particularidades do dispositivo; o restante do kernel usa endereços lógicos.

## 3. Exemplo
Com 2.000 LBAs e 4.096 bytes por bloco:
- primeiro LBA: 0;
- último LBA: 1.999;
- deslocamento inicial do LBA 10: 10 × 4.096 = 40.960 bytes;
- capacidade apresentada: 2.000 × 4.096 = 8.192.000 bytes.

## 4. Vocabulário que precisa ficar separado
Setor lógico, setor físico, bloco de alocação, página NAND e bloco de apagamento não são sinônimos.

## 5. Perguntas de fixação
1. O que o LBA representa?
2. Qual é o último LBA de um dispositivo com 2.000 blocos?
3. Como calcular o deslocamento em bytes?
4. Por que CHS não descreve a organização interna de um SSD moderno?
5. Cite três tipos diferentes de bloco e a camada a que pertencem.
