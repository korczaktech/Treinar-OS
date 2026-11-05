# Agrupamento e divisão de requisições de I/O

## Objetivo

Nesta aula, você estudará agrupamento e divisão de requisições de i/o e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Agrupamento combina requisições compatíveis e contíguas para reduzir overhead. Divisão separa operações que excedem limites de transferência, buffer ou fila.

## 2. Exemplo de funcionamento

Agrupe apenas pedidos do mesmo dispositivo, com direção e semântica compatíveis e faixas contíguas. Na divisão, cada segmento recebe LBA e offset de buffer corretos; a soma dos segmentos deve reproduzir a solicitação original.

## 3. Validação e segurança

Não apagar prioridades, deadlines ou dependências durante agrupamento. A conclusão agregada deve comunicar falha parcial e quantidade efetivamente processada.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS pode implementar coalescência limitada na camada de blocos, com regras determinísticas e testes de entradas e saídas.

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
