# Particionamento e Mapa do Disco

## Objetivo

Um dispositivo pode disponibilizar milhões de blocos lógicos. Em vez de tratar todo o espaço como uma região sem organização, podemos dividi-lo em regiões chamadas partições. Nesta aula estudaremos como descrever essas regiões e validar seus limites.

## 1. O que é uma partição?

Partição é uma região delimitada dentro do espaço lógico de um dispositivo. Um disco pode ter uma região reservada à inicialização, outra ao sistema e outra aos dados. Essas regiões não precisam ser dispositivos físicos separados.

## 2. Início e quantidade

Uma partição é descrita por LBA inicial e quantidade de blocos. Se começa em 100 e possui 500 blocos, sua faixa é [100, 600). Ela inclui 100 até 599; 600 é o limite exclusivo.

O dispositivo com 10.000 blocos é representado por [0, 10000). Uma partição que começa em 9500 e possui 500 blocos cabe exatamente. Com 501, ultrapassa o limite.

A validação deve confirmar início não negativo, quantidade positiva, início dentro do dispositivo e quantidade menor ou igual ao espaço restante. Use a regra segura da Aula 4 antes de calcular o limite final.

## 3. Partições não podem se sobrepor

Considere [100, 500) e [500, 900). São adjacentes: a primeira termina onde a segunda começa. Não compartilham blocos.

Agora considere [100, 500) e [450, 900). Os blocos 450 a 499 aparecem nas duas regiões. Há sobreposição.

Para intervalos semiabertos A e B, existe sobreposição quando o início de cada faixa é menor que o fim da outra. Valide os limites antes de calcular os finais.

## 4. Tabela de partições

A tabela registra como o espaço foi dividido. Pode conter início, tamanho, tipo, identificador e atributos. Ela descreve as regiões, não o conteúdo completo delas.

O firmware, bootloader ou sistema operacional pode consultar essa estrutura para descobrir as partições.

## 5. MBR e GPT

MBR (Master Boot Record) é um esquema antigo de particionamento, com limitações históricas de quantidade de partições e endereçamento. Também ocupa uma posição especial no início do disco.

GPT (GUID Partition Table) é um esquema mais moderno, usa identificadores únicos e mantém estruturas redundantes e verificações para aumentar a robustez. Também possui uma área protetora para compatibilidade com ferramentas antigas.

Não precisamos implementar os formatos nesta aula. O essencial é compreender que eles definem como as partições são descritas.

## 6. Partição não é sistema de arquivos

Uma partição delimita espaço. Um sistema de arquivos organiza diretórios, arquivos e metadados dentro desse espaço.

Uma partição pode conter um sistema de arquivos, estar vazia ou ser reservada para outra finalidade. Encontrar uma partição não significa que o ZenithOS já possa abrir arquivos nela.

## 7. Alinhamento de partições

O início pode ser escolhido para respeitar fronteiras recomendadas pelo dispositivo. Isso não é o mesmo que alinhar variáveis na memória. A política de 8 bytes do ZenithOS não deve ser usada automaticamente para particionar discos.

## 8. Responsabilidades no ZenithOS

Uma arquitetura clara separa:
1. descoberta do dispositivo;
2. leitura da tabela;
3. validação de partições;
4. detecção de sobreposição;
5. identificação do conteúdo;
6. montagem do sistema de arquivos compatível.

O gerenciador de partições interpreta o mapa. O sistema de arquivos interpreta o conteúdo de uma região.

## 9. Perguntas de compreensão

1. Uma partição é um dispositivo físico separado?
2. Qual é o limite exclusivo de uma partição iniciada em 100 com 500 blocos?
3. Qual a diferença entre regiões adjacentes e sobrepostas?
4. Para que serve a tabela de partições?
5. GPT é um sistema de arquivos?
6. Por que alinhamento de partição não é alinhamento de memória?

## 10. Exercícios de código

- EXN1A8.nbx — validar se uma partição cabe no dispositivo.
- EXN2A8.nbx — detectar sobreposição entre duas partições válidas.

## Critério de conclusão

Você deve descrever uma partição por início e quantidade, validar seus limites e explicar a diferença entre tabela de partições e sistema de arquivos.
