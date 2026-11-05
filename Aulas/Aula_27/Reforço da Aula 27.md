# Reforço da Aula 27 — Alinhamento de partições e limites físicos

## Regra de conversão
Para transformar uma fronteira de alinhamento em LBAs, divida o tamanho da fronteira em bytes pelo tamanho do setor lógico, quando a divisão for exata.

## Exemplo
Setor lógico de 512 bytes e fronteira de 4.096 bytes: 4.096 / 512 = 8 LBAs. Inícios 0, 8, 16 e 24 respeitam esse alinhamento. O LBA 25 não respeita.

## Cuidados
Alinhamento de partição não é alinhamento de buffer DMA nem de estruturas na RAM. O alinhamento pode evitar trabalho extra, mas não garante por si só desempenho nem integridade.

## Perguntas
1. Quantos setores lógicos de 512 bytes formam 4 KiB?
2. O LBA 40 está alinhado a uma fronteira de 8 setores?
3. Por que alinhamento inadequado não significa necessariamente corrupção?
4. Quem informa requisitos específicos do dispositivo?
5. Por que o padrão de 8 bytes do ZenithOS não deve ser aplicado automaticamente às partições?
