# Dispositivos compostos e encadeamento de volumes

## Objetivo

Nesta aula, você estudará dispositivos compostos e encadeamento de volumes e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Um dispositivo composto apresenta interface própria, mas encaminha operações para dispositivos inferiores. Pode representar uma faixa, concatenação ou camada de transformação.

## 2. Exemplo de funcionamento

O mapeamento valida a faixa na entrada e traduz segmentos para a camada inferior. Pedidos que cruzam fronteiras podem ser divididos. O grafo de dependências não pode conter ciclos.

## 3. Validação e segurança

Propague falhas inferiores e remoções para todos os volumes dependentes. Controle referências e operações pendentes para evitar uso de objetos liberados.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

No ZenithOS, dispositivos compostos declaram dependências e capacidades derivadas. A capacidade publicada nunca excede a região respaldada.

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
> - **Duração:** 60 minutos
