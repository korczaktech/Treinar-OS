# Operações de leitura e escrita em múltiplos blocos

## Objetivo

Nesta aula, você estudará operações de leitura e escrita em múltiplos blocos e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Uma requisição de múltiplos blocos transfere LBAs consecutivos em um comando. Agrupar operações reduz overhead, mas o protocolo, o controlador, o buffer e o driver podem impor limites máximos.

## 2. Exemplo de funcionamento

Valide início, quantidade, capacidade restante, multiplicação por tamanho do bloco e capacidade do buffer. Se o limite por comando for menor que a operação, divida em segmentos contíguos sem lacunas nem sobreposição.

## 3. Validação e segurança

Uma transferência pode terminar parcialmente. O contrato deve informar quantos blocos foram concluídos e qual erro ocorreu. Não presuma que uma requisição grande seja atomicamente concluída.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS pode oferecer operação lógica grande e deixar o driver dividir conforme seus limites. O resultado preserva quantidade concluída e erro.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Por que uma requisição de vários blocos pode exceder o limite do driver?
2. Divida 300 blocos em segmentos com máximo de 128. Quais são as quantidades?
3. Como calcular o LBA inicial do segundo segmento?
4. Por que a soma das quantidades precisa ser igual à requisição original?
5. O que informar se os dois primeiros segmentos concluírem e o terceiro falhar?
6. Quais outros limites, além da quantidade máxima, podem exigir divisão?

## 6. Divisão por limite máximo
Suponha que uma requisição solicite 300 blocos, mas o driver aceite no máximo 128 por comando. A camada pode produzir três segmentos: 128, 128 e 44 blocos. O segundo começa após os primeiros 128; o terceiro começa após 256. A soma precisa ser exatamente 300.

Cada segmento também precisa respeitar limite de buffer, alinhamento, fronteira de endereço e profundidade de fila.

## 7. Resultados parciais
Se o primeiro e o segundo segmentos forem concluídos e o terceiro falhar, o sistema não pode declarar que toda a requisição teve sucesso. Deve informar quantos blocos foram concluídos e qual falha ocorreu. Para gravações, também é importante definir como a camada superior lida com conteúdo parcialmente atualizado.

## 8. Exemplo guiado
Requisição inicial: LBA 1.000, quantidade 300. Limite por comando: 128.
- Segmento 1: LBA 1.000, 128 blocos.
- Segmento 2: LBA 1.128, 128 blocos.
- Segmento 3: LBA 1.256, 44 blocos.
Os intervalos são adjacentes e não possuem lacunas nem sobreposição.

## 9. Método de aprendizagem
Desenhe a faixa original e marque cada segmento. Some as quantidades, confira os inícios e simule falha em cada segmento.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
