# Reforço da Aula 101 — Mapa físico e descoberta de memória

## Ideia central

O mapa físico informa quais regiões existem e qual é a finalidade conhecida de cada uma. O kernel ainda precisa validar, normalizar e reservar áreas antes de disponibilizar páginas ao alocador.

## Exemplo guiado

Região: início 0x100000, tamanho 0x300000. Limite exclusivo: 0x400000. A região inclui o endereço inicial e termina imediatamente antes de 0x400000. Se o tamanho da página for 0x1000, apenas páginas inteiras dentro do intervalo podem ser disponibilizadas. Uma região reservada que intercepte uma página impede que ela seja entregue por inteiro.

## Cinco cuidados

1. Detectar overflow em início + tamanho.
2. Não presumir que o mapa esteja ordenado.
3. Detectar sobreposições e entradas inválidas.
4. Não converter tipos desconhecidos em memória livre.
5. Subtrair kernel, bootloader e demais reservas antes de publicar páginas livres.

## Perguntas de revisão

1. Quem fornece o mapa físico durante o boot?
2. Por que o kernel precisa validar o mapa recebido?
3. Qual a vantagem de usar limite exclusivo?
4. O que acontece com uma página parcialmente reservada?
5. Por que parser e alocador devem ser módulos separados?

## Revisão ativa

Desenhe três regiões: uma utilizável, uma reservada e uma com tipo desconhecido. Mostre quais páginas completas podem ser candidatas à alocação e explique cada exclusão.
