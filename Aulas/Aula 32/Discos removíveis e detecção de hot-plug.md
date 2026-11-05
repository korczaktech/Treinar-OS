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

1. O que significa hot-plug e de quais componentes depende?
2. Por que o kernel deve bloquear novas requisições após detectar remoção?
3. Qual é a função de um contador de geração da conexão?
4. Como tratar uma conclusão tardia depois que o dispositivo foi removido?
5. Por que o buffer de uma operação pendente não pode ser liberado imediatamente?
6. O que deve ocorrer quando outro dispositivo ocupa o mesmo endereço de barramento?

## 6. Ciclo de vida de um dispositivo removível
Uma unidade pode passar por PRESENTE, REMOVENDO, AUSENTE e ERRO. Ao detectar remoção, o kernel impede novas requisições, marca referências como indisponíveis e trata operações pendentes. Não deve esperar indefinidamente por uma resposta que talvez nunca chegue.

A remoção física pode acontecer enquanto uma gravação está em andamento. O driver precisa comunicar o resultado real: sucesso confirmado, falha ou resultado desconhecido. Não invente conclusão.

## 7. Geração de conexão
Um identificador de geração distingue diferentes instâncias de conexão. Uma solicitação criada para a geração 4 não pode ser aceita como pertencente à geração 5 só porque o mesmo endereço de barramento foi reutilizado.

Isso evita que uma conclusão atrasada de uma unidade removida seja atribuída a uma unidade recém-conectada.

## 8. Exemplo guiado
Uma operação de leitura está pendente quando um pendrive é removido. O registro muda para REMOVENDO; novas operações são rejeitadas; a fila é encerrada conforme o protocolo; o pedido pendente recebe erro apropriado; os buffers só são liberados quando não houver mais acesso DMA possível.

## 9. Método de aprendizagem
Simule conexão, operação, remoção, conclusão tardia e reconexão. Verifique se nenhuma referência da conexão antiga pode afetar a nova.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
