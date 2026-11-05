# Interrupções, Polling e Conclusão de Operações

## Objetivo

Depois de enviar uma operação ao dispositivo, o sistema precisa descobrir quando ela terminou. Duas estratégias comuns são polling e interrupções. Nesta aula vamos comparar seus comportamentos e entender como o kernel deve tratar notificações sem comprometer a estabilidade.

## 1. Como saber que terminou?

O dispositivo pode expor um estado ou mecanismo de notificação. O driver precisa detectar conclusão, erro ou mudança de estado e comunicar o resultado à camada superior.

Esperar sem estratégia pode desperdiçar CPU. Nunca verificar pode deixar pedidos sem conclusão.

## 2. Polling

Polling significa consultar repetidamente um estado para descobrir se houve mudança. É simples e pode ser útil em operações curtas, inicialização ou ambientes em que interrupções ainda não estão disponíveis.

Porém, consultar continuamente pode consumir CPU e barramento, especialmente se o dispositivo demorar.

Uma implementação deve ter limite ou condição de saída. Um loop infinito esperando o dispositivo pode travar o sistema.

## 3. Interrupções

Uma interrupção permite que o dispositivo ou controlador sinalize que precisa de atenção. O processador interrompe temporariamente o fluxo atual e executa uma rotina apropriada.

A rotina de interrupção deve ser curta. Ela pode reconhecer a notificação, capturar informações essenciais e adiar trabalho mais pesado para outro contexto.

## 4. Contexto de interrupção

Nem toda função segura em código comum é segura dentro de uma rotina de interrupção. Operações que podem bloquear, alocar memória sem garantia ou esperar por outro evento podem causar deadlock ou travamento.

O kernel deve definir quais ações são permitidas nesse contexto e quais precisam ser adiadas.

## 5. Interrupções compartilhadas e identificação

Uma linha ou vetor pode estar associado a mais de uma origem, dependendo da arquitetura. O driver precisa verificar se a notificação pertence ao seu dispositivo antes de tratá-la como conclusão própria.

Não assuma que toda interrupção recebida significa que sua solicitação terminou.

## 6. Polling e interrupção podem coexistir

Uma arquitetura pode usar polling em determinadas fases e interrupções em operação normal. Também pode usar polling em filas de alta frequência quando a relação entre latência e custo justificar.

A escolha depende de hardware, carga e objetivos de latência.

## 7. Timeout

Se a conclusão não chega dentro do prazo, o driver precisa tratar timeout. Isso não prova automaticamente que o dispositivo está fisicamente morto. Pode ser congestionamento, falha de comunicação ou operação lenta.

A política pode consultar estado, tentar recuperação ou marcar o dispositivo como indisponível. Repetir cegamente pode agravar a situação.

## 8. Aplicação no ZenithOS

O ZenithOS deve manter o tratamento de interrupção separado do processamento completo da operação. A rotina registra o evento; uma etapa segura atualiza estados, conclui pedidos e acorda solicitantes.

## 9. Perguntas de compreensão

1. O que é polling?
2. Qual o custo de consultar o dispositivo continuamente?
3. Por que a rotina de interrupção deve ser curta?
4. Por que não se deve bloquear dentro de uma rotina de interrupção?
5. Toda interrupção recebida pertence necessariamente ao driver que a observou?
6. Timeout prova que o hardware foi destruído?

## 10. Exercícios de código

- EXN1A14.nbx — implementar polling limitado com timeout.
- EXN2A14.nbx — processar eventos de conclusão e ignorar notificações que não pertencem à operação ativa.


## Método de estudo e exemplo guiado
Considere uma operação curta e outra que demora. Para a curta, polling limitado pode ser simples; para a longa, consultar continuamente desperdiça CPU e uma interrupção pode ser mais adequada. Desenhe a rotina de interrupção como uma etapa curta que registra o evento, e o trabalho pesado como processamento adiado. Inclua um timeout e diferencie “não chegou a conclusão” de “hardware destruído”.