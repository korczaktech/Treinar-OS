# Capacidades e características anunciadas por dispositivos

## Objetivo

Nesta aula, você estudará capacidades e características anunciadas por dispositivos e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Dispositivos anunciam capacidade, tamanho lógico e físico, limites de transferência, suporte a flush, discard, filas e recursos opcionais. Esses dados orientam drivers e camadas superiores.

## 2. Exemplo de funcionamento

Capacidade e limites devem ser normalizados para unidades internas consistentes. Recursos opcionais precisam distinguir suportado, não suportado e desconhecido; ausência de informação não significa suporte.

## 3. Validação e segurança

Validar respostas e não tratar anúncios como garantia de sucesso de toda operação. Recursos não compreendidos devem permanecer desabilitados. Tratar erros mesmo quando o dispositivo declarou suporte.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve expor uma estrutura comum de capacidades, separando propriedades, recursos opcionais e limites operacionais. Sistemas de arquivos não consultam comandos específicos do protocolo.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Cite quatro capacidades que um dispositivo pode anunciar.
2. Qual a diferença entre não suportado e desconhecido?
3. Por que o limite máximo de transferência precisa indicar sua unidade?
4. Um dispositivo anuncia suporte a flush. Isso garante que toda gravação futura terá sucesso? Explique.
5. O que o driver deve fazer com uma capacidade incoerente?
6. Por que a camada de arquivos não deve depender de comandos específicos do protocolo?

## 6. Capacidades não são promessas absolutas
O dispositivo pode anunciar tamanho lógico, capacidade, limite máximo de transferência, alinhamento, profundidade de fila e suporte a flush ou discard. Essas informações descrevem o que a interface declara suportar, mas uma operação específica ainda pode falhar.

O sistema deve distinguir três estados: suportado, não suportado e desconhecido. Tratar desconhecido como suportado pode levar a comandos inválidos ou perda de dados.

## 7. Normalização
Drivers diferentes podem reportar propriedades com representações distintas. O ZenithOS deve normalizar os dados em um descritor comum, mantendo unidades explícitas e preservando informações necessárias para o driver.

Por exemplo, tamanho de bloco deve ser expresso em bytes por bloco lógico. Limite de transferência deve declarar se está em blocos ou bytes.

## 8. Exemplo guiado
Um dispositivo anuncia tamanho lógico de 4.096 bytes, máximo de 128 blocos por comando e suporte a flush, mas não informa suporte a discard. O ZenithOS pode dividir pedidos maiores que 128 blocos e usar flush conforme o contrato. Não deve enviar discard até obter confirmação de suporte.

## 9. Método de aprendizagem
Para cada capacidade, registre nome, unidade, origem, validade, comportamento quando ausente e qual camada a utiliza.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
