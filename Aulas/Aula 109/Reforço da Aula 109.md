# Reforço da Aula 109 — Quadros e páginas de memória física

## Ideia central

Distinguir páginas físicas de quadros físicos e organizar a memória em unidades de alocação consistentes. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

tamanho de página definido pela arquitetura; quadro físico; alinhamento; número do quadro (PFN); endereço-base; deslocamento; páginas parciais; regiões reservadas.

## Exemplo comentado

Com páginas de 4096 bytes, o endereço físico 0x12345 pertence ao quadro cujo início é 0x12000 e possui deslocamento 0x345. O quadro é identificado pelo PFN correspondente ao endereço-base dividido por 4096.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** escolher uma única unidade canônica para contabilidade; manter conversões explícitas entre endereço físico, PFN e deslocamento; não assumir que o primeiro PFN é zero
- **Fluxo:** receber intervalos elegíveis; alinhar limites; dividir em páginas completas; atribuir PFNs; marcar reservas; inserir quadros livres na estrutura escolhida
- **Riscos:** confundir página virtual com quadro físico; arredondar limites para o lado errado; overflow na multiplicação PFN*tamanho; incluir páginas parcialmente reservadas
- **Validação:** endereço alinhado; endereço desalinhado; primeira e última página; intervalo menor que uma página; multiplicação com overflow; quadro reservado; PFN máximo

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
