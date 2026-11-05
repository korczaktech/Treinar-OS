# Reforço da Aula 122 — Endereços e espaços de memória virtual

## Ideia central

Compreender a separação entre endereços virtuais e físicos e como cada processo pode possuir um espaço lógico isolado. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

endereço virtual; endereço físico; espaço de endereçamento; tradução; isolamento; regiões; canonicalidade conforme arquitetura; espaço de usuário e kernel.

## Exemplo comentado

Dois processos podem usar o mesmo endereço virtual 0x400000 e obter quadros físicos diferentes. O valor do ponteiro, isoladamente, não identifica a célula física.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** definir regiões virtuais sem confundi-las com RAM instalada; manter política de usuário/kernel; documentar intervalos reservados e guardas
- **Fluxo:** processo acessa endereço virtual; hardware consulta tradução; verifica presença e permissões; produz endereço físico ou gera exceção
- **Riscos:** tratar ponteiro virtual como endereço físico; permitir overflow de intervalo; mapear duas regiões incompatíveis; ignorar bits reservados da arquitetura
- **Validação:** mesmo virtual em processos distintos; endereço não mapeado; região com limite exclusivo; overflow; endereço não canônico; acesso fora da região

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
