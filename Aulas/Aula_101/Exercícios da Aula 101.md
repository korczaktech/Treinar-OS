# Exercícios da Aula 101 — Mapa físico e descoberta de memória

**Objetivo:** interpretar mapas de memória física, identificar regiões que podem ou não ser usadas e preparar dados seguros para o alocador de páginas do ZenithOS.

## Exercício 1 — Classificação de regiões

Classifique cada região como candidata a memória utilizável, reservada ou dependente de tratamento específico. Justifique:

- Região A: início 0x00100000, tamanho 0x00400000, tipo utilizável.
- Região B: início 0x00000000, tamanho 0x0009F000, tipo reservado.
- Região C: início 0xFEC00000, tamanho 0x00100000, tipo dispositivo mapeado em memória.
- Região D: início 0x00500000, tamanho 0x00100000, tipo desconhecido.

Não assuma que uma região marcada como utilizável pode ser entregue imediatamente ao alocador.

## Exercício 2 — Limites exclusivos

Uma região começa em 0x200000 e possui 0x180000 bytes.

1. Calcule o limite exclusivo.
2. Informe se o endereço 0x37FFFF pertence à região.
3. Informe se 0x380000 pertence à região.
4. Explique por que usar limite exclusivo facilita verificar sobreposição.

## Exercício 3 — Conversão em páginas

Considere páginas de 0x1000 bytes e uma região utilizável que começa em 0x201800 e termina no limite exclusivo 0x208900.

1. Determine o primeiro endereço alinhado que pode iniciar uma página completa.
2. Determine o limite exclusivo alinhado para baixo.
3. Calcule quantas páginas completas cabem.
4. Explique por que não é seguro disponibilizar as partes incompletas nas extremidades.

## Exercício 4 — Detecção de sobreposição

Considere estas regiões:

- A: [0x100000, 0x300000)
- B: [0x280000, 0x380000)
- C: [0x400000, 0x500000)

Identifique quais intervalos se sobrepõem. Proponha uma regra geral para detectar sobreposição entre dois intervalos com início e fim exclusivos.

## Exercício 5 — Validação defensiva

Descreva como o parser deve reagir a:

- tamanho de entrada menor que o cabeçalho;
- quantidade de entradas incompatível com o tamanho recebido;
- overflow ao calcular início + tamanho;
- tipo de região desconhecido;
- mapa fora de ordem;
- regiões sobrepostas.

Diferencie rejeitar o mapa inteiro de rejeitar somente uma entrada, e justifique a política escolhida.

## Exercício 6 — Reservas do ZenithOS

Faça uma lista das regiões que o kernel deve preservar durante a inicialização, incluindo kernel carregado, estruturas do bootloader, mapa de memória, pilhas, tabelas de páginas e framebuffer quando aplicável. Explique em que momento cada reserva pode deixar de ser necessária.

## Exercício 7 — Projeto do parser

Desenhe a interface de um parser que receba bytes do mapa e produza uma lista normalizada de regiões. Especifique entradas, saídas, erros e invariantes. Mantenha o parser independente do alocador físico.

## Exercício 8 — Testes

Crie uma matriz com pelo menos oito casos de teste, cobrindo mapa válido, mapa vazio, entrada truncada, overflow, sobreposição, tipo desconhecido, desalinhamento e região no limite do espaço de endereçamento.

## Desafio opcional em Nebula (.nbx)

Crie um programa com intervalos fictícios que receba início e tamanho, valide se o intervalo não excede um limite definido e informe se duas regiões se sobrepõem. Não tente ler ou escrever endereços físicos reais.

## Critério de conclusão

Você concluiu quando conseguir classificar regiões, calcular limites e alinhamentos, detectar sobreposição e explicar como o ZenithOS evita disponibilizar memória reservada.
