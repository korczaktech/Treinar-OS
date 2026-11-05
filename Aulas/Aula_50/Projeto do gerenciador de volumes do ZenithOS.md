# Projeto do gerenciador de volumes do ZenithOS

## Objetivo

Nesta aula, você estudará projeto do gerenciador de volumes do zenithos e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

O gerenciador de volumes fica entre descoberta de dispositivos e sistemas de arquivos. Interpreta partições, valida regiões, cria volumes, traduz endereços relativos e publica unidades disponíveis.

## 2. Exemplo de funcionamento

Um volume registra identidade, origem, início, quantidade de blocos, tamanho lógico, capacidades, estado e referências. Tradução valida a faixa relativa antes de calcular LBA absoluto. Composição exige grafo sem ciclos.

## 3. Validação e segurança

Trate tabela desconhecida, metadados corrompidos, partições sobrepostas, remoção e falhas de I/O. Nenhum volume inválido deve ser publicado parcialmente; recuperação deve ser separada da descoberta normal.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

No ZenithOS, comece com modelo em memória e testes puros. Depois conecte dispositivo RAM, leitores GPT/MBR, registro de volumes e montagem. Hardware real vem após contratos e testes automatizados.

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
> - **Duração:** 60 minutos
