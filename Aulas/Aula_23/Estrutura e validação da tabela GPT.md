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

1. Qual problema esta aula procura resolver?
2. Quais informações precisam ser conhecidas antes de executar a operação estudada?
3. Que dado inválido poderia causar acesso fora dos limites ou perda de consistência?
4. Qual responsabilidade pertence ao ZenithOS e qual pertence ao driver?
5. Que teste automatizado ajudaria a detectar uma implementação incorreta?

## 6. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
