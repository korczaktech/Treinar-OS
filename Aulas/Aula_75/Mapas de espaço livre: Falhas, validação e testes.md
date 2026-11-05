# Aula 75 — Mapas de espaço livre: falhas, validação e testes

## Objetivo

Preservar invariantes diante de entradas inválidas, corrupção e interrupções. No contexto de mapas de espaço livre, você deverá explicar o conceito, reconhecer seus limites e relacioná-lo às decisões do ZenithOS.

## Pré-requisitos

Aula 74 — Mapas de espaço livre: Implementação prática no ZenithOS. Revise os conceitos e invariantes definidos nela.

## 1. Conceito central

O mapa de espaço livre responde quais unidades podem ser alocadas. Bitmap usa um bit por unidade; listas encadeiam unidades; árvores ou grupos aceleram buscas por intervalos. A escolha depende do tamanho e do padrão de uso.

O foco desta aula é **bitmap, listas livres, busca e atualização**. Não confunda a representação lógica com a disposição física no dispositivo, nem estado transitório com estado persistente.

## 2. Modelo e responsabilidades

Para bitmap, documente correspondência índice→bloco, ordem dos bits e significado de cada estado. Contadores derivados precisam ser reconciliáveis. Lista livre exige proteção contra ciclos e referências repetidas.

Para cada campo ou referência, registre significado, unidade, faixa válida, origem e responsável pela alteração. Dados vindos do disco são entrada externa: decodifique e valide antes de usar.

## 3. Exemplo trabalhado

Considere um volume com 1.000 blocos. Uma operação precisa usar uma região iniciada no bloco lógico 120. Antes de executá-la, identifique a unidade, valide a faixa completa contra o limite exclusivo, confirme o estado do objeto e determine quem persiste a alteração. Se a segunda etapa falhar, não deixe a primeira alteração parcialmente publicada.

## 4. Falhas e validação

Riscos principais: Bit invertido, bloco fora do volume, contagem incorreta, liberação dupla, atualização concorrente e bitmap parcialmente persistido. Valide tamanho antes de decodificar; índice antes de acessar; overflow antes de calcular intervalos; referências antes de dereferenciar; e estado antes de executar transições.

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

> **Dificuldade:** Muito difícil  
> **Duração estimada:** 55 minutos
