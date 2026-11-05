# Organização e Alocação de Arquivos

## Objetivo

Depois de descobrir um dispositivo e interpretar suas partições, ainda falta entender como os arquivos são organizados dentro de uma região. Essa é a responsabilidade do sistema de arquivos.

Ao final, você deverá explicar a função de um sistema de arquivos, diferenciar LBA de unidade de alocação, entender metadados, comparar estratégias de alocação e explicar como o espaço livre é controlado.

## 1. O que o sistema de arquivos resolve?

Uma partição fornece uma região. Ela não oferece automaticamente nomes, pastas e arquivos. O sistema de arquivos cria essa organização e responde quais arquivos existem, quais diretórios existem, qual é o tamanho de cada arquivo, onde seu conteúdo está e quais unidades estão livres.

Sem essa camada, o sistema teria uma sequência de bytes sem uma organização compreensível de arquivos.

## 2. Arquivos, diretórios e caminhos

Um arquivo representa dados associados a um nome e metadados. Um diretório organiza referências a arquivos e outros diretórios.

O caminho /sistema/config/inicializacao.cfg informa a posição lógica na árvore. Ele não revela diretamente o LBA onde os bytes estão. O sistema de arquivos consulta suas estruturas para traduzir a localização lógica em regiões de armazenamento.

## 3. Metadados de arquivo

Um arquivo pode ter tamanho lógico, identificador interno, datas, permissões, atributos e referências às unidades que armazenam seu conteúdo. O formato define quais campos existem e como são representados.

Esses metadados não são os metadados do dispositivo estudados na Aula 7. Um descritor de dispositivo informa capacidade e tamanho de bloco; metadados de arquivo descrevem um arquivo específico.

## 4. LBA e unidade de alocação

O dispositivo apresenta blocos lógicos endereçados por LBA. O sistema de arquivos pode agrupar vários desses blocos em uma unidade maior de alocação, também chamada de cluster ou bloco de alocação conforme o formato.

Exemplo: setor lógico de 512 bytes e unidade de alocação de 4096 bytes. A unidade reúne 8 setores lógicos.

Um arquivo de 1000 bytes pode reservar uma unidade inteira de 4096 bytes. O espaço restante dentro dela é desperdício interno, associado à fragmentação interna.

## 5. Estratégias de alocação

**Contígua:** o arquivo ocupa unidades consecutivas. É simples e favorece leitura sequencial, mas pode ser difícil encontrar uma região grande e o crescimento pode exigir movimentação. Pode haver fragmentação externa.

**Encadeada:** cada unidade aponta para a próxima, ou uma estrutura externa mantém a sequência. Facilita ocupar regiões dispersas, mas percorrer o arquivo pode exigir seguir vários vínculos. Uma referência corrompida pode interromper a cadeia.

**Indexada ou por extensões:** uma estrutura registra os blocos ou regiões do arquivo. Uma extensão descreve uma sequência por início e quantidade. Isso pode reduzir metadados quando os dados são contíguos, mas arquivos muito fragmentados exigem mais entradas.

Nenhuma estratégia é perfeita para todos os cenários.

## 6. Controle de espaço livre

O sistema precisa saber quais unidades estão disponíveis. Uma técnica é o bitmap: cada posição representa uma unidade e indica se está livre ou ocupada.

Exemplo didático: 0 = livre e 1 = ocupado. No mapa 1, 1, 0, 0, 1, as unidades 2 e 3 estão livres.

O mapa precisa ser atualizado ao criar, ampliar, truncar ou remover arquivos. Uma falha entre atualizações pode deixar o mapa inconsistente, tema relacionado à Aula 10.

## 7. Fragmentação

Fragmentação interna ocorre quando uma unidade reservada possui espaço não utilizado pelo arquivo.

Fragmentação externa ocorre quando o espaço livre fica dividido em regiões separadas. O espaço livre total pode ser suficiente, mas não existir uma região contínua grande o bastante para determinada alocação.

## 8. Remoção não é apagamento físico imediato

Em muitos sistemas, remover um arquivo atualiza metadados e marca suas unidades como livres. Os bytes antigos podem permanecer até serem sobrescritos ou tratados por mecanismos específicos.

Em SSDs, o controlador, o remapeamento e mecanismos como TRIM tornam a situação mais complexa. Arquivo removido, espaço marcado como livre e células fisicamente apagadas são eventos diferentes.

## 9. Camadas no ZenithOS

O sistema de arquivos recebe operações como abrir, ler, gravar e remover. Ele traduz posições de arquivos em regiões de armazenamento. A camada de armazenamento valida e encaminha operações de bloco. O driver conversa com o dispositivo.

O sistema de arquivos não deve controlar diretamente os detalhes internos do controlador.

## 10. Perguntas de compreensão

1. Por que uma partição não é suficiente para organizar arquivos?
2. Qual é a diferença entre LBA e unidade de alocação?
3. Um arquivo de 1000 bytes pode reservar 4096 bytes? Por quê?
4. Qual a vantagem e desvantagem da alocação contígua?
5. Para que serve um bitmap de espaço livre?
6. Qual a diferença entre fragmentação interna e externa?
7. Por que remover um arquivo não significa apagar imediatamente os dados físicos?

## 11. Exercícios de código

- EXN1A9.nbx — consultar e atualizar um bitmap de espaço livre.
- EXN2A9.nbx — calcular quantas unidades são necessárias para armazenar um arquivo.
- EXN3A9.nbx — validar uma extensão dentro da região de uma partição.

## Critério de conclusão

Você deve explicar como o sistema de arquivos organiza uma região em arquivos e diretórios e como controla a ocupação das unidades.
