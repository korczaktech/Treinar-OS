# Exercícios da Aula 80 — Inodes e identificação de arquivos: Falhas e testes

**Objetivo:** praticar identidade, geração, links, metadados e mapa de blocos e aplicar o raciocínio ao ZenithOS.

**Orientação:** responda com suas próprias palavras. Quando a questão pedir um desenho, tabela ou fluxo, inclua a representação e explique as decisões. Os enunciados não fornecem as soluções.

## Exercício 1 — Audite inconsistências

Analise casos de inode órfão, contador negativo, bloco repetido e diretório apontando para inode livre. Indique como detectar cada um.

**Atividade prática:** monte uma matriz com cenário, condição inicial, operação, resultado esperado e invariante protegido.

## Exercício 2 — Aplicação ao ZenithOS

Imagine que você está implementando inodes e identificação de arquivos no ZenithOS. Descreva como esse componente conversa com a camada anterior e com a próxima camada. Indique quais dados recebe, o que valida, o que modifica e o que devolve.

## Exercício 3 — Caso concreto

Crie um cenário pequeno com valores e objetos definidos, relacionado a identidade, geração, links, metadados e mapa de blocos. Resolva-o passo a passo e destaque os limites que precisam ser respeitados.

## Exercício 4 — Diagnóstico

Um teste do ZenithOS apresentou um comportamento incorreto relacionado ao tema desta aula. Proponha três causas possíveis, explique como distinguir cada uma e indique qual evidência coletaria antes de alterar o código.

## Exercício 5 — Decisão técnica

Apresente duas maneiras de resolver um problema relacionado ao conteúdo da aula. Compare simplicidade, custo, desempenho, segurança e dificuldade de manutenção. Escolha uma e justifique sem usar apenas a frase “é mais rápido”.

## Exercício 6 — Verificação de aprendizagem

Explique o conceito central sem copiar a aula. Depois, formule duas perguntas que alguém deveria saber responder antes de integrar esse componente ao kernel.


## Critério de conclusão

Considere os exercícios concluídos quando suas respostas estiverem justificadas, os cálculos puderem ser conferidos e os cenários inválidos tiverem resultados esperados explícitos. Não é necessário escrever código em todas as aulas.
