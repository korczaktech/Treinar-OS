# Aula 51 — Conceitos e responsabilidades de um sistema de arquivos: fundamentos, finalidade e limites

## Objetivo

Compreender o problema, o vocabulário e as fronteiras da responsabilidade. No contexto de conceitos e responsabilidades de um sistema de arquivos, você deverá explicar o conceito, reconhecer seus limites e relacioná-lo às decisões do ZenithOS.

## Pré-requisitos

Aulas 1 a 50 e noções de armazenamento em blocos, volumes e validação de intervalos.

## 1. Conceito central

O sistema de arquivos transforma blocos em objetos nomeados e organiza conteúdo, diretórios e metadados. O dispositivo fornece operações de bloco; o sistema de arquivos define como esses blocos representam objetos persistentes. A montagem conecta uma instância a uma árvore de diretórios, mas não altera por si só o conteúdo físico.

O foco desta aula é **abstração de arquivo, volume, persistência, interface e limites**. Não confunda a representação lógica com a disposição física no dispositivo, nem estado transitório com estado persistente.

## 2. Modelo e responsabilidades

Separe dispositivo, volume, instância montada, objeto persistente e descritor aberto. A interface deve definir operações, argumentos, resultados e erros. O estado em memória não deve ser confundido com o estado persistido.

Para cada campo ou referência, registre significado, unidade, faixa válida, origem e responsável pela alteração. Dados vindos do disco são entrada externa: decodifique e valide antes de usar.

## 3. Exemplo trabalhado

Considere um volume com 1.000 blocos. Uma operação precisa usar uma região iniciada no bloco lógico 120. Antes de executá-la, identifique a unidade, valide a faixa completa contra o limite exclusivo, confirme o estado do objeto e determine quem persiste a alteração. Se a segunda etapa falhar, não deixe a primeira alteração parcialmente publicada.

## 4. Limites e fronteiras

A camada deve cumprir sua responsabilidade sem assumir tarefas das camadas vizinhas. Ela recebe dados, valida o contrato, aplica sua política e devolve resultado ou erro. Não deve presumir que dados do disco sejam confiáveis.

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

## 8. Critério de conclusão

Você concluiu quando conseguir explicar o conceito com suas palavras, desenhar o modelo ou fluxo, justificar as validações e propor testes específicos para o ZenithOS.

> **Dificuldade:** Fácil  
> **Duração estimada:** 35 minutos
