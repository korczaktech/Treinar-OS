# Reforço da Aula 27 — Alinhamento de partições e limites físicos

## 1. Ideia principal

Alinhamento posiciona regiões em múltiplos de uma unidade. Setor lógico, setor físico, página NAND e bloco de apagamento pertencem a camadas diferentes.

## 2. Cuidados que não podem ser esquecidos

Consulte requisitos reais. O alinhamento interno de 8 bytes do ZenithOS não substitui alinhamento de partição ou DMA.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
