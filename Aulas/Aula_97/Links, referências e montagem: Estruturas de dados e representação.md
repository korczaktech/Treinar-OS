# Aula 97 — Links, referências e montagem: estruturas de dados e representação

## Objetivo

Representar o estado sem ambiguidades, com unidades e invariantes explícitos. No contexto de links, referências e montagem, você deverá explicar o conceito, reconhecer seus limites e relacioná-lo às decisões do ZenithOS.

## Pré-requisitos

Aula 96 — Links, referências e montagem: Fundamentos, finalidade e limites. Revise os conceitos e invariantes definidos nela.

## 1. Conceito central

Hard links criam mais de um nome para a mesma identidade; links simbólicos guardam caminho a resolver. Montagem conecta árvore de diretórios a outra instância. Essas relações afetam resolução, ciclo de vida e segurança.

O foco desta aula é **hard links, links simbólicos, pontos de montagem e desmontagem**. Não confunda a representação lógica com a disposição física no dispositivo, nem estado transitório com estado persistente.

## 2. Modelo e responsabilidades

Hard link aponta ao mesmo inode e altera contagem de links. Link simbólico é objeto cujo conteúdo representa destino. Ponto de montagem associa diretório de cobertura à raiz montada.

Para cada campo ou referência, registre significado, unidade, faixa válida, origem e responsável pela alteração. Dados vindos do disco são entrada externa: decodifique e valide antes de usar.

## 3. Exemplo trabalhado

Considere um volume com 1.000 blocos. Uma operação precisa usar uma região iniciada no bloco lógico 120. Antes de executá-la, identifique a unidade, valide a faixa completa contra o limite exclusivo, confirme o estado do objeto e determine quem persiste a alteração. Se a segunda etapa falhar, não deixe a primeira alteração parcialmente publicada.

## 4. Representação segura

Não copie diretamente estruturas persistidas para estruturas nativas. Defina serialização, tamanho, endianness, alinhamento e versão. Use tipos distintos para bytes, blocos, identificadores e índices. Estados devem ser enumerações validadas, não números mágicos.

## 5. Aplicação no ZenithOS

Mantenha as regras puras separadas de persistência e de acesso ao dispositivo. Comece com modelo em memória e testes determinísticos. Depois use dispositivo de armazenamento simulado, persistência e integração. Não comece pelo hardware real: isso mistura defeitos de protocolo, lógica e arquitetura.

## 6. Método de aprendizagem

1. Explique o conceito sem consultar o texto.
2. Desenhe as estruturas ou o fluxo envolvido.
3. Marque dados persistentes, transitórios e referências externas.
4. Simule um caso válido e pelo menos dois inválidos.
5. Explique em qual etapa cada validação acontece e qual estado permanece após uma falha.

## 7. Exercícios de compreensão

1. Qual problema esta camada resolve e qual problema não resolve?
2. Quais dados ou referências precisam ser validados antes da operação?
3. Qual invariante não pode ser violado?
4. Descreva um caso inválido e o resultado correto.
5. Como separar a regra de domínio da persistência e do controlador?
6. Que teste revelaria uma falha de fronteira ou de recuperação?

## 8. Exercício .nbx (opcional)

Crie um programa com valores fictícios para validar uma regra relacionada ao tema. Informe os casos aceitos e rejeitados. Não simule acesso real ao disco nem use recursos da Nebula que ainda não foram estudados.

## 9. Critério de conclusão

Você concluiu quando conseguir explicar o conceito com suas palavras, desenhar o modelo ou fluxo, justificar as validações e propor testes específicos para o ZenithOS.

> **Dificuldade:** Média  
> **Duração estimada:** 45 minutos
