# Reforço da Aula 30 — Validação defensiva de metadados

## 1. Ideia principal

Metadados do disco são entrada não confiável. Valide assinatura, versão, tamanhos, referências, alinhamento, intervalos e profundidade.

## 2. Cuidados que não podem ser esquecidos

Detecte overflow, ciclos e alocações excessivas. Parser deve recusar inconsistências em vez de adivinhar.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
