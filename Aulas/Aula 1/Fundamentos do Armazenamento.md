# Aula 1 - Fundamentos de Armazenamento

## Objetivos da Aula :
### Entender como um computador armazena informações, como essas informações são organizafas e por que precisamos de um formato de disco próprio para o ZenithOS

> - O Que é armazenamento?

- Após leitura do tópico na aula, eu tirei minha conclusão, a seguinte:

R | O armazenamento, é o local físico onde todas as informações do computador, que precisam ser armazenadas ficam, para não haver perca.
```Exemplos ditos:```
{ SSD | HDD | Pendrive | NVMe }

> - O que existe dentro do armazenamento?

- Após leitura do tópico na aula, eu tirei minha conclusão, a seguinte:

R | Ela trabalha convertendo informações, trazendo informações como as que nós entendemos, e depois convertendo para bits ou bytes(ainda não sei exatamente o que são). 
R² | São organizados em estruturas físicas e lógicas, como bits, Byte, Blocos.
R³ | Bits são a menor unidade de informação, representa 0 ou 1(`Sistema Binário`); Bytes, conjunto maior de bits juntos, sendo 8 Bits conjuntos; Blocos, são unidades de organização ou tranferência de dados, depende da tecnologia ou camada que se utiliza.
```Exemplos Ditos:```
{ Byte 0-16, cada posição guarda um byte, que consequentemente guardam 8 bits }

> - Por que precisamos de um formato de Disco?

- Após leitura do tópico da aula, tirei as seguintes conclusões:

R | Mesmo que o Zenith só encontre um dispositivo como um SSD conectado, ele não saberia onde começa e onde termina as informações, e nem o que fazer com isso.
R² | Por isso precisamos estabelecer regras para organização, isso é chamado de formato de disco.

> - Exercícios de Compressão

- 1. Se um SSD possui 1.000GB de capacidade, isso significa que ele sabe organizar arquivos automaticamente?
> Não, mesmo que possua bilhoes de PB de capacidade, a única forma de saber como organizar os bits, bytes e blocos, é tendo um formato de disco.
- 2. Qual a diferença entre um byte e um Bloco?
> A diferença, é que um byte é uma unidade de medida e armazenamento, e um bloco é uma unidade de organização ou transferencias de dados, depende de como o sistema utiliza.
- 3. Por que o ZenithOS precisa definir regras próprias para organizar os dados em um disco?
> Porquê sem essas regras, ele não sabe o que fazer com as informações, mesmo que haja milhoes de SSDs conectados. 