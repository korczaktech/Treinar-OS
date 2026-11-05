# Reforço da Aula 45 — Reconstrução e sincronização RAID

## Reconstrução
Após substituir um membro, o conjunto lê os membros restantes, calcula os dados ou paridade necessários e grava o novo membro. O processo percorre o volume e pode durar bastante.

## Verificação
Verificação procura divergências entre dados e paridade/cópias. Reconstrução produz conteúdo para um membro ausente. São tarefas relacionadas, mas não iguais.

## Exemplo
Em um espelho, A é saudável e B foi substituído. O sistema copia faixas de A para B. Se uma gravação nova atingir uma faixa já copiada, a política precisa garantir que B receba a versão mais recente.

## Cuidados
Persistir progresso, tratar erros, permitir retomada e informar que o conjunto continua vulnerável durante a reconstrução.

## Perguntas
1. Qual a diferença entre reconstruir e verificar?
2. Por que a reconstrução consome recursos?
3. Por que o conjunto fica vulnerável durante o processo?
4. Como tratar gravações concorrentes?
5. O que precisa ser salvo para retomar após reinicialização?
