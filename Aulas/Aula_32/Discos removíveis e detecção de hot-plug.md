# Discos removíveis e detecção de hot-plug

## Objetivo

Nesta aula, você estudará discos removíveis e detecção de hot-plug e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Hot-plug permite conectar ou remover dispositivos enquanto o sistema está ativo, quando barramento, controlador e driver suportam esse comportamento. Eventos podem vir de interrupções, notificações ou varredura.

## 2. Exemplo de funcionamento

Ao remover um dispositivo, o kernel marca-o como indisponível, bloqueia novas requisições e trata as pendentes. Um dispositivo reconectado pode ocupar o mesmo endereço físico, mas não deve herdar operações antigas.

## 3. Validação e segurança

Remoção pode interromper gravações e deixar dados em cache. Use estado e geração de conexão para detectar referências obsoletas; não espere indefinidamente por hardware ausente.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve modelar estados presente, removendo, ausente e erro. Cada operação precisa verificar se a referência ainda pertence à conexão atual.

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
