# Reforço da Aula 34 — Setores lógicos, setores físicos e tamanhos avançados

## 1. Ideia principal

Setor lógico é a unidade endereçável; setor físico é a unidade física reportada. 512e e 4Kn são exemplos de relações diferentes entre tamanhos.

## 2. Cuidados que não podem ser esquecidos

Use tamanho lógico para LBA. Não confunda setores com páginas NAND ou blocos de sistema de arquivos.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
