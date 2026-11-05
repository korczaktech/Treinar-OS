# Reforço da Aula 127 — Tabelas de páginas multinível

## Ideia central

Entender como tabelas hierárquicas traduzem endereços virtuais sem exigir uma tabela plana para todo o espaço. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

divisão do endereço em índices e deslocamento; níveis; entradas presentes; tabela folha; tamanho de página; páginas grandes; bits de permissão.

## Exemplo comentado

Em uma arquitetura hipotética com índices de 9 bits por nível e deslocamento de 12 bits, cada índice seleciona uma entrada e os 12 bits finais permanecem como deslocamento dentro da página. Os valores reais dependem do modo de paginação escolhido.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** seguir exatamente os níveis e a largura de índice definidos pela arquitetura do ZenithOS; encapsular leitura/escrita de entradas; evitar assumir layout universal
- **Fluxo:** extrair índices; consultar raiz; validar entrada; avançar nível; localizar folha; combinar base física com deslocamento; verificar permissões
- **Riscos:** índice fora do limite; confundir endereço da tabela com endereço mapeado; esquecer bit presente; aceitar flags reservadas; liberar tabela ainda referenciada
- **Validação:** entrada ausente em cada nível; folha válida; deslocamento preservado; página grande; flags inválidas; índice no limite

## Perguntas para revisão ativa

1. Quais estruturas representam o componente?
2. Qual é a unidade de cada campo: bytes, páginas, identificadores ou estados?
3. Quais campos podem ser derivados e quais precisam ser armazenados?
4. Como representar ausência, erro e recurso reservado?
5. Quais invariantes devem permanecer verdadeiros?
6. Como evitar overflow, duplicidade e referências pendentes?

## Exercício rápido de recuperação

Sem olhar a aula principal, desenhe um modelo de dados anotado com campos, unidades, invariantes e estados inválidos. Depois compare seu desenho com as estruturas, fluxo e invariantes descritos na aula. Corrija o que estiver incompleto e explique em voz alta por que cada etapa existe.

## Quando revisar novamente

Faça uma revisão curta no dia seguinte e outra alguns dias depois. Em cada revisão, tente reconstruir o fluxo sem reler o texto primeiro. Consulte o material apenas para corrigir lacunas.
