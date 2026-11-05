# Aula 105 — Mapa físico e descoberta de memória: falhas, validação e testes

## Objetivo

Ao final desta aula, você deverá ser capaz de interpretar a descrição de regiões físicas fornecida no boot e convertê-la, após validação e reservas, em intervalos seguros para o gerenciador de memória.

## Pré-requisitos

- Aulas anteriores da sequência de memória e processos, conforme o tema.
- Noções de endereços, intervalos, estruturas de dados e validação.
- Capacidade de acompanhar exemplos numéricos e representar estados em diagramas.

Não avance supondo que conceitos ainda não estudados estejam dominados. Se algum termo aparecer pela primeira vez, registre-o e consulte sua definição antes de implementar.

## 1. Contexto e responsabilidade

Mapa físico e descoberta de memória faz parte da infraestrutura central do ZenithOS. Sua função é interpretar a descrição de regiões físicas fornecida no boot e convertê-la, após validação e reservas, em intervalos seguros para o gerenciador de memória. Esse componente não deve assumir responsabilidades que pertencem a outros módulos: a fronteira entre subsistemas precisa permanecer explícita.

O problema central desta aula é entender undefined. A solução correta depende de contratos bem definidos, entradas verificadas e estados que possam ser explicados. Em um kernel, um erro de contabilidade ou de validação pode comprometer processos que não participaram da operação original.

## 2. Conceitos essenciais

mapa fornecido pelo firmware ou bootloader; tipos de região; intervalos com limite exclusivo; overflow; ordenação; sobreposição; regiões desconhecidas; reservas do kernel, bootloader, tabelas e framebuffer.

É importante separar conceito, política e mecanismo. O mecanismo executa a operação; a política decide quando ela é permitida; e o contrato define o que cada módulo pode esperar do outro. Misturar essas três coisas torna o componente difícil de testar e perigoso de alterar.

## 3. Representação e invariantes

entrada bruta do mapa, descritor normalizado com início, limite exclusivo e tipo, lista de reservas e relatório de rejeições.

Para cada campo, documente:
- significado e unidade;
- intervalo de valores permitido;
- quem é responsável por alterá-lo;
- quando o dado deixa de ser válido;
- como uma condição inválida será detectada.

Um invariante é uma condição que precisa continuar verdadeira antes e depois de cada operação concluída. Exemplos aplicáveis ao tema: nenhum recurso pode pertencer a dois donos exclusivos ao mesmo tempo; nenhum intervalo pode ultrapassar o limite representável; nenhuma referência pode apontar para um objeto já liberado.

## 4. Falhas, validação e testes

Liste entradas válidas, inválidas e extremas. Para cada caso, defina o resultado esperado e o estado que deve permanecer intacto. Teste primeiro a lógica isolada e depois as interações entre componentes.

Um teste não deve verificar apenas o retorno. Também deve verificar filas, contadores, referências e recursos que deveriam permanecer inalterados após uma falha.

### Exemplo trabalhado

Considere uma região [0x100000, 0x500000) e uma reserva [0x280000, 0x300000). A memória elegível precisa ser dividida em [0x100000, 0x280000) e [0x300000, 0x500000), antes de aplicar alinhamento de páginas.

**Raciocínio:** identifique primeiro as entradas e suas unidades; valide os limites; execute a transformação em uma cópia ou estado temporário; confira os invariantes; somente então publique o resultado. Esse método evita que um dado parcialmente processado se torne estado oficial.

## 5. Funcionamento e integração com outros subsistemas

receber bytes; validar cabeçalho e tamanho; decodificar entradas; validar aritmética; classificar tipos; ordenar; detectar conflitos; subtrair reservas; publicar somente intervalos utilizáveis.

No ZenithOS, o componente deverá comunicar-se por interfaces estreitas. O gerenciador de memória, o escalonador, o carregador e os mecanismos de entrada/saída não devem modificar diretamente estruturas internas uns dos outros. Uma interface deve definir quem solicita, quem valida, quem executa e quem mantém a propriedade do recurso.

## 6. Decisões de arquitetura para o ZenithOS

manter parser, normalizador e política de reservas separados; preservar cópia original para diagnóstico; não permitir que o parser escreva diretamente no alocador.

Adote estas regras durante o projeto:
1. Valide dados na fronteira em que entram no kernel.
2. Use tipos e nomes que expressem unidades e propriedade.
3. Evite estado global mutável quando uma estrutura pertencente ao componente for suficiente.
4. Defina o comportamento de erro antes de implementar o caminho feliz.
5. Mantenha a lógica independente de hardware testável por simulação.
6. Registre decisões que dependem da arquitetura escolhida, sem apresentá-las como universais.

## 7. Falhas e riscos

Os erros mais relevantes neste tema incluem: overflow em início+tamanho; mapa truncado; entradas duplicadas; tipos desconhecidos tratados como livres; mapa não ordenado; reservas esquecidas.

Quando uma operação falhar, o kernel deve retornar um resultado coerente, preservar estruturas válidas e liberar apenas os recursos que realmente pertencem à operação interrompida. Não tente corrigir silenciosamente uma entrada ambígua se isso puder transformar uma região proibida em recurso utilizável.

## 8. Método de aprendizagem

1. Reescreva o objetivo da aula com suas próprias palavras.
2. Desenhe a estrutura principal e marque os campos e suas unidades.
3. Trace um caso normal do início ao fim.
4. Repita o fluxo com uma entrada inválida.
5. Identifique quais invariantes precisam ser conferidos.
6. Explique como o componente será isolado para testes no ZenithOS.

## 9. Exercícios de compreensão

Os exercícios específicos desta aula estão em **Exercícios da Aula 105.md**. Eles devem ser respondidos sem consultar uma solução pronta. Se não souber uma resposta, volte à seção correspondente e reconstrua o raciocínio antes de tentar novamente.

## 10. Exercício de código

O desafio de programação também está em **Exercícios da Aula 105.md**. Ele utiliza Nebula (.nbx) como linguagem de prática quando os recursos já estudados forem suficientes. Não invente bibliotecas, chamadas de kernel ou APIs que ainda não existem no projeto Nebula ou no ZenithOS. Se uma estrutura avançada ainda não estiver disponível na linguagem, implemente primeiro um modelo reduzido com variáveis, condições e repetições já aprendidas.

## 11. Critério de conclusão

Considere a aula concluída quando conseguir:
- explicar o objetivo e os limites do componente;
- descrever sua representação ou fluxo, conforme o foco da aula;
- trabalhar o exemplo sem pular as validações;
- identificar falhas e explicar como preservar os invariantes;
- resolver os exercícios de compreensão;
- implementar e explicar o desafio de código, sem copiar uma solução.

> **Dificuldade:** Muito difícil  
> **Duração estimada:** 60 minutos
