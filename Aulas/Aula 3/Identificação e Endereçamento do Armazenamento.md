# Aula 3 - Identificação e Endereçamento do Armazenamento
## Fundamentos de Armazenamento

### O Problema que Precisamos Resolver

- Imagine que o ZenithOS tenha um SSD de 512GB.

- O sistema consegue enxergar o dispositivo, mas ainda precisa responder:
> 1. Onde começa o espaço disponível?
> 2. Onde termina?
> 3. Como identificar uma região específica?
> 4. Como solicitar a leitura de uma posição?
> 5. Como evitar acessar uma região fora dos limites?
- Para resolver isso, precisamos aprender um conceito fundamental: o **`Endereçamento`**

### O Que é um Endereço de Armazenamento?

- Um endereço identifica uma posição ou unidade dentro de um espaço endereçável.

- Pense em uma rua:
    - A rua representa o dispositivo;
    - Cada número representa um endereço;
    - A casa representa uma unidade de armazenamento acessível.

- O sistema não precisa perguntar ao SSD onde está fisicamente cada célula NAND. Ele utiliza endereços lógicos que o dispositivo apresenta.

### LBA - Logical Block Addressing
###### Conceito Central

- LBA significa Logical Block Addressing, ou endereçamento lógico de blocos.

- É um sistema no qual os blocos são identificados por números sequenciais

[!CAUTION] **`Exemplos Simplificados`**
| Endereço LBA | Posição Lógica |
| 0 | Primeiro Bloco |
| 1 | Segundo Bloco |
| 2 | Terceiro Bloco |
| 3 | Quarto Bloco |]
- Se cada setor lógico tiver 512 bytes, podemos calcular:
$$
{\text{Posição em bytes} = \color{white}{\text{LBA}} \times \color{amber}{512}}
$$
- Por exemplo, o LBA 10 representa o início da posição:
$$
\large \color{white}{10} \times 512 = \mathbf{5120\text{ bytes}}
$$
- Se o setor lógico tiver 4096 bytes, a mesma operação usa 4096 no lugar do 512.
[!IMPORTANT] LBA não é um endereço físico de uma célula NAND. É um endereço lógico apresentado pelo dispositivo

### Como isso chega ao ZenithOS
- Nossa arquitetura terá repsonsabilidades separadas:
- ZenithOS
> - Solicita operação de armazenamento
- Camada de armazenamento
> - Organiza e valida as solicitações
- Driver do dispositivo
> - Comunica com a interface do Hardware
- Controlador do SSD
> - Traduz Lógica para operações internas
- Essa sepração evita que o restante do sistema precise conhecer os detalhes internos de cada SSD.

### Um cuidado fundamental: Limites

- Imagine um dispositivo com 100 blocos, numerados de 0 até 99.

- Uma solicitação para ler o bloco 50 é válida.
- Uma solicitação para ler o bloco 50, está fora dos limites

- O ZenithOS precisará validar as operações antes de enviá-las ao dispositivo. Mais adiante, estudaremos como fazer essa validação com segurança, inclusive quando uma operação envolve vários blocos.

### Exercicios de Compreensão

##### 1. Qual a diferença entre um endereço lógico e uma posição física dentro do SSD?
> R | O endereçamento lógico, é apenas o que o dispositivo usa para conseguir representar o endereçamento físico sem precisar mexer em toda a parte elétrica do hardware. 
> R | O endereçamento lógico não diz exatamente sobre o endereçamento físico, é mais como uma forma de representá-lo, é o que é usado na interface, o Fisico é o endereçamento real do armazenamento, como em um ssd, hdd, nvme, ou pendrive.
##### 2. Se um dispositivo possui setores lógicos de 4096 ytes, quanto representa o início do LBA 5 em bytes?
> R | 20480
##### 3. Por que o ZenithOS não deveria precisar conhecer a posição exata de cada célula NAND?
> R | O Controlador SSD ja faz isso por nós, para que não precisemos conhecer totalmente a rede elétrica e o hardware do dispositivo, facilitando muito as coisas
##### 4. Um dispositivo possui 200 blocos, numerados de 0 a 199. Uma solicitação tenta acessar o bloco 200. O que deve acontecer?
> R | Deve dar erro, Mas não sei qual erro exato, por que voce disse que ia explicar posteriormente
##### 5. Por que precisamos separar a camada de armazenamento do driver do dispositivo?
> R | Porque cada uma possui uma funcionalidade diferente

## Método de estudo
Sempre separe quantidade de blocos, intervalo válido, tamanho lógico e deslocamento em bytes. Faça primeiro um exemplo de um único LBA e depois uma faixa. Por último, explique qual camada valida e qual camada traduz o endereço.
