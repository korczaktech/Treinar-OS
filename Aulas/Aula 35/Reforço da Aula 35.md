# Reforço da Aula 35 — Operações em múltiplos blocos

## Dividir sem perder a faixa
Uma solicitação de 300 blocos com limite de 128 por comando vira segmentos de 128, 128 e 44 blocos. Os LBAs iniciais avançam conforme a quantidade já coberta.

## Exemplo
Início 1.000:
- 1.000 a 1.127;
- 1.128 a 1.255;
- 1.256 a 1.299.

A soma precisa ser 300, sem lacunas e sem repetição.

## Resultados parciais
Se dois segmentos concluem e o terceiro falha, o resultado agregado não é sucesso total. Informe quantidade concluída e erro.

## Perguntas
1. Por que dividir uma requisição?
2. Como calcular o início do próximo segmento?
3. Por que a soma deve corresponder ao pedido original?
4. O que informar após uma falha parcial?
5. Que limites além da quantidade podem exigir divisão?
