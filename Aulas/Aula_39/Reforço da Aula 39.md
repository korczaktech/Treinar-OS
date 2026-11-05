# Reforço da Aula 39 — Agrupamento e divisão de requisições de I/O

## Agrupamento
Só una pedidos compatíveis: mesmo dispositivo, direção e semântica, faixas adjacentes, buffers compatíveis e dependências preservadas.

## Divisão
Uma requisição de 350 blocos com máximo de 128 vira 128 + 128 + 94. Os inícios avançam pelo total já coberto.

## Resultados
A conclusão agregada precisa informar se todos os segmentos terminaram, quantos blocos foram concluídos e qual erro ocorreu. Não esconda falhas parciais.

## Perguntas
1. Quais condições permitem agrupar duas requisições?
2. Por que não agrupar dispositivos diferentes?
3. Divida 350 blocos em segmentos de no máximo 128.
4. Como evitar lacunas e sobreposição?
5. Como representar falha no último segmento?
