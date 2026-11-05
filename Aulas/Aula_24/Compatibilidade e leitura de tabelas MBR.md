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

1. Quais informações principais são encontradas no MBR clássico?
2. Para que serve uma partição estendida?
3. Qual é o papel de um EBR?
4. Por que um parser de EBR precisa detectar ciclos e limitar a quantidade de passos?
5. O que deve acontecer se uma partição lógica ultrapassar os limites da partição estendida?
6. Por que o MBR protetor de GPT não deve ser interpretado como uma tabela MBR convencional?

## 6. Estrutura do MBR clássico
O MBR clássico ocupa o primeiro setor lógico e reserva espaço para código de inicialização, identificador do disco, quatro entradas de partição e uma assinatura final. Cada entrada descreve tipo, início e tamanho. Os campos históricos CHS também podem aparecer, mas sistemas modernos normalmente usam os campos LBA para localizar regiões.

As quatro entradas não significam que só possam existir quatro volumes no total. Uma entrada pode descrever uma partição estendida, que contém uma cadeia de registros EBR para partições lógicas.

## 7. Como percorrer uma cadeia EBR
O primeiro EBR é localizado a partir do início da partição estendida. Cada registro pode descrever a partição lógica atual e apontar para o próximo EBR. Os endereços relativos seguem regras específicas do formato; não some todos os campos ao mesmo ponto de referência.

O parser deve limitar a quantidade de registros percorridos, detectar endereços repetidos, impedir ciclos e garantir que todos os EBRs e partições lógicas permaneçam dentro da região estendida e do disco.

## 8. Exemplo guiado
Imagine uma partição estendida entre os LBAs 10.000 e 50.000. Um EBR encontrado nela aponta para uma partição lógica que ultrapassa o LBA 50.000. Mesmo que o registro tenha assinatura correta, a partição lógica é inválida e não pode ser publicada.

## 9. Limites de compatibilidade
MBR possui limitações de endereçamento e quantidade de entradas. O ZenithOS pode suportá-lo para compatibilidade, mas deve preferir GPT em cenários modernos quando o ambiente permitir. Um MBR protetor de GPT não deve ser apresentado como mapa MBR válido de partições convencionais.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos


## Método de estudo
Desenhe o primeiro setor lógico e marque o código de inicialização, o identificador do disco, as quatro entradas e a assinatura. Depois crie uma partição estendida e percorra uma cadeia de EBRs. Em cada passo, anote o endereço do registro, a referência relativa, o intervalo da partição lógica e os limites da região estendida. Termine simulando um ciclo e uma entrada fora dos limites.
