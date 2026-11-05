# Reforço da Aula 190 — Segmentos e layout de executáveis

## Ideia central

Interpretar regiões de código, dados e memória não inicializada e posicioná-las corretamente no espaço virtual. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

segmentos; código; dados; BSS; alinhamento; flags R/W/X; tamanho em arquivo; tamanho em memória; entry point; layout.

## Exemplo comentado

Um segmento com 0x200 bytes no arquivo e 0x500 bytes em memória exige copiar 0x200 bytes e inicializar os 0x300 restantes conforme a semântica do formato, normalmente com zero para BSS.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** validar alinhamento e sobreposição; distinguir bytes armazenados de bytes que devem existir em memória; aplicar W^X; respeitar limites do espaço
- **Fluxo:** ler tabela; validar intervalos; reservar regiões; copiar bytes presentes; zerar cauda BSS; aplicar permissões; verificar entry point
- **Riscos:** copiar tamanho de memória do arquivo; não zerar BSS; permitir segmento executável gravável sem política; conflito entre segmentos; alinhamento inválido
- **Validação:** tamanho em memória menor que arquivo; BSS; segmentos sobrepostos; alinhamento inválido; flags proibidas; entry point fora do código

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
