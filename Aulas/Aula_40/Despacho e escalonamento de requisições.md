# Despacho e escalonamento de requisições

## Objetivo

Nesta aula, você estudará despacho e escalonamento de requisições e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

O despachante escolhe qual pedido encaminhar. FIFO, prioridade e agrupamento são políticas possíveis. Discos mecânicos e SSDs têm características diferentes; proximidade de LBA nem sempre é a melhor métrica.

## 2. Exemplo de funcionamento

Throughput mede trabalho por tempo; latência mede duração de cada pedido; justiça avalia se todos recebem oportunidade. Políticas que maximizam throughput podem causar starvation em pedidos de baixa prioridade.

## 3. Validação e segurança

Limite profundidade de fila e memória consumida. Aging pode reduzir starvation. Cancelamento e timeout precisam funcionar mesmo enquanto o pedido aguarda despacho.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve começar com política simples e previsível, medir resultados e só depois otimizar. Dependências e justiça devem ser preservadas.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Qual é a diferença entre despacho e escalonamento?
2. Como FIFO escolhe o próximo pedido?
3. O que é starvation e como aging pode reduzi-lo?
4. Por que maximizar throughput pode aumentar a latência?
5. Qual é a finalidade de uma política baseada em deadline?
6. Por que o ZenithOS deve medir antes de trocar sua política de escalonamento?

## 6. Políticas comuns
- **FIFO:** atende pela ordem de chegada. É simples e previsível, mas pode não maximizar desempenho.
- **Prioridade:** atende pedidos importantes antes de outros. Sem controle, pode deixar pedidos comuns esperando indefinidamente.
- **Aging:** aumenta gradualmente a prioridade de pedidos que esperam há muito tempo.
- **Agrupamento:** combina pedidos compatíveis para reduzir overhead.
- **Deadline:** tenta impedir que uma requisição ultrapasse um tempo máximo de espera definido pela política.

Nenhuma política é ideal para todos os dispositivos e cargas.

## 7. Métricas que entram em conflito
Throughput mede volume de dados por tempo. Latência mede quanto uma requisição demora. Justiça observa como o tempo de espera é distribuído. Melhorar uma métrica pode piorar outra.

Por exemplo, manter uma fila cheia pode aumentar throughput em um dispositivo, mas elevar latência para operações interativas.

## 8. Exemplo guiado
Três pedidos chegam: A de baixa prioridade, B e C de alta prioridade. Uma política estrita pode executar B e C primeiro repetidamente, deixando A sem atendimento. Aging aumenta a prioridade de A enquanto espera e reduz o risco de starvation.

## 9. Método de aprendizagem
Use uma pequena fila de pedidos com chegada, prioridade e duração. Simule FIFO e prioridade, compare ordem, espera e latência. Depois aplique aging e veja se todos recebem oportunidade.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
