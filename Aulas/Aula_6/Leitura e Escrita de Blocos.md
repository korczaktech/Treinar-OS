# Leitura e Escrita de Blocos

## Objetivo

Nesta aula vamos acompanhar uma operação de leitura ou gravação desde o pedido inicial até sua conclusão. O foco é compreender o papel do buffer, os campos de uma solicitação, a comunicação entre camada de armazenamento e driver e os estados de uma operação.

## 1. Leitura e gravação são direções opostas

Uma leitura traz dados do dispositivo para a memória. Uma gravação envia dados da memória para o dispositivo.

Na leitura, o buffer recebe os bytes. Na gravação, o buffer fornece os bytes. A direção precisa estar clara para evitar que o sistema use a região errada como origem ou destino.

## 2. O que é um buffer?

Buffer é uma região de memória temporária associada à operação. Se o dispositivo apresenta blocos de 4096 bytes e a solicitação pede 3 blocos, o volume esperado é 12.288 bytes.

Um buffer menor não comporta a operação inteira. A camada deve validar sua capacidade antes de encaminhar o pedido. Também pode ser necessário validar alinhamento e limites de endereço, conforme o mecanismo de transferência.

## 3. Descritor de operação

Uma solicitação pode ser representada por uma estrutura com:
- identificador do dispositivo;
- LBA inicial;
- quantidade de blocos;
- direção (leitura ou gravação);
- endereço ou referência do buffer;
- capacidade do buffer;
- estado atual;
- resultado ou código de erro.

O descritor representa a operação, não o conteúdo do arquivo nem os bytes transferidos.

## 4. Fluxo de leitura

Um fluxo simplificado no ZenithOS:
1. Um componente solicita uma leitura.
2. A camada de armazenamento recebe dispositivo, LBA, quantidade e buffer.
3. A camada valida os parâmetros, a faixa e a capacidade do buffer.
4. A camada encaminha o pedido ao driver adequado.
5. O driver prepara a operação conforme a interface do dispositivo.
6. O dispositivo executa a leitura.
7. O driver identifica conclusão ou falha.
8. A camada comunica o resultado ao solicitante.

O mecanismo real pode usar interrupções, filas, polling ou DMA. Nem toda operação é necessariamente síncrona.

## 5. Fluxo de gravação

Na gravação, o buffer contém os dados que serão enviados. A camada valida o pedido, o driver prepara a transferência e o dispositivo executa a operação. Depois, o resultado retorna pelas camadas.

Não confunda dados enviados com dados garantidamente persistidos. Caches do sistema ou do dispositivo podem fazer com que a conclusão de uma etapa não represente ainda a persistência em mídia não volátil. Esse problema será aprofundado na Aula 10.

## 6. Estados de uma operação

Um modelo didático pode conter:
- CRIADA: solicitação recebida;
- VALIDADA: parâmetros aprovados;
- EM_EXECUCAO: trabalho iniciado;
- CONCLUIDA: operação terminou com sucesso;
- FALHOU: operação terminou com erro;
- CANCELADA: operação interrompida antes da execução, se o mecanismo permitir.

Uma operação em execução ainda não está concluída. Estados finais não devem voltar para execução. As transições precisam ser definidas no contrato do sistema.

## 7. Erros antes e durante a execução

Erros detectáveis antes do hardware:
- dispositivo inexistente;
- LBA fora dos limites;
- quantidade inválida;
- buffer insuficiente;
- alinhamento incompatível.

Erros que podem aparecer durante a execução:
- falha de comunicação;
- dispositivo indisponível;
- erro de mídia;
- tempo limite excedido;
- cancelamento não previsto.

Distinguir essas categorias facilita diagnóstico e testes.

## 8. Responsabilidade das camadas

A camada de armazenamento oferece uma interface comum e aplica regras gerais. O driver conhece o protocolo e os detalhes de comunicação. O controlador executa operações internas conforme o projeto do dispositivo.

O sistema de arquivos não deve precisar conhecer registradores específicos do controlador para pedir a leitura de blocos.

## 9. Testes sem hardware

Antes de conectar um SSD real, o ZenithOS pode usar um dispositivo simulado. O simulador pode aceitar operações válidas, rejeitar limites inválidos e produzir falhas controladas. Assim, é possível testar contratos e estados sem depender do hardware físico.

## 10. Perguntas de compreensão

1. Qual é a direção dos dados em uma leitura?
2. Qual é a direção em uma gravação?
3. Por que a capacidade do buffer precisa ser validada?
4. Uma operação validada ainda pode falhar? Dê um exemplo.
5. Por que pedido enviado não significa necessariamente gravação persistida?
6. Por que a camada superior não deve conhecer os registradores do controlador?

## 11. Exercícios de código

- EXN1A6.nbx — verificar se um buffer comporta a quantidade de bytes solicitada.
- EXN2A6.nbx — validar os campos de um descritor de operação.
- EXN3A6.nbx — validar transições entre estados de uma operação.

## Critério de conclusão

Você deve descrever o caminho de uma leitura e de uma gravação e distinguir solicitação, validação, execução, conclusão e persistência.
