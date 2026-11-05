# Reforço da Aula 199 — Threads e compartilhamento de recursos

## Ideia central

Distinguir processo de thread e entender quais recursos são compartilhados e quais pertencem individualmente a cada fluxo de execução. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

thread; TID; pilha própria; registradores próprios; espaço de endereçamento compartilhado; descritores compartilhados conforme política; TLS; sincronização futura.

## Exemplo comentado

Duas threads do mesmo processo podem acessar o mesmo heap, mas cada uma precisa de sua própria pilha e contexto de registradores. Encerrar uma thread não encerra automaticamente todo o processo.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** definir claramente propriedade e ciclo de vida; contar referências a recursos compartilhados; separar estado por thread do estado do processo
- **Fluxo:** criar thread; alocar contexto e pilha; associar ao processo; inserir na fila; executar; compartilhar recursos definidos; terminar e liberar recursos próprios
- **Riscos:** duas threads usando a mesma pilha; liberar espaço compartilhado enquanto outra thread usa; confundir TID e PID; estado local compartilhado acidentalmente
- **Validação:** duas threads; pilha duplicada; thread termina; processo termina; referência compartilhada; TID duplicado; thread órfã

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
