# Reforço da Aula 11 — Cache de Armazenamento e Coerência

## 1. Cache é uma cópia

O cache mantém dados temporariamente para acelerar acessos. Se a cópia não corresponder à versão atual, ela não pode ser usada como resposta correta.

## 2. Duas políticas de escrita

Write-through encaminha a gravação à próxima camada conforme o contrato e mantém o cache coerente. Write-back pode manter a alteração apenas em memória por algum tempo. É mais flexível, mas dados pendentes podem ser perdidos em uma queda de energia.

## 3. Entrada limpa e suja

Limpa: não possui modificação pendente. Suja: foi modificada e precisa ser sincronizada. Não descarte uma entrada suja sem concluir ou tratar a gravação.

## 4. Chave do cache

LBA 10 do dispositivo A não é o mesmo bloco que LBA 10 do dispositivo B. A identidade da unidade faz parte da chave.

## 5. Fixação

1. O cache substitui o armazenamento permanente?
2. Qual política pode manter gravações pendentes na RAM?
3. Por que uma leitura pode ficar desatualizada?
4. O que deve acontecer antes de remover uma entrada suja?
5. Por que dispositivo e LBA formam uma chave mais segura que LBA isolado?
