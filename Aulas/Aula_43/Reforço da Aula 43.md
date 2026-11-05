# Reforço da Aula 43 — Volumes distribuídos e espelhados

## Distribuição
Divide dados entre membros para capacidade ou paralelismo. Sem redundância, a falha de um membro pode tornar parte do volume inacessível.

## Espelhamento
Mantém cópias equivalentes. O conjunto precisa definir quando uma gravação é considerada concluída e como lidar com cópias divergentes.

## Exemplo
Em um espelho, A conclui a gravação e B falha. O conjunto não pode declarar ambos sincronizados. Precisa registrar o estado degradado e planejar verificação ou reconstrução.

## Não é backup
Exclusão, corrupção lógica e malware podem ser replicados para todas as cópias.

## Perguntas
1. Qual é o objetivo da distribuição?
2. Qual é o objetivo do espelhamento?
3. Como tratar gravação concluída apenas em um membro?
4. Por que redundância não protege contra exclusão?
5. Como escolher uma cópia para leitura?
