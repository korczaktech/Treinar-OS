# Intervalos e Validação de Operações de Armazenamento

## Objetivo

Na Aula 3, aprendemos que o LBA identifica um bloco lógico. Agora vamos estudar como representar uma operação que acessa vários blocos consecutivos e como impedir que ela ultrapasse a capacidade do dispositivo.

Ao final, você deverá conseguir:
- representar uma faixa por um endereço inicial e uma quantidade;
- calcular o deslocamento em bytes de um LBA;
- validar uma solicitação que envolve vários blocos;
- explicar por que validar apenas o primeiro endereço não é suficiente.

## 1. Uma operação pode acessar vários blocos

Imagine um dispositivo com 200 blocos lógicos. Como a numeração começa em zero, seus endereços vão de 0 até 199.

Uma operação pode solicitar apenas o bloco 25. Mas também pode solicitar quatro blocos consecutivos: 25, 26, 27 e 28.

Para representar essa operação, usamos dois valores:

- **Início:** primeiro LBA solicitado.
- **Quantidade:** número de blocos consecutivos.

Exemplo:
- Início: 25.
- Quantidade: 4.
- Blocos acessados: 25, 26, 27 e 28.

Não precisamos listar todos os endereços. O início e a quantidade descrevem a faixa.

## 2. Limite final exclusivo

Vamos representar uma faixa assim:

    [início, fim_exclusivo)

O início está incluído; o limite final não está incluído.

Se começamos no bloco 25 e solicitamos 4 blocos:

    fim_exclusivo = início + quantidade
    fim_exclusivo = 25 + 4
    fim_exclusivo = 29

A faixa é [25, 29). Ela contém 25, 26, 27 e 28. Não contém 29.

A quantidade pode ser calculada pela diferença:

    quantidade = fim_exclusivo - início

Um dispositivo com 200 blocos pode ser representado pelo intervalo completo [0, 200). O último LBA válido é 199, mas o limite final exclusivo é 200.

**Não confunda:** o limite final exclusivo não é o último bloco acessado. É a posição imediatamente posterior ao último bloco da faixa.

## 3. Como identificar uma faixa inválida?

Considere um dispositivo com 200 blocos, numerados de 0 a 199.

Uma solicitação começa no LBA 198 e pede 2 blocos:
- Início: 198.
- Quantidade: 2.
- Faixa: [198, 200).
- Blocos acessados: 198 e 199.

Ela é válida. O limite exclusivo 200 pode ser igual à quantidade total de blocos.

Se a solicitação pedir 3 blocos, tentará acessar 198, 199 e 200. O bloco 200 não existe nesse dispositivo. Portanto, a operação é inválida.

Para validar uma faixa, precisamos confirmar:
1. O total de blocos é positivo.
2. O endereço inicial não é negativo.
3. A quantidade solicitada é positiva.
4. O endereço inicial está dentro do dispositivo.
5. A quantidade cabe a partir do endereço inicial.

O fato de o primeiro endereço ser válido não garante que todos os endereços seguintes também sejam válidos.

## 4. Validar sem provocar estouro numérico

Uma ideia seria calcular primeiro:

    fim = início + quantidade

E depois verificar se fim é menor ou igual ao total.

Matematicamente, a ideia faz sentido. Porém, inteiros possuem limites. Se a soma ultrapassar o maior valor representável pelo tipo, pode ocorrer um **estouro numérico** (*integer overflow*).

Podemos validar a quantidade antes de somar:

    quantidade <= total - início

Essa comparação só deve acontecer depois de confirmar:
- total > 0;
- início >= 0;
- início < total;
- quantidade > 0.

Exemplo:
- Total: 200.
- Início: 198.
- Quantidade: 2.

Primeiro calculamos o espaço restante:

    200 - 198 = 2

Depois comparamos:

    2 <= 2

A faixa cabe.

Se a quantidade fosse 3:

    3 <= 2

A operação seria rejeitada.

A subtração só é feita depois de confirmar que o início está dentro do dispositivo. Isso evita usar um endereço inválido nessa conta.

## 5. Do LBA para bytes

Na Aula 3, aprendemos que o deslocamento inicial em bytes é calculado assim:

    deslocamento = LBA × tamanho_do_setor_lógico

Considere setores lógicos de 4096 bytes e uma solicitação que começa no LBA 5:

    5 × 4096 = 20480 bytes

O deslocamento inicial é 20.480 bytes.

Se a operação solicitar 3 blocos lógicos consecutivos, o tamanho total será:

    3 × 4096 = 12288 bytes

