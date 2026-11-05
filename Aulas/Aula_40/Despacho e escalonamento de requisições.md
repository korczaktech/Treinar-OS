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

1. Qual problema esta aula procura resolver?
2. Quais informações precisam ser conhecidas antes de executar a operação estudada?
3. Que dado inválido poderia causar acesso fora dos limites ou perda de consistência?
4. Qual responsabilidade pertence ao ZenithOS e qual pertence ao driver?
5. Que teste automatizado ajudaria a detectar uma implementação incorreta?

## 6. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
