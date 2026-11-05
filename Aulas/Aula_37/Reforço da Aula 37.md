# Reforço da Aula 37 — Atomicidade e limites de operações

## Três garantias distintas
Atomicidade: operação observada como unidade. Consistência: invariantes continuam verdadeiras. Durabilidade: alteração persiste conforme a garantia prometida.

## Exemplo
Se o dispositivo garante atomicidade de 4 KiB, duas gravações de 4 KiB não formam automaticamente uma transação de 8 KiB. A camada superior precisa de mecanismo próprio para coordenar as duas.

## Cuidados
Flush trata de ordenação/persistência conforme o contrato; não torna várias operações indivisíveis. Sempre consulte tamanho, alinhamento e condições da garantia atômica.

## Perguntas
1. O que é atomicidade?
2. Como ela difere de durabilidade?
3. Por que duas gravações atômicas não formam automaticamente uma operação atômica maior?
4. O que flush garante e o que não garante?
5. Cite um mecanismo de sistema de arquivos que ajude a preservar consistência.
