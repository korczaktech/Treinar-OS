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
