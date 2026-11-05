# TRIM, discard e liberação de blocos

## Objetivo

Nesta aula, você estudará trim, discard e liberação de blocos e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Quando o sistema de arquivos libera blocos, TRIM/discard informa ao dispositivo que certas faixas não precisam mais preservar dados. Isso pode ajudar coleta de lixo e gerenciamento interno de SSDs.

## 2. Exemplo de funcionamento

A operação informa intervalos não utilizados; não ordena necessariamente apagamento físico imediato. O dispositivo pode processar descarte de modo assíncrono e impor granularidade e limites.

## 3. Validação e segurança

TRIM não é apagamento seguro nem garantia de destruição forense. Ler depois de descartar pode ter comportamento variável. Descartar faixa ainda referenciada pode destruir dados válidos.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS encaminha discard apenas após confirmação de que a faixa está livre. O recurso é opcional e anunciado pelo driver.

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
> - **Duração:** 60 minutos
