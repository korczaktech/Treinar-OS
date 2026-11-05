# Reforço da Aula 2 — Organização física e lógica

## Organização física
É a maneira como a tecnologia do dispositivo guarda os dados. Em SSDs, células NAND armazenam estados de carga; o controlador administra programação, leitura, apagamento e remapeamento.

## Organização lógica
É a representação apresentada ao sistema operacional. A interface pode mostrar uma sequência de LBAs, sem revelar a posição física exata das células.

## Não confunda as unidades
- Setor lógico: unidade endereçável apresentada ao host.
- Página NAND: unidade usada em operações de programação/leitura da flash, conforme a tecnologia.
- Bloco de apagamento NAND: conjunto de páginas apagado como unidade pelo controlador.
- Bloco de alocação: unidade reservada pelo sistema de arquivos.

## Exemplo
Um SSD pode apresentar setores lógicos de 512 bytes, enquanto internamente programa páginas maiores e apaga blocos que reúnem muitas páginas. O controlador coordena essa diferença; o kernel usa a interface lógica.

## Perguntas de revisão
1. Qual a diferença entre organização física e lógica?
2. Por que o controlador abstrai as células NAND?
3. Por que setor lógico e bloco de apagamento não são equivalentes?
4. O que o driver acrescenta à abstração do controlador?
5. Como a separação de camadas permite usar SSDs diferentes?
