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


## 6. Exemplo completo de divisão
Uma solicitação começa no LBA 800 e pede 350 blocos. O limite máximo por comando é 128 blocos. A divisão correta é:
- segmento 1: LBA 800, quantidade 128;
- segmento 2: LBA 928, quantidade 128;
- segmento 3: LBA 1.056, quantidade 94.

Os segmentos devem cobrir exatamente a faixa original. A soma 128 + 128 + 94 é 350. O segundo começa no primeiro LBA depois do segmento anterior, e o terceiro segue a mesma regra.

## 7. Compatibilidade para agrupamento
Além de adjacência, verifique mesmo dispositivo, mesma direção, compatibilidade dos buffers, mesma classe de prioridade e ausência de dependências que impeçam a união. Um pedido de leitura não deve ser unido a uma gravação só porque os LBAs são vizinhos.

## 8. Método de aprendizagem
Desenhe a faixa original, divida-a, confira a soma, confira o LBA inicial de cada segmento e simule erro em um deles. Registre o resultado agregado sem esconder a falha parcial.

## Exercícios de compreensão
1. Quais condições precisam ser verdadeiras para agrupar duas requisições?
2. Por que duas faixas adjacentes de dispositivos diferentes não podem ser agrupadas?
3. Divida uma requisição de 350 blocos em segmentos de no máximo 128 blocos.
4. Como garantir que a divisão não crie lacunas nem sobreposição?
5. O que fazer se um dos segmentos falhar depois que os anteriores concluíram?
6. Por que direção, prioridade e dependências importam no agrupamento?