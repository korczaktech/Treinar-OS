# Aula 3 — Identificação e endereçamento do armazenamento

## Objetivos de aprendizagem
Ao final, você deverá explicar o que é um endereço lógico, compreender o LBA, converter um LBA em deslocamento de bytes, identificar os limites válidos de um dispositivo e descrever como a solicitação atravessa as camadas do ZenithOS.

## 1. O problema do endereçamento
Imagine um SSD que apresenta 512 GB. Saber a capacidade não basta para ler um dado específico. O sistema precisa identificar uma unidade dentro do espaço disponibilizado, saber onde a região começa e termina e rejeitar endereços que não existem.

Um endereço de armazenamento identifica uma posição lógica dentro do espaço que o dispositivo apresenta ao sistema operacional.

## 2. Endereço lógico e posição física
O endereço lógico é a forma pela qual o host solicita uma unidade de armazenamento. Ele não precisa revelar a posição física exata onde os dados estão gravados.

Em um SSD, o controlador pode mover dados entre páginas NAND, remapear regiões e realizar coleta de lixo. O mesmo LBA lógico pode ser atendido por diferentes posições físicas ao longo do tempo.

Por isso, o ZenithOS trabalha com a interface lógica e deixa o controlador administrar os detalhes internos da mídia.

## 3. LBA — Logical Block Addressing
LBA significa endereçamento lógico de blocos. Cada bloco lógico recebe um número sequencial:
| LBA | Posição |
|---:|---|
| 0 | Primeiro bloco |
| 1 | Segundo bloco |
| 2 | Terceiro bloco |
| 3 | Quarto bloco |

A numeração começa em zero. Se o dispositivo possui 100 blocos, os endereços válidos são 0 até 99.

## 4. Converter LBA em deslocamento de bytes
Para encontrar o deslocamento inicial em bytes, multiplicamos o LBA pelo tamanho do setor lógico:

deslocamento_em_bytes = LBA × tamanho_do_setor_lógico

Exemplo com setores lógicos de 512 bytes:
- LBA 0: 0 × 512 = 0 bytes.
- LBA 1: 1 × 512 = 512 bytes.
- LBA 10: 10 × 512 = 5.120 bytes.

Com setores lógicos de 4.096 bytes:
- LBA 5: 5 × 4.096 = 20.480 bytes.

O tamanho lógico precisa ser obtido das informações do dispositivo. Não suponha que todos os dispositivos usem 512 bytes.

## 5. Quantidade de blocos e maior LBA
Se um dispositivo apresenta N blocos, o intervalo válido é [0, N). O maior LBA válido é N−1.

Exemplo:
- quantidade total: 200 blocos;
- primeiro LBA: 0;
- último LBA: 199;
- LBA 200: inválido.

Não confunda a quantidade total com o último endereço. Essa diferença evita erros de uma posição (*off-by-one*).

## 6. Como a solicitação chega ao ZenithOS
As responsabilidades são separadas:
1. O sistema de arquivos ou serviço solicita uma operação.
2. A camada de armazenamento recebe o dispositivo e o LBA.
3. A camada valida endereço, quantidade e buffer.
4. O driver traduz o pedido para a interface do hardware.
5. O controlador executa a operação no dispositivo.
6. O resultado retorna ao sistema.

O sistema de arquivos não precisa conhecer a localização de cada célula NAND, e o driver não precisa interpretar nomes de arquivos.

## 7. Exemplo guiado
Um dispositivo possui 200 blocos lógicos de 4.096 bytes. O sistema solicita leitura do LBA 5:
1. O endereço 5 está dentro de 0 até 199.
2. O deslocamento inicial é 5 × 4.096 = 20.480 bytes.
3. Se a solicitação for de um bloco, o buffer precisa comportar 4.096 bytes.
4. A camada valida os parâmetros antes de encaminhar o pedido.
5. O driver executa a leitura e retorna sucesso ou erro.

Se o sistema solicitar o LBA 200, a operação deve ser rejeitada antes do acesso ao hardware.

## 8. Método de estudo
Sempre escreva quatro dados: quantidade total de blocos, intervalo válido, tamanho lógico e LBA solicitado. Depois calcule o deslocamento e explique por que o endereço está dentro ou fora dos limites. Faça isso primeiro para um bloco e depois para uma faixa.

## 9. Erros comuns
- Confundir LBA com endereço físico NAND.
- Usar o tamanho de setor errado na conversão.
- Considerar que N é um LBA válido quando N é a quantidade total.
- Confundir quantidade de blocos com maior endereço.
- Supor que o driver e o controlador sejam a mesma camada.

## 10. Exercícios de compreensão
1. Qual é a diferença entre um endereço lógico e uma posição física dentro do SSD?
2. Se um dispositivo possui setores lógicos de 4.096 bytes, quanto representa o início do LBA 5 em bytes?
3. Por que o ZenithOS não precisa conhecer a posição exata de cada célula NAND?
4. Um dispositivo possui 200 blocos, numerados de 0 a 199. Uma solicitação tenta acessar o bloco 200. O que deve acontecer?
5. Por que precisamos separar a camada de armazenamento do driver do dispositivo?
6. Um dispositivo apresenta 500 blocos lógicos. Qual é o intervalo válido e qual é o maior LBA?
7. Se o tamanho lógico é 512 bytes, qual deslocamento corresponde ao LBA 12?

## 11. Anotações originais do estudante
As respostas abaixo foram registradas durante o estudo inicial e são mantidas como histórico de aprendizagem.

- **Endereço lógico e posição física:** o endereço lógico representa a posição pela interface; ele não revela diretamente a localização física da mídia.
- **LBA 5 com setores de 4.096 bytes:** 20.480 bytes.
- **Por que não acessar células NAND diretamente:** o controlador administra a organização interna e suas particularidades.
- **Acesso ao LBA 200 em um dispositivo de 200 blocos:** deve ser rejeitado por estar fora dos limites.
- **Separação entre camada e driver:** cada componente possui uma responsabilidade diferente.

## Critério de conclusão
Você deve conseguir explicar LBA, calcular deslocamentos, identificar os endereços válidos e descrever o caminho da solicitação sem confundir endereçamento lógico e físico.

## Metadados
- Dificuldade: Média
- Duração: 35 minutos
