# Integridade e recuperação de tabelas de partição

## Objetivo

Nesta aula, você estudará integridade e recuperação de tabelas de partição e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Tabelas podem ser corrompidas por desligamento, falha de gravação, defeito ou ferramenta incorreta. GPT possui cópias principal e de backup e CRCs; MBR clássico não oferece a mesma redundância.

## 2. Exemplo de funcionamento

O diagnóstico verifica cada cópia, compara posições e entradas e identifica divergências. Uma cópia válida pode estar desatualizada; não basta escolher automaticamente a que passou no CRC.

## 3. Validação e segurança

CRC não prova autenticidade. Reparar modifica dados persistentes: preserve uma imagem quando possível, explique a origem dos dados recuperados e não invente entradas quando não houver evidência suficiente.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

A primeira versão do ZenithOS deve diagnosticar sem reparar. Um futuro reparador deverá ser explícito, gerar plano verificável e exigir autorização antes de escrever.

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
