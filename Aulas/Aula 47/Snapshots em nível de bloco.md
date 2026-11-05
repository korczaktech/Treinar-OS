# Snapshots em nível de bloco

## Objetivo

Nesta aula, você estudará snapshots em nível de bloco e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Snapshot preserva uma visão anterior do volume enquanto gravações continuam. Copy-on-write guarda a versão antiga antes de sobrescrever o bloco; outras estratégias redirecionam gravações para novas áreas.

## 2. Exemplo de funcionamento

Mapas relacionam blocos lógicos às versões físicas. Snapshots podem compartilhar blocos, exigindo contagem de referências ou estrutura equivalente. Metadados crescem conforme blocos mudam.

## 3. Validação e segurança

Snapshot não é necessariamente backup e pode ser perdido com o mesmo dispositivo. Espaço reservado pode acabar; o sistema precisa definir comportamento quando não consegue preservar uma versão.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

No ZenithOS, snapshots devem ter escopo e limites explícitos. Proteja mapas e referências e teste interrupções durante suas atualizações.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. O que um snapshot preserva?
2. Como copy-on-write permite manter uma versão antiga enquanto o volume continua recebendo gravações?
3. Por que um snapshot pode continuar ocupando espaço depois da exclusão de um arquivo?
4. O que deve acontecer quando o espaço reservado para snapshots acaba?
5. Por que snapshot não é necessariamente backup?
6. Qual coordenação pode ser necessária para criar um snapshot consistente para uma aplicação?

## 6. Copy-on-write
Em uma estratégia copy-on-write, o snapshot e o volume ativo podem inicialmente apontar para os mesmos blocos. Antes de sobrescrever um bloco compartilhado, o sistema preserva a versão antiga em outra região e atualiza os mapas. Assim, o snapshot continua mostrando o conteúdo anterior enquanto o volume ativo recebe a nova versão.

O custo aparece quando muitos blocos mudam: é preciso reservar espaço para versões antigas e manter mapas de referência.

## 7. Espaço e ciclo de vida
Snapshots consomem metadados e podem reter blocos que o volume ativo já não precisa. Apagar um arquivo no volume ativo não libera necessariamente a região física se um snapshot ainda referencia a versão antiga.

Se o espaço reservado acabar, o sistema precisa definir comportamento explícito: interromper gravações, invalidar o snapshot, ou aplicar outra política documentada. Não pode sobrescrever silenciosamente a única cópia preservada.

## 8. Exemplo guiado
Bloco X contém “A” e é compartilhado pelo volume e pelo snapshot. O volume grava “B”. Antes da alteração, a estratégia preserva “A” para o snapshot e direciona o volume ativo para a nova versão. O snapshot continua lendo “A”; o volume ativo lê “B”.

## 9. Consistência do snapshot
Um snapshot em nível de bloco pode capturar uma visão que ainda não é consistente para uma aplicação se houver gravações relacionadas em andamento. É necessário coordenar flush, barreiras ou congelamento da camada superior conforme a garantia desejada.

## 10. Método de aprendizagem
Desenhe dois mapas: volume ativo e snapshot. Acompanhe uma gravação e conte quantas versões precisam ser preservadas. Depois simule falta de espaço e interrupção durante atualização dos mapas.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 60 minutos
