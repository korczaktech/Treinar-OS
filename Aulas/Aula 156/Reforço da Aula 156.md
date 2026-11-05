# Reforço da Aula 156 — Estados e ciclo de vida de processos

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
