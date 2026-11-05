# Reforço da Aula 47 — Snapshots em nível de bloco

## O que é preservado?
Snapshot mantém uma visão anterior do volume. Copy-on-write preserva a versão antiga antes de permitir que o volume ativo grave uma versão nova.

## Exemplo
O volume e o snapshot apontam para o bloco X. O volume altera X de A para B. A versão A é preservada para o snapshot; o volume ativo passa a ver B.

## Cuidados
Snapshots ocupam espaço e metadados. Podem reter blocos antigos mesmo após exclusão no volume ativo. Não são backup e precisam de coordenação para consistência.

## Perguntas
1. O que é copy-on-write?
2. Por que um snapshot mantém dados que o volume ativo já liberou?
3. O que deve ocorrer se o espaço reservado acabar?
4. Snapshot substitui backup?
5. Como garantir uma visão consistente para uma aplicação?
