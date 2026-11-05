# Reforço da Aula 157 — Estados e ciclo de vida de processos

## Ideia central

Representar as transições entre criação, execução, espera, prontidão e término sem estados impossíveis. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

novo; pronto; executando; bloqueado; terminado; preempção; evento de despertar; fila de prontos; fila de espera; transições permitidas.

## Exemplo comentado

Um processo executando solicita leitura de disco: passa a bloqueado. Ao receber conclusão, volta a pronto; não deve voltar diretamente a executando sem seleção do escalonador.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** definir tabela explícita de transições; atualizar estado e fila atomicamente; impedir que processo esteja simultaneamente em filas incompatíveis
- **Fluxo:** criar em novo; preparar; inserir em pronto; escalonador seleciona; executar; bloquear ou sofrer preempção; despertar; terminar
- **Riscos:** executar processo bloqueado; perder processo ao despertar; inserir duas vezes na fila; transição direta inválida; terminar sem limpar recursos
- **Validação:** todas as transições válidas; transição inválida; despertar duplicado; término durante bloqueio; fila inconsistente; preempção

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
