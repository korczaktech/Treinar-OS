# Sincronização, Flush e Barreiras de Escrita

## Objetivo

Na Aula 11 vimos que uma gravação pode permanecer pendente em cache mesmo depois de a camada superior receber uma confirmação inicial. Nesta aula vamos aprofundar a sincronização: como solicitar que dados pendentes avancem pelas camadas, por que a ordem importa e como definir garantias realistas de durabilidade.

## 1. As várias etapas de uma gravação

Uma gravação pode passar por:
1. aplicação ou sistema de arquivos;
2. cache do kernel;
3. fila do driver;
4. cache do controlador ou dispositivo;
5. mídia não volátil.

A conclusão em uma etapa não prova, sozinha, que todas as etapas seguintes terminaram. O contrato da interface precisa dizer o que foi garantido.

## 2. Flush

Flush é uma solicitação para encaminhar ou persistir gravações pendentes conforme as garantias do protocolo e do dispositivo. Não é simplesmente "limpar a RAM". O significado exato depende da interface.

Um flush bem-sucedido só oferece a garantia que o dispositivo e o caminho de armazenamento realmente implementam. Hardware defeituoso ou firmware que informa sucesso incorretamente pode quebrar a expectativa.

## 3. Ordenação

Imagine atualizar um arquivo:
1. gravar os dados novos;
2. atualizar o metadado que aponta para esses dados.

Se o metadado persistir antes dos dados, após uma queda o arquivo pode apontar para conteúdo incompleto. A ordem das gravações precisa respeitar as dependências.

## 4. Barreiras

Uma barreira de escrita estabelece uma fronteira de ordenação: operações anteriores precisam alcançar o ponto de garantia definido antes que operações posteriores ultrapassem essa fronteira.

Barreira não significa necessariamente que cada byte foi escrito imediatamente. Ela organiza a ordem e as garantias de conclusão.

## 5. Dependências e grupos

Uma atualização pode ser composta por várias gravações relacionadas. O sistema deve identificar quais dependem umas das outras. Não é seguro presumir que a ordem em que chamadas foram emitidas será sempre a ordem de persistência, especialmente com filas e caches.

## 6. Durabilidade e custo

Sincronizar frequentemente reduz a janela de perda, mas pode diminuir o desempenho. O projeto deve escolher pontos de sincronização de acordo com a importância dos dados e as garantias prometidas.

Dados temporários podem tolerar perda; metadados críticos de sistema de arquivos exigem cuidado muito maior.

## 7. Aplicação no ZenithOS

O ZenithOS precisa oferecer uma operação explícita de sincronização e documentar seu escopo: qual dispositivo, quais gravações anteriores, qual fila e qual garantia de persistência. A camada superior não deve interpretar um simples retorno de escrita como durabilidade.

## 8. Perguntas de compreensão

1. Por que uma gravação pode retornar antes da persistência física?
2. Para que serve um flush?
3. O que uma barreira de escrita organiza?
4. Por que dados precisam persistir antes de certos metadados?
5. Sincronizar toda gravação é sempre a melhor escolha? Por quê?
6. Por que a garantia depende também do dispositivo?

## 9. Exercícios de código

- EXN1A12.nbx — verificar se uma sequência de operações respeita dependências de ordenação.
- EXN2A12.nbx — modelar um grupo de gravações e identificar quais ainda precisam de sincronização.


## Método de estudo e exemplo guiado
Desenhe duas gravações: A grava os dados de um arquivo; B atualiza o metadado que aponta para esses dados. Marque a dependência A antes de B. Agora imagine que o dispositivo pode reordenar comandos. Identifique onde uma barreira ou flush é necessário e qual garantia precisa ser obtida antes de confirmar a atualização. Repita o raciocínio com dados temporários, que podem aceitar uma política menos rigorosa.

## Metadados da aula
- Dificuldade: Difícil
- Duração: 45 minutos
