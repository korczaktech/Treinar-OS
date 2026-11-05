# Reforço da Aula 49 — TRIM, discard e liberação de blocos

## 1. Ideia principal

TRIM/discard informa ao dispositivo que faixas não precisam mais preservar dados, ajudando o gerenciamento interno de SSDs.

## 2. Cuidados que não podem ser esquecidos

Não significa apagamento seguro ou imediato. Só descarte faixas comprovadamente livres e respeite granularidade e limites.

## 3. Ligação com o ZenithOS

A implementação deve separar política, validação e acesso ao dispositivo. O gerenciador de volumes oferece uma abstração consistente, enquanto drivers executam operações específicas e comunicam falhas reais.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
