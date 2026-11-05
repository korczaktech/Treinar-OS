# Atomicidade e limites de operações

## Objetivo

Nesta aula, você estudará atomicidade e limites de operações e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Atomicidade significa que uma atualização é observada como unidade indivisível segundo um contrato. Não é sinônimo de durabilidade: uma operação pode ser atômica durante execução e ainda não estar persistida após falta de energia.

## 2. Exemplo de funcionamento

Dispositivos podem anunciar limites de escrita atômica, com tamanho, alinhamento e condições específicas. Sem garantia explícita, uma gravação que cruza setores pode ser parcialmente aplicada.

## 3. Validação e segurança

Journal, copy-on-write e ordenação são mecanismos usados por sistemas de arquivos para consistência. Flush ordena persistência conforme contrato, mas não transforma várias gravações em uma transação indivisível.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve separar conclusão, atomicidade e durabilidade nas interfaces. Quando o hardware não garante atomicidade suficiente, a camada superior usa mecanismo próprio.

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
