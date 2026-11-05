# Cache de Armazenamento e Coerência

## Objetivo

Uma operação de armazenamento pode envolver memória principal, cache do sistema operacional, filas do driver e cache interno do dispositivo. Nesta aula vamos entender por que caches existem, quais dados podem estar em cada camada e como evitar que leituras e gravações observem versões incompatíveis.

## 1. O que é cache?

Cache é uma cópia temporária de dados mantida em uma camada mais rápida ou conveniente para reduzir acessos a uma camada mais lenta. No armazenamento, o sistema pode manter em RAM blocos lidos recentemente. Um SSD também pode possuir cache interno.

Cache não é o local definitivo do dado. É uma cópia cuja validade precisa ser controlada.

## 2. Cache de leitura

Quando um bloco é lido, o sistema pode guardar uma cópia. Se o mesmo bloco for solicitado novamente e a cópia ainda for válida, a resposta pode vir da RAM.

Isso evita uma nova operação no dispositivo. Porém, se o conteúdo do bloco mudar, a cópia antiga precisa ser atualizada ou invalidada. Caso contrário, o sistema entrega dados desatualizados.

## 3. Cache de escrita

Em uma política write-through, a gravação é encaminhada à camada seguinte e a cópia em cache é atualizada de acordo com as garantias definidas.

Em write-back, o sistema pode confirmar a atualização da cópia em RAM antes de enviar os dados ao dispositivo. A gravação fica pendente. Isso melhora desempenho, mas cria uma janela em que uma queda de energia pode perder dados ainda não persistidos.

A palavra "concluída" precisa ter significado explícito: atualizada no cache? enviada ao dispositivo? persistida em mídia não volátil?

## 4. Coerência e invalidação

Se duas camadas mantêm cópias do mesmo bloco, uma gravação precisa coordenar essas cópias. Uma estratégia pode atualizar todas as cópias; outra pode invalidar cópias antigas e recarregá-las quando necessário.

O contrato precisa impedir que uma leitura posterior retorne uma versão anterior à gravação que ela deveria observar.

## 5. Identidade de uma entrada

Uma entrada de cache não pode ser identificada apenas pelo número LBA. O mesmo LBA pode existir em dispositivos diferentes. Uma chave adequada inclui, no mínimo, a identidade do dispositivo e o LBA, além de informações de versão ou estado quando a implementação exigir.

Também é necessário considerar a remoção do dispositivo: entradas associadas a uma unidade removida não podem ser reutilizadas como se fossem de outra.

## 6. Estados úteis

Uma entrada pode estar:
- LIMPA: cópia válida e sem gravação pendente;
- SUJA: foi modificada e ainda precisa ser enviada;
- EM_CARREGAMENTO: leitura em andamento;
- INVALIDA: não pode ser usada como dado atual.

O significado e as transições devem ser definidos. Uma entrada suja não pode ser descartada silenciosamente.

## 7. Política de substituição

Quando o cache está cheio, precisa escolher entradas para remover. LRU é uma política conhecida: tenta remover a entrada que ficou mais tempo sem uso. Outras políticas consideram frequência, custo de recarga ou prioridade.

Uma entrada suja exige tratamento antes de ser reutilizada. O sistema pode gravá-la primeiro ou mantê-la até que a gravação seja concluída.

## 8. Aplicação no ZenithOS

O ZenithOS deve separar cache de blocos de cache de arquivos. O cache de blocos trabalha com identidade do dispositivo e LBA. O cache de arquivos trabalha com objetos e semântica do sistema de arquivos. Eles podem cooperar, mas não devem confundir suas chaves nem prometer as mesmas garantias.

## 9. Perguntas de compreensão

1. Por que cache não é armazenamento definitivo?
2. Qual a diferença entre write-through e write-back?
3. O que pode acontecer se uma cópia antiga não for invalidada?
4. Por que a chave do cache precisa identificar o dispositivo além do LBA?
5. O que significa uma entrada suja?
6. Por que uma entrada suja não pode ser descartada como uma entrada limpa?

## 10. Exercícios de código

- EXN1A11.nbx — modelar estados de uma entrada de cache e validar transições.
- EXN2A11.nbx — consultar uma entrada usando dispositivo e LBA como chave, evitando colisões entre dispositivos.

## Critério de conclusão

Você deve explicar quando uma cópia em cache é válida, o que diferencia uma entrada limpa de uma suja e quais garantias uma política de escrita oferece.


## Método de estudo e exemplo guiado
Imagine que o cache contém a versão A do LBA 20. Uma gravação produz a versão B. Antes de responder uma nova leitura, a política precisa garantir que ela não receba A por engano. Simule duas estratégias: atualizar a entrada ou invalidá-la para recarga. Depois marque a entrada como SUJA quando a nova versão ainda não foi persistida. O exercício deve separar validade da cópia e durabilidade no dispositivo.

## Metadados da aula
- Dificuldade: Difícil
- Duração: 45 minutos
