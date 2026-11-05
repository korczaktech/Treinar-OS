# Reforço da Aula 151 — Diferença entre programa e processo

## Ideia central

Separar o arquivo executável e suas instruções da instância em execução, com estado e recursos próprios. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

programa como artefato; processo como execução isolada; PID; espaço virtual; recursos; estado; múltiplas instâncias; identidade e ciclo de vida.

## Exemplo comentado

Duas execuções do mesmo programa podem ter PIDs, pilhas, heaps e variáveis independentes, mesmo carregando instruções originadas do mesmo arquivo.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** não confundir nome de arquivo com identidade do processo; definir PID sem colisões; separar imagem executável de estado mutável
- **Fluxo:** selecionar executável; validar formato; criar processo; preparar memória e contexto; torná-lo elegível; executar; finalizar e liberar recursos
- **Riscos:** assumir que um arquivo corresponde a um único processo; reutilizar PID prematuramente; compartilhar estado mutável por acidente; deixar recursos após término
- **Validação:** duas instâncias; PID duplicado; processo terminado; recursos compartilhados; imagem ausente; falha na criação

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
