# Reforço da Aula 172 — Modo usuário e modo kernel

## Ideia central

Explicar a separação de privilégios da CPU e como o sistema controla operações sensíveis. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

níveis de privilégio; instruções privilegiadas; espaço de usuário; espaço de kernel; transição; pilhas; proteção de memória; superfície de ataque.

## Exemplo comentado

Um programa não deve escrever diretamente em registradores de controle da CPU. Ele solicita ao kernel uma operação permitida, e o kernel verifica se o pedido é válido.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** manter drivers e operações críticas no nível apropriado; validar ponteiros e parâmetros vindos do usuário; minimizar código privilegiado
- **Fluxo:** programa executa em usuário; solicita serviço ou ocorre exceção; hardware muda privilégio; kernel valida pedido; executa operação; retorna com estado controlado
- **Riscos:** confiar em ponteiro de usuário; executar instrução privilegiada em usuário; retornar com flags perigosas; compartilhar pilha de kernel
- **Validação:** operação permitida; operação privilegiada em usuário; ponteiro inválido; retorno com privilégio incorreto; pilha de kernel ausente

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
