# Diagnóstico de desempenho de armazenamento

## Objetivo

Nesta aula, você estudará diagnóstico de desempenho de armazenamento e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Latência mede duração de um pedido; throughput mede dados transferidos por tempo; IOPS mede operações por segundo. Os resultados dependem do tamanho do pedido, padrão sequencial ou aleatório, cache, concorrência e profundidade de fila.

## 2. Exemplo de funcionamento

Média pode esconder picos. Percentis p50, p95 e p99 ajudam a observar a distribuição. Um benchmark precisa declarar carga, duração, aquecimento, sincronização e se mede cache ou mídia.

## 3. Validação e segurança

Benchmarks de escrita podem sobrescrever dados e desgastar SSDs. Métricas isoladas não identificam a causa: CPU, memória, driver, barramento e dispositivo podem ser gargalos.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve registrar tempo em fila, tempo de serviço, tamanho de pedidos, erros e profundidade. Use dispositivos simulados e cargas controladas antes de alterar políticas.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Qual é a diferença entre latência, throughput e IOPS?
2. Por que p95 e p99 podem revelar problemas que a média esconde?
3. Calcule o throughput de 1.000 MiB transferidos em 10 segundos.
4. Por que o tamanho do bloco e o padrão de acesso precisam ser documentados?
5. Cite três camadas que podem ser responsáveis por um gargalo.
6. Por que benchmarks de escrita precisam de cuidado com dados e desgaste do SSD?

## 6. Métricas fundamentais
- **Latência:** tempo entre solicitar e concluir uma operação.
- **Throughput:** quantidade de dados transferidos por unidade de tempo.
- **IOPS:** quantidade de operações concluídas por segundo.
- **Profundidade de fila:** quantidade de pedidos pendentes ou em andamento.
- **Percentis:** p50, p95 e p99 mostram pontos da distribuição de latência.

Uma média baixa não garante que todas as operações sejam rápidas. p99 elevado pode indicar que uma pequena parte dos pedidos sofre atrasos importantes.

## 7. Carga de teste importa
Leitura sequencial, leitura aleatória, gravação sequencial e gravação aleatória podem produzir resultados muito diferentes. Tamanho do bloco, concorrência, aquecimento, cache e sincronização alteram o resultado. Um benchmark deve documentar essas condições para que a comparação seja justa.

## 8. Exemplo guiado
Se um teste transfere 1.000 MiB em 10 segundos, throughput médio é 100 MiB/s. Se conclui 2.000 operações em 10 segundos, IOPS médio é 200. Essas métricas não dizem sozinhas se a latência p99 é aceitável; precisamos observar a distribuição dos tempos.

## 9. Encontrar o gargalo
O atraso pode estar na fila do kernel, no driver, no barramento, no controlador, no dispositivo ou na sincronização da aplicação. Medir apenas o tempo total não identifica a camada responsável. O ZenithOS deve registrar tempos por etapa quando possível.

## 10. Método de aprendizagem
Defina hipótese, carga, métrica e resultado esperado antes de executar um teste. Altere uma variável por vez e compare resultados repetíveis. Não faça benchmarks destrutivos em dados importantes.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Difícil
> - **Duração:** 50 minutos
