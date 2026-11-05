# Reforço da Aula 48 — Clonagem e duplicação de volumes

## 1. Ideia principal

Cópia física transfere blocos; clone lógico pode compartilhar dados até a primeira alteração. Consistência da origem é essencial.

## 2. Cuidados que não podem ser esquecidos

Evite sobreposição entre origem e destino. Identificadores duplicados podem conflitar; destino interrompido deve ficar marcado como incompleto.

## 3. Ligação com o ZenithOS

A implementação deve separar política, validação e acesso ao dispositivo. O gerenciador de volumes oferece uma abstração consistente, enquanto drivers executam operações específicas e comunicam falhas reais.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
