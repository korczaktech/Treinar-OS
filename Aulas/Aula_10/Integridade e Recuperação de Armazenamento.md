# Integridade e Recuperação de Armazenamento

## Objetivo

Um sistema de armazenamento não pode considerar apenas o cenário em que todas as operações terminam corretamente. Energia pode acabar, dispositivos podem falhar, dados podem ser corrompidos e o sistema pode reiniciar durante uma atualização.

Nesta aula estudaremos integridade e recuperação: como detectar inconsistências, reduzir o risco de estruturas parcialmente atualizadas e recuperar um estado utilizável depois de uma falha.

## 1. O que significa integridade?

Integridade significa que dados e estruturas mantêm as propriedades esperadas. Um descritor não deve conter capacidade impossível; uma partição não deve ultrapassar o dispositivo; uma entrada de diretório não deve apontar para uma referência inexistente; uma unidade não deve estar simultaneamente livre e atribuída a dois arquivos quando o formato não permite isso.

Integridade não significa ausência absoluta de falhas. Significa possuir regras para detectar inconsistências e mecanismos para evitar ou tratar danos.

## 2. Corrupção de dados

Corrupção ocorre quando dados ou estruturas deixam de representar corretamente a informação esperada. Pode ser causada por queda de energia, defeito de mídia, falha de memória, erro de software, transferência incompleta ou problema de comunicação.

Nem toda falha causa corrupção e nem toda corrupção é detectada automaticamente. O sistema precisa de mecanismos adequados ao risco.

## 3. Checksum e detecção

Checksum é um valor calculado a partir de um conjunto de dados. Ao ler os dados novamente, o sistema calcula outro valor e compara os resultados. Se forem diferentes, há evidência de alteração ou erro.

Checksums simples detectam algumas alterações acidentais, mas não oferecem proteção criptográfica. Para resistir a adulteração intencional, são necessários mecanismos criptográficos adequados.

Detectar não é corrigir. Um checksum pode indicar corrupção, mas não sabe qual era o conteúdo correto e não reconstrói os bytes perdidos.

## 4. Atualizações interrompidas

Imagine que o sistema precise marcar uma unidade como ocupada e registrar que ela pertence a um arquivo. Se a energia acabar entre as etapas, as estruturas podem discordar.

Uma parte pode indicar que a unidade está ocupada, enquanto outra não possui referência para ela. Esse é um problema de consistência entre atualizações relacionadas.

A ordem das operações, o registro de intenção e a recuperação após reinício ajudam a evitar estados impossíveis de interpretar.

## 5. Journaling

Journaling é uma técnica na qual o sistema registra informações sobre alterações antes de aplicá-las definitivamente às estruturas principais, conforme o protocolo do formato.

Em uma abordagem simplificada:
1. registrar a operação planejada;
2. persistir o registro conforme as garantias necessárias;
3. atualizar as estruturas principais;
4. marcar a operação como concluída ou liberar o registro.

Após uma interrupção, o sistema consulta o journal para identificar operações que precisam ser repetidas ou desfeitas.

O comportamento varia conforme o sistema de arquivos. Alguns journals registram metadados, outros podem registrar dados. Journaling não é backup e não protege contra perda física completa do mesmo dispositivo.

## 6. Atomicidade e consistência

Uma operação é atômica quando, segundo o contrato definido, aparece como concluída ou não aplicada parcialmente. Nem toda gravação física é automaticamente atômica.

Consistência significa que as regras internas continuam verdadeiras antes e depois da operação. Por exemplo, uma unidade não deve pertencer simultaneamente a dois arquivos se o formato não permitir.

A recuperação deve levar o sistema a um estado válido mesmo que a operação original não tenha terminado.

## 7. Cache e persistência

Dados podem estar na memória do sistema, em trânsito, no cache do dispositivo ou persistidos em mídia não volátil.

Uma operação reportada como concluída pode ter garantias diferentes conforme o protocolo, os caches e os comandos de sincronização. Quando uma aplicação precisa garantir que uma atualização sobreviva à perda de energia, o sistema deve usar as primitivas de sincronização apropriadas e respeitar a ordem exigida.

Não prometa durabilidade apenas porque uma chamada de gravação retornou sucesso.

## 8. Verificação de consistência

Um verificador pode procurar:
- unidades atribuídas a mais de um arquivo;
- unidades ocupadas sem referência;
- entradas de diretório inválidas;
- contagens de espaço livre incorretas;
- referências fora da partição.

A correção automática precisa ser conservadora. Se o sistema não souber qual versão é correta, inventar uma resposta pode piorar os danos. Em alguns casos, é melhor preservar evidências, impedir novas gravações e solicitar recuperação especializada.

## 9. Recuperação não é backup

| Mecanismo | Objetivo |
|---|---|
| Checksum | Detectar alterações ou corrupção |
| Verificação de consistência | Encontrar contradições nas estruturas |
| Journal | Ajudar a recuperar atualizações interrompidas |
| Backup | Manter outra cópia dos dados |
| Redundância | Manter cópias ou informações adicionais para tolerar falhas |

Um journal no mesmo dispositivo não protege contra a perda física do dispositivo. Um checksum não recria dados. Um backup antigo pode não conter as alterações recentes.

## 10. Aplicação no ZenithOS

O ZenithOS precisa definir quando uma gravação é considerada concluída, como sincronizar dados e metadados, como identificar estruturas corrompidas, como recuperar operações interrompidas e como informar quando a integridade não pode ser garantida.

A implementação deve começar com contratos e testes simulados. Depois, os mecanismos podem ser integrados aos drivers e aos formatos de sistema de arquivos suportados.

## 11. Perguntas de compreensão

1. Qual é a diferença entre detectar corrupção e recuperar dados?
2. Por que checksum não substitui backup?
3. O que pode acontecer se a energia acabar entre duas atualizações relacionadas?
4. Qual é o papel do journal?
5. Por que journaling não é backup?
6. Qual é a diferença entre dados enviados e dados persistidos?
7. Por que uma verificação não deve corrigir estruturas com base em suposições?

## 12. Exercícios de código

- EXN1A10.nbx — calcular e comparar um checksum didático, sem alegar segurança criptográfica.
- EXN2A10.nbx — analisar registros simplificados e classificar operações para recuperação.

## Critério de conclusão

Você deve explicar como detectar inconsistências, por que atualizações interrompidas são perigosas e por que recuperação e backup são mecanismos diferentes.
