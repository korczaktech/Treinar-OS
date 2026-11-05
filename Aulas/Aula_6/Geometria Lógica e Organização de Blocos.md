# Aula 6 — Geometria lógica e organização de blocos

## Objetivos
Entender como um dispositivo apresenta seu espaço endereçável, conhecer a geometria histórica de discos, relacioná-la ao endereçamento LBA e distinguir unidades de blocos que pertencem a camadas diferentes.

## 1. O espaço de armazenamento como uma sequência
Para o sistema operacional, o dispositivo costuma ser apresentado como uma sequência de unidades lógicas numeradas. Cada unidade possui um endereço e um tamanho definido pela interface. O LBA identifica essas unidades em sequência: 0, 1, 2, 3...

Se um dispositivo apresenta 10.000 blocos lógicos, os endereços válidos vão de 0 até 9.999. A quantidade é 10.000; o maior endereço é 9.999.

## 2. Geometria física e geometria lógica
Discos rígidos tradicionais possuem pratos, superfícies, trilhas e setores. Uma trilha é uma trajetória circular; setores dividem a trilha em regiões endereçáveis. Cilindros agrupam trilhas de mesmo raio em diferentes superfícies.

Esses elementos ajudam a explicar a organização física de HDDs. Entretanto, o sistema operacional moderno normalmente não precisa escolher diretamente prato, cabeça e trilha para cada leitura.

## 3. CHS e LBA
CHS (Cylinder-Head-Sector) é uma forma histórica de descrever posições usando cilindro, cabeça e setor. LBA substitui essa representação por uma sequência linear de endereços lógicos.

A tradução entre LBA e geometria física, quando necessária, pertence ao dispositivo/controlador. O sistema não deve presumir que um LBA corresponde a uma posição física fixa em SSDs.

## 4. Exemplo de endereçamento linear
Imagine, apenas para fins didáticos, um disco com 4 setores por trilha e 2 cabeças. A primeira trilha contém setores que podem ser numerados em sequência. A representação CHS exige conhecer os componentes da geometria; LBA permite solicitar diretamente o bloco lógico numerado.

O exemplo não deve ser usado para inferir a geometria real de um dispositivo moderno. Ele serve para comparar dois modelos de endereçamento.

## 5. O que significa “bloco”?
A palavra bloco muda de significado conforme a camada:
- **Bloco lógico do dispositivo:** unidade acessada por LBA.
- **Bloco de alocação:** unidade que um sistema de arquivos reserva para arquivos.
- **Página NAND:** unidade de programação da memória flash.
- **Bloco de apagamento NAND:** conjunto de páginas apagado como unidade pelo controlador.

Essas unidades podem ter tamanhos e regras diferentes. Nunca use o tamanho de uma delas como se fosse automaticamente o tamanho das outras.

## 6. Relação entre setor e bloco lógico
Em uma interface de blocos, o tamanho do setor lógico determina quantos bytes correspondem a cada LBA. Se cada setor lógico tem 512 bytes, o LBA 8 começa no deslocamento 8 × 512 = 4.096 bytes. Se o tamanho lógico for 4.096 bytes, o mesmo LBA começa em 32.768 bytes.

O tamanho precisa vir das informações do dispositivo, não de uma suposição universal.

## 7. Aplicação no ZenithOS
O ZenithOS deve representar separadamente quantidade de blocos, tamanho do bloco lógico e capacidades físicas reportadas. O driver converte comandos da interface para a comunicação com o controlador. Camadas superiores trabalham com LBA e contratos comuns, sem depender de geometria física interna.

## 8. Método de estudo
- Primeiro desenhe a sequência de LBAs.
- Depois associe cada LBA ao tamanho lógico em bytes.
- Em seguida compare essa representação com CHS.
- Por fim, classifique cada “bloco” conforme a camada responsável.

## 9. Exercícios de compreensão
1. Qual é a diferença entre geometria física e representação lógica?
2. Por que LBA é mais conveniente para o sistema operacional do que CHS?
3. Um dispositivo possui 4.000 blocos lógicos. Qual é o maior LBA válido?
4. Com setores lógicos de 512 bytes, qual deslocamento em bytes corresponde ao LBA 8?
5. Por que uma página NAND não deve ser tratada como se fosse um setor lógico?
6. Qual componente normalmente esconde a tradução entre LBA e a organização física de um SSD?

## 10. Exercícios de código
- **EXN1A6.nbx:** converter LBA em deslocamento de bytes com tamanho lógico variável.
- **EXN2A6.nbx:** validar um descritor de geometria lógica (quantidade de blocos e tamanho por bloco).
- **EXN3A6.nbx:** classificar unidades conforme a camada: LBA, alocação, página NAND ou bloco de apagamento.

## Critério de conclusão
Você deve explicar por que o ZenithOS trabalha com endereços lógicos e distinguir pelo menos quatro unidades chamadas de bloco.

## Metadados da aula
- **Dificuldade:** Média
- **Duração:** 35 minutos
