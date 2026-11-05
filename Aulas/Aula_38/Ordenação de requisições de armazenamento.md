# Ordenação de requisições de armazenamento

## Objetivo

Nesta aula, você estudará ordenação de requisições de armazenamento e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Filas podem reordenar pedidos para reduzir overhead e explorar paralelismo. Entretanto, dependências precisam ser preservadas: metadados que apontam para um bloco recém-alocado não devem persistir antes dos dados necessários.

## 2. Exemplo de funcionamento

A camada superior define dependências e pontos de sincronização. O escalonador pode reorganizar operações independentes, mas barreiras e flushes estabelecem limites de ordenação e persistência.

## 3. Validação e segurança

Ordem de submissão não garante ordem de execução nem de persistência. O contrato do driver deve dizer o que a conclusão e o flush realmente garantem.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve representar dependências explicitamente e impedir que otimizações de fila violem consistência do sistema de arquivos.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Por que a ordem de submissão não garante a ordem de persistência?
2. Qual risco existe se metadados persistirem antes dos dados a que se referem?
3. Como representar dependências entre requisições?
4. O que uma barreira estabelece?
5. Qual é a diferença entre ordem de execução e ordem de persistência?
6. Por que o escalonador não pode reordenar operações sem considerar as dependências?

## 6. Dependências entre operações
Algumas requisições são independentes e podem ser reordenadas. Outras possuem dependências. Se um metadado passa a apontar para um bloco recém-alocado, a gravação do conteúdo ou a inicialização necessária pode precisar persistir antes do metadado.

O sistema de arquivos ou a camada que conhece a semântica da atualização define essas dependências. O escalonador não deve tentar deduzi-las apenas olhando para os LBAs.

## 7. Ordem de submissão, execução e persistência
São três ordens diferentes:
- ordem em que o kernel envia comandos;
- ordem em que o dispositivo executa ou conclui os comandos;
- ordem em que os dados se tornam persistentes.

Filas e caches podem alterar a relação entre elas. Barreiras e flushes estabelecem garantias específicas, mas só funcionam conforme o contrato do driver e do dispositivo.

## 8. Exemplo guiado
Operação A grava dados em um bloco. Operação B atualiza um metadado para apontar para esse bloco. Se B persistir antes de A e houver queda de energia, o metadado pode apontar para dados incompletos. O sistema precisa impor a dependência A antes de B no ponto de persistência adequado.

## 9. Método de aprendizagem
Desenhe um grafo de dependências. Cada operação é um nó; uma seta A → B significa que A precisa cumprir sua garantia antes de B ultrapassar a fronteira definida. Só reordene nós sem dependência.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
