# Reforço da Aula 141 — Heap, pilha e mapeamentos de memória

## Ideia central

Diferenciar áreas de alocação dinâmica, pilhas de execução e mapeamentos explícitos, controlando limites e ciclo de vida. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

heap; stack; crescimento; ponteiro de pilha; frames de chamada; guard pages; mmap conceitual; regiões anônimas e apoiadas em arquivo; desalocação.

## Exemplo comentado

Um processo pode reservar 64 MiB de espaço virtual para heap e ter apenas algumas páginas físicas comprometidas inicialmente. Reserva virtual não equivale a consumo imediato de RAM.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** definir limites por processo; separar reserva virtual de compromisso físico; usar guard pages; documentar alinhamento e política de crescimento
- **Fluxo:** solicitar região; reservar intervalo virtual; mapear páginas conforme política; usar região; remover mapeamento; devolver quadros quando não houver referências
- **Riscos:** stack overflow; heap overlap; liberar região errada; crescimento sem limite; confundir memória virtual reservada com memória física comprometida
- **Validação:** crescimento normal; limite atingido; guard page; heap e stack se aproximando; desalocação; região sobreposta; reserva sem quadro físico

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
