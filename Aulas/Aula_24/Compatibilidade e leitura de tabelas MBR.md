# Compatibilidade e leitura de tabelas MBR

## Objetivo

Nesta aula, você estudará compatibilidade e leitura de tabelas mbr e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

MBR clássico ocupa o primeiro setor lógico e contém código de inicialização, identificador do disco, quatro entradas de partição e assinatura. Entradas registram tipo, início e tamanho. Partições estendidas usam EBRs encadeados para descrever partições lógicas.

## 2. Exemplo de funcionamento

O leitor interpreta as entradas primárias e, quando existir uma partição estendida, percorre a cadeia de EBRs. Cada endereço de EBR é relativo conforme as regras do formato e precisa ser interpretado corretamente.

## 3. Validação e segurança

A cadeia pode conter ciclos, endereços inválidos e entradas fora da partição estendida. Limite a quantidade de passos e detecte endereços repetidos. MBR protetor de GPT não deve ser confundido com uma tabela MBR convencional.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS pode oferecer MBR como compatibilidade legada opcional. O parser deve validar todas as regiões e nunca permitir que uma partição lógica escape da região estendida ou do disco.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Qual problema esta aula procura resolver?
2. Quais informações precisam ser conhecidas antes de executar a operação estudada?
3. Que dado inválido poderia causar acesso fora dos limites ou perda de consistência?
4. Qual responsabilidade pertence ao ZenithOS e qual pertence ao driver?
5. Que teste automatizado ajudaria a detectar uma implementação incorreta?

## 6. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Média
> - **Duração:** 45 minutos
