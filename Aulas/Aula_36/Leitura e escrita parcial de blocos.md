# Leitura e escrita parcial de blocos

## Objetivo

Nesta aula, você estudará leitura e escrita parcial de blocos e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

A interface de blocos normalmente transfere setores completos, mas arquivos e aplicações podem alterar poucos bytes. A camada superior localiza o setor, lê, modifica a região e grava o setor completo quando não há escrita parcial nativa.

## 2. Exemplo de funcionamento

Para offset em bytes, a divisão pelo tamanho do setor fornece LBA relativo e resto interno. Uma operação pode atravessar vários setores e exige tratar o primeiro, os intermediários e o último.

## 3. Validação e segurança

Leitura-modificação-escrita pode perder atualizações concorrentes se duas operações alterarem regiões diferentes do mesmo setor. Falhas entre leitura e gravação também precisam de política explícita.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

No ZenithOS, operações parciais ficam acima da interface de blocos. Locks ou serialização protegem setores compartilhados quando a camada promete consistência.

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
