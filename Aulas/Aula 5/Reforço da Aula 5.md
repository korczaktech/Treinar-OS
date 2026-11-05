# Reforço da Aula 5 — Unidades de capacidade e conversões

## A ideia central
A mesma quantidade de bytes pode ser apresentada usando unidades decimais ou binárias. O valor armazenado não muda quando mudamos a unidade de exibição.

## Quadro de referência
| Unidade | Base | Valor em bytes |
|---|---:|---:|
| kB | 1000 | 1.000 |
| KiB | 1024 | 1.024 |
| MB | 1000² | 1.000.000 |
| MiB | 1024² | 1.048.576 |
| GB | 1000³ | 1.000.000.000 |
| GiB | 1024³ | 1.073.741.824 |

## Exemplo passo a passo
Um dispositivo de 256 GB decimal oferece 256.000.000.000 bytes. Para converter em GiB, divida por 1.073.741.824. O resultado fica próximo de 238,42 GiB. Não houve perda física: apenas usamos outra unidade.

## Não confunda
- Capacidade do dispositivo: total que ele apresenta.
- Capacidade do volume: região atribuída ao volume.
- Espaço livre: parte ainda não alocada.
- GB: unidade decimal.
- GiB: unidade binária.

## Método rápido
1. Anote o valor e a unidade original.
2. Escreva a base da conversão.
3. Converta para bytes antes de trocar entre convenções.
4. Confira se o resultado faz sentido.
5. Identifique a unidade no resultado final.

## Perguntas de fixação
1. Quantos bytes existem em 4 KiB?
2. Quantos bytes existem em 4 kB?
3. Por que 1 TB não equivale exatamente a 1 TiB?
4. O espaço livre de um volume é necessariamente igual à capacidade do dispositivo?
5. Por que o código deve verificar overflow ao multiplicar uma capacidade?