Nesse exemplo:
- deslocamento inicial: 20.480 bytes;
- quantidade: 3 blocos;
- tamanho total: 12.288 bytes;
- faixa de LBA: [5, 8).

O cálculo considera que cada LBA corresponde a uma unidade lógica de 4096 bytes. O tamanho precisa ser obtido das informações do dispositivo; não devemos presumir que todos usam o mesmo tamanho.

**Atenção à terminologia:** nesta aula, “bloco lógico” é a unidade identificada pelo LBA. Isso não significa que seja igual ao bloco de alocação de um sistema de arquivos ou ao bloco físico de apagamento da NAND.

## 6. Como isso será usado no ZenithOS?

Quando o ZenithOS precisar ler ou gravar uma faixa, a camada de armazenamento deverá receber informações que descrevam a operação, por exemplo:
- dispositivo selecionado;
- LBA inicial;
- quantidade de blocos;
- direção da operação (leitura ou gravação);
- região de memória usada como origem ou destino dos dados.

Antes de encaminhar a solicitação ao driver, a camada deverá validar os limites e os parâmetros.

Nesta aula, ainda não vamos acessar hardware. Vamos implementar os cálculos e as validações que precisam estar corretos antes de qualquer comunicação com um dispositivo real.

## 7. Sintaxe Nebula necessária

Os exercícios usam construções básicas da Nebula:

    funcao calcular(inicio: inteiro, quantidade: inteiro): inteiro {
        devolver inicio + quantidade
    }

    funcao quantidade_positiva(quantidade: inteiro): logico {
        devolver quantidade > 0
    }

Observe:
- **funcao** declara uma função;
- os parâmetros recebem tipos;
- **inteiro** representa um valor inteiro;
- **logico** representa verdadeiro ou falso;
- **quando** inicia uma condição;
- **devolver** retorna o resultado;
- **falso** e **verdadeiro** são valores lógicos.

Os exemplos mostram sintaxe válida, mas não implementam todas as verificações exigidas nos exercícios.

## 8. Exercícios de código

Os exercícios de programação estão nos arquivos NBX desta pasta. Faça-os na ordem proposta:

1. **EXN1A4.nbx — Conversão de LBA para deslocamento:** implementar o cálculo do deslocamento inicial em bytes.
2. **EXN2A4.nbx — Validação de intervalo:** verificar se uma solicitação de vários blocos cabe no dispositivo, usando a comparação segura apresentada na aula.
3. **EXN3A4.nbx — Limite final exclusivo:** validar uma solicitação e calcular seu limite final exclusivo sem realizar a soma antes da validação.

Não é necessário acessar um SSD real. O objetivo é implementar corretamente as regras matemáticas e os limites.

## 9. Perguntas de compreensão

Estas perguntas são diferentes dos exercícios NBX:

1. Por que um dispositivo com 200 blocos tem endereços de 0 até 199, mas seu intervalo completo é escrito como [0, 200)?
> R| Porque o computador vê o ultimo numero como a barreira, como um numero que nao deveria contar.
2. Qual é a diferença entre o último bloco acessado e o limite final exclusivo?
> R| O ultimo bloco acessado, é o ultimo que `Quantidade` pede, e limite final exclusivo é o numero logo após o ultimo bloco acessado
3. Por que verificar somente se o LBA inicial é válido não garante que uma operação com vários blocos seja válida?
> R | traria estouro numerico
4. Por que a comparação quantidade <= total - início pode ser mais segura do que somar início e quantidade antes de validar?
> R | Porque ja quebra dois erros, o de total - inicio dar negativo, e quantidade ser maior que o numero possivel de blocos.
5. Se uma operação começa no LBA 40 e solicita 6 blocos, quais endereços serão acessados e qual será o limite final exclusivo?
> R | 40, 41, 42, 43, 44, 45, 46. E o final Exclusivo é 47.
## 10. Critério de conclusão

A aula estará compreendida quando você conseguir:
- calcular o deslocamento de um LBA;
- representar uma faixa com início e limite final exclusivo;
- validar uma solicitação que envolve vários blocos;
- explicar como a validação impede acessos além da capacidade do dispositivo.

Não avance apenas por conseguir repetir uma fórmula. Tente explicar por que ela funciona.


## Método de estudo
Desenhe a faixa com início incluído e fim exclusivo. Marque cada bloco acessado, compare a quantidade com o espaço restante e só depois calcule o limite final. Repita com uma faixa válida no limite exato e outra que ultrapassa um bloco.


## Metadados da aula
- Dificuldade: Média
- Duração: 35 minutos
