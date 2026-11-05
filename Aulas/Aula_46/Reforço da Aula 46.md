# Reforço da Aula 46 — Falhas parciais e degradação de conjuntos RAID

## 1. Ideia principal

Conjunto degradado perdeu parte da redundância, mas pode continuar oferecendo dados conforme o nível e as falhas.

## 2. Cuidados que não podem ser esquecidos

Registre divergências e saúde de cada membro. Não apresente conjunto degradado como saudável nem esconda risco de nova falha.

## 3. Ligação com o ZenithOS

A implementação deve separar política, validação e acesso ao dispositivo. O gerenciador de volumes oferece uma abstração consistente, enquanto drivers executam operações específicas e comunicam falhas reais.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
