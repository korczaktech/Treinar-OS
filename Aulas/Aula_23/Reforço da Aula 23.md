# Reforço da Aula 23 — Estrutura e validação da tabela GPT

## 1. Ideia principal

GPT usa cabeçalhos, matriz de entradas, CRCs e cópia de backup; um MBR protetor não deve ser lido como tabela principal.

## 2. Cuidados que não podem ser esquecidos

CRC detecta corrupção acidental, não autenticidade. Limite tamanhos e contagens antes de alocar ou ler entradas.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
