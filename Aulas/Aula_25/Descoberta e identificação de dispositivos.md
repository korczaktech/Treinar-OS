# Descoberta e identificação de dispositivos

## Objetivo

Nesta aula, você estudará descoberta e identificação de dispositivos e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

A descoberta enumera controladores e dispositivos, identifica interfaces reconhecidas e consulta capacidades como quantidade de blocos, tamanho lógico, limites de transferência e comandos disponíveis. Identidade física, caminho de conexão e identificador interno são conceitos distintos.

## 2. Exemplo de funcionamento

Um dispositivo pode receber um número interno durante o boot, mas esse número pode mudar após reinicialização. Se o hardware for removido e outro ocupar o mesmo endereço, referências antigas não podem passar a representar o novo dispositivo.

## 3. Validação e segurança

Tratar respostas incompletas, capacidades absurdas, timeouts e remoção durante descoberta. Não assumir que um endereço de barramento é identidade permanente. Validar capacidades antes de registrar o dispositivo.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve registrar dispositivos em uma estrutura comum com identificador, estado, capacidades e driver responsável. As camadas superiores não devem depender de endereços específicos do barramento.

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
