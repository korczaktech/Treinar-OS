# Reforço da Aula 50 — Projeto do gerenciador de volumes do ZenithOS

## 1. Ideia principal

Gerenciador interpreta partições, valida regiões, cria volumes, traduz endereços e publica unidades para sistemas de arquivos.

## 2. Cuidados que não podem ser esquecidos

Comece com modelo em memória e testes puros; depois conecte leitores GPT/MBR e montagem. Não publique volumes parcialmente validados.

## 3. Ligação com o ZenithOS

A implementação deve separar política, validação e acesso ao dispositivo. O gerenciador de volumes oferece uma abstração consistente, enquanto drivers executam operações específicas e comunicam falhas reais.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
