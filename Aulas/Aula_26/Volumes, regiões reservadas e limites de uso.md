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

1. Qual problema esta aula procura resolver?
2. Quais informações precisam ser conhecidas antes de executar a operação estudada?
3. Que dado inválido poderia causar acesso fora dos limites ou perda de consistência?
4. Qual responsabilidade pertence ao ZenithOS e qual pertence ao driver?
5. Que teste automatizado ajudaria a detectar uma implementação incorreta?

## 6. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
