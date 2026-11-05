# Reforço da Aula 19 — Dispositivos Virtuais

## 1. Dispositivo não precisa ser hardware

Software pode apresentar uma interface de blocos e armazenar os dados em RAM ou encaminhar operações para outra unidade.

## 2. Disco em RAM

É rápido e útil para testes, mas normalmente perde o conteúdo quando a memória deixa de ser alimentada.

## 3. Simulação

Permite testar erros, atrasos, limites e remoção sem depender de um SSD real.

## 4. Capacidades

Uma interface comum não significa que todos suportam flush, discard ou os mesmos tamanhos de transferência. O sistema consulta o descritor.

## 5. Encadeamento

Uma camada pode encaminhar para outra, mas deve validar limites, impedir ciclos e propagar erros.

## 6. Fixação

1. Um disco em RAM é persistente?
2. Por que simular falhas?
3. O que o descritor informa sobre capacidades?
4. Qual problema um ciclo de encaminhamento pode causar?
5. Por que um dispositivo virtual tem identidade própria?
