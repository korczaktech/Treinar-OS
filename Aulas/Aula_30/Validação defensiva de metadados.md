# Validação defensiva de metadados

## Objetivo

Nesta aula, você estudará validação defensiva de metadados e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Metadados lidos do disco são entrada não confiável. Corrupção, falhas de energia, defeitos e adulteração podem produzir tamanhos, offsets, contagens e referências inconsistentes.

## 2. Exemplo de funcionamento

Um parser valida assinatura, versão, tamanho mínimo e máximo, intervalos, alinhamento, referências, ciclos e limites de profundidade. Um cabeçalho válido não torna automaticamente válidas as estruturas que ele aponta.

## 3. Validação e segurança

Limitar consumo de memória e CPU. Detectar somas com overflow, referências inexistentes, ciclos e estruturas profundamente aninhadas. Ao encontrar inconsistência, interromper com erro claro em vez de adivinhar uma interpretação.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

No ZenithOS, parsers devem ser funções testáveis e não devem corrigir o disco automaticamente. Diagnóstico e recuperação são operações separadas.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Por que metadados lidos do disco devem ser tratados como entrada não confiável?
2. Qual é a ordem segura para validar cabeçalho, tamanho, offset e matriz?
3. Como uma multiplicação de contagem por tamanho pode provocar overflow?
4. Por que ciclos e profundidade excessiva precisam ser detectados?
5. Qual é a diferença entre parser, diagnóstico e reparador?
6. O que deve acontecer quando um campo essencial é inconsistente?

## 6. Validação em etapas
Um parser defensivo não tenta interpretar tudo de uma vez. Ele avança por etapas:
1. verifica se o buffer possui o tamanho mínimo para o cabeçalho;
2. valida assinatura e versão;
3. valida tamanho declarado e limites máximos;
4. verifica multiplicações e somas sem overflow;
5. valida offsets e intervalos contra o tamanho do volume;
6. valida referências entre estruturas;
7. detecta ciclos e profundidade excessiva;
8. só então cria objetos internos para uso pelo kernel.

Cada etapa depende das anteriores. Não use um campo de tamanho para alocar memória antes de impor limites.

## 7. Consumo de recursos também é segurança
Um metadado pode ser pequeno, mas declarar milhões de entradas, cadeias muito profundas ou ciclos. O parser precisa limitar memória, tempo de CPU, quantidade de nós e profundidade de recursão. Um formato malformado não pode travar o sistema.

## 8. Exemplo guiado
Um cabeçalho declara que a matriz começa no byte 4.096 e possui 100 entradas de 128 bytes. A matriz exige 12.800 bytes. Antes de ler, verifique a multiplicação, a soma do offset com o tamanho e se o intervalo completo cabe no volume. Se qualquer condição falhar, retorne erro sem acessar a região.

## 9. Diagnóstico separado de reparo
Parser deve interpretar e validar. Diagnóstico explica o que está inconsistente. Recuperação decide se existe uma fonte confiável para restaurar. Reparo altera dados persistentes e precisa de política explícita, autorização e proteção contra interrupções.

## 10. Método de aprendizagem
Para cada campo do formato, pergunte: pode controlar um tamanho? pode controlar um endereço? pode criar uma referência? pode consumir recursos? Defina uma validação para cada risco.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
