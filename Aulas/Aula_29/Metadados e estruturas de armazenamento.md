# Metadados e estruturas de armazenamento

## Objetivo

Nesta aula, você estudará metadados e estruturas de armazenamento e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Metadados descrevem dados e organização: cabeçalhos, superblocos, mapas de espaço livre, diretórios, registros de arquivos, índices e estados. Estruturas persistentes em disco não são iguais às estruturas temporárias em memória.

## 2. Exemplo de funcionamento

Um formato binário precisa definir tamanho, versão, ordem dos campos, endianness, alinhamento e significado dos campos reservados. Gravar diretamente uma estrutura nativa da linguagem pode introduzir padding e incompatibilidades entre versões.

## 3. Validação e segurança

Validar campos antes de usá-los como tamanho, índice ou endereço. Ponteiros, locks e referências internas da memória nunca devem ser serializados como se fossem metadados persistentes.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve especificar formatos binários versionados e implementar serialização explícita. Estruturas internas podem mudar sem alterar o formato no disco.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Qual problema esta aula procura resolver?
2. Quais informações precisam ser conhecidas antes de executar a operação estudada?
3. Que dado inválido poderia causar acesso fora dos limites ou perda de consistência?
4. Qual responsabilidade pertence ao ZenithOS e qual pertence ao driver?
5. Que teste automatizado ajudaria a detectar uma implementação incorreta?

## 6. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
