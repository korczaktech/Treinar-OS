# Particionamento e tabelas de partição

## Objetivo

Nesta aula, você estudará particionamento e tabelas de partição e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Uma partição é uma faixa contínua de LBAs delimitada por início e quantidade. A tabela descreve as regiões, seus tipos e atributos; não cria outro dispositivo físico. Uma partição pode conter um sistema de arquivos, dados brutos ou estruturas de boot.

## 2. Exemplo de funcionamento

Em um disco de 100.000 blocos, uma partição iniciada em 2.048 e com 20.000 blocos ocupa [2.048, 22.048). O limite final exclusivo pode ser igual à capacidade total, mas nenhum LBA acessado pode ser igual a esse limite.

## 3. Validação e segurança

Validar capacidade, início, quantidade, soma sem overflow e sobreposição entre regiões. Não presumir que toda partição contém um sistema de arquivos nem que todo disco possui tabela de partições.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O gerenciador de volumes do ZenithOS deve interpretar o esquema suportado e publicar somente regiões validadas. A camada de blocos continua validando cada requisição dentro dos limites da partição.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Em um disco com 100.000 blocos, uma partição começa em 2.048 e tem 20.000 blocos. Qual é seu limite final exclusivo?
2. As faixas [2.048, 22.048) e [22.048, 30.000) se sobrepõem? Justifique.
3. Por que uma partição pode existir sem conter um sistema de arquivos?
4. Quais verificações devem acontecer antes de publicar uma partição para as camadas superiores?
5. O que o ZenithOS deve fazer ao encontrar um tipo de partição desconhecido?
6. Por que a tabela de partições não deve ser tratada como entrada confiável?

## 6. Exemplo guiado: validar duas partições
Considere um dispositivo com 100.000 LBAs. A partição A começa em 2.048 e possui 20.000 blocos: seu intervalo é [2.048, 22.048). A partição B começa em 22.048 e possui 10.000 blocos: seu intervalo é [22.048, 32.048). Elas são adjacentes, não sobrepostas. Se B começasse em 22.047, compartilharia um bloco com A e deveria ser rejeitada quando o formato não permite sobreposição.

Antes de publicar qualquer região, o parser precisa validar os campos, confirmar que cada intervalo cabe no dispositivo e comparar as regiões entre si. Uma tabela sintaticamente legível ainda pode conter uma partição fora dos limites.

## 7. Tipos e atributos
O tipo de partição é um identificador que comunica a finalidade ou o formato esperado da região. Atributos podem indicar características adicionais. O ZenithOS não deve interpretar um tipo desconhecido como se fosse automaticamente um sistema de arquivos conhecido. Deve preservar ou ignorar de forma controlada, conforme a política de compatibilidade.

## 8. Método de aprendizagem
Desenhe o disco como uma linha de LBAs. Para cada entrada da tabela, marque início e limite exclusivo. Em seguida, verifique capacidade, sobreposição e tipo. Por último, explique por que localizar uma partição não equivale a montá-la.

## 9. Erros comuns
Confundir quantidade com LBA final; aceitar sobreposição; presumir que todas as regiões contêm arquivos; tratar a tabela como confiável só porque o dispositivo a forneceu.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
