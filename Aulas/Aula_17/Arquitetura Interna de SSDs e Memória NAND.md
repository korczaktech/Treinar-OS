# Arquitetura Interna de SSDs e Memória NAND

## Objetivo

Até aqui tratamos o dispositivo como uma unidade de blocos lógicos. Agora vamos olhar por trás dessa interface e entender por que um SSD não funciona como uma simples coleção de setores regraváveis. O foco é NAND, páginas, blocos de apagamento, FTL, garbage collection e desgaste.

## 1. A interface lógica esconde a mídia

O sistema operacional envia leituras e gravações por endereços lógicos. O controlador do SSD decide onde os dados serão colocados fisicamente. Essa tradução permite que o dispositivo apresente uma sequência lógica estável mesmo quando a localização física muda.

## 2. Páginas e blocos NAND

A memória NAND é organizada em páginas e blocos de apagamento. Em termos gerais, a leitura e a programação ocorrem em unidades de página, enquanto o apagamento ocorre em unidades maiores chamadas blocos.

Os tamanhos e regras exatos dependem da geração e do tipo de NAND. Não assuma valores universais.

## 3. Por que não sobrescrever diretamente?

Em muitas tecnologias NAND, uma página programada não pode simplesmente ser sobrescrita como um byte em RAM. Para reutilizar espaço, pode ser necessário apagar um bloco inteiro.

Assim, uma atualização lógica pode ser implementada gravando uma nova versão em outra página e marcando a antiga como inválida. Mais tarde, o controlador reorganiza os dados e apaga blocos que possam ser reutilizados.

## 4. FTL

FTL (Flash Translation Layer) é a camada do controlador que mapeia endereços lógicos apresentados ao host para localizações físicas na NAND.

Ela também participa de gerenciamento de blocos defeituosos, coleta de lixo, distribuição de desgaste e outras tarefas. O sistema operacional normalmente não escolhe a página NAND física de cada LBA.

## 5. Garbage collection

A coleta de lixo identifica blocos que contêm páginas válidas e inválidas. O controlador pode copiar páginas ainda válidas para outro local, apagar o bloco e disponibilizá-lo novamente.

Essa movimentação gera trabalho interno e pode afetar latência e desempenho, principalmente quando há pouco espaço livre.

## 6. Wear leveling

Células NAND suportam uma quantidade finita de ciclos de programação e apagamento. Wear leveling distribui o desgaste para evitar que poucas regiões sejam usadas muito mais que outras.

Não significa que todas as células terão exatamente a mesma quantidade de ciclos, mas busca evitar concentração excessiva do desgaste.

## 7. TRIM e descarte de blocos lógicos

Quando o sistema de arquivos libera uma região, pode informar ao SSD que determinados LBAs não contêm mais dados necessários. Esse aviso é conhecido como TRIM em algumas interfaces, ou discard/deallocate em termos mais gerais.

O aviso permite ao controlador tratar essas páginas como não necessárias em futuras operações internas. Não significa necessariamente apagamento físico imediato, nem deve ser tratado como mecanismo de apagamento seguro.

## 8. Amplificação de escrita

Uma pequena gravação lógica pode provocar movimentação e gravação de mais dados internamente. A razão entre escrita interna e escrita solicitada pelo host é chamada amplificação de escrita.

Coleta de lixo, padrão de uso, espaço livre e organização dos dados influenciam esse fenômeno.

## 9. Aplicação no ZenithOS

O ZenithOS deve trabalhar com a interface lógica do dispositivo e usar comandos padronizados de descarte quando suportados. Não deve presumir que conhece a localização física das páginas NAND. Políticas de sistema de arquivos podem reduzir gravações desnecessárias, mas o gerenciamento físico permanece responsabilidade do controlador.

## 10. Perguntas de compreensão

1. Por que o LBA não revela a página NAND física?
2. Qual é a diferença entre página e bloco de apagamento?
3. O que o FTL faz?
4. Por que o SSD pode gravar uma nova página em vez de sobrescrever a antiga?
5. O que é garbage collection?
6. Qual é o objetivo do wear leveling?
7. TRIM apaga fisicamente os dados imediatamente?
8. O que significa amplificação de escrita?

## 11. Exercícios de código

- EXN1A17.nbx — simular um mapa lógico para páginas físicas, permitindo remapeamento.
- EXN2A17.nbx — simular coleta de lixo com páginas válidas e inválidas, preservando o conteúdo válido.


## Método de estudo e exemplo guiado
Acompanhe um LBA que aponta para uma página NAND. Quando o host atualiza o conteúdo, o controlador pode gravar uma nova página e alterar o mapeamento do FTL, deixando a página antiga inválida. Depois, a coleta de lixo precisa preservar páginas válidas antes de apagar o bloco. Marque quais decisões pertencem ao controlador e quais informações o host realmente conhece.