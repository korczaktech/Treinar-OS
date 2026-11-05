# Reforço da Aula 29 — Metadados e estruturas de armazenamento

## Persistente versus temporário
Estruturas em memória podem conter ponteiros, locks e referências que só fazem sentido durante aquela execução. Formatos persistentes devem usar campos definidos e referências relativas.

## Exemplo de formato
Um cabeçalho pode definir assinatura, versão, tamanho e offset. O parser lê cada campo conforme o tamanho e endianness especificados. O offset é validado contra o volume; não é convertido diretamente em ponteiro.

## Compatibilidade
Defina versão, tamanho mínimo, campos obrigatórios e política para campos desconhecidos. Não dependa do padding automático da linguagem.

## Perguntas
1. Por que ponteiros não devem ser gravados como metadados persistentes?
2. O que endianness define?
3. Qual a diferença entre offset e ponteiro?
4. Por que uma estrutura nativa pode mudar de layout?
5. Como lidar com uma versão de formato desconhecida?
