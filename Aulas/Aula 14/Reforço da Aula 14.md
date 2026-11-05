# Reforço da Aula 14 — Interrupções e Polling

## 1. Polling consulta

O driver consulta o estado repetidamente. É simples, mas pode gastar CPU. Deve possuir limite e condição de saída.

## 2. Interrupção notifica

O hardware sinaliza um evento. O processador executa uma rotina de tratamento. Essa rotina deve fazer o mínimo necessário e deixar trabalho pesado para depois.

## 3. Contexto restrito

Uma rotina de interrupção não deve esperar indefinidamente, bloquear ou executar operações que dependam de um contexto que pode estar interrompido.

## 4. Timeout

Timeout significa que o resultado não chegou no prazo definido. É necessário investigar e aplicar uma política, não presumir imediatamente que o dispositivo morreu.

## 5. Fixação

1. Qual a diferença entre polling e interrupção?
2. Por que polling infinito é perigoso?
3. O que deve ser adiado para fora da rotina de interrupção?
4. Por que uma interrupção pode não pertencer ao seu dispositivo?
5. O que timeout realmente informa?


## Exemplo guiado: polling e interrupção
Uma operação de inicialização curta pode usar polling limitado. Uma leitura longa pode aguardar uma interrupção para evitar consultar continuamente o estado. A rotina de interrupção registra o evento e agenda o processamento completo fora do contexto restrito.

## Como revisar
Compare custo de CPU, latência e complexidade. Simule um timeout e explique por que ele informa ausência de conclusão no prazo, não a causa física da falha.