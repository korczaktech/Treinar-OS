# Reforço da Aula 31 — Integridade e recuperação de tabelas de partição

## Diagnosticar antes de reparar
GPT possui cópia principal e de backup. Cada uma precisa ser validada separadamente. CRC correto é apenas uma verificação; posições, dimensões e entradas também precisam fazer sentido.

## Exemplo
Se a cópia principal falha no CRC e a cópia de backup passa, existe uma candidata para recuperação. Ainda é necessário verificar se ela descreve o mesmo disco e se as partições cabem. Não faça a gravação sem decisão explícita.

## Política conservadora
Preserve evidências, evite sobrescrever a região danificada e documente de onde virão os dados restaurados. O MBR clássico não possui a mesma redundância da GPT.

## Perguntas
1. Por que CRC válido não prova validade semântica?
2. Qual é a vantagem da cópia GPT de backup?
3. Por que não escolher automaticamente uma cópia válida?
4. O MBR clássico tem redundância equivalente?
5. Quais cuidados vêm antes de escrever uma tabela recuperada?
