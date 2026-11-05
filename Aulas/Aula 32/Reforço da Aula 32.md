# Reforço da Aula 32 — Discos removíveis e hot-plug

## Ciclo de vida
Conectar não é o mesmo que inicializar. Ao remover, o kernel bloqueia novas requisições, trata as pendentes e invalida referências antigas. Uma reconexão cria uma nova instância operacional.

## Exemplo
Uma leitura fica pendente e o pendrive é removido. O pedido deve receber erro ou resultado definido pelo protocolo. O buffer continua reservado até não existir possibilidade de DMA. Uma nova unidade no mesmo endereço não herda o pedido.

## Perguntas
1. O que é hot-plug?
2. Qual a diferença entre PRESENTE e PRONTO?
3. Por que a remoção bloqueia novas operações?
4. Para que serve a geração de conexão?
5. Quando o buffer pode ser liberado?
