# Reforço da Aula 12 — Sincronização, Flush e Barreiras de Escrita

## 1. Retorno não é necessariamente persistência

Uma gravação pode estar apenas no cache do kernel ou do dispositivo. É necessário conhecer o contrato da operação.

## 2. Flush

Solicita que gravações pendentes avancem até o ponto de persistência garantido pela interface. Não é uma promessa mágica: depende do dispositivo e do protocolo.

## 3. Ordem importa

Se um metadado aponta para dados novos, os dados precisam estar seguros antes de tornar essa referência persistente. Caso contrário, uma queda pode deixar uma referência sem conteúdo válido.

## 4. Barreira

Uma barreira separa operações anteriores e posteriores segundo uma regra de ordenação. Ela evita que dependências sejam violadas pelo reordenamento.

## 5. Fixação

1. O que pode permanecer pendente depois de uma escrita?
2. O que o flush solicita?
3. Por que a ordem entre dados e metadados importa?
4. Uma barreira é igual a uma gravação?
5. Qual é o custo de sincronizar a todo instante?


## Exemplo guiado: dados antes do metadado
A operação A grava o conteúdo de um arquivo. A operação B atualiza o metadado que aponta para esse conteúdo. Se B persistir primeiro, uma queda pode deixar uma referência para dados incompletos. A dependência exige que A alcance a garantia necessária antes de B ultrapassar a fronteira.

## Como revisar
Escreva as operações em ordem, marque as dependências e indique onde o flush/barreira é necessário. Diferencie envio, conclusão e persistência.