# Clonagem e duplicação de volumes

## Objetivo

Nesta aula, você estudará clonagem e duplicação de volumes e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Cópia física transfere blocos; clone lógico pode compartilhar dados e copiar somente quando houver alteração. Clonar um volume não é igual a copiar arquivos, pois pode incluir metadados e espaço não alocado.

## 2. Exemplo de funcionamento

Antes da cópia, valide capacidade, tamanho de bloco, sobreposição e estado. Origem ativa pode mudar durante a operação; consistência exige snapshot, congelamento ou coordenação.

## 3. Validação e segurança

Duplicar identificadores únicos pode gerar conflito quando origem e clone ficam conectados simultaneamente. Interrupção deve deixar destino marcado como incompleto, não como volume válido.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve distinguir cópia bruta, clone consistente e clone copy-on-write. Publique destino somente após validação final.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Qual é a diferença entre cópia de arquivos, cópia bruta e clone lógico?
2. Por que uma origem ativa pode produzir uma cópia inconsistente?
3. Como um snapshot pode ajudar durante a clonagem?
4. Por que identificadores duplicados podem causar conflitos?
5. O que deve acontecer se o destino for menor que o escopo da origem?
6. Quando um destino deve ser publicado como volume válido?

## 6. Cópia bruta e clone lógico
Uma cópia bruta transfere blocos da origem para o destino, incluindo regiões que não pertencem a arquivos ativos, conforme o escopo escolhido. Um clone lógico pode compartilhar blocos e copiar apenas quando uma das versões muda. Uma cópia de arquivos, por sua vez, interpreta diretórios e arquivos e não necessariamente preserva todo o layout do volume.

Cada operação tem objetivos diferentes e deve declarar o que será copiado.

## 7. Consistência da origem
Se a origem continuar recebendo gravações durante a cópia, o destino pode misturar versões de momentos diferentes. Para obter uma imagem consistente, use snapshot, pause gravações ou coordene a operação com a camada superior.

## 8. Identificadores duplicados
Clonar um volume pode duplicar GUIDs, UUIDs e outros identificadores. Se origem e clone forem conectados ao mesmo tempo, o sistema pode confundir os volumes. O processo precisa decidir quais identificadores devem ser preservados e quais devem ser regenerados.

## 9. Exemplo guiado
Uma origem de 10.000 blocos é copiada para destino de 8.000 blocos. A operação deve ser rejeitada se o escopo exigir copiar os 10.000 blocos. Se o destino tiver espaço suficiente, ainda será necessário validar sobreposição, consistência da origem e identidade final.

## 10. Método de aprendizagem
Compare três cenários: cópia de arquivos, cópia bruta e clone copy-on-write. Para cada um, identifique o que é preservado, o que exige espaço e como lida com alterações concorrentes.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 60 minutos
