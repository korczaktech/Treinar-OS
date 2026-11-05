# Reforço da Aula 1 — Fundamentos do armazenamento

## 1. Conceitos essenciais
- Bit: unidade que representa 0 ou 1.
- Byte: grupo de 8 bits.
- Bloco lógico: unidade endereçável apresentada pela interface de armazenamento.
- Dispositivo: hardware ou unidade virtual que oferece armazenamento.
- Formato: regras para interpretar a organização dos dados.

## 2. Exemplo
Um dispositivo apresenta 1.000 blocos de 512 bytes:
- capacidade: 1.000 × 512 = 512.000 bytes;
- primeiro LBA: 0;
- último LBA: 999.

Mesmo conhecendo capacidade e endereços, o sistema ainda não sabe quais regiões contêm partições, volumes ou arquivos.

## 3. A ideia mais importante
Hardware guarda e transfere dados. Formatos e sistemas de arquivos dão significado e organização a esses dados. O ZenithOS precisa de ambos, com responsabilidades separadas.

## 4. Perguntas de revisão
1. Quantos bits formam um byte?
2. Qual é a diferença entre um bloco lógico e um arquivo?
3. Por que capacidade não significa organização?
4. Qual é a função de um formato?
5. O que precisa existir entre o sistema de arquivos e o hardware?
