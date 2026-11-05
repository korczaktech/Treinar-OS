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

1. Qual problema esta aula procura resolver?
2. Quais informações precisam ser conhecidas antes de executar a operação estudada?
3. Que dado inválido poderia causar acesso fora dos limites ou perda de consistência?
4. Qual responsabilidade pertence ao ZenithOS e qual pertence ao driver?
5. Que teste automatizado ajudaria a detectar uma implementação incorreta?

## 6. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Difícil
> - **Duração:** 50 minutos
