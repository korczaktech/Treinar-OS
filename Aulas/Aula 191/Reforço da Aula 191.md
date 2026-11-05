# Reforço da Aula 191 — Pilha inicial e ambiente de execução

## Ideia central

Preparar a pilha e os argumentos iniciais para que o programa comece com um estado de execução coerente com a ABI. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

stack pointer; alinhamento; argumentos; ambiente; argc/argv conceituais; strings; endereço de retorno quando aplicável; frame inicial; convenção de ABI.

## Exemplo comentado

Ao montar três argumentos, o kernel precisa reservar espaço para as strings e para o vetor de ponteiros, calcular endereços finais e só então definir o registrador de pilha.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** seguir ABI definida para a arquitetura; validar quantidade e tamanho de argumentos; manter ponteiros dentro da pilha do processo; reservar guard page
- **Fluxo:** reservar stack; calcular espaço; copiar strings; montar vetores; alinhar ponteiro; posicionar metadados; definir registradores iniciais; transferir para entry point
- **Riscos:** stack pointer desalinhado; ponteiros para cópias temporárias; overflow de soma; strings sem terminador quando exigido; ordem incorreta dos dados
- **Validação:** zero argumentos; muitos argumentos; string longa; alinhamento; buffer insuficiente; ponteiro fora da pilha; overflow

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
