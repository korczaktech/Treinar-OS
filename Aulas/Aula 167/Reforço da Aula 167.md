# Reforço da Aula 167 — Contexto e troca de contexto

## Ideia central

Compreender quais informações da CPU precisam ser preservadas para interromper uma execução e retomá-la corretamente. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

registradores gerais; ponteiro de instrução; ponteiro de pilha; flags; registradores especiais; contexto de thread; contexto de processo; custo de troca.

## Exemplo comentado

Se o ponteiro de instrução não for salvo, a thread pode retornar a uma posição errada. Se o ponteiro de pilha for trocado incorretamente, as chamadas seguintes corrompem a pilha.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** definir assembly de entrada/saída conforme ABI e arquitetura; distinguir contexto voluntário de interrupção; documentar registradores preservados pelo chamador e pelo kernel
- **Fluxo:** interrupção ou decisão de escalonamento; salvar estado exigido; selecionar próxima thread; trocar pilha/espaço quando necessário; restaurar estado; retornar
- **Riscos:** omitir registrador; restaurar ordem errada; usar pilha inválida; misturar contexto de processo e thread; trocar espaço sem tratar TLB
- **Validação:** contexto completo; registrador omitido; pilha inválida; troca repetida; interrupção aninhada; mudança de espaço

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
