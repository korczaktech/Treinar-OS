# Reforço da Aula 30 — Validação defensiva de metadados

## Ordem de validação
Comece pelo tamanho mínimo do buffer; valide assinatura e versão; imponha limites; verifique multiplicações e somas; valide offsets; depois examine referências e estruturas relacionadas.

## Exemplo
Uma matriz possui 200 entradas de 64 bytes. Seu tamanho é 12.800 bytes. Antes de acessar, confirme que a multiplicação é representável e que o intervalo completo cabe no volume.

## Segurança
Ciclos, profundidade excessiva e declarações enormes podem consumir CPU e memória. O parser deve falhar de modo controlado. Diagnóstico e reparo são etapas separadas.

## Perguntas
1. Por que o parser não deve confiar em um tamanho declarado?
2. O que precisa ser verificado antes de ler uma matriz?
3. Como um ciclo pode prejudicar o parser?
4. Por que impor limites de memória e profundidade?
5. Qual é a diferença entre rejeitar dados inválidos e reparar o disco?
