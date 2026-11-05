# Aula 8 — Fluxo de leitura e escrita de blocos

## Objetivos
Acompanhar operações de leitura e gravação, entender a direção dos dados, identificar os elementos de uma requisição e conhecer as validações anteriores ao acesso ao dispositivo.

## 1. O que é uma operação de bloco?
A camada de armazenamento oferece operações sobre unidades lógicas endereçadas por LBA. Uma requisição identifica o dispositivo, o LBA inicial, a quantidade de blocos, a direção e o buffer de memória usado na transferência.

A camada não deve receber apenas “leia alguma coisa”. Ela precisa saber de qual dispositivo, de qual faixa e para qual região de memória a operação será feita.

## 2. Caminho de uma leitura
Na leitura, os dados saem do dispositivo e chegam à memória:
1. uma camada superior solicita dados;
2. a camada de blocos valida dispositivo, faixa e buffer;
3. o driver prepara o comando da interface;
4. o controlador executa a leitura;
5. os dados são transferidos para o buffer;
6. o driver verifica o resultado e informa a conclusão;
7. a camada superior recebe os dados ou um erro.

Exemplo: dois blocos de 512 bytes exigem um buffer com pelo menos 1.024 bytes. Se o buffer possui somente 800 bytes, a solicitação deve ser rejeitada antes da transferência.

## 3. Caminho de uma gravação
Na gravação, a direção é inversa: os dados saem do buffer de memória e são enviados ao dispositivo. O buffer precisa conter todos os bytes solicitados e permanecer válido enquanto o dispositivo puder acessá-lo.

Exemplo: gravar 3 blocos de 4.096 bytes exige 12.288 bytes de origem. O driver não deve ler além dessa região.

## 4. Campos de uma requisição
Uma estrutura didática pode conter identificador da requisição, identificador do dispositivo, LBA inicial, quantidade de blocos, tamanho lógico, direção, referência do buffer, capacidade do buffer, estado e resultado.

O tamanho total esperado é quantidade multiplicada pelo tamanho lógico. A multiplicação precisa ser validada para evitar overflow.

## 5. Estados da operação
Uma operação pode passar por criada, validada, em execução e concluída. Também pode falhar ou ser cancelada quando o contrato permitir. Validada não significa concluída: significa apenas que os parâmetros passaram pelas verificações iniciais.

O resultado precisa informar sucesso ou erro. Em operações que permitem conclusão parcial, também deve indicar quantos blocos foram efetivamente transferidos.

## 6. Validação antes de enviar
Verifique se o dispositivo existe e está disponível; se LBA e quantidade são válidos; se a faixa cabe na capacidade; se o buffer é suficiente e acessível; se sua vida útil é adequada; e se o dispositivo suporta os limites da operação.

## 7. Aplicação no ZenithOS
O ZenithOS deve definir uma estrutura comum de requisição de bloco. Drivers traduzem essa estrutura para SATA, NVMe ou outra interface. O sistema de arquivos não precisa conhecer os detalhes de cada controlador.

## 8. Método de estudo
Desenhe duas setas: dispositivo para memória em uma leitura e memória para dispositivo em uma gravação. Para cada exemplo, calcule o tamanho em bytes, valide o buffer e percorra as etapas.

## 9. Erros comuns
Inverter a direção dos dados; confundir LBA com deslocamento em bytes; aceitar buffer menor que a transferência; liberar o buffer antes da conclusão; tratar validação como garantia de sucesso do hardware.

## 10. Exercícios de compreensão
1. Em uma leitura, qual é a origem e qual é o destino dos dados?
2. Em uma gravação, por que o buffer precisa permanecer válido?
3. Quantos bytes são necessários para transferir 3 blocos de 4.096 bytes?
4. Por que uma requisição precisa identificar dispositivo e LBA?
5. Qual é a diferença entre uma operação validada e uma operação concluída?
6. Que informação deve ser devolvida quando apenas parte da transferência foi concluída?

## 11. Exercícios de código
- EXN1A8.nbx: validar o tamanho de um buffer para uma transferência.
- EXN2A8.nbx: modelar as etapas e estados de uma requisição de leitura ou gravação.

## Critério de conclusão
Você deve explicar as duas direções, calcular o tamanho da transferência e apontar as verificações necessárias antes de encaminhar uma requisição.

## Metadados
- Dificuldade: Média
- Duração: 35 minutos
