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

1. Por que não devemos gravar diretamente ponteiros de uma estrutura em memória?
2. O que significa serializar e desserializar metadados?
3. Quais informações o formato binário precisa definir além dos nomes dos campos?
4. Por que o padding de uma estrutura nativa pode causar incompatibilidade?
5. Qual é a diferença entre um offset persistente e um ponteiro virtual?
6. Como o parser deve reagir a uma versão desconhecida?

## 6. Estrutura em memória e formato persistente
Uma estrutura usada pelo kernel pode conter ponteiros, locks, referências e campos específicos da arquitetura. Esses elementos não devem ser gravados diretamente no disco como se fossem um formato estável. Endereços de memória mudam entre inicializações e não têm significado em outra execução.

O formato persistente deve descrever os dados usando campos explicitamente definidos, tamanhos fixos e referências relativas ao próprio volume ou arquivo.

## 7. Serialização
Serializar é transformar os campos de uma estrutura em uma sequência de bytes segundo uma regra definida. Desserializar é interpretar esses bytes novamente. O formato precisa definir ordem dos bytes (endianness), tamanhos, alinhamento, versão e significado dos campos reservados.

Padding automático da linguagem pode mudar entre compiladores ou arquiteturas. Por isso, não dependa do layout nativo de uma struct sem um contrato binário explícito.

## 8. Exemplo guiado
Um cabeçalho pode conter assinatura de 4 bytes, versão de 2 bytes, tamanho de 2 bytes e um offset de 8 bytes. O parser deve ler cada campo conforme a ordem definida e validar o offset antes de usá-lo. Não deve interpretar o offset como ponteiro direto.

## 9. Evolução de versões
Uma versão nova pode adicionar campos. O parser precisa verificar se conhece a versão e se o tamanho declarado comporta os campos obrigatórios. Campos desconhecidos só podem ser ignorados quando o formato permitir isso com segurança.

## 10. Método de aprendizagem
Faça uma tabela com nome do campo, tamanho, unidade, endianness, valores permitidos e regra de validação. Essa tabela é parte da especificação do formato.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
