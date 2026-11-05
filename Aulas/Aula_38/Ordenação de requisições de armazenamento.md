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

1. Qual problema esta aula procura resolver?
2. Quais informações precisam ser conhecidas antes de executar a operação estudada?
3. Que dado inválido poderia causar acesso fora dos limites ou perda de consistência?
4. Qual responsabilidade pertence ao ZenithOS e qual pertence ao driver?
5. Que teste automatizado ajudaria a detectar uma implementação incorreta?

## 6. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Difícil
> - **Duração:** 55 minutos
