# Reforço da Aula 183 — Carregamento de executáveis

## Ideia central

Entender como o kernel valida um arquivo executável e transforma sua imagem em um processo pronto para iniciar. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

formato executável; cabeçalho; arquitetura; ponto de entrada; segmentos; tamanho em arquivo e memória; relocação quando aplicável; dependências; rejeição.

## Exemplo comentado

Se um segmento declara offset 0x800 e tamanho 0x400, o parser precisa confirmar que todo o intervalo está dentro do arquivo antes de copiar qualquer byte.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** separar parser do carregador; validar todos os offsets e tamanhos antes de ler; limitar recursos; nunca executar arquivo parcialmente validado
- **Fluxo:** abrir arquivo; validar cabeçalho; conferir arquitetura e formato; validar tabelas; reservar espaço virtual; mapear/carregar segmentos; preparar pilha; definir entry point
- **Riscos:** offset fora do arquivo; soma com overflow; segmento sobreposto; ponto de entrada fora de região executável; arquivo truncado; arquitetura errada
- **Validação:** magic inválido; cabeçalho truncado; offset fora do arquivo; overflow; segmento vazio; segmento sobreposto; entry point inválido

## Perguntas para revisão ativa

1. Qual é o primeiro evento que inicia o fluxo?
2. Quais etapas são obrigatórias e em que ordem?
3. Quais componentes são chamados e quais dados atravessam cada fronteira?
4. Em que ponto o estado se torna visível para outros componentes?
5. Como o fluxo reage a interrupção, erro ou falta de recurso?
6. Quais operações precisam ser atômicas ou protegidas?

## Exercício rápido de recuperação

Sem olhar a aula principal, desenhe um fluxograma com caminhos de sucesso, erro e recuperação. Depois compare seu desenho com as estruturas, fluxo e invariantes descritos na aula. Corrija o que estiver incompleto e explique em voz alta por que cada etapa existe.

## Quando revisar novamente

Faça uma revisão curta no dia seguinte e outra alguns dias depois. Em cada revisão, tente reconstruir o fluxo sem reler o texto primeiro. Consulte o material apenas para corrigir lacunas.
