# Reforço da Aula 16 — Timeouts e Recuperação

## 1. Timeout não explica a causa

Ele informa que o resultado não chegou no prazo. A causa pode ser lentidão, congestionamento, falha de comunicação ou dispositivo indisponível.

## 2. Repetição exige cuidado

Leituras geralmente podem ser repetidas com menos risco. Uma gravação pode ter sido executada sem que a confirmação chegasse. É preciso conhecer a semântica antes de tentar novamente.

## 3. Backoff

Aumenta o intervalo entre tentativas para evitar sobrecarregar o dispositivo. Deve existir limite de tentativas e de tempo total.

## 4. Remoção

Novas solicitações devem falhar. Operações antigas precisam ser encerradas com segurança e os buffers só podem ser liberados quando não houver mais acesso.

## 5. Fixação

1. O que timeout significa?
2. Por que uma escrita pode ser perigosa de repetir?
3. Para que serve backoff?
4. Por que tentativas precisam de limite?
5. O que deve acontecer com uma solicitação enviada a um dispositivo removido?


## Exemplo guiado: quando repetir?
Uma solicitação é rejeitada por parâmetro inválido: corrigir o parâmetro é necessário, repetir o mesmo pedido não ajuda. Outra solicitação sofre timeout: o resultado pode ser incerto, especialmente se era uma gravação. O driver precisa consultar o estado ou seguir a política de recuperação antes de repetir. Uma falha de mídia pode ser permanente para aquela região.

## Como revisar
Para cada erro, indique se a operação pode ser repetida, se precisa de consulta de estado e qual risco existe em repetir cegamente.