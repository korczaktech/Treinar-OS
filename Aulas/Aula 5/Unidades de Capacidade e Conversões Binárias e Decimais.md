# Aula 5 — Unidades de capacidade e conversões binárias e decimais

## Objetivos de aprendizagem
Ao final, você deverá distinguir unidades decimais e binárias, converter valores entre bytes e unidades maiores, interpretar a capacidade anunciada por um dispositivo e evitar erros de cálculo no ZenithOS.

## 1. O que uma unidade de capacidade mede?
A capacidade indica quantos bytes podem ser armazenados. O byte é formado por 8 bits. Para expressar capacidades grandes, agrupamos bytes em unidades maiores. O cuidado é que existem duas convenções diferentes: decimal e binária.

## 2. Unidades decimais: base 1000
Fabricantes de dispositivos normalmente anunciam capacidades usando unidades decimais:
- 1 kB = 1.000 bytes;
- 1 MB = 1.000 kB = 1.000.000 bytes;
- 1 GB = 1.000 MB = 1.000.000.000 bytes;
- 1 TB = 1.000 GB = 1.000.000.000.000 bytes.

Cada passo multiplica por 1.000. Essa convenção é usada em especificações comerciais e em diversas interfaces.

## 3. Unidades binárias: base 1024
Na computação também usamos unidades baseadas em potências de 2:
- 1 KiB = 1.024 bytes;
- 1 MiB = 1.024 KiB;
- 1 GiB = 1.024 MiB;
- 1 TiB = 1.024 GiB.

O prefixo “i” é importante: KiB, MiB e GiB identificam unidades binárias. Não escreva GB quando o cálculo foi feito em GiB.

## 4. Exemplo resolvido: por que a capacidade parece mudar?
Considere um dispositivo anunciado como 500 GB decimais:
1. A capacidade anunciada é 500 × 1.000.000.000 bytes.
2. Isso corresponde a 500.000.000.000 bytes.
3. Para expressar em GiB, dividimos por 1.024 três vezes.
4. O resultado é aproximadamente 465,66 GiB.

O dispositivo não perdeu capacidade. A diferença vem das unidades usadas para expressá-la. Partições, metadados e reservas também podem reduzir o espaço disponível ao usuário, mas são outro fenômeno.

## 5. Conversões sem confundir as bases
Para converter de uma unidade decimal maior para bytes, multiplique por 1.000 a cada nível. Para unidades binárias, multiplique por 1.024. No sentido inverso, divida pela mesma base. Não misture uma etapa decimal com outra binária.

Exemplo: 3 MiB = 3 × 1.024 × 1.024 = 3.145.728 bytes.
Exemplo: 3 MB = 3 × 1.000 × 1.000 = 3.000.000 bytes.

## 6. Capacidade total, utilizável e livre
São valores diferentes:
- **Capacidade apresentada:** total de bytes ou blocos disponibilizados pelo dispositivo.
- **Capacidade utilizável pelo volume:** parte atribuída ao volume depois de limites e reservas.
- **Espaço livre:** parte ainda não ocupada dentro de uma estrutura de alocação.

O ZenithOS não deve confundir a capacidade física anunciada com espaço livre de um sistema de arquivos.

## 7. Aplicação no ZenithOS
O kernel deve manter uma unidade interna explícita, preferencialmente bytes ou contagens de blocos com tamanho conhecido. Toda conversão deve verificar overflow e arredondamento. Para exibição, o sistema pode escolher unidades decimais ou binárias, mas deve identificá-las corretamente.

## 8. Método de estudo
1. Identifique a unidade de origem e a unidade de destino.
2. Decida se a conversão usa base 1000 ou 1024.
3. Escreva cada multiplicação ou divisão.
4. Confira a ordem de grandeza.
5. Só então interprete o resultado no contexto do dispositivo.

## 9. Erros comuns
- Tratar GB e GiB como sinônimos exatos.
- Dividir por 1.000 em uma etapa e por 1.024 na seguinte sem justificar.
- Confundir capacidade total com espaço livre.
- Converter valores grandes sem verificar o limite do tipo inteiro usado pelo código.

## 10. Exercícios de compreensão
1. Qual é a diferença entre 1 GB e 1 GiB?
2. Converta 2 MiB para bytes e mostre as operações.
3. Um SSD anuncia 1 TB decimal. Por que o sistema pode exibir aproximadamente 931 GiB?
4. Qual é a diferença entre capacidade apresentada, capacidade utilizável e espaço livre?
5. Por que uma conversão de capacidade em código precisa considerar overflow?
6. Se o ZenithOS exibir “500 GB”, que informação adicional deve deixar clara para evitar ambiguidade?

## 11. Exercícios de código
- **EXN1A5.nbx:** converter bytes para KiB, MiB e GiB usando divisão inteira e resto, sem misturar bases.
- **EXN2A5.nbx:** converter GB decimal para bytes e depois para GiB, rejeitando valores que ultrapassem o limite representável.

## Critério de conclusão
Você deve conseguir explicar as duas convenções, realizar conversões manualmente e justificar qual unidade está usando em cada resultado.

## Metadados da aula
- **Dificuldade:** Média
- **Duração:** 35 minutos
