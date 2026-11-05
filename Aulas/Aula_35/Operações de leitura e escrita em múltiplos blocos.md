# Operações de leitura e escrita em múltiplos blocos

## Objetivo

Nesta aula, você estudará operações de leitura e escrita em múltiplos blocos e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Uma requisição de múltiplos blocos transfere LBAs consecutivos em um comando. Agrupar operações reduz overhead, mas o protocolo, o controlador, o buffer e o driver podem impor limites máximos.

## 2. Exemplo de funcionamento

Valide início, quantidade, capacidade restante, multiplicação por tamanho do bloco e capacidade do buffer. Se o limite por comando for menor que a operação, divida em segmentos contíguos sem lacunas nem sobreposição.

## 3. Validação e segurança

Uma transferência pode terminar parcialmente. O contrato deve informar quantos blocos foram concluídos e qual erro ocorreu. Não presuma que uma requisição grande seja atomicamente concluída.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS pode oferecer operação lógica grande e deixar o driver dividir conforme seus limites. O resultado preserva quantidade concluída e erro.

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
