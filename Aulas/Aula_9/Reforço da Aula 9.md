# Reforço da Aula 9 — Limites de endereçamento e erros

## Regra de endereçamento
Com N blocos, os endereços válidos são [0, N). O último LBA é N−1. Exemplo: 100 blocos significa LBAs 0 a 99. O endereço 100 é inválido.

## Regra de faixa
Valide primeiro: total positivo; início não negativo; início menor que total; quantidade positiva. Depois verifique quantidade <= total − início. Assim, evita somar valores antes de saber se a faixa cabe.

## Tipos de falha
- Validação: o pedido já contém parâmetros inválidos.
- Execução: o pedido era válido, mas houve falha de comunicação, mídia, timeout ou remoção.

Não confunda falha com sucesso parcial. Se apenas parte dos blocos foi transferida, o resultado precisa informar isso.

## Perguntas de fixação
1. Qual é o último LBA de um dispositivo com 80 blocos?
2. A faixa com total 80, início 78 e quantidade 2 é válida?
3. Por que início igual a total deve ser rejeitado?
4. Cite duas falhas que podem acontecer depois da validação.
5. Por que não se deve converter timeout automaticamente em “dispositivo destruído”?
