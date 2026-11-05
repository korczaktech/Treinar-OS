# Reforço da Aula 33 — Capacidades anunciadas por dispositivos

## O que deve ser consultado?
Capacidade, tamanho lógico, tamanho físico quando disponível, máximo de transferência, alinhamento, profundidade de fila e suporte a flush ou discard.

## Três estados
Suportado significa que a interface declara o recurso. Não suportado significa que a interface informa sua ausência. Desconhecido significa que não há informação suficiente. Não trate desconhecido como suportado.

## Exemplo
Se o máximo por comando é 128 blocos, uma requisição maior precisa ser dividida. Se discard é desconhecido, não envie esse comando.

## Perguntas
1. Cite quatro capacidades importantes.
2. Por que unidades dos limites precisam ser explícitas?
3. Suporte declarado garante sucesso de toda operação?
4. Como tratar um recurso desconhecido?
5. Por que normalizar capacidades em um descritor comum?
