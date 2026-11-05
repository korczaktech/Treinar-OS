# Reforço da Aula 194 — Pilha inicial e ambiente de execução

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

1. Quais módulos e interfaces precisam existir?
2. Que dados entram e saem de cada interface?
3. Qual componente mantém a propriedade do recurso?
4. Como o ZenithOS inicia, usa e encerra esse componente?
5. Que parte pode ser simulada antes da integração real?
6. Como evitar dependências circulares e estado global desnecessário?

## Exercício rápido de recuperação

Sem olhar a aula principal, desenhe um desenho de módulos, interfaces, sequência de implementação e plano de integração. Depois compare seu desenho com as estruturas, fluxo e invariantes descritos na aula. Corrija o que estiver incompleto e explique em voz alta por que cada etapa existe.

## Quando revisar novamente

Faça uma revisão curta no dia seguinte e outra alguns dias depois. Em cada revisão, tente reconstruir o fluxo sem reler o texto primeiro. Consulte o material apenas para corrigir lacunas.
