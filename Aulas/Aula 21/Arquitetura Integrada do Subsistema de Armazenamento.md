# Arquitetura Integrada do Subsistema de Armazenamento

## Objetivo

Nesta aula vamos reunir os conceitos das aulas 1 a 20 em uma arquitetura coerente para o ZenithOS. O objetivo não é implementar todo o subsistema de uma vez, mas compreender como as responsabilidades se conectam, quais contratos precisam existir e como testar cada camada de forma independente.

## 1. Visão geral

Uma arquitetura de armazenamento pode ser organizada em camadas:
1. aplicações e serviços solicitam operações de arquivo;
2. sistema de arquivos organiza nomes, diretórios, metadados e alocação;
3. camada de volumes e partições delimita regiões;
4. cache de blocos reduz operações repetidas e coordena cópias;
5. camada de blocos valida pedidos e oferece uma interface comum;
6. gerenciador de dispositivos mantém descritores e capacidades;
7. drivers traduzem operações para interfaces específicas;
8. controladores e dispositivos executam transferências;
9. subsistema de memória fornece buffers e mapeamentos DMA.

As camadas podem interagir de maneiras adicionais, mas suas responsabilidades precisam continuar explícitas.

## 2. Caminho de uma leitura

Imagine que um programa solicite ler um arquivo:
1. o sistema de arquivos encontra os metadados e identifica as unidades alocadas;
2. transforma a posição do arquivo em uma ou mais faixas de blocos;
3. consulta o cache de blocos;
4. para dados ausentes, envia uma solicitação à camada de blocos;
5. a camada valida dispositivo, faixa, tamanho e buffer;
6. o driver prepara a transferência;
7. o controlador acessa o dispositivo;
8. a conclusão retorna pelo driver;
9. o cache atualiza sua entrada;
10. o sistema de arquivos entrega os dados ao solicitante.

Cada etapa pode falhar. O resultado precisa ser propagado sem ser convertido indevidamente em sucesso.

## 3. Caminho de uma gravação

Uma gravação pode atualizar dados, metadados e mapas de alocação. O sistema de arquivos define dependências. O cache pode manter entradas sujas. A camada de blocos encaminha pedidos. O driver conclui a transferência. Flush e barreiras garantem a ordem e a persistência conforme o contrato.

O sistema não deve afirmar durabilidade antes de cumprir as garantias exigidas.

## 4. Contratos entre camadas

Cada interface deve documentar:
- parâmetros e unidades;
- limites e alinhamento;
- propriedade e vida útil do buffer;
- sincronismo ou assincronismo;
- estados e códigos de erro;
- regras de cancelamento;
- garantias de conclusão e persistência;
- capacidades opcionais.

Contratos claros reduzem dependências acidentais e facilitam testes.

## 5. Descoberta e montagem

O dispositivo é descoberto e registrado com um descritor válido. O gerenciador de partições interpreta o mapa e valida as regiões. O sistema identifica um formato de sistema de arquivos compatível e tenta montá-lo.

Montar não deve significar confiar cegamente nos metadados. Estruturas precisam ser verificadas antes de serem usadas para acessar dados.

## 6. Inicialização e boot

O processo de boot depende de uma sequência confiável: firmware ou estágio anterior localiza o bootloader; o bootloader encontra os componentes necessários; o kernel inicializa memória e drivers; o subsistema descobre dispositivos e disponibiliza o volume necessário.

O ZenithOS possui o ZBL como bootloader próprio. O desenho exato das etapas de leitura precisa respeitar as capacidades do firmware e do dispositivo, sem pressupor que o kernel já está ativo antes de ser carregado.

## 7. Testes por camada

Não comece testando apenas com um SSD físico. Use testes progressivos:
- funções puras: limites, alinhamento e conversões;
- dispositivo em RAM: leitura, gravação e persistência durante a execução;
- dispositivo simulado com falhas: timeout, remoção e erros;
- testes de integração: partições, cache e sistema de arquivos;
- testes de reinicialização e recuperação;
- testes em hardware real quando houver ambiente apropriado.

Cada teste deve ter resultado esperado e ser repetível.

## 8. Invariantes essenciais

Algumas propriedades precisam permanecer verdadeiras:
- nenhuma operação ultrapassa a capacidade do dispositivo;
- nenhum buffer é acessado fora de sua vida útil;
- uma entrada suja não é descartada sem tratamento;
- uma conclusão pertence a uma solicitação ativa;
- uma partição não ultrapassa o dispositivo nem se sobrepõe indevidamente;
- uma unidade alocada não é atribuída a dois arquivos incompatíveis;
- erros não são apresentados como sucesso;
- dados e metadados respeitam a ordem de persistência definida.

Essas propriedades devem virar testes automatizados.

## 9. Decisões de projeto e decisões do hardware

O ZenithOS define suas interfaces, estruturas, políticas de cache, regras de validação e formato de sistema de arquivos. O hardware define capacidades e restrições que o driver precisa respeitar. O sistema não deve transformar uma escolha interna, como alinhamento padrão de 8 bytes, em regra universal para todos os dispositivos.

## 10. Evolução incremental

Uma ordem razoável de implementação:
1. tipos e contratos de bloco;
2. dispositivo em RAM;
3. testes de faixa e buffer;
4. registro de dispositivos;
5. camada de partições;
6. cache;
7. drivers físicos;
8. sistema de arquivos;
9. sincronização e recuperação;
10. segurança, monitoramento e integração com o boot.

Não implemente tudo ao mesmo tempo. Cada etapa precisa manter testes verdes antes de avançar.

## 11. Perguntas de compreensão

1. Por que o sistema de arquivos não deve conversar diretamente com registradores do controlador?
2. Qual é o caminho simplificado de uma leitura?
3. Quais garantias um contrato de buffer precisa definir?
4. Por que montagem exige validação de metadados?
5. Qual é a vantagem de começar com um dispositivo em RAM?
6. Cite quatro invariantes que devem virar testes automatizados.
7. Qual é a diferença entre decisões do ZenithOS e restrições do hardware?
8. Por que o bootloader precisa de uma sequência própria antes de o kernel inicializar os drivers?

## 12. Exercícios de código

- EXN1A21.nbx — criar um validador integrado de solicitação de bloco usando dispositivo, faixa, buffer e capacidades.
- EXN2A21.nbx — construir um simulador de operações que percorra estados, filas e resultados, incluindo falhas.
- EXN3A21.nbx — criar uma bateria de testes de invariantes para um dispositivo em RAM.

## Critério de conclusão

Você deve conseguir explicar o caminho de uma operação desde o sistema de arquivos até o dispositivo, identificar a responsabilidade de cada camada e propor testes que verifiquem os contratos essenciais do ZenithOS.


## Método de estudo e exemplo guiado
Escolha uma leitura de arquivo e percorra todas as camadas, anotando entrada, validação, transformação e resultado de cada uma. Repita com uma gravação que falha depois da submissão. Por fim, transforme invariantes em casos de teste: faixa fora do limite, buffer liberado cedo, conclusão atrasada, partição sobreposta e erro de mídia. A arquitetura só está clara quando é possível localizar a responsabilidade de cada falha.

## Metadados da aula
- Dificuldade: Muito difícil
- Duração: 50 minutos
