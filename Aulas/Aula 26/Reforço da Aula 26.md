# Reforço da Aula 26 — Volumes, regiões reservadas e limites

## 1. Três conceitos
- Dispositivo: unidade física ou virtual que apresenta blocos.
- Partição: região descrita no mapa do dispositivo.
- Volume: unidade lógica que o sistema disponibiliza para uso.

## 2. Tradução de endereço
Volume começa no LBA 2.000 e possui 500 blocos. Uma requisição relativa no LBA 20 corresponde ao LBA absoluto 2.020. Primeiro valide a faixa dentro do volume; só depois some o início.

## 3. Regiões reservadas
Áreas de boot, metadados e recuperação não podem ser contadas como espaço livre de outro volume. A propriedade de cada faixa precisa ser inequívoca.

## 4. Perguntas de revisão
1. Uma partição sempre corresponde a um volume?
2. Por que reservar regiões?
3. Qual é o LBA absoluto para início de volume 2.000 e LBA relativo 20?
4. Um volume de 500 blocos aceita início relativo 499 e quantidade 1?
5. Por que a tradução precisa validar a faixa antes de somar os endereços?


## Exemplo guiado de limite do volume
Um volume começa no LBA 10.000 e possui 5.000 blocos. O último LBA relativo válido é 4.999. Uma requisição relativa que começa em 4.990 e pede 10 blocos acessa 4.990 até 4.999 e cabe exatamente. Se pedir 11, ultrapassa o volume, mesmo que o dispositivo físico possua outros blocos depois dele.
