# Alinhamento de partições e limites físicos

## Objetivo

Nesta aula, você estudará alinhamento de partições e limites físicos e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Alinhamento posiciona o início ou o tamanho de uma região em múltiplos de uma unidade exigida ou recomendada. Setores lógicos, setores físicos, páginas NAND e blocos de apagamento pertencem a camadas diferentes.

## 2. Exemplo de funcionamento

Se o setor lógico possui 512 bytes e o alinhamento desejado é 4.096 bytes, oito setores lógicos formam essa unidade. Inícios múltiplos de oito setores respeitam esse alinhamento específico.

## 3. Validação e segurança

Alinhamento inadequado pode causar operações extras ou perda de desempenho, mas não significa automaticamente corrupção. Não confundir alinhamento de partição com alinhamento de buffer DMA ou alinhamento de estruturas na memória.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve consultar requisitos reportados pelo dispositivo e separar alinhamento de hardware de convenções internas. O padrão de 8 bytes adotado para estruturas não é uma regra universal de disco.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Qual problema esta aula procura resolver?
2. Quais informações precisam ser conhecidas antes de executar a operação estudada?
3. Que dado inválido poderia causar acesso fora dos limites ou perda de consistência?
4. Qual responsabilidade pertence ao ZenithOS e qual pertence ao driver?
5. Que teste automatizado ajudaria a detectar uma implementação incorreta?

## 6. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Difícil
> - **Duração:** 55 minutos
