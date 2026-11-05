# Estrutura e validação da tabela GPT

## Objetivo

Nesta aula, você estudará estrutura e validação da tabela gpt e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

GPT descreve partições por meio de cabeçalhos e uma matriz de entradas. Em um disco GPT típico existem cabeçalho principal e cópia de backup, matriz de entradas e MBR protetor. Cabeçalhos informam posições, dimensões e CRC32 para detectar corrupção acidental.

## 2. Exemplo de funcionamento

A validação verifica assinatura, tamanho do cabeçalho, posições dentro do dispositivo, quantidade e tamanho de entradas, CRC do cabeçalho e CRC da matriz. A cópia de backup fica próxima ao fim do disco e permite diagnóstico quando a estrutura principal está danificada.

## 3. Validação e segurança

Não confiar em contagens e tamanhos antes de impor limites e validar multiplicações e intervalos. CRC não autentica os dados; apenas detecta alterações em relação ao valor armazenado. Não interpretar estruturas desconhecidas parcialmente.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve ter parser GPT defensivo, limites de memória e regras explícitas para versões e atributos aceitos. Divergência entre cópias deve gerar diagnóstico, não reparo automático.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Qual é a função do cabeçalho principal e da cópia de backup da GPT?
2. Para que serve o MBR protetor e por que ele não é uma tabela MBR comum?
3. Se existem 4.000 entradas de 128 bytes, qual é o tamanho total da matriz?
4. Por que é perigoso confiar no tamanho declarado antes de validar a multiplicação e os limites?
5. O que um CRC válido demonstra e o que ele não demonstra?
6. Por que uma divergência entre GPT principal e backup exige diagnóstico cuidadoso?

## 6. Como a GPT é organizada
A GPT normalmente mantém um cabeçalho principal próximo ao início do disco, uma matriz de entradas de partição e uma cópia de backup próxima ao fim. O cabeçalho informa, entre outros campos, a posição da matriz, a quantidade de entradas e o tamanho de cada entrada. O GUID do disco identifica a estrutura; cada partição também pode possuir GUID próprio e um GUID de tipo.

A GPT inclui um MBR protetor no LBA 0 para reduzir o risco de ferramentas antigas interpretarem o disco como vazio e sobrescreverem sua estrutura. Esse MBR protetor não transforma a GPT em uma tabela MBR convencional.

## 7. Ordem segura de validação
1. Confirme que o dispositivo possui blocos suficientes para as estruturas.
2. Leia o cabeçalho dentro de um buffer limitado.
3. Verifique assinatura e tamanho declarado do cabeçalho.
4. Valide posições e dimensões antes de alocar ou ler a matriz.
5. Calcule e confira o CRC do cabeçalho conforme o campo de checksum definido.
6. Calcule e confira o CRC da matriz de entradas.
7. Valide cada partição e seus atributos.
8. Repita o diagnóstico para a cópia de backup.

CRC32 detecta alterações acidentais, mas não autentica o conteúdo contra um atacante que pode recalcular o CRC.

## 8. Exemplo guiado
Se o cabeçalho declarar 4.000 entradas de 128 bytes, a matriz terá 512.000 bytes. O parser não deve alocar esse tamanho cegamente. Primeiro deve impor limites definidos pelo sistema, verificar multiplicação sem overflow e confirmar que a região declarada cabe no dispositivo.

## 9. Método de aprendizagem
Estude a GPT como um parser de formato binário: primeiro assinatura e cabeçalho, depois matriz, depois entradas e por último as relações entre cópia principal e cópia de backup.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
