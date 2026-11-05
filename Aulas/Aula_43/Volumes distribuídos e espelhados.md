# Volumes distribuídos e espelhados

## Objetivo

Nesta aula, você estudará volumes distribuídos e espelhados e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Distribuição divide dados entre dispositivos para capacidade ou paralelismo; espelhamento mantém cópias equivalentes para tolerar certas falhas. Cada estratégia possui custo e comportamento distintos.

## 2. Exemplo de funcionamento

No espelhamento, defina quando uma gravação é considerada concluída e como escolher cópia saudável para leitura. Em distribuição, perda de um membro pode tornar faixas inacessíveis.

## 3. Validação e segurança

Redundância não substitui backup: exclusão, corrupção lógica e malware podem ser replicados. Falhas simultâneas e erros silenciosos também podem comprometer o conjunto.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve expor estado de cada membro, divergências e capacidade útil. Não prometa proteção absoluta nem disponibilidade além das garantias reais.

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
