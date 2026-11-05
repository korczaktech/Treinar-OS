# Reforço da Aula 42 — Dispositivos compostos

## Composição
Um dispositivo composto oferece uma interface lógica e encaminha pedidos para membros inferiores. Concatenação coloca regiões em sequência; mapeamento traduz faixas; outras camadas podem transformar dados.

## Exemplo
A concatena A com 1.000 blocos e B com 2.000. O pedido lógico 990–1.009 cruza a fronteira: 10 blocos vêm de A e 10 de B.

## Cuidados
Divida operações que cruzam fronteiras, propague falhas, controle referências e rejeite ciclos no grafo de dependências. Capacidade publicada deve ser respaldada pelos membros.

## Perguntas
1. Qual a diferença entre concatenação e espelhamento?
2. Como mapear uma operação que cruza membros?
3. O que é um ciclo de dependência?
4. O que acontece quando um membro é removido?
5. Composição sempre oferece redundância?
