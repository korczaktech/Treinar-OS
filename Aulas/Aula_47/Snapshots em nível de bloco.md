# Snapshots em nível de bloco

## Objetivo

Nesta aula, você estudará snapshots em nível de bloco e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Snapshot preserva uma visão anterior do volume enquanto gravações continuam. Copy-on-write guarda a versão antiga antes de sobrescrever o bloco; outras estratégias redirecionam gravações para novas áreas.

## 2. Exemplo de funcionamento

Mapas relacionam blocos lógicos às versões físicas. Snapshots podem compartilhar blocos, exigindo contagem de referências ou estrutura equivalente. Metadados crescem conforme blocos mudam.

## 3. Validação e segurança

Snapshot não é necessariamente backup e pode ser perdido com o mesmo dispositivo. Espaço reservado pode acabar; o sistema precisa definir comportamento quando não consegue preservar uma versão.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

No ZenithOS, snapshots devem ter escopo e limites explícitos. Proteja mapas e referências e teste interrupções durante suas atualizações.

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
