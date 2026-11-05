# Reforço da Aula 149 — Permissões e proteção de memória

## Ideia central

Aplicar isolamento e privilégios aos mapeamentos para impedir leitura, escrita ou execução não autorizadas. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

R/W/X; user/supervisor; NX; W^X; permissões por página; privilégio mínimo; proteção de kernel; transições controladas.

## Exemplo comentado

Uma região de código normalmente recebe leitura e execução, mas não escrita; uma região de dados recebe leitura e escrita, mas não execução. A política W^X reduz superfícies de ataque.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** evitar páginas simultaneamente graváveis e executáveis quando possível; proteger kernel; validar mudanças de permissão; não confiar em checagem apenas em software
- **Fluxo:** definir política; criar mapeamento; CPU verifica privilégio e operação; violação gera exceção; kernel registra e decide resposta
- **Riscos:** página de código gravável; dado executável; usuário acessando kernel; mudança de permissão sem TLB invalidation; permissões inconsistentes entre região e página
- **Validação:** leitura válida; escrita proibida; execução proibida; usuário em página supervisor; NX; W^X; alteração de permissão e invalidação

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
