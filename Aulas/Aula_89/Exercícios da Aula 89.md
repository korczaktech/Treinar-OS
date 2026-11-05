# Exercícios da Aula 89 — Criação, abertura e remoção de arquivos: Implementação

**Objetivo:** praticar descritores, flags, referências abertas e unlink e aplicar o raciocínio ao ZenithOS.

**Orientação:** responda com suas próprias palavras. Quando a questão pedir um desenho, tabela ou fluxo, inclua a representação e explique as decisões. Os enunciados não fornecem as soluções.

## Exercício 1 — Desenhe o fluxo

Escreva os passos de criação atômica, desde validar o nome até publicar a entrada no diretório.

**Atividade prática:** escreva um plano de implementação em etapas pequenas. Para cada etapa, indique entradas, saídas, invariantes e testes.

## Exercício 2 — Aplicação ao ZenithOS

Imagine que você está implementando criação, abertura e remoção de arquivos no ZenithOS. Descreva como esse componente conversa com a camada anterior e com a próxima camada. Indique quais dados recebe, o que valida, o que modifica e o que devolve.

## Exercício 3 — Caso concreto

Crie um cenário pequeno com valores e objetos definidos, relacionado a descritores, flags, referências abertas e unlink. Resolva-o passo a passo e destaque os limites que precisam ser respeitados.

## Exercício 4 — Diagnóstico

Um teste do ZenithOS apresentou um comportamento incorreto relacionado ao tema desta aula. Proponha três causas possíveis, explique como distinguir cada uma e indique qual evidência coletaria antes de alterar o código.

## Exercício 5 — Decisão técnica

Apresente duas maneiras de resolver um problema relacionado ao conteúdo da aula. Compare simplicidade, custo, desempenho, segurança e dificuldade de manutenção. Escolha uma e justifique sem usar apenas a frase “é mais rápido”.

## Exercício 6 — Verificação de aprendizagem

Explique o conceito central sem copiar a aula. Depois, formule duas perguntas que alguém deveria saber responder antes de integrar esse componente ao kernel.

## Desafio opcional em Nebula (.nbx)

Crie um programa independente que valide uma regra numérica ou lógica relacionada ao assunto desta aula, usando valores fictícios. Exiba mensagens diferentes para entradas válidas e inválidas. Não implemente acesso a disco nem invente bibliotecas de sistema que ainda não existem na linguagem. Consulte a sintaxe atual do Nebula antes de escrever o código.

## Critério de conclusão

Considere os exercícios concluídos quando suas respostas estiverem justificadas, os cálculos puderem ser conferidos e os cenários inválidos tiverem resultados esperados explícitos. Não é necessário escrever código em todas as aulas.
