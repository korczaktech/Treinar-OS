# Exercícios da Aula 95 — Leitura, escrita e truncamento de arquivos: Falhas e testes

**Objetivo:** praticar offset, EOF, operações parciais, extensão e truncamento e aplicar o raciocínio ao ZenithOS.

**Orientação:** responda com suas próprias palavras. Quando a questão pedir um desenho, tabela ou fluxo, inclua a representação e explique as decisões. Os enunciados não fornecem as soluções.

## Exercício 1 — Teste limites

Crie testes para EOF, offset além do EOF, overflow offset+quantidade, buffer inválido, escrita parcial e falha em bloco intermediário.

**Atividade prática:** monte uma matriz com cenário, condição inicial, operação, resultado esperado e invariante protegido.

## Exercício 2 — Aplicação ao ZenithOS

Imagine que você está implementando leitura, escrita e truncamento de arquivos no ZenithOS. Descreva como esse componente conversa com a camada anterior e com a próxima camada. Indique quais dados recebe, o que valida, o que modifica e o que devolve.

## Exercício 3 — Caso concreto

Crie um cenário pequeno com valores e objetos definidos, relacionado a offset, EOF, operações parciais, extensão e truncamento. Resolva-o passo a passo e destaque os limites que precisam ser respeitados.

## Exercício 4 — Diagnóstico

Um teste do ZenithOS apresentou um comportamento incorreto relacionado ao tema desta aula. Proponha três causas possíveis, explique como distinguir cada uma e indique qual evidência coletaria antes de alterar o código.

## Exercício 5 — Decisão técnica

Apresente duas maneiras de resolver um problema relacionado ao conteúdo da aula. Compare simplicidade, custo, desempenho, segurança e dificuldade de manutenção. Escolha uma e justifique sem usar apenas a frase “é mais rápido”.

## Exercício 6 — Verificação de aprendizagem

Explique o conceito central sem copiar a aula. Depois, formule duas perguntas que alguém deveria saber responder antes de integrar esse componente ao kernel.


## Critério de conclusão

Considere os exercícios concluídos quando suas respostas estiverem justificadas, os cálculos puderem ser conferidos e os cenários inválidos tiverem resultados esperados explícitos. Não é necessário escrever código em todas as aulas.
