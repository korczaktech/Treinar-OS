# Setores lógicos, setores físicos e tamanhos avançados

## Objetivo

Nesta aula, você estudará setores lógicos, setores físicos e tamanhos avançados e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Setor lógico é a unidade endereçável pela interface de blocos; setor físico é a unidade física reportada. Em 512e, setores lógicos de 512 bytes podem estar apoiados em setores físicos de 4 KiB; em 4Kn, ambos são 4 KiB.

## 2. Exemplo de funcionamento

Tamanhos diferentes podem fazer uma gravação lógica pequena exigir trabalho interno adicional. O driver informa os tamanhos conhecidos para que camadas superiores escolham alinhamento e tamanho de operação adequados.

## 3. Validação e segurança

Setor lógico, setor físico, página NAND, bloco de apagamento e bloco de sistema de arquivos não são sinônimos. Use o tamanho lógico para endereçamento LBA e os demais dados para decisões específicas de camada.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve expor tamanhos reportados pelo dispositivo e manter cálculos de endereçamento na unidade lógica. Otimizações não devem presumir detalhes internos não anunciados.

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
