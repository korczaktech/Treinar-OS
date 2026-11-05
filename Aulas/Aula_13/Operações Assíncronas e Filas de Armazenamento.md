# Operações Assíncronas e Filas de Armazenamento

## Objetivo

Uma leitura não precisa bloquear a CPU até o dispositivo responder. Sistemas modernos podem enviar pedidos, continuar trabalhando e receber a conclusão depois. Nesta aula estudaremos operações assíncronas, filas, identificadores e concorrência.

## 1. Síncrono e assíncrono

Em uma operação síncrona, o solicitante espera o resultado antes de continuar naquele fluxo. Em uma operação assíncrona, ele envia o pedido e recebe a conclusão posteriormente por um mecanismo definido.

Assíncrono não significa necessariamente paralelo. Significa que o solicitante não precisa permanecer bloqueado aguardando cada etapa.

## 2. Fila de solicitações

Uma fila organiza pedidos aguardando processamento. Cada pedido precisa conter informações suficientes: dispositivo, LBA, quantidade, direção, buffer, identificador e estado.

O driver pode retirar pedidos da fila e submetê-los ao dispositivo conforme os limites da interface.

## 3. Identificadores e correlação

Se várias operações estiverem em andamento, a conclusão precisa ser associada ao pedido correto. Um identificador único durante a vida da operação permite correlacionar solicitação e resultado.

Não reutilize um identificador enquanto ainda houver possibilidade de uma conclusão antiga chegar e ser confundida com uma nova operação.

## 4. Concorrência

Duas solicitações podem acessar regiões diferentes ao mesmo tempo. Se acessarem a mesma região, podem existir dependências ou conflitos. O sistema precisa definir regras de ordenação, bloqueio ou coordenação.

A fila não resolve sozinha a coerência dos dados.

## 5. Limites de fila

O dispositivo pode aceitar apenas certa quantidade de pedidos simultâneos. O driver precisa respeitar profundidade máxima, tamanho de transferência e recursos disponíveis.

Quando a fila está cheia, o sistema pode aguardar, rejeitar temporariamente ou manter a solicitação em uma fila superior. A política deve evitar crescimento ilimitado de memória.

## 6. Cancelamento e conclusão tardia

Cancelar uma operação não significa que o hardware parou imediatamente. A interface pode não suportar cancelamento real depois da submissão. O sistema deve distinguir pedido de cancelamento, cancelamento confirmado e conclusão normal que chegou antes.

Buffers não podem ser liberados enquanto o dispositivo ainda puder acessá-los.

## 7. Aplicação no ZenithOS

A camada de armazenamento pode expor uma API assíncrona com identificador e resultado futuro ou callback. O contrato deve definir propriedade do buffer, vida útil, cancelamento, erros e momento da conclusão.

## 8. Perguntas de compreensão

1. Qual a diferença entre síncrono e assíncrono?
2. Por que cada operação precisa de identificador?
3. Uma fila impede conflitos entre duas gravações no mesmo bloco?
4. O que fazer quando a fila atinge seu limite?
5. Por que não liberar um buffer logo após pedir cancelamento?
6. Assíncrono significa que tudo acontece em paralelo?

## 9. Exercícios de código

- EXN1A13.nbx — modelar fila limitada de solicitações.
- EXN2A13.nbx — correlacionar identificadores e conclusões sem reutilização prematura.


## Método de estudo e exemplo guiado
Envie três pedidos com identificadores 10, 11 e 12. Simule as conclusões chegando na ordem 12, 10 e 11. O sistema deve associar cada resultado ao pedido correto, independentemente da ordem de conclusão. Depois limite a fila a dois pedidos e decida como tratar o terceiro. Simule cancelamento e uma conclusão tardia para verificar se o buffer continua protegido.

## Metadados da aula
- Dificuldade: Difícil
- Duração: 45 minutos
