# Volumes, regiões reservadas e limites de uso

## Objetivo

Nesta aula, você estudará volumes, regiões reservadas e limites de uso e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Disco é o dispositivo físico ou virtual; partição é uma região descrita por uma tabela; volume é uma unidade lógica disponibilizada ao sistema. Um volume pode corresponder a uma partição, a um disco inteiro ou a uma composição de regiões.

## 2. Exemplo de funcionamento

Se uma região do disco for reservada para metadados, boot ou recuperação, ela não pode ser entregue simultaneamente ao sistema de arquivos como espaço livre. O volume deve expor apenas a capacidade que realmente pertence a ele.

## 3. Validação e segurança

Validar início e quantidade da região, excluir reservas e impedir sobreposições. Ao converter LBA relativo do volume em LBA do dispositivo, validar primeiro a faixa relativa e só depois calcular o deslocamento absoluto.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve representar volumes com identidade, capacidade, tamanho de bloco, estado e referência à origem. Sistemas de arquivos recebem um volume validado, não offsets arbitrários.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Explique a diferença entre dispositivo, partição e volume.
2. Por que uma região reservada não pode ser contabilizada como espaço livre?
3. Um volume começa no LBA 10.000. Qual é o LBA absoluto correspondente ao LBA relativo 50?
4. Um volume possui 5.000 blocos. Uma requisição relativa começa em 4.990 e pede 10 blocos. Ela cabe? E se pedir 11?
5. Por que validar apenas contra a capacidade total do disco não basta?
6. Quais informações devem fazer parte do descritor de um volume?

## 6. Partição, volume e dispositivo
Dispositivo é a unidade física ou virtual que apresenta blocos. Partição é uma região descrita por um mapa de particionamento. Volume é uma unidade lógica que o sistema disponibiliza para uso. Um volume pode corresponder a uma partição, ao disco inteiro ou a uma composição de regiões.

A diferença é importante: o volume pode aplicar políticas próprias e ocultar a origem física. O sistema de arquivos trabalha com o volume disponibilizado, não precisa conhecer diretamente todos os dispositivos inferiores.

## 7. Regiões reservadas
Uma área pode ser reservada para metadados, boot, recuperação, alinhamento ou uso interno. Ela não pode ser contabilizada como espaço livre de outro volume ao mesmo tempo. O gerenciador deve manter um mapa de propriedade das regiões para evitar sobreposição.

## 8. Tradução de endereços relativos
Se um volume começa no LBA 10.000 do dispositivo e uma requisição usa o LBA relativo 50, o endereço absoluto será 10.050. Antes da soma, valide se o LBA relativo e a quantidade cabem na capacidade do volume. Depois valide se a região absoluta continua dentro do dispositivo. Isso evita que uma camada superior escape dos limites da região que recebeu.

## 9. Exemplo guiado
Volume: início 10.000, quantidade 5.000. Requisição relativa: início 4.990, quantidade 10. A faixa termina exatamente no limite do volume e é válida. Com quantidade 11, ultrapassa o volume e deve ser rejeitada, mesmo que o dispositivo físico tenha espaço depois dele.

## 10. Método de aprendizagem
Desenhe o dispositivo, marque partições e reservas, depois destaque o volume. Faça duas traduções: uma que termina exatamente no limite e outra que ultrapassa uma unidade.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
