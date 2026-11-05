# Reforço da Aula 4 — Intervalos e Validação de Operações de Armazenamento

Este reforço retoma os conceitos da aula com exemplos menores e passo a passo. Os exercícios de código devem ser feitos depois de entender como uma faixa de blocos é representada e validada.

## 1. Um bloco ou vários blocos?

Na aula anterior, aprendemos que o LBA identifica um bloco lógico.

Por exemplo:
- LBA 10 identifica um bloco;
- LBA 11 identifica o bloco seguinte;
- LBA 12 identifica o próximo.

Mas uma operação pode precisar acessar vários blocos seguidos. Em vez de enviar uma lista com todos os endereços, podemos informar o primeiro endereço e quantos blocos queremos acessar.

Exemplo:
- início: 10;
- quantidade: 3.

Os blocos acessados são 10, 11 e 12.

A quantidade não é o endereço final. Ela informa quantos blocos fazem parte da operação.

## 2. Entendendo o limite final exclusivo

Vamos representar a faixa assim:

    [início, fim_exclusivo)

O primeiro endereço está incluído. O limite final não está incluído.

Exemplo:

    [10, 13)

Quais números estão dentro dessa faixa?
- 10: sim;
- 11: sim;
- 12: sim;
- 13: não.

Portanto, são três blocos.

A fórmula é:

    fim_exclusivo = início + quantidade

No exemplo:

    10 + 3 = 13

O limite final é 13, mas o último bloco acessado é 12.

### Por que usar esse formato?

Porque a quantidade fica fácil de descobrir:

    quantidade = fim_exclusivo - início

E porque um dispositivo com 100 blocos pode ser descrito como [0, 100). O último endereço existente continua sendo 99.

## 3. Validando uma solicitação

Imagine um dispositivo com 100 blocos: de 0 até 99.

Uma solicitação pede:
- início: 97;
- quantidade: 3.

A faixa seria [97, 100). Ela acessa 97, 98 e 99. É válida.

Agora, se pedir 4 blocos, a faixa seria [97, 101). Ela tentaria acessar 97, 98, 99 e 100. O bloco 100 não existe. É inválida.

A regra não pode verificar apenas se o endereço inicial existe. O LBA 97 é válido, mas isso não significa que qualquer quantidade a partir dele também seja válida.

## 4. Validando sem somar antes

É tentador fazer:

    fim = início + quantidade

E depois comparar o resultado com o total.

Mas inteiros possuem limites. Se a soma ultrapassar o maior valor que o tipo consegue representar, ocorre um estouro numérico. O resultado deixa de ser confiável.

Uma alternativa é calcular quanto espaço ainda existe depois do início:

    espaço_restante = total - início

Depois verificar:

    quantidade <= espaço_restante

Exemplo:
- total: 100;
- início: 97;
- espaço restante: 100 - 97 = 3;
- quantidade solicitada: 3.

Como 3 é menor ou igual a 3, a faixa cabe.

Se a quantidade fosse 4, não caberia.

**Ordem importante:** antes de calcular total - início, confirme que o total é positivo e que o início está entre zero e total menos um. Antes da comparação, confirme também que a quantidade é positiva.

## 5. Calculando o deslocamento em bytes

O LBA identifica um bloco lógico. Para calcular o deslocamento em bytes, precisamos saber o tamanho da unidade lógica apresentada pelo dispositivo.

    deslocamento = LBA × tamanho_do_setor_lógico

Se cada setor lógico possui 4096 bytes e queremos o LBA 5:

    5 × 4096 = 20480 bytes

O começo do LBA 5 fica no deslocamento de 20.480 bytes.

Se quisermos três blocos, o tamanho total da operação será:

    3 × 4096 = 12288 bytes

Isso não muda o endereço inicial: o início continua sendo o LBA 5.

## 6. Não confunda as unidades

Nesta aula, quando falamos de LBA, estamos tratando de blocos lógicos endereçáveis pelo dispositivo.

Existem outras unidades chamadas de bloco em outras camadas:
- bloco lógico apresentado pelo dispositivo;
- bloco de alocação de um sistema de arquivos;
- bloco físico de apagamento da memória NAND.

Esses conceitos não são intercambiáveis. Os exercícios desta aula trabalham apenas com o espaço lógico endereçado por LBA.

## 7. Exemplo de raciocínio completo

Considere:
- total do dispositivo: 100 blocos;
- início solicitado: 96;
- quantidade: 4.

Primeiro, verificamos se o total é positivo: sim.

Depois, verificamos se o início é válido:
- 96 não é negativo;
- 96 é menor que 100.

Agora calculamos o espaço restante:

    100 - 96 = 4

Comparamos a quantidade:

    4 <= 4

A solicitação é válida. Ela acessa os blocos 96, 97, 98 e 99. Seu limite final exclusivo é 100.

Se a quantidade fosse 5, a solicitação seria inválida.

## 8. Pequeno exemplo em Nebula

A linguagem permite escrever uma função que devolve um valor lógico:

    funcao quantidade_positiva(quantidade: inteiro): logico {
        devolver quantidade > 0
    }

Essa função só verifica se a quantidade é positiva. Ela ainda não verifica se a faixa cabe no dispositivo. Essa validação exige também o total de blocos e o endereço inicial.

## 9. Perguntas de fixação

1. Em [20, 25), quais blocos estão incluídos?
> R | Inicio 20, Quantidade 4, Final exclusivo 25
2. Quantos blocos existem em [20, 25)?
> R | Existem 4
3. Um dispositivo possui 50 blocos. Uma solicitação começa no LBA 48 e pede 2 blocos. É válida? Por quê?
> R | Não é válida, por que começa no LBA 0, e termina no 49. 48 + 2 é 50, estouro numerico.
4. Por que uma solicitação que começa em um endereço válido ainda pode ultrapassar o dispositivo?
> R | Talvez a validação foi feita errada.
5. Qual é a vantagem de verificar a quantidade usando o espaço restante antes de calcular o limite final?
> R | Não sei responder essa.

## 10. Preparação para os exercícios

Faça os arquivos nesta ordem:
- **EXN1A4.nbx:** calcule o deslocamento de um LBA em bytes.
- **EXN2A4.nbx:** valide uma faixa de blocos.
- **EXN3A4.nbx:** valide a faixa e calcule o limite final exclusivo.

Se travar, volte à seção correspondente e tente explicar o exemplo com números diferentes. Não precisa memorizar as fórmulas sem entender o que cada valor representa.
