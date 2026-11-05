# Reforço da Aula 140 — Falhas de página e tratamento

## Ideia central

Distinguir falhas de tradução e proteção e construir uma resposta segura do kernel a acessos inválidos ou ainda não carregados. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

page fault; endereço causador; presença; permissões; demanda; copy-on-write; página inválida; pilha em crescimento; recuperação versus encerramento.

## Exemplo comentado

Uma leitura em página válida sob demanda pode provocar carregamento e retomada. Uma escrita em região somente leitura deve gerar proteção, não concessão automática de escrita.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** separar classificação da falha de ações de alocação; impedir recursão descontrolada no handler; definir política para falhas no kernel
- **Fluxo:** CPU gera exceção; handler salva contexto; identifica endereço e causa; consulta região; decide mapear, copiar, negar ou encerrar; retoma apenas se estado for consistente
- **Riscos:** mapear qualquer endereço solicitado; ignorar escrita em página somente leitura; falha durante tratamento; loop infinito de retentativa; confundir ausência com violação de permissão
- **Validação:** página ausente válida; endereço fora de região; escrita proibida; copy-on-write; falha durante handler; falha no modo kernel; falta de quadros

## Perguntas para revisão ativa

1. Quais entradas malformadas devem ser rejeitadas?
2. Quais limites numéricos e de capacidade precisam ser testados?
3. Como detectar corrupção, duplicidade ou uso após liberação?
4. O que precisa ser revertido quando uma etapa falha?
5. Como provar que o erro não deixou recursos vazados?
6. Quais invariantes podem ser verificados automaticamente?

## Exercício rápido de recuperação

Sem olhar a aula principal, desenhe uma matriz de testes com entradas, resultado esperado, estado posterior e critério de aprovação. Depois compare seu desenho com as estruturas, fluxo e invariantes descritos na aula. Corrija o que estiver incompleto e explique em voz alta por que cada etapa existe.

## Quando revisar novamente

Faça uma revisão curta no dia seguinte e outra alguns dias depois. Em cada revisão, tente reconstruir o fluxo sem reler o texto primeiro. Consulte o material apenas para corrigir lacunas.
