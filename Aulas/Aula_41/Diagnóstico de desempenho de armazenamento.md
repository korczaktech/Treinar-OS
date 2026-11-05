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

1. Qual problema esta aula procura resolver?
2. Quais informações precisam ser conhecidas antes de executar a operação estudada?
3. Que dado inválido poderia causar acesso fora dos limites ou perda de consistência?
4. Qual responsabilidade pertence ao ZenithOS e qual pertence ao driver?
5. Que teste automatizado ajudaria a detectar uma implementação incorreta?

## 6. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Difícil
> - **Duração:** 50 minutos
