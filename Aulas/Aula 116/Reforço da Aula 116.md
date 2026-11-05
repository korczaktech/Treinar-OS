# Reforço da Aula 116 — Fragmentação e compactação de memória

## Ideia central

Identificar desperdício por fragmentação e avaliar técnicas que reduzem ou contornam a dispersão de espaços livres. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

fragmentação interna e externa; blocos contíguos; alocação variável; compactação; realocação; coalescência; custo e impossibilidade de mover certas regiões físicas.

## Exemplo comentado

Há 100 MiB livres no total, mas distribuídos em blocos de 1 MiB. Uma solicitação contígua de 8 MiB falha apesar do total livre; a métrica relevante é o maior intervalo disponível.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** preferir paginação quando contiguidade física não for requisito; não compactar memória física em uso sem mecanismo seguro de realocação e atualização de referências
- **Fluxo:** registrar alocações; liberar intervalos; coalescer vizinhos; medir fragmentação; decidir entre nova busca, paginação, compactação ou falha
- **Riscos:** confundir memória total livre com maior bloco contíguo; mover dados ainda referenciados; medir apenas percentual livre; compactar sem sincronização
- **Validação:** liberação adjacente; lacunas alternadas; total livre alto e maior bloco pequeno; pedido impossível; coalescência; overflow de métricas

## Perguntas para revisão ativa

1. Qual problema este componente resolve no sistema operacional?
2. Quais responsabilidades pertencem a ele e quais pertencem a outro subsistema?
3. Que premissas precisam ser verdadeiras para seu funcionamento?
4. Quais limites de hardware, memória ou privilégio afetam a solução?
5. O que deve acontecer quando o recurso solicitado não existe?
6. Que risco aparece se o kernel confiar cegamente nos dados recebidos?

## Exercício rápido de recuperação

Sem olhar a aula principal, desenhe um diagrama conceitual que mostre entradas, saídas, responsabilidades e limites do componente. Depois compare seu desenho com as estruturas, fluxo e invariantes descritos na aula. Corrija o que estiver incompleto e explique em voz alta por que cada etapa existe.

## Quando revisar novamente

Faça uma revisão curta no dia seguinte e outra alguns dias depois. Em cada revisão, tente reconstruir o fluxo sem reler o texto primeiro. Consulte o material apenas para corrigir lacunas.
