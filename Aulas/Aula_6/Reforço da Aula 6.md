# Reforço da Aula 6 — Leitura e Escrita de Blocos

## 1. Direção dos dados

Leitura: dispositivo para memória. Gravação: memória para dispositivo. O buffer é o ponto de encontro dos dados com a operação.

## 2. Exemplo de leitura

Uma leitura pede 2 blocos de 512 bytes. O tamanho esperado é 1024 bytes. O buffer precisa ter pelo menos essa capacidade. Se tiver 800 bytes, a operação deve ser rejeitada antes de começar.

## 3. Exemplo de gravação

Se o buffer contém 1024 bytes e a operação grava 2 blocos de 512 bytes, o buffer é a origem e o dispositivo é o destino.

## 4. Camada e driver

A camada de armazenamento recebe uma solicitação genérica, valida seus parâmetros e seleciona o driver. O driver traduz o pedido para a interface do dispositivo. Isso evita que o sistema de arquivos dependa de detalhes de cada controlador.

## 5. Estados não são resultados

VALIDADA significa que os parâmetros passaram pelas verificações. EM_EXECUCAO significa que o trabalho começou. CONCLUIDA significa que o mecanismo reportou sucesso segundo seu contrato. Uma operação pode ser validada e depois falhar.

## 6. Perguntas de fixação

1. Em uma leitura, quem fornece os dados?
2. Em uma gravação, quem contém inicialmente os dados?
3. Por que 900 bytes não comportam 2 blocos de 512 bytes?
4. Qual é a diferença entre erro de validação e erro de execução?
5. Por que uma operação em execução não deve aparecer como concluída?
6. Para que serve um dispositivo simulado nos testes?
