# Montagem e desmontagem de volumes

## Objetivo

Nesta aula, você estudará montagem e desmontagem de volumes e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Montagem associa um sistema de arquivos de um volume a um ponto da árvore de diretórios. Exige identificar o formato, validar metadados essenciais, preparar estruturas em memória e publicar o ponto somente quando estiver consistente.

## 2. Exemplo de funcionamento

Durante o uso, arquivos abertos, diretórios, operações pendentes e dados sujos mantêm referências ao volume. Desmontar exige impedir novas operações, concluir ou cancelar operações conforme contrato, sincronizar dados quando possível e liberar estruturas.

## 3. Validação e segurança

Desmontagem pode falhar por referências ativas, erros de I/O ou falha de sincronização. Forçar remoção não torna dados pendentes persistentes. Remoção física inesperada exige marcar o volume como indisponível.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve manter estados explícitos de montagem, referências ativas e políticas distintas para desmontagem normal e forçada. Um ponto de montagem nunca deve ficar visível parcialmente.

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
