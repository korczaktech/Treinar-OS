# Reforço da Aula 22 — Particionamento e tabelas de partição

## 1. O que uma partição representa?
Uma partição é uma faixa de LBAs dentro de um dispositivo. A tabela descreve início, tamanho, tipo e atributos. Ela não armazena a árvore de arquivos e não transforma a região em um disco físico separado.

## 2. Exemplo passo a passo
Dispositivo com 1.000 blocos. Partição começa em 100 e possui 300 blocos:
- início incluído: 100;
- limite final exclusivo: 400;
- últimos blocos acessados: 398 e 399;
- LBA 400 já pertence ao espaço posterior.

Outra partição [400, 700) é adjacente, não sobreposta. A faixa [399, 600) se sobrepõe em um bloco.

## 3. Validações essenciais
Confirme início e quantidade, valide a capacidade, rejeite overflow, detecte sobreposição e não presuma que o tipo seja conhecido. Uma região só deve ser publicada depois de todas as verificações.

## 4. Ligação com o ZenithOS
O gerenciador de partições interpreta o mapa. O sistema de arquivos só entra depois, quando o conteúdo da região for identificado e validado.

## 5. Perguntas de revisão
1. Calcule o limite exclusivo de [100, 400) descrito por início 100 e quantidade 300.
2. [100, 400) e [400, 500) se sobrepõem?
3. Por que uma partição não é sinônimo de sistema de arquivos?
4. Cite três campos que uma entrada de partição pode conter.
5. O que fazer com uma entrada que ultrapassa o dispositivo?
