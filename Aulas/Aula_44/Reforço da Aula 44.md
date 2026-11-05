# Reforço da Aula 44 — Níveis RAID

## Resumo dos níveis
- RAID 0: distribuição sem redundância.
- RAID 1: espelhamento.
- RAID 5: distribuição com paridade simples; tolera uma falha.
- RAID 6: paridade dupla; tolera duas falhas.
- RAID 10: espelhamento combinado com distribuição; depende de quais membros falham.

## Exemplo de capacidade
Quatro discos de 2 TB:
- RAID 0: aproximadamente 8 TB;
- RAID 5: aproximadamente 6 TB;
- RAID 6: aproximadamente 4 TB;
- RAID 10: aproximadamente 4 TB.

Capacidade não revela sozinha desempenho ou tolerância.

## Cuidados
RAID não substitui backup. Em RAID 10, falhas em dois membros do mesmo par podem destruir o conjunto, enquanto falhas em pares diferentes podem ser toleradas.

## Perguntas
1. Qual nível não possui redundância?
2. Quantas falhas RAID 5 e RAID 6 toleram?
3. Como RAID 10 pode tolerar duas falhas em alguns casos?
4. Calcule a capacidade aproximada de quatro discos de 1 TB em RAID 5.
5. Por que RAID não substitui backup?
