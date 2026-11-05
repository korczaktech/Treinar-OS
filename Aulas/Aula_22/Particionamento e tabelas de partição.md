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

1. Qual problema esta aula procura resolver?
2. Quais informações precisam ser conhecidas antes de executar a operação estudada?
3. Que dado inválido poderia causar acesso fora dos limites ou perda de consistência?
4. Qual responsabilidade pertence ao ZenithOS e qual pertence ao driver?
5. Que teste automatizado ajudaria a detectar uma implementação incorreta?

## 6. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
