# Reforço da Aula 22 — Particionamento e tabelas de partição

## 1. Ideia principal

Partição é uma faixa de LBAs, definida por início e quantidade. A tabela descreve onde começa, quanto ocupa e qual finalidade declara.

## 2. Cuidados que não podem ser esquecidos

Valide capacidade, limites, soma sem overflow e sobreposição. Partição não é sinônimo de sistema de arquivos.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
