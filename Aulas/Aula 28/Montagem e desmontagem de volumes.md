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

1. O que significa montar um sistema de arquivos?
2. Por que o ponto de montagem só deve ser publicado depois da validação?
3. Por que um arquivo aberto pode impedir uma desmontagem normal?
4. Qual é a diferença entre desmontagem forçada e remoção inesperada do dispositivo?
5. O que deve acontecer com gravações pendentes antes de liberar as estruturas?
6. Por que uma falha de sincronização pode impedir uma desmontagem segura?

## 6. O que acontece durante a montagem?
Montar um volume é associar um sistema de arquivos a um ponto da árvore de diretórios. O processo pode incluir identificar o formato, ler o superbloco, validar versão e tamanhos, carregar estruturas essenciais, reconstruir índices em memória e só então publicar o ponto de montagem.

Se a validação falhar, o volume não deve aparecer como parcialmente montado. A montagem também precisa considerar opções como somente leitura quando o formato estiver danificado ou quando não houver suporte seguro para gravação.

## 7. O que precisa acontecer antes de desmontar?
A desmontagem normal impede novas referências, verifica arquivos e diretórios ainda em uso, finaliza ou aguarda operações pendentes, sincroniza dados e metadados quando possível e libera estruturas em memória. Se houver falha de I/O, a desmontagem pode não conseguir garantir persistência.

Desmontagem forçada e remoção física inesperada são situações diferentes. A remoção pode tornar impossível concluir gravações; o kernel deve marcar o volume como indisponível e propagar os erros.

## 8. Exemplo guiado
Um volume possui um arquivo aberto e uma gravação pendente. Uma solicitação de desmontagem chega. O sistema não deve simplesmente liberar a estrutura do volume: isso deixaria o arquivo ou a operação apontando para memória inválida. Primeiro precisa resolver as referências e o trabalho pendente segundo o contrato.

## 9. Método de aprendizagem
Desenhe os estados DESMONTADO, MONTANDO, MONTADO, DESMONTANDO e ERRO. Para cada transição, escreva qual condição permite avançar e quais recursos precisam permanecer válidos.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
