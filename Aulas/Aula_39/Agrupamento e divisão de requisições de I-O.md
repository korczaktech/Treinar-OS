# Agrupamento e divisão de requisições de I/O

## Objetivo

Aprender critérios para unir operações adjacentes e dividir requisições grandes, preservando limites, buffers, ordem e resultados parciais.

## 1. Agrupamento

Agrupamento combina requisições compatíveis quando seus LBAs são contíguos, as direções coincidem e as condições de buffer e prioridade permitem. Isso pode reduzir overhead de comandos. Não agrupe pedidos de dispositivos diferentes, faixas não contíguas ou operações com semânticas incompatíveis.

## 2. Divisão

Uma requisição pode exceder o limite de transferência, o tamanho máximo de buffer ou a profundidade disponível na fila. Nesse caso, divida-a em segmentos. Cada segmento precisa ter LBA inicial, quantidade e offset de buffer corretos. A soma das quantidades deve corresponder exatamente à operação original, sem lacunas nem sobreposição.

## 3. Ordem e resultados

Agrupamento pode alterar latência e ordem de conclusão. Não descarte prioridades, deadlines ou dependências. A conclusão agregada precisa informar falhas parciais e a quantidade efetivamente concluída.

## 4. Aplicação no ZenithOS

A camada de blocos pode manter uma etapa limitada de coalescência. O driver continua responsável por limites específicos do protocolo. A política deve ser determinística e testada com entradas conhecidas.

## 5. Perguntas de compreensão

1. Quando duas requisições podem ser agrupadas?
2. Por que uma requisição grande pode precisar ser dividida?
3. Como garantir que a divisão não perca nem repita blocos?
4. Por que prioridades e dependências precisam ser preservadas?

## Critério de conclusão

Você concluiu quando conseguir agrupar operações compatíveis, dividir uma operação maior que o limite e explicar como os resultados parciais são comunicados.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
