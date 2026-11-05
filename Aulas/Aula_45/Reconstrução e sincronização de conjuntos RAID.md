# Reconstrução e sincronização de conjuntos RAID

## Objetivo

Nesta aula, você estudará reconstrução e sincronização de conjuntos raid e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Reconstrução repõe dados em um membro substituído usando membros restantes e, conforme o nível, dados e paridade. Sincronização também ocorre ao criar ou verificar um conjunto.

## 2. Exemplo de funcionamento

Acompanhe progresso por faixa, erros de leitura e gravação e estado persistente para retomar após reinicialização. Escritas concorrentes precisam ser coordenadas com a faixa em reconstrução.

## 3. Validação e segurança

Uma segunda falha durante reconstrução pode ser fatal, dependendo do nível. A leitura completa pode revelar setores irrecuperáveis. A prioridade equilibra tempo de recuperação e responsividade.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

No ZenithOS, reconstrução é tarefa controlada, cancelável e monitorável. Estados reconstruindo, sincronizado, degradado e falha devem ser explícitos.

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
> - **Duração:** 65 minutos
