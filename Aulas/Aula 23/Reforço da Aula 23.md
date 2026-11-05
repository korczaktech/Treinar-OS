# Reforço da Aula 23 — Estrutura e validação da GPT

## 1. Componentes
A GPT possui cabeçalho principal, matriz de entradas e cópia de backup. O MBR protetor ocupa o início do disco para reduzir incompatibilidades com ferramentas antigas.

## 2. Exemplo de tamanho da matriz
Se há 128 entradas de 128 bytes, a matriz possui 16.384 bytes. O parser deve validar a multiplicação e a região antes de ler ou alocar memória.

## 3. CRC e segurança
CRC32 permite detectar alterações acidentais em relação ao checksum registrado. Não prova autoria e não impede que alguém altere dados e recalcule o CRC.

## 4. Procedimento seguro
Validar assinatura e cabeçalho; impor limites; validar posições; conferir CRC; ler entradas; validar cada partição; diagnosticar a cópia de backup. Divergência não deve provocar reparo automático sem análise.

## 5. Perguntas de revisão
1. Qual é a finalidade da cópia de backup da GPT?
2. Para que serve o MBR protetor?
3. Por que se valida o tamanho da matriz antes de alocar memória?
4. CRC32 é um mecanismo de autenticação? Explique.
5. Por que uma cópia válida pode ainda estar desatualizada?
