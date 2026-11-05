# TRIM, discard e liberação de blocos

## Objetivo

Nesta aula, você estudará trim, discard e liberação de blocos e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Quando o sistema de arquivos libera blocos, TRIM/discard informa ao dispositivo que certas faixas não precisam mais preservar dados. Isso pode ajudar coleta de lixo e gerenciamento interno de SSDs.

## 2. Exemplo de funcionamento

A operação informa intervalos não utilizados; não ordena necessariamente apagamento físico imediato. O dispositivo pode processar descarte de modo assíncrono e impor granularidade e limites.

## 3. Validação e segurança

TRIM não é apagamento seguro nem garantia de destruição forense. Ler depois de descartar pode ter comportamento variável. Descartar faixa ainda referenciada pode destruir dados válidos.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS encaminha discard apenas após confirmação de que a faixa está livre. O recurso é opcional e anunciado pelo driver.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Qual é a finalidade de TRIM/discard?
2. Por que liberar uma unidade no sistema de arquivos não significa apagá-la fisicamente?
3. Que risco existe em descartar uma faixa ainda referenciada por um snapshot?
4. Por que o dispositivo pode impor granularidade e limites ao discard?
5. TRIM é um mecanismo de apagamento seguro? Explique.
6. Por que uma leitura posterior à operação de discard não deve ser usada como forma de recuperar dados?

## 6. Da exclusão ao descarte
Quando um arquivo é removido, o sistema de arquivos pode liberar suas unidades no bitmap ou estrutura equivalente. A camada de blocos não deve presumir que todo espaço liberado precisa ser enviado imediatamente ao dispositivo. Uma política pode agrupar faixas e emitir discard posteriormente.

Antes de descartar, é essencial confirmar que nenhuma estrutura ativa ainda referencia a faixa. Um erro de contabilidade pode fazer o sistema informar ao SSD que dados válidos não são mais necessários.

## 7. Granularidade e limites
Dispositivos podem impor alinhamento, tamanho mínimo, quantidade máxima de intervalos e limites por comando de discard. O driver deve reportar essas capacidades e a camada deve dividir ou agrupar pedidos respeitando-as.

## 8. Comportamento após discard
O comando comunica que o conteúdo de uma faixa pode ser descartado pelo dispositivo. Não significa que as células NAND foram apagadas imediatamente. O comportamento de uma leitura posterior pode depender do protocolo e do dispositivo; não use a leitura pós-discard como mecanismo de recuperação.

## 9. Exemplo guiado
O sistema de arquivos libera a faixa [1.000, 1.100). Depois de atualizar seus metadados e confirmar que a faixa não é mais referenciada, pode enviar discard. Se um snapshot ainda referencia blocos dessa faixa, o descarte não pode ser enviado para esses blocos.

## 10. Método de aprendizagem
Siga o ciclo: arquivo removido, unidades liberadas, referências verificadas, faixa agrupada, capacidade do dispositivo consultada, discard enviado e resultado tratado.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 60 minutos
