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

1. Qual é a responsabilidade do gerenciador de volumes?
2. Quais campos essenciais devem existir em um descritor de volume?
3. Por que o gerenciador só deve publicar volumes depois de validar todo o mapeamento?
4. Como traduzir um LBA relativo para absoluto com segurança?
5. O que deve acontecer com volumes dependentes quando o dispositivo de origem é removido?
6. Qual ordem incremental reduz o risco de implementar todo o gerenciador de uma só vez?
7. Por que identificar um volume não significa que seu sistema de arquivos já pode ser montado?

## 6. Modelo de dados do gerenciador
Uma representação inicial de volume deve conter identidade, dispositivo de origem, LBA inicial, quantidade de blocos, tamanho lógico, capacidades, estado e referências às dependências. Os campos precisam ter unidades explícitas. A identidade do volume não deve ser confundida com o endereço do dispositivo ou com o GUID encontrado no disco.

## 7. Fluxo de descoberta até publicação
1. Receber um dispositivo já inicializado.
2. Validar o descritor e as capacidades.
3. Ler a tabela de partições suportada.
4. Validar cabeçalhos, entradas, limites e sobreposição.
5. Aplicar regiões reservadas.
6. Criar objetos de volume ainda não publicados.
7. Validar cada mapeamento e dependência.
8. Publicar somente volumes consistentes.
9. Permitir que o sistema de arquivos tente identificar e montar o conteúdo.

Falha em uma etapa não deve deixar objetos parcialmente acessíveis.

## 8. Tradução de LBA relativo
Se o volume começa no LBA absoluto V e a requisição usa início relativo R, o início absoluto é V + R. Mas a soma só ocorre depois de validar que a faixa relativa cabe na quantidade do volume. Em seguida, a camada confirma que o resultado continua dentro do dispositivo de origem.

## 9. Estados e ciclo de vida
Um volume pode estar DETECTADO, VALIDANDO, DISPONIVEL, MONTADO, INDISPONIVEL ou COM_ERRO. Remoção do dispositivo de origem deve propagar indisponibilidade. Desmontagem e remoção precisam respeitar referências ativas e operações pendentes.

## 10. Plano de implementação incremental
Comece com estruturas em memória e funções puras para intervalos e traduções. Depois use um dispositivo em RAM e testes de partições. Integre leitores GPT e MBR, depois descoberta real, montagem e drivers. Não comece com RAID, snapshots e hardware real simultaneamente.

## 11. Método de aprendizagem
Desenhe o fluxo completo, marque em cada etapa quais dados entram, quais validações são feitas e qual estado é publicado. Crie ao menos um cenário válido e três inválidos: partição sobreposta, offset fora do volume e dispositivo removido durante validação.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 60 minutos
