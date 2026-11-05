# Reforço da Aula 115 — Alocadores de memória do kernel

## Ideia central

Entender como o kernel solicita e devolve unidades físicas de memória e como um alocador mantém a disponibilidade sem duplicar ou perder quadros. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

alocação e liberação; bitmap; lista livre; buddy allocator; ordem; divisão e união de blocos; custo de busca; fragmentação interna.

## Exemplo comentado

Um bloco de ordem 3 representa oito unidades mínimas. Para atender um pedido de ordem 1, o alocador pode dividi-lo em metades sucessivas, reservar uma parte e reinserir as demais na lista de ordens correspondentes.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** começar com interface pequena de alocar/liberar; documentar alinhamento e tamanho mínimo; detectar liberação dupla; manter contabilidade verificável
- **Fluxo:** validar pedido; encontrar bloco compatível; dividir quando necessário; marcar posse; devolver bloco; localizar parceiro; unir blocos quando possível
- **Riscos:** dupla alocação; dupla liberação; perder bloco durante divisão; unir blocos que não são parceiros; aceitar ordem inválida; metadados corrompidos
- **Validação:** memória esgotada; pedido mínimo; pedido maior; divisão em várias ordens; união de parceiros; dupla liberação; fragmentação; estado inconsistente

## Perguntas para revisão ativa

1. Quais entradas malformadas devem ser rejeitadas?
2. Quais limites numéricos e de capacidade precisam ser testados?
3. Como detectar corrupção, duplicidade ou uso após liberação?
4. O que precisa ser revertido quando uma etapa falha?
5. Como provar que o erro não deixou recursos vazados?
6. Quais invariantes podem ser verificados automaticamente?

## Exercício rápido de recuperação

Sem olhar a aula principal, desenhe uma matriz de testes com entradas, resultado esperado, estado posterior e critério de aprovação. Depois compare seu desenho com as estruturas, fluxo e invariantes descritos na aula. Corrija o que estiver incompleto e explique em voz alta por que cada etapa existe.

## Quando revisar novamente

Faça uma revisão curta no dia seguinte e outra alguns dias depois. Em cada revisão, tente reconstruir o fluxo sem reler o texto primeiro. Consulte o material apenas para corrigir lacunas.
