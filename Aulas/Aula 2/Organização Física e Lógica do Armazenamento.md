# Aula 2 - Organização Física e Lógica do Armazenamento
## Fundamentos da Arquitetura

### - Organização Física.

- Um dispositivo de armazenamento possui uma estrutura física responsável por guardar os dados.
- Por exemplo, em um SSD, existem células de memória NAND que armazenam informações por meio de diferentes níveis de carga elétrica.
- **`O importante é entender`**
1. O SSD possui componentes físicos
2. Esses componentes guardam as informações
3. O controlador do dispositivo gerencia operações de leitura e escrita
4. O sistema operacional não precisa conhecer todos os detalhes elétricos do dispositivo

**__Uma distinção importante__** : O ZenithOS não precisa controlar diretamente cada célula NAND. Essa responsabilidade normalmente pertence ao controlador do SSD

### Organização Lógica

- A organização lógica é a maneira como o sistema operacional enxerga e organiza o armazenamento
- Imagine um disco com capacidade para armazenar milhões de bytes.
- O ZenithOS pode enxergar esse espaço como uma sequência de endereços.
{ Endereço 0 }
{ Endereço 1 }
{ Endereço X }

- Cada endereço representa uma posição dentro do espaço de armazenamento disponibilizado pelo dispositivo.
- Isso permite que o sistema solicite operações como:
> 1. Ler dados de determinado endereço
> 2. Gravar dados em determinado endereço
> 3. Identificar regiões ocupadas
> 4. Identificar regiões disponíveis

### Setores

- Em discos rígidos tradicionais, os dados são organizados fisicamente em estruturas chamadas **`trilhas`** e **`setores`**.
- Um setor é uma unidade de endereçamento e transferência de dados.

- Valores comuns incluem:

> 1. 512 bytes;
> 2. 4096 bytes;
> 3. 4KiB

- Em SSDs, a organização interna é diferente, mas o dispositivo pode apresentar setores lógicos de 512 ou 4096 bytes ao sistema operacional.
[!Warning] Setor lógico, página NAND e bloco de apagamento NAND são coisas diferentes. Vamos estudar esas diferenças posteriormente

### Blocos

> Lembra que na aula 1 identificamos os blocos?
> Agora iremos nos aprofundar mais

- A palavra bloco pode representar unidades diferentes, dependendo da camada:
| Camada | Exemplo |
| Dispositivo | Bloco Lógico |
| Sistema de Arquivos | Bloco de Alocação |
| SSD NAND | Bloco de Apagamento |
> Não podemos tratar todos como se fossem a mesma coisa

- No nosso projeto, precisaremos definir cuidadosamente o significado de cada unidade

### A Arquitetura que estamos construindo

#### O Objetivo é separar as responsabilidades

- ZenithOS >
  - Formato de Disco Zenith >
    - Camada de Armazenamento >
      - SSD / HDD / NVMe

- Essa separação é importante porque queremos desenvolver um formato próprio sem precisar reinventar o funcionamento elétrico de cada dispositivo.

### Exercicios de Compreensão

##### 1. Qual é a diferença entre organização física e organização lógica?
> - Na física, eles são armazenados de acordo com diferentes niveis de carga elétrica. Na lógica, é a maneira como o SO armazena essas informações e como enxerga
[!WARNING] Organização Lógica não é necessariamente como o SO armazena os dados, mas a maneira como ele representa, endereça e organiza o espaço.
##### 2. Por que o ZenithOS não precisa conhecer diretamente as células NAND de um SSD?
> - Por que o controlador já faz esse trabalho pelo SO.
##### 3. Qual é a diferença entre um setor lógico de 4096 bytes e um bloco de apagamento NAND?
> - Não sei, não foi explicado na aula. Você disse que seria feito nas posteriores.
[!IMPORTANT] **Setor Lógico de 4096 bytes:** unidade de endereçamento apresentada pelo dispositivo ao sistema operacional. O SO pode solicitar a leitura ou escrita dessa unidade.
[!IMPORTANT] **Bloco de Apagamento NAND:** Agrupamento físico de páginas NAND que o controlador precisa apagar como uma unidade
##### 4. Por que não devemos tratar todos os tipos de blocos como se fossem iguais?
> - Porque isso pode quebrar o SO, cada bloco deve ser tratado de acordo com a camada em que está
##### 5. Se dois SSDs possuem estruturas físicas diferentes, como o ZenithOS pode utilizar ambos através de uma mesma arquitetura?
> - Através do Controlador de SSDs.
[!WARNING] Sua resposta está no caminho certo. O controlador interno do SSD abstrai as particularidades da memória NAND. Além disso, o ZenithOS precisa de uma camada de drivers e comunicação com interfaces NVMe e SATA.


## Método de estudo
Desenhe duas representações do mesmo dispositivo: primeiro, componentes físicos simplificados; depois, a sequência lógica de endereços apresentada ao sistema. Compare o que cada camada conhece e o que permanece escondido pelo controlador.

## Exemplo adicional
Um SSD apresenta setores lógicos de 512 bytes. Internamente, sua NAND pode usar páginas de programação e blocos de apagamento maiores. O sistema operacional continua solicitando LBAs; o controlador traduz esses pedidos para suas operações internas. A camada de blocos não deve presumir que um setor lógico corresponda a uma página NAND.
