# Validação defensiva de metadados

## Objetivo

Nesta aula, você estudará validação defensiva de metadados e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Metadados lidos do disco são entrada não confiável. Corrupção, falhas de energia, defeitos e adulteração podem produzir tamanhos, offsets, contagens e referências inconsistentes.

## 2. Exemplo de funcionamento

Um parser valida assinatura, versão, tamanho mínimo e máximo, intervalos, alinhamento, referências, ciclos e limites de profundidade. Um cabeçalho válido não torna automaticamente válidas as estruturas que ele aponta.

## 3. Validação e segurança

Limitar consumo de memória e CPU. Detectar somas com overflow, referências inexistentes, ciclos e estruturas profundamente aninhadas. Ao encontrar inconsistência, interromper com erro claro em vez de adivinhar uma interpretação.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

No ZenithOS, parsers devem ser funções testáveis e não devem corrigir o disco automaticamente. Diagnóstico e recuperação são operações separadas.

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
