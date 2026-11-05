# Aula 10 — Camadas do subsistema de armazenamento

## Objetivos
Compreender por que o armazenamento é dividido em camadas, identificar a responsabilidade de cada componente, acompanhar o caminho de uma operação e entender como essa separação facilita suporte a diferentes dispositivos.

## 1. Por que dividir em camadas?
Um sistema operacional precisa oferecer arquivos e volumes sem exigir que cada serviço conheça registradores, filas e comandos específicos de todos os dispositivos. A divisão em camadas reduz dependências e permite trocar uma implementação sem reescrever todo o sistema.

Camadas não existem apenas para organizar pastas de código. Cada uma precisa ter uma responsabilidade e um contrato bem definido.

## 2. Camadas principais
Uma arquitetura possível para o ZenithOS:
1. Aplicações e serviços: solicitam operações de alto nível.
2. Sistema de arquivos: organiza arquivos, diretórios e metadados.
3. Gerenciador de volumes e partições: delimita regiões e oferece volumes.
4. Cache de blocos: mantém cópias temporárias e coordena leituras e gravações.
5. Camada de blocos: valida e padroniza requisições.
6. Gerenciador de dispositivos: registra unidades, capacidades e estados.
7. Driver: traduz a interface comum para o protocolo específico.
8. Controlador e dispositivo: executam as operações.

O subsistema de memória também participa, fornecendo buffers e mapeamentos para transferências.

## 3. Exemplo: leitura de um arquivo
O programa pede a leitura. O sistema de arquivos localiza os metadados e descobre quais blocos contêm os dados. O gerenciador de volumes confirma a região. O cache verifica se os blocos já estão disponíveis. Se necessário, a camada de blocos cria uma requisição. O driver prepara o comando. O dispositivo transfere os dados para a memória. A conclusão retorna às camadas superiores.

Cada camada faz uma parte do trabalho. Nenhuma precisa assumir a responsabilidade de todas as outras.

## 4. Exemplo: falha de leitura
Se o dispositivo reportar erro de mídia, o driver traduz o resultado. A camada de blocos propaga a falha. O cache não deve marcar dados inválidos como válidos. O sistema de arquivos informa que a leitura não foi concluída.

Se a camada inferior retornar erro, uma camada superior não pode inventar dados nem transformar a falha em sucesso.

## 5. Contratos entre camadas
Uma interface precisa definir parâmetros, unidades, limites, alinhamento, propriedade e vida útil do buffer, sincronismo, estados, erros e garantias de conclusão e persistência.

Sem contrato, componentes começam a depender de detalhes internos uns dos outros.

## 6. O que não deve acontecer
O sistema de arquivos não deve emitir comandos NVMe diretamente. Uma aplicação não deve escrever em qualquer LBA sem autorização. O driver não deve interpretar nomes de arquivos. A camada de blocos não deve presumir que todo hardware possui os mesmos recursos.

## 7. Aplicação no ZenithOS
O ZenithOS deve começar com uma interface de blocos comum e um dispositivo em RAM para testes. Depois pode integrar drivers reais. O sistema de arquivos usa a interface superior, enquanto os drivers conhecem os protocolos específicos.

## 8. Método de estudo
Desenhe as camadas em ordem. Para uma leitura, escreva o que cada camada recebe, valida, transforma e devolve. Depois repita para uma falha de hardware e observe como o erro sobe pela arquitetura.

## 9. Exercícios de compreensão
1. Por que o sistema de arquivos não deve depender diretamente de um driver NVMe?
2. Qual é a responsabilidade da camada de blocos?
3. Qual é a diferença entre gerenciador de volumes e gerenciador de dispositivos?
4. Descreva o caminho de uma leitura desde a aplicação até o dispositivo.
5. Como um erro de mídia deve retornar às camadas superiores?
6. Cite três informações que um contrato entre camadas precisa definir.
7. Qual vantagem existe em testar primeiro com um dispositivo em RAM?

## 10. Exercícios de código
- EXN1A10.nbx: representar as camadas e validar se uma solicitação passa pelas verificações na ordem correta.
- EXN2A10.nbx: simular uma leitura e propagar sucesso ou erro sem transformar falha em sucesso.

## Critério de conclusão
Você deve conseguir desenhar a arquitetura, explicar a responsabilidade de cada camada e acompanhar tanto uma operação bem-sucedida quanto uma falha.

## Metadados
- Dificuldade: Média
- Duração: 35 minutos
