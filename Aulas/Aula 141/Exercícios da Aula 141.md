# Exercícios da Aula 141 — Heap, pilha e mapeamentos de memória

**Objetivo:** demonstrar que você compreendeu diferenciar áreas de alocação dinâmica, pilhas de execução e mapeamentos explícitos, controlando limites e ciclo de vida e consegue aplicar o raciocínio ao ZenithOS.

## Parte A — Exercícios de compreensão

### 1. Explicação com suas palavras

Explique qual problema heap, pilha e mapeamentos de memória resolve no sistema operacional. Diferencie sua responsabilidade das responsabilidades dos componentes vizinhos.

### 2. Conceitos e limites

Defina os seguintes conceitos relacionados à aula: heap; stack; crescimento; ponteiro de pilha; frames de chamada; guard pages; mmap conceitual; regiões anônimas e apoiadas em arquivo; desalocação. Escolha pelo menos cinco termos e explique também uma situação em que cada um pode ser usado incorretamente.

### 3. Representação

Desenhe ou descreva a estrutura principal do componente. Inclua campos, unidades, estados possíveis, proprietário dos dados e pelo menos três invariantes que precisam ser preservados.

### 4. Análise de cenário

Considere o seguinte caso: Um processo pode reservar 64 MiB de espaço virtual para heap e ter apenas algumas páginas físicas comprometidas inicialmente. Reserva virtual não equivale a consumo imediato de RAM.

Descreva as etapas necessárias para processar esse cenário. Mostre quais validações precisam ocorrer antes da alteração do estado e qual resultado deve ser produzido.

### 5. Diagnóstico de falhas

Analise os riscos abaixo: stack overflow; heap overlap; liberar região errada; crescimento sem limite; confundir memória virtual reservada com memória física comprometida. Para cada um, explique:
- como a falha pode acontecer;
- qual parte do sistema pode ser afetada;
- como detectá-la;
- como impedir que ela corrompa o estado do kernel.

### 6. Decisão técnica

Considere a proposta: “Para simplificar, o componente pode confiar que os outros módulos sempre enviarão dados corretos”.

Você concorda? Justifique com pelo menos três argumentos técnicos e proponha uma fronteira de validação adequada.

### 7. Aplicação no ZenithOS

Descreva como esse componente deve se integrar ao ZenithOS. Identifique quais módulos solicitam seus serviços, quais dados atravessam a interface e quem mantém a propriedade dos recursos.

### 8. Verificação de aprendizagem

Crie três casos de teste: um normal, um limite extremo e um inválido. Para cada um, escreva a entrada, o resultado esperado e o invariante que deve continuar verdadeiro.

## Parte B — Exercício de código (.nbx)

<text></text>
**Desafio:** simule heap e pilha em intervalos virtuais, detectando colisão, estouro de limite e liberação inválida; mantenha o exercício independente de APIs de sistema não implementadas.

### Requisitos

1. Escreva o programa em Nebula (.nbx), usando apenas construções cuja sintaxe você já estudou.
2. Separe entrada, validação, processamento e resultado.
3. Não use APIs fictícias do ZenithOS nem tente acessar hardware real.
4. Trate pelo menos um caso inválido.
5. Inclua comentários explicando as decisões importantes.
6. Teste manualmente com um caso válido, um limite e um caso inválido.
7. Não copie o enunciado como se fosse a implementação: o objetivo é construir a lógica.

### Registro dos testes

Anote:
- entrada utilizada;
- resultado que você esperava;
- resultado obtido;
- diferença encontrada;
- correção realizada.

## Critério de conclusão

A parte de compreensão está concluída quando você justificar as decisões sem depender de frases decoradas. A parte de código está concluída quando o programa implementar a lógica pedida, tratar entradas inválidas e apresentar resultados coerentes nos testes registrados.

**Importante:** o desafio é de aprendizagem. Ele não representa uma implementação real do subsistema no ZenithOS e não deve ser tratado como código de kernel pronto.
