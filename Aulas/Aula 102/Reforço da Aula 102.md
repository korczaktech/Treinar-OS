# Reforço da Aula 102 — Mapa físico e descoberta de memória

## Ideia central

Interpretar a descrição de regiões físicas fornecida no boot e convertê-la, após validação e reservas, em intervalos seguros para o gerenciador de memória. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

mapa fornecido pelo firmware ou bootloader; tipos de região; intervalos com limite exclusivo; overflow; ordenação; sobreposição; regiões desconhecidas; reservas do kernel, bootloader, tabelas e framebuffer.

## Exemplo comentado

Considere uma região [0x100000, 0x500000) e uma reserva [0x280000, 0x300000). A memória elegível precisa ser dividida em [0x100000, 0x280000) e [0x300000, 0x500000), antes de aplicar alinhamento de páginas.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** manter parser, normalizador e política de reservas separados; preservar cópia original para diagnóstico; não permitir que o parser escreva diretamente no alocador
- **Fluxo:** receber bytes; validar cabeçalho e tamanho; decodificar entradas; validar aritmética; classificar tipos; ordenar; detectar conflitos; subtrair reservas; publicar somente intervalos utilizáveis
- **Riscos:** overflow em início+tamanho; mapa truncado; entradas duplicadas; tipos desconhecidos tratados como livres; mapa não ordenado; reservas esquecidas
- **Validação:** mapa vazio; entrada truncada; tamanho zero; overflow; região desconhecida; mapa fora de ordem; sobreposição; reserva que cobre uma região inteira; reserva parcial; limite máximo

## Perguntas para revisão ativa

1. Quais estruturas representam o componente?
2. Qual é a unidade de cada campo: bytes, páginas, identificadores ou estados?
3. Quais campos podem ser derivados e quais precisam ser armazenados?
4. Como representar ausência, erro e recurso reservado?
5. Quais invariantes devem permanecer verdadeiros?
6. Como evitar overflow, duplicidade e referências pendentes?

## Exercício rápido de recuperação

Sem olhar a aula principal, desenhe um modelo de dados anotado com campos, unidades, invariantes e estados inválidos. Depois compare seu desenho com as estruturas, fluxo e invariantes descritos na aula. Corrija o que estiver incompleto e explique em voz alta por que cada etapa existe.

## Quando revisar novamente

Faça uma revisão curta no dia seguinte e outra alguns dias depois. Em cada revisão, tente reconstruir o fluxo sem reler o texto primeiro. Consulte o material apenas para corrigir lacunas.
