# Reforço da Aula 17 — SSD e NAND

## 1. O SSD apresenta blocos lógicos

O host usa LBA. O controlador traduz esses endereços para posições internas da NAND. O LBA não revela a localização física.

## 2. Página e bloco de apagamento

A NAND é programada em páginas e apagada em unidades maiores. Por isso, atualizar dados pode exigir escrever uma nova página e invalidar a antiga.

## 3. FTL

Mantém o mapeamento entre endereços lógicos e localizações físicas e participa do gerenciamento da memória flash.

## 4. Coleta de lixo

Move páginas ainda válidas, apaga blocos que podem ser reutilizados e recupera espaço interno.

## 5. Desgaste e TRIM

Wear leveling distribui ciclos de apagamento. TRIM informa que certos LBAs não precisam mais preservar os dados para o host. Não é garantia de apagamento físico imediato.

## 6. Fixação

1. Quem traduz LBA para posição NAND?
2. Por que apagar exige unidade maior que a página?
3. O que acontece com uma página antiga após uma atualização?
4. Por que existe coleta de lixo?
5. TRIM é uma ferramenta de destruição segura?
6. O que o wear leveling tenta evitar?
