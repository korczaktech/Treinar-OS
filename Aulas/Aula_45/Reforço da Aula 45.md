# Reforço da Aula 45 — Reconstrução e sincronização de conjuntos RAID

## 1. Ideia principal

Reconstrução repõe dados em membro substituído; sincronização verifica ou iguala membros e paridade.

## 2. Cuidados que não podem ser esquecidos

Acompanhe progresso, erros e estado persistente. Outra falha durante reconstrução pode causar perda conforme o nível.

## 3. Ligação com o ZenithOS

A implementação deve separar política, validação e acesso ao dispositivo. O gerenciador de volumes oferece uma abstração consistente, enquanto drivers executam operações específicas e comunicam falhas reais.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
