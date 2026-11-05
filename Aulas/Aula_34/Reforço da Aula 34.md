# Reforço da Aula 34 — Setores lógicos e físicos

## Três modelos
- 512n: lógico 512 B, físico 512 B.
- 512e: lógico 512 B, físico 4.096 B.
- 4Kn: lógico 4.096 B, físico 4.096 B.

## Exemplo
Em 512e, oito setores lógicos de 512 bytes correspondem a um setor físico de 4.096 bytes. Uma gravação pequena desalinhada pode exigir trabalho interno adicional.

## Cuidados
Use tamanho lógico para endereçar LBAs. Use informações físicas para decisões de alinhamento. Não confunda setor com página NAND, bloco de apagamento ou unidade de alocação.

## Perguntas
1. O que caracteriza 512e?
2. Quantos setores lógicos de 512 bytes formam 4 KiB?
3. Qual tamanho entra no cálculo do deslocamento LBA?
4. Por que gravações desalinhadas podem custar mais?
5. Setor físico é o mesmo que bloco de apagamento NAND?
