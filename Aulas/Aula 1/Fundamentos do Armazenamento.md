# Aula 1 — Fundamentos do armazenamento

## Objetivos de aprendizagem
Ao final desta aula, você deverá explicar o que é armazenamento, distinguir informação lógica de suporte físico, compreender bits, bytes e blocos e justificar por que um sistema operacional precisa de regras para organizar um dispositivo.

## 1. O que é armazenamento?
Armazenamento é o conjunto de recursos que mantém dados disponíveis depois que deixam de estar sendo usados imediatamente pelo processador. Ele guarda programas, documentos, configurações e informações necessárias para iniciar o sistema.

Memória RAM e armazenamento persistente não são a mesma coisa. A RAM é usada durante a execução e normalmente perde seu conteúdo quando a máquina é desligada. SSDs, HDDs e pendrives são exemplos de dispositivos que mantêm dados sem alimentação contínua.

## 2. Exemplos de dispositivos
- **HDD:** guarda dados em mídia magnética, com pratos e cabeças de leitura/gravação.
- **SSD:** usa memória flash NAND e um controlador para administrar as operações.
- **Pendrive:** também utiliza memória flash, normalmente com controlador integrado.
- **NVMe:** é um protocolo/interface de comunicação usado por dispositivos de armazenamento, normalmente sobre PCI Express; não é, por si só, um tipo de memória.

O formato físico e a tecnologia interna podem variar. O sistema operacional precisa de uma forma comum de solicitar operações.

## 3. Bits: a menor unidade de informação
Um bit pode representar 0 ou 1. Esses dois estados são a base da representação binária usada pelos computadores. Um bit isolado guarda pouca informação, mas grupos de bits podem representar números, caracteres, instruções e outros dados.

Exemplo: com 1 bit existem 2 combinações possíveis: 0 e 1. Com 2 bits existem 4 combinações: 00, 01, 10 e 11. Com 8 bits existem 256 combinações possíveis.

## 4. Bytes
Um byte é formado por 8 bits. É uma unidade muito usada para expressar tamanhos de dados e capacidade de memória.

Exemplo: 3 bytes correspondem a 24 bits. Um arquivo com 100 bytes contém 800 bits de informação, sem considerar metadados e estruturas adicionais usadas para armazená-lo.

Não confunda byte (B) com bit (b). Em unidades de rede, por exemplo, é comum usar bits por segundo; em capacidade de armazenamento, bytes são mais comuns.

## 5. Blocos e setores
O sistema operacional normalmente não solicita ao dispositivo que grave um bit isolado. A interface de armazenamento apresenta unidades endereçáveis, frequentemente chamadas de setores lógicos ou blocos lógicos.

Um bloco lógico pode conter 512 ou 4.096 bytes, por exemplo. O tamanho depende do que o dispositivo apresenta. A palavra “bloco” também aparece em outras camadas, como sistema de arquivos e memória NAND; esses significados não são necessariamente iguais.

## 6. Por que o sistema precisa de um formato?
Imagine conectar um dispositivo que contém milhões de bytes. O hardware pode permitir ler e gravar posições, mas isso não explica automaticamente:
- onde começa uma partição;
- como identificar volumes;
- onde ficam os metadados;
- como localizar arquivos e diretórios;
- quais regiões estão livres ou reservadas;
- como detectar estruturas corrompidas.

Um formato define regras e estruturas para interpretar os dados. O formato do dispositivo, a tabela de partições e o sistema de arquivos resolvem problemas relacionados, mas diferentes.

## 7. Relação com o ZenithOS
O ZenithOS precisará definir contratos para acessar dispositivos, validar endereços e interpretar regiões. O formato de disco e o sistema de arquivos serão especificações próprias do projeto, mas isso não significa que o ZenithOS deva reinventar os protocolos elétricos ou a comunicação com cada controlador.

A arquitetura deve separar o dispositivo físico, o driver, a camada de blocos, o gerenciador de volumes e o sistema de arquivos.

## 8. Exemplo guiado
Considere um SSD que apresenta 1.000 blocos lógicos de 512 bytes:
1. Cada bloco contém 512 bytes.
2. O dispositivo apresenta 1.000 endereços, de 0 a 999.
3. A capacidade apresentada é 1.000 × 512 = 512.000 bytes.
4. Isso ainda não informa quais blocos pertencem a arquivos, partições ou áreas reservadas.
5. Para interpretar essas regiões, o sistema precisa de estruturas e formatos definidos.

## 9. Método de aprendizagem
Leia cada conceito e tente explicá-lo sem repetir a definição. Depois classifique exemplos: bit, byte, bloco lógico, dispositivo físico, formato e sistema de arquivos. Por fim, desenhe a sequência “dispositivo → blocos lógicos → partições/volumes → sistema de arquivos → arquivos”.

## 10. Erros comuns
- Confundir RAM com armazenamento persistente.
- Tratar bit e byte como a mesma unidade.
- Achar que ter capacidade significa que o dispositivo organiza arquivos.
- Tratar todo tipo de bloco como equivalente.
- Confundir NVMe, que é um protocolo, com a memória física do dispositivo.

## 11. Exercícios de compreensão
1. Qual é a diferença entre memória RAM e armazenamento persistente?
2. Quantos bits existem em 5 bytes?
3. Por que um dispositivo com grande capacidade não sabe, sozinho, como organizar arquivos?
4. Qual é a diferença entre bloco lógico do dispositivo e bloco de alocação de um sistema de arquivos?
5. O que um formato de disco precisa definir para que o ZenithOS interprete os dados?
6. Por que o ZenithOS deve separar drivers e sistema de arquivos?
7. Um SSD apresenta 1.000 blocos de 512 bytes. Qual é a capacidade apresentada em bytes e quais são os LBAs válidos?

## 12. Anotações originais do estudante
As respostas abaixo foram registradas durante o estudo inicial. São mantidas como histórico de aprendizagem e podem ser comparadas com as explicações desta versão.

- **O que é armazenamento?** O armazenamento é o local físico onde informações que precisam ser mantidas ficam guardadas. Exemplos: SSD, HDD e pendrive.
- **O que existe dentro do armazenamento?** O dispositivo possui estruturas físicas e lógicas. Bits representam 0 ou 1; bytes agrupam 8 bits; blocos organizam unidades de acesso ou transferência conforme a camada.
- **Por que precisamos de um formato de disco?** Porque o sistema precisa de regras para descobrir como os dados estão organizados e o que cada região significa.

## Critério de conclusão
Você deve conseguir explicar armazenamento, bit, byte e bloco com suas palavras, calcular uma capacidade simples e justificar por que o sistema operacional precisa de formatos e camadas de organização.

## Metadados
- Dificuldade: Fácil
- Duração: 35 minutos
