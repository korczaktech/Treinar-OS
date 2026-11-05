# Reforço da Aula 121 — Endereços e espaços de memória virtual

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
