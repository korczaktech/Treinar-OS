# Aula 131 — TLB e tradução de endereços: fundamentos, finalidade e limites

## Objetivo

Ao final desta aula, você deverá ser capaz de explicar o cache de traduções do processador e manter coerência quando o kernel altera mapeamentos.

## Pré-requisitos

- Aulas anteriores da sequência de memória e processos, conforme o tema.
- Noções de endereços, intervalos, estruturas de dados e validação.
- Capacidade de acompanhar exemplos numéricos e representar estados em diagramas.

Não avance supondo que conceitos ainda não estudados estejam dominados. Se algum termo aparecer pela primeira vez, registre-o e consulte sua definição antes de implementar.

## 1. Contexto e responsabilidade

TLB e tradução de endereços faz parte da infraestrutura central do ZenithOS. Sua função é explicar o cache de traduções do processador e manter coerência quando o kernel altera mapeamentos. Esse componente não deve assumir responsabilidades que pertencem a outros módulos: a fronteira entre subsistemas precisa permanecer explícita.

O problema central desta aula é entender problema, finalidade, conceitos e limites. A solução correta depende de contratos bem definidos, entradas verificadas e estados que possam ser explicados. Em um kernel, um erro de contabilidade ou de validação pode comprometer processos que não participaram da operação original.

## 2. Conceitos essenciais

Translation Lookaside Buffer; hit/miss; page walk; contexto de endereço; ASID/PCID quando suportado; invalidação local e remota; custo de flush.

É importante separar conceito, política e mecanismo. O mecanismo executa a operação; a política decide quando ela é permitida; e o contrato define o que cada módulo pode esperar do outro. Misturar essas três coisas torna o componente difícil de testar e perigoso de alterar.

## 3. Representação e invariantes

metadados de contexto, identificador de espaço, geração de mapeamento e registros de invalidação.

Para cada campo, documente:
- significado e unidade;
- intervalo de valores permitido;
- quem é responsável por alterá-lo;
- quando o dado deixa de ser válido;
- como uma condição inválida será detectada.

Um invariante é uma condição que precisa continuar verdadeira antes e depois de cada operação concluída. Exemplos aplicáveis ao tema: nenhum recurso pode pertencer a dois donos exclusivos ao mesmo tempo; nenhum intervalo pode ultrapassar o limite representável; nenhuma referência pode apontar para um objeto já liberado.

## 4. Fundamentos, finalidade e limites

Comece definindo o problema que o componente resolve. Depois identifique o que ele controla, o que não controla e quais garantias dependem da arquitetura ou do protocolo escolhido.

Comece pelo cenário normal e compare-o com os casos em que o componente não deve atuar. Não confunda uma possibilidade do hardware com uma garantia oferecida pelo ZenithOS.

### Exemplo trabalhado

Se virtual X apontava para quadro A e passa a apontar para quadro B, uma entrada antiga no TLB pode continuar direcionando acessos para A até a invalidação apropriada.

**Raciocínio:** identifique primeiro as entradas e suas unidades; valide os limites; execute a transformação em uma cópia ou estado temporário; confira os invariantes; somente então publique o resultado. Esse método evita que um dado parcialmente processado se torne estado oficial.

## 5. Funcionamento e integração com outros subsistemas

acesso consulta TLB; em miss percorre tabelas; registra tradução; alteração de mapeamento atualiza tabelas e invalida entradas relevantes antes de reutilizar recursos.

No ZenithOS, o componente deverá comunicar-se por interfaces estreitas. O gerenciador de memória, o escalonador, o carregador e os mecanismos de entrada/saída não devem modificar diretamente estruturas internas uns dos outros. Uma interface deve definir quem solicita, quem valida, quem executa e quem mantém a propriedade do recurso.

## 6. Decisões de arquitetura para o ZenithOS

centralizar mudanças de mapeamento; escolher invalidação específica ou ampla conforme arquitetura; considerar CPUs múltiplas e identificadores de contexto.

Adote estas regras durante o projeto:
1. Valide dados na fronteira em que entram no kernel.
2. Use tipos e nomes que expressem unidades e propriedade.
3. Evite estado global mutável quando uma estrutura pertencente ao componente for suficiente.
4. Defina o comportamento de erro antes de implementar o caminho feliz.
5. Mantenha a lógica independente de hardware testável por simulação.
6. Registre decisões que dependem da arquitetura escolhida, sem apresentá-las como universais.

## 7. Falhas e riscos

Os erros mais relevantes neste tema incluem: usar tradução antiga após liberar quadro; invalidar apenas uma CPU; confundir flush de cache de dados com TLB; assumir que toda arquitetura oferece ASID.

Quando uma operação falhar, o kernel deve retornar um resultado coerente, preservar estruturas válidas e liberar apenas os recursos que realmente pertencem à operação interrompida. Não tente corrigir silenciosamente uma entrada ambígua se isso puder transformar uma região proibida em recurso utilizável.

## 8. Método de aprendizagem

1. Reescreva o objetivo da aula com suas próprias palavras.
2. Desenhe a estrutura principal e marque os campos e suas unidades.
3. Trace um caso normal do início ao fim.
4. Repita o fluxo com uma entrada inválida.
5. Identifique quais invariantes precisam ser conferidos.
6. Explique como o componente será isolado para testes no ZenithOS.

## 9. Exercícios de compreensão

Os exercícios específicos desta aula estão em **Exercícios da Aula 131.md**. Eles devem ser respondidos sem consultar uma solução pronta. Se não souber uma resposta, volte à seção correspondente e reconstrua o raciocínio antes de tentar novamente.

## 10. Exercício de código

O desafio de programação também está em **Exercícios da Aula 131.md**. Ele utiliza Nebula (.nbx) como linguagem de prática quando os recursos já estudados forem suficientes. Não invente bibliotecas, chamadas de kernel ou APIs que ainda não existem no projeto Nebula ou no ZenithOS. Se uma estrutura avançada ainda não estiver disponível na linguagem, implemente primeiro um modelo reduzido com variáveis, condições e repetições já aprendidas.

## 11. Critério de conclusão

Considere a aula concluída quando conseguir:
- explicar o objetivo e os limites do componente;
- descrever sua representação ou fluxo, conforme o foco da aula;
- trabalhar o exemplo sem pular as validações;
- identificar falhas e explicar como preservar os invariantes;
- resolver os exercícios de compreensão;
- implementar e explicar o desafio de código, sem copiar uma solução.

> **Dificuldade:** Média  
> **Duração estimada:** 45 minutos
