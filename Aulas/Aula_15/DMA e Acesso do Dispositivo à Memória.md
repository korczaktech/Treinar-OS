# DMA e Acesso do Dispositivo à Memória

## Objetivo

Transferir dados byte a byte pela CPU pode ser caro. Muitos dispositivos usam DMA (Direct Memory Access) para transferir dados entre o dispositivo e a memória sem exigir que a CPU copie cada byte. Nesta aula vamos entender o papel do DMA, seus limites e a segurança dos buffers.

## 1. O que é DMA?

DMA é um mecanismo pelo qual um dispositivo ou controlador realiza transferências envolvendo memória principal. A CPU prepara a operação e acompanha sua conclusão, mas não precisa executar uma instrução para cada byte transferido.

DMA não significa ausência total de trabalho da CPU. O kernel ainda precisa preparar descritores, mapear memória, sincronizar dados e tratar conclusão e erros.

## 2. Buffer e descritor DMA

O driver prepara uma região de memória e descreve ao controlador onde e quanto transferir. Dependendo da arquitetura, o dispositivo pode não conseguir acessar qualquer endereço físico.

O endereço usado pelo dispositivo pode ser um endereço DMA ou IOVA, que não deve ser confundido automaticamente com um ponteiro virtual do processo.

## 3. Memória virtual e física

Um processo usa endereços virtuais. O hardware acessa endereços físicos ou endereços traduzidos por uma IOMMU. O driver precisa usar os mecanismos do kernel para mapear a região corretamente.

Nunca entregue diretamente um ponteiro arbitrário de usuário ao dispositivo como se fosse um endereço DMA válido.

## 4. IOMMU

Uma IOMMU pode traduzir e restringir os endereços que um dispositivo consegue acessar. Isso ajuda a isolar dispositivos e impedir acessos fora das regiões autorizadas.

Ela não elimina a necessidade de validar descritores, tamanhos e vida útil dos buffers.

## 5. Direção da transferência

Em uma leitura do armazenamento, o dispositivo escreve no buffer de memória. Em uma gravação, o dispositivo lê o buffer. O mapeamento e a sincronização devem respeitar a direção.

Confundir direção pode causar dados incorretos ou exposição de conteúdo antigo.

## 6. Vida útil e sincronização

O buffer precisa permanecer válido enquanto o dispositivo puder acessá-lo. Liberar ou reutilizar a memória cedo demais pode permitir que o DMA sobrescreva dados de outra operação.

Em arquiteturas não coerentes, o kernel pode precisar sincronizar cache da CPU e do dispositivo antes ou depois da transferência.

## 7. Limites e fragmentação

Uma região virtual contínua não é necessariamente fisicamente contínua. O mecanismo pode aceitar uma lista de segmentos, exigir memória contígua ou limitar tamanho e fronteiras. O driver deve seguir o contrato específico.

## 8. Aplicação no ZenithOS

A camada de armazenamento não deve fabricar endereços DMA. O driver solicita mapeamento ao subsistema de memória e prepara descritores conforme a interface. O subsistema de memória controla permissões, mapeamento e liberação.

## 9. Perguntas de compreensão

1. O que o DMA permite?
2. A CPU deixa de participar completamente da operação?
3. Por que um endereço virtual não é automaticamente um endereço DMA?
4. Para que serve uma IOMMU?
5. Por que o buffer não pode ser liberado antes da conclusão?
6. Qual a diferença de direção do DMA em leitura e gravação?

## 10. Exercícios de código

- EXN1A15.nbx — validar um descritor DMA didático.
- EXN2A15.nbx — controlar a vida útil de buffers até a conclusão ou cancelamento confirmado.


## Método de estudo e exemplo guiado
Em uma leitura DMA, o dispositivo escreve no buffer; em uma gravação DMA, o dispositivo lê o buffer. Para cada caso, identifique quem é o proprietário da região, qual mapeamento DMA é necessário e em que momento o buffer pode ser liberado. Simule uma conclusão normal e um cancelamento ainda não confirmado. O buffer só pode ser reutilizado quando o dispositivo não puder mais acessá-lo.