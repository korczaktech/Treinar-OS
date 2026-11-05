# Reforço da Aula 13 — Operações Assíncronas e Filas

## 1. Não bloquear esperando

Uma operação assíncrona é enviada e sua conclusão chega depois. O solicitante pode realizar outro trabalho enquanto aguarda.

## 2. Fila

A fila organiza pedidos. Cada pedido precisa identificar dispositivo, faixa, direção, buffer e estado.

## 3. Identificador

Com várias operações ativas, o identificador permite descobrir a qual pedido pertence cada conclusão. Reutilizá-lo cedo demais pode confundir resultados.

## 4. Limites

Uma fila não pode crescer sem controle. Se estiver cheia, o sistema deve aplicar uma política definida.

## 5. Cancelamento

Solicitar cancelamento não prova que o hardware parou. O buffer continua protegido até que o sistema saiba que não será mais acessado.

## 6. Fixação

1. O que acontece depois do envio de uma operação assíncrona?
2. Para que serve o identificador?
3. O que significa profundidade máxima da fila?
4. Por que cancelamento solicitado não é cancelamento confirmado?
5. Uma fila garante que duas gravações conflitantes serão ordenadas corretamente?
