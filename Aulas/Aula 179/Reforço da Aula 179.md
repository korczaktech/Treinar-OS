# Reforço da Aula 179 — Chamadas de sistema e ABI

## Ideia central

Definir uma fronteira estável entre aplicações e kernel, incluindo convenção de chamada, números de serviço, argumentos e erros. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

syscall; ABI; número de chamada; registradores de argumentos; instrução de transição; convenção de retorno; compatibilidade; validação de parâmetros.

## Exemplo comentado

Uma chamada que lê dados precisa validar o destino e o tamanho antes de copiar para memória do usuário; aceitar qualquer ponteiro pode derrubar ou comprometer o kernel.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** documentar ABI por arquitetura e versão; não expor ponteiros internos; validar buffers; definir comportamento de chamadas desconhecidas
- **Fluxo:** aplicação prepara argumentos; executa instrução de syscall; stub salva o necessário; kernel identifica serviço; valida argumentos; executa; retorna valor/erro
- **Riscos:** ordem de argumentos divergente; tamanho de inteiro inconsistente; ponteiro inválido; número de syscall reutilizado; retorno ambíguo; quebra de compatibilidade
- **Validação:** número válido; número desconhecido; argumentos ausentes; tamanho excessivo; ponteiro inválido; erro propagado; versão incompatível

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
