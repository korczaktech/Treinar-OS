# Reforço da Aula 9 — Organização e Alocação de Arquivos

## 1. Partição é espaço; sistema de arquivos é organização

Uma partição delimita uma região do dispositivo. O sistema de arquivos organiza essa região em arquivos, diretórios e metadados.

Encontrar uma partição não significa encontrar automaticamente uma árvore de diretórios.

## 2. Caminho não é LBA

O caminho /documentos/relatorio.txt identifica a posição lógica de um arquivo. O sistema de arquivos consulta metadados para descobrir onde os bytes estão. O caminho não informa diretamente o LBA.

## 3. Unidades de alocação

Imagine uma unidade de 4096 bytes. Um arquivo de 1000 bytes pode reservar uma unidade inteira. Um arquivo de 5000 bytes pode precisar de duas unidades. O espaço reservado pode ser maior que o tamanho lógico.

## 4. Mapa de espaço livre

Um bitmap pode usar 0 para livre e 1 para ocupado. No mapa 1, 0, 1, 0, as unidades 1 e 3 estão livres. O sistema atualiza o mapa quando aloca ou libera unidades.

## 5. Estratégias e fragmentação

Contígua: unidades consecutivas; simples, mas pode sofrer com fragmentação externa.
Encadeada: unidades ligadas; permite dispersão, mas dificulta certos acessos.
Indexada ou por extensões: uma estrutura registra as regiões usadas.

Fragmentação interna desperdiça espaço dentro de unidades reservadas. Fragmentação externa divide o espaço livre em regiões separadas.

## 6. Exclusão

Remover um arquivo pode apenas marcar suas unidades como livres e remover suas referências. Os dados antigos podem continuar presentes até serem sobrescritos ou tratados por mecanismos específicos.

## 7. Perguntas de fixação

1. O que o sistema de arquivos acrescenta a uma partição?
2. Por que o caminho de um arquivo não é um LBA?
3. Quantas unidades de 4096 bytes são necessárias para 5000 bytes?
4. O que significa 0 em um bitmap?
5. Qual fragmentação deixa espaço dentro de uma unidade reservada?
6. Por que exclusão lógica não garante apagamento físico imediato?
