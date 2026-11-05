# Aula 2 — Organização física e lógica do armazenamento

## Objetivos de aprendizagem
Ao final, você deverá distinguir a organização física da organização lógica, explicar o papel do controlador, reconhecer setores lógicos e compreender por que a palavra “bloco” pode representar unidades diferentes.

## 1. Organização física
A organização física descreve como a tecnologia do dispositivo guarda os dados. Em um HDD, os dados são registrados magneticamente em pratos que giram. Em um SSD, as informações são armazenadas em células de memória flash NAND.

Uma célula NAND mantém estados elétricos que representam informação. Dependendo da tecnologia, uma célula pode representar um ou mais bits. O dispositivo também precisa de circuitos para controlar leitura, programação, apagamento e correção de erros.

O sistema operacional não precisa controlar diretamente a carga elétrica de cada célula. Essa tarefa pertence à eletrônica e ao controlador do dispositivo.

## 2. O papel do controlador
O controlador recebe comandos da interface apresentada ao computador e coordena o funcionamento interno do dispositivo. Em um SSD, pode administrar:
- tradução entre endereços lógicos e páginas físicas;
- correção de erros;
- remapeamento de regiões inadequadas;
- distribuição de desgaste;
- coleta de lixo;
- cache e filas internas.

Essas tarefas escondem grande parte da complexidade física. O ZenithOS solicita operações usando a interface lógica, enquanto o controlador decide como executá-las internamente.

## 3. Organização lógica
A organização lógica é a representação do espaço que o dispositivo apresenta ao sistema operacional. Em uma interface de blocos, o sistema pode enxergar uma sequência de endereços:
- LBA 0;
- LBA 1;
- LBA 2;
- e assim por diante.

Cada endereço identifica uma unidade lógica. O sistema pode solicitar leitura ou gravação nessa unidade sem saber em qual célula NAND ou região magnética os dados estão fisicamente.

## 4. Setores lógicos
Um setor lógico é uma unidade de endereçamento apresentada pelo dispositivo. Tamanhos comuns incluem 512 bytes e 4.096 bytes. O tamanho precisa ser consultado; não se deve presumir que todos os dispositivos usam o mesmo valor.

Em HDDs tradicionais, a organização física envolve trilhas e setores. Em dispositivos modernos, a interface lógica pode esconder detalhes da geometria física. Em SSDs, setor lógico não significa página NAND.

## 5. Tipos diferentes de bloco
A palavra “bloco” depende da camada:
| Camada | Unidade | Função |
|---|---|---|
| Interface do dispositivo | Bloco lógico/LBA | Unidade endereçável pelo host |
| Sistema de arquivos | Bloco de alocação | Unidade reservada para arquivos |
| Memória NAND | Página | Unidade de leitura/programação conforme a tecnologia |
| Memória NAND | Bloco de apagamento | Grupo de páginas apagado como unidade |

Essas unidades não são equivalentes. Podem possuir tamanhos e regras diferentes. Uma camada não deve usar automaticamente o tamanho de outra.

## 6. Exemplo guiado
Considere um SSD que apresenta setores lógicos de 512 bytes. O sistema solicita o LBA 10. Para o host, essa solicitação identifica o décimo primeiro bloco lógico, porque a contagem começa em zero. O controlador traduz o pedido para sua organização interna, que pode envolver páginas NAND e mapeamentos diferentes.

O sistema operacional não precisa saber qual página física foi usada. Precisa saber que o dispositivo concluiu a leitura ou reportou um erro.

## 7. Arquitetura que estamos construindo
O ZenithOS deve separar:
1. formato de disco e estruturas lógicas;
2. camada de armazenamento e validação de requisições;
3. driver que conhece a interface do dispositivo;
4. controlador que administra o hardware;
5. mídia física que guarda os dados.

Essa separação permite que o mesmo sistema utilize dispositivos com organizações internas diferentes.

## 8. Método de estudo
Desenhe duas representações do mesmo dispositivo. Na primeira, mostre a mídia física e o controlador. Na segunda, mostre a sequência de LBAs apresentada ao sistema. Compare o que cada camada conhece e o que permanece escondido.

## 9. Erros comuns
- Achar que o sistema operacional precisa manipular diretamente as células NAND.
- Confundir setor lógico com página NAND.
- Tratar bloco de alocação e bloco de apagamento como a mesma unidade.
- Achar que o controlador substitui completamente o driver. O controlador é hardware; o driver é código que o sistema operacional usa para comunicar com ele.

## 10. Exercícios de compreensão
1. Qual é a diferença entre organização física e organização lógica?
2. Por que o ZenithOS não precisa conhecer diretamente as células NAND de um SSD?
3. Qual é a diferença entre um setor lógico de 4.096 bytes e um bloco de apagamento NAND?
4. Por que não devemos tratar todos os tipos de blocos como se fossem iguais?
5. Se dois SSDs possuem estruturas físicas diferentes, como o ZenithOS pode utilizar ambos por meio de uma arquitetura comum?
6. Qual é a diferença entre controlador e driver?
7. O que o sistema operacional precisa receber depois de solicitar uma leitura?

## 11. Anotações originais do estudante
As respostas abaixo foram registradas durante o estudo inicial e são mantidas como histórico de aprendizagem.

- **Organização física e lógica:** a física trata de como a mídia guarda os dados; a lógica é como o sistema representa e endereça o espaço.
- **Controlador NAND:** o controlador administra o funcionamento interno do SSD.
- **Setor lógico e bloco de apagamento:** o setor lógico é apresentado ao sistema operacional para endereçamento; o bloco de apagamento reúne páginas NAND que o controlador apaga como unidade.
- **Tipos de bloco:** cada unidade precisa ser tratada conforme a camada em que existe.
- **Uso de SSDs diferentes:** a interface lógica, a camada de drivers e os controladores permitem que o ZenithOS use dispositivos diferentes sem conhecer todos os detalhes físicos.

## Critério de conclusão
Você deve explicar a diferença entre físico e lógico, descrever o papel do controlador e distinguir pelo menos três unidades de armazenamento de camadas diferentes.

## Metadados
- Dificuldade: Fácil
- Duração: 35 minutos
