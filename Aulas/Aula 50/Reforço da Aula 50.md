# Reforço da Aula 50 — Projeto do gerenciador de volumes do ZenithOS

## Responsabilidade
O gerenciador descobre regiões, interpreta partições, valida limites, aplica reservas, cria volumes e traduz endereços relativos para o dispositivo de origem.

## Exemplo de tradução
Volume começa no LBA 4.000 e possui 2.000 blocos. Pedido relativo: início 1.990, quantidade 10. A faixa termina no limite exclusivo 2.000 e cabe. Depois de validar, o LBA absoluto inicial é 5.990. Se pedir 11 blocos, rejeite antes da soma.

## Ordem incremental
1. Modelo em memória.
2. Funções puras de intervalos e tradução.
3. Dispositivo em RAM.
4. Testes de partições e reservas.
5. Parsers GPT/MBR.
6. Registro e ciclo de vida de volumes.
7. Montagem e integração com drivers.

## Perguntas
1. Quais são as responsabilidades do gerenciador?
2. Por que validar o intervalo relativo antes da soma?
3. O que impede publicar um volume parcialmente validado?
4. Como a remoção do dispositivo de origem afeta o volume?
5. Por que começar com dispositivo em RAM?
