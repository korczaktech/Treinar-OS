# Reforço da Aula 25 — Descoberta e identificação de dispositivos

## 1. Ideia principal

Descoberta enumera hardware, identifica interfaces e consulta capacidades. Identidade física, caminho de conexão e identificador interno não são a mesma coisa.

## 2. Cuidados que não podem ser esquecidos

Não trate número interno como identidade permanente. Valide respostas, capacidades e estado antes de registrar dispositivo.

## 3. Ligação com o ZenithOS

A camada responsável deve validar os dados antes de encaminhar operações e expor um contrato claro às camadas superiores. O driver continua responsável pelos detalhes específicos do dispositivo.

## 4. Revisão

1. Explique a ideia principal sem consultar a aula.
2. Cite duas validações importantes.
3. Descreva uma falha que o sistema precisa detectar.
4. Explique como o ZenithOS deve reagir sem comprometer dados ou memória.
