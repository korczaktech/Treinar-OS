# Aula 7 — Controladores e comunicação com dispositivos de armazenamento

## Objetivos
Compreender o papel do controlador, distinguir controlador, driver e dispositivo, conhecer a ideia de protocolos de comunicação e acompanhar o caminho de uma solicitação do ZenithOS até o hardware.

## 1. Por que existe um controlador?
O sistema operacional não controla diretamente a eletricidade das células NAND nem movimenta cabeças de um HDD. O dispositivo possui eletrônica de controle que recebe comandos, organiza operações internas e apresenta uma interface ao computador.

Em um SSD, o controlador administra memória NAND, correção de erros, remapeamento e outras tarefas internas. Em um HDD, a eletrônica controla motores, cabeças e leitura/gravação magnética.

## 2. Controlador, driver e dispositivo
- **Dispositivo:** unidade que armazena os dados.
- **Controlador:** componente que gerencia o dispositivo e expõe uma interface de comunicação.
- **Driver:** código do sistema operacional que conhece essa interface e traduz operações do kernel para comandos aceitos pelo controlador.
- **Camada de armazenamento:** recebe solicitações genéricas, valida parâmetros e coordena operações sem depender de um protocolo específico.

Esses papéis podem estar integrados fisicamente, mas continuam sendo responsabilidades diferentes na arquitetura.

## 3. Protocolos e barramentos
SATA é uma interface comum em unidades que usam o protocolo AHCI. NVMe é um protocolo projetado para dispositivos de armazenamento não volátil que normalmente se comunicam por PCI Express.

O barramento transporta dados e comandos; o protocolo define como as operações são representadas e concluídas. Não confunda o conector físico com o protocolo.

## 4. Como uma solicitação chega ao dispositivo
1. Uma camada superior solicita leitura ou gravação.
2. A camada de blocos valida LBA, quantidade e buffer.
3. O driver prepara estruturas e comandos exigidos pelo protocolo.
4. O controlador recebe a solicitação.
5. O dispositivo executa ou agenda a operação.
6. O controlador informa conclusão ou erro.
7. O driver traduz o resultado e comunica a camada superior.

Cada etapa pode falhar. O kernel deve preservar a associação entre solicitação e conclusão.

**Exemplo prático:** o ZenithOS recebe uma leitura genérica do LBA 40. A camada de blocos valida o endereço e o buffer. O driver NVMe transforma a solicitação em uma entrada de fila conforme o protocolo. O controlador processa o comando e publica uma conclusão. O driver associa essa conclusão ao pedido original e devolve o resultado à camada superior. Se o controlador não foi inicializado, a requisição deve ser recusada antes da submissão.

## 5. Registradores, filas e memória
Algumas interfaces usam registradores de controle e estado. Interfaces modernas também podem usar filas de submissão e conclusão em memória. O driver precisa respeitar a ordem de publicação, barreiras de memória e regras do protocolo.

Uma fila não é apenas uma lista comum: os campos, alinhamento, endereços e ciclo de vida das estruturas são definidos pela interface.

## 6. Inicialização e descoberta
Antes de enviar comandos normais, o driver pode precisar detectar o controlador, mapear recursos, negociar ou consultar capacidades e inicializar filas. Se uma etapa falhar, o dispositivo não deve ser publicado como pronto.

## 7. Aplicação no ZenithOS
O ZenithOS deve separar drivers SATA/AHCI, NVMe e outras interfaces de uma API comum de blocos. Assim, o sistema de arquivos não precisa saber qual protocolo existe atrás do volume. O driver reporta capacidades reais e a camada superior valida operações conforme esses limites.

## 8. Método de estudo
Desenhe quatro caixas: camada de armazenamento, driver, controlador e dispositivo. Siga uma leitura e depois uma gravação. Em cada seta, escreva quais informações são enviadas e qual erro pode retornar.

## 9. Erros comuns
- Chamar o driver de controlador.
- Achar que SATA e NVMe são apenas tamanhos diferentes de disco.
- Supor que todo dispositivo aceita os mesmos comandos.
- Publicar o dispositivo antes de concluir sua inicialização.

## 10. Exercícios de compreensão
1. Qual é a diferença entre controlador e driver?
2. Por que o sistema de arquivos não deve emitir comandos NVMe diretamente?
3. Qual é a função do protocolo de comunicação?
4. Descreva o caminho de uma leitura desde a camada de blocos até o dispositivo.
5. O que deve acontecer se a inicialização do controlador falhar?
6. Por que as capacidades anunciadas precisam ser consultadas e validadas?

## 11. Exercício de código
- **EXN1A7.nbx:** modelar estados de inicialização de um controlador e aceitar operações somente depois de pronto.

## Critério de conclusão
Você deve conseguir explicar o papel de cada camada e desenhar o caminho de uma operação sem misturar driver, controlador e dispositivo.

## Metadados da aula
- **Dificuldade:** Média
- **Duração:** 35 minutos
