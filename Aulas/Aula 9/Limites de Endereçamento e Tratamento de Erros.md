# Aula 9 — Limites de endereçamento e tratamento de erros

## Objetivos
Aprender a identificar endereços válidos, validar operações de um ou vários blocos, reconhecer erros antes e durante a transferência e entender por que o kernel nunca deve transformar uma falha em sucesso.

## 1. Capacidade e intervalo de endereços
Se um dispositivo apresenta N blocos, os LBAs válidos são 0 até N−1. A quantidade de blocos não é o maior endereço: o maior endereço é N−1.

Exemplo: um dispositivo com 200 blocos aceita LBAs de 0 a 199. O LBA 200 está fora dos limites.

## 2. Validar uma única posição
Para acessar um LBA, o dispositivo precisa existir, estar disponível e o endereço precisa ser não negativo e menor que a quantidade total de blocos.

Não use a condição LBA menor ou igual ao total. O valor igual ao total já está fora do intervalo. Para 200 blocos, 199 é válido; 200 é inválido.

## 3. Validar uma faixa
Uma operação pode solicitar vários blocos. Use início e quantidade. Depois de verificar início dentro do dispositivo e quantidade positiva, compare a quantidade com o espaço restante: quantidade <= total − início.

Exemplo: total 200, início 197, quantidade 3. O espaço restante é 3, portanto a faixa cabe e acessa 197, 198 e 199. Se quantidade for 4, a operação deve ser rejeitada.

## 4. Categorias de erro
Os erros devem informar a natureza da falha: dispositivo inexistente ou indisponível; parâmetro inválido; endereço fora dos limites; quantidade inválida; buffer insuficiente; recurso não suportado; falha de comunicação; erro de mídia; timeout; dispositivo removido durante a operação.

Erros diferentes podem exigir ações diferentes. Um parâmetro inválido deve ser rejeitado antes do driver; um erro de mídia vem da execução no dispositivo.

## 5. Erro de validação e erro de execução
Erro de validação significa que o pedido já era inválido antes de iniciar a transferência. Erro de execução significa que o pedido passou pela validação, mas falhou durante a comunicação ou operação.

Uma solicitação válida ainda pode falhar por desconexão, timeout ou defeito. Validar não significa prever o futuro.

## 6. Propagação correta
O driver deve traduzir o resultado do protocolo para uma representação entendida pelo kernel. A camada superior deve receber o erro real, sem dados falsos ou sucesso inventado. Se houve transferência parcial, informe a quantidade concluída.

## 7. Aplicação no ZenithOS
O ZenithOS deve centralizar regras de limites e códigos de erro. A camada de blocos valida parâmetros genéricos; o driver informa falhas específicas da interface; serviços superiores decidem se podem repetir, cancelar ou comunicar o problema.

## 8. Método de estudo
Para cada cenário, escreva: capacidade total, intervalo válido, pedido recebido, primeira condição que falha e resultado esperado. Isso evita tentar resolver tudo com uma condição lógica confusa.

## 9. Erros comuns
Aceitar o LBA igual ao total; esquecer que LBA começa em zero; validar apenas o primeiro bloco de uma faixa; repetir automaticamente qualquer erro; retornar sucesso quando a transferência foi parcial.

## 10. Exercícios de compreensão
1. Um dispositivo possui 512 blocos. Qual é o menor e o maior LBA válido?
2. Por que o LBA 512 é inválido nesse dispositivo?
3. Total 200, início 197, quantidade 3: a faixa é válida? Quais blocos são acessados?
4. O que diferencia erro de validação de erro de execução?
5. Por que um timeout não prova que o dispositivo foi destruído?
6. Como o sistema deve informar uma transferência parcial?
7. Por que a camada superior não deve receber sucesso quando o driver reporta erro?

## 11. Exercícios de código
- EXN1A9.nbx: validar um único LBA.
- EXN2A9.nbx: validar uma faixa com vários blocos sem overflow.
- EXN3A9.nbx: classificar erros de validação e execução em categorias distintas.

## Critério de conclusão
Você deve validar endereços e faixas, explicar os erros mais comuns e justificar por que o resultado real da operação precisa ser preservado.

## Metadados
- Dificuldade: Média
- Duração: 35 minutos
