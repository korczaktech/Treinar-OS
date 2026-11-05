# Reforço da Aula 49 — TRIM, discard e liberação de blocos

## Fluxo correto
O sistema de arquivos libera uma faixa; confirma que ela não possui referências ativas; agrupa pedidos compatíveis; consulta suporte, granularidade e limites; envia discard; trata o resultado.

## Exemplo
A faixa [1.000, 1.100) foi liberada. Se um snapshot ainda referencia parte dos blocos, não descarte essa parte. O dispositivo precisa preservar dados que ainda podem ser usados.

## O que discard não significa
Não garante apagamento físico imediato, não é apagamento seguro e não garante que a leitura posterior retorne zeros.

## Perguntas
1. O que o comando discard comunica ao dispositivo?
2. Por que uma faixa ainda referenciada não pode ser descartada?
3. TRIM apaga fisicamente as células na hora?
4. Por que o suporte e os limites precisam ser consultados?
5. Qual a diferença entre liberar no sistema de arquivos e apagar fisicamente?
