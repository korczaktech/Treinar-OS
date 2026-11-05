# Falhas parciais e degradação de conjuntos RAID

## Objetivo

Nesta aula, você estudará falhas parciais e degradação de conjuntos raid e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Conjunto degradado perdeu membro ou redundância, mas ainda pode disponibilizar alguns dados. O comportamento depende do nível, da posição e da quantidade de falhas.

## 2. Exemplo de funcionamento

Gravações podem alcançar alguns membros e falhar em outros. O sistema registra divergência; leituras podem exigir paridade ou escolha de cópia válida. Erros silenciosos exigem verificação.

## 3. Validação e segurança

Em estado degradado, outra falha pode ser fatal. O sistema pode limitar operações, sinalizar urgência e impedir alterações administrativas perigosas. Não apresente o estado como normal.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS expõe saúde por membro e saúde geral do conjunto. Cada operação consulta o estado e aplica a política de leitura, gravação e recuperação.

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
