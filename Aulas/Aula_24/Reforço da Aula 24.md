# Reforço da Aula 24 — Compatibilidade e leitura de MBR

## 1. Estrutura básica
O MBR clássico contém código de inicialização, identificador do disco, quatro entradas de partição e assinatura. Uma partição estendida permite descrever partições lógicas por meio de EBRs encadeados.

## 2. Exemplo de validação
Se uma partição estendida ocupa [10.000, 50.000), nenhuma partição lógica descrita por seus EBRs pode escapar desse intervalo. Uma entrada que termina em 50.001 é inválida, mesmo que a assinatura do EBR esteja correta.

## 3. Cuidados com EBR
O encadeamento pode estar corrompido. O parser precisa limitar passos, detectar endereços repetidos, impedir ciclos e validar a referência de cada registro. Os campos relativos devem ser interpretados conforme a regra do formato.

## 4. Compatibilidade
MBR é legado e possui limites. GPT é preferível em cenários modernos compatíveis. MBR protetor não é mapa MBR convencional.

## 5. Perguntas de revisão
1. Quantas entradas primárias existem no MBR clássico?
2. Qual é a função da partição estendida?
3. O que o EBR descreve?
4. Como detectar uma cadeia de EBRs cíclica?
5. Por que uma partição lógica deve caber dentro da região estendida?
