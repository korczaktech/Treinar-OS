# Timeouts, Erros e Recuperação de Dispositivos

## Objetivo

Um dispositivo pode demorar, responder com erro ou deixar de responder. Um kernel robusto precisa transformar essas situações em resultados controlados. Nesta aula vamos estudar categorias de erro, timeout, tentativas repetidas, recuperação e remoção segura do dispositivo.

## 1. Erros diferentes exigem tratamentos diferentes

Exemplos:
- parâmetro inválido: erro detectado antes de enviar ao hardware;
- faixa fora dos limites: solicitação rejeitada;
- falha de comunicação: o driver não conseguiu completar o protocolo;
- erro de mídia: o dispositivo reportou problema ao acessar determinada região;
- timeout: a conclusão não chegou no prazo;
- dispositivo removido: a unidade deixou de estar disponível.

Um único código genérico dificulta diagnóstico e recuperação.

## 2. Timeout é um limite de espera

Timeout define quanto tempo o sistema aceita esperar por uma etapa. O valor precisa considerar a operação, o dispositivo e o contexto. Um tempo curto demais gera falsos erros; longo demais pode deixar o sistema aparentemente travado.

O timeout não prova a causa. Ele apenas informa que o resultado esperado não chegou dentro do prazo.

## 3. Repetir operações

Uma tentativa repetida pode ser útil em falhas transitórias, mas nem toda operação é segura para repetição.

Uma leitura normalmente não altera o conteúdo. Uma gravação pode ter sido executada mesmo que a confirmação tenha se perdido. Repetir uma gravação sem conhecer a semântica pode produzir efeitos duplicados em operações que não sejam idempotentes.

O driver precisa saber se a operação é repetível e em quais condições.

## 4. Backoff

Quando uma falha transitória permite nova tentativa, backoff aumenta o intervalo entre tentativas. Isso evita sobrecarregar um dispositivo que já está com dificuldade.

Um limite máximo de tentativas e de tempo total evita loops intermináveis.

## 5. Recuperação escalonada

Uma política pode:
1. registrar o erro;
2. verificar o estado do dispositivo;
3. aguardar e repetir se a operação for segura;
4. reinicializar a fila ou interface se permitido;
5. marcar o dispositivo como degradado ou indisponível;
6. notificar a camada superior.

Nem todo dispositivo suporta reinicialização durante operações ativas. O contrato do driver é determinante.

## 6. Remoção e operações pendentes

Quando uma unidade é removida, novas solicitações devem ser rejeitadas. Operações em andamento precisam receber resultado definido e seus buffers só podem ser liberados depois que não houver mais acesso pelo dispositivo.

Identificadores e referências antigas precisam ser invalidados sem confundir uma unidade recém-conectada com a anterior.

## 7. Logs e diagnóstico

Registre tipo do erro, dispositivo, operação, faixa afetada, etapa e número da tentativa. Evite registrar conteúdo sensível dos buffers.

Logs devem ajudar a investigar sem expor dados privados nem inundar o sistema em falhas repetidas.

## 8. Aplicação no ZenithOS

O ZenithOS deve definir erros tipados, prazos por operação, política de repetição e estados de saúde do dispositivo. A camada superior recebe um resultado compreensível, enquanto o driver preserva detalhes técnicos úteis para diagnóstico.

## 9. Perguntas de compreensão

1. Timeout revela necessariamente a causa da falha?
2. Por que uma gravação não deve ser repetida cegamente?
3. O que é backoff?
4. Por que limitar tentativas?
5. O que acontece com novas operações após remoção do dispositivo?
6. Quais dados ajudam a diagnosticar uma falha?

## 10. Exercícios de código

- EXN1A16.nbx — classificar erros e escolher ações permitidas.
- EXN2A16.nbx — calcular agenda de tentativas com backoff e limite máximo.


## Método de estudo e exemplo guiado
Classifique cinco situações: parâmetro inválido, timeout, erro de mídia, falha de comunicação e remoção. Para cada uma, decida se a operação pode ser repetida. Uma leitura pode ser repetível em algumas condições; uma gravação pode ter resultado incerto se a conexão cair depois que o dispositivo recebeu o comando. Simule backoff com limite máximo e um número finito de tentativas. Explique por que repetir cegamente pode piorar a falha.

## Metadados da aula
- Dificuldade: Difícil
- Duração: 45 minutos
