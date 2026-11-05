# Reforço da Aula 36 — Leitura e escrita parcial de blocos

## Offset e LBA
Divida o offset em bytes pelo tamanho do setor. O quociente é o LBA relativo; o resto é a posição dentro do setor.

Exemplo: 1.300 bytes / 512 = LBA 2, resto 276.

## Leitura-modificação-escrita
Quando só há transferência de setores completos, a camada lê o setor, altera a parte desejada e grava o setor inteiro. Se duas operações modificarem o mesmo setor ao mesmo tempo, uma pode apagar a alteração da outra. É necessário coordenar o acesso.

## Exemplo de fronteira
Alterar 20 bytes a partir do offset 500, com setores de 512 bytes, afeta 12 bytes do primeiro setor e 8 bytes do seguinte.

## Perguntas
1. O que o quociente da divisão do offset representa?
2. O que o resto representa?
3. Quantos setores o exemplo de offset 500 afeta?
4. Por que leitura-modificação-escrita pode perder atualizações?
5. Por que escrita parcial não é automaticamente atômica?
