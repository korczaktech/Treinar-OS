# Reforço da Aula 10 — Integridade e Recuperação de Armazenamento

## 1. Integridade mantém as regras verdadeiras

Imagine que um arquivo esteja registrado como ocupando três unidades, mas o mapa de espaço livre indique que uma delas está disponível. As estruturas discordam. O sistema precisa detectar isso antes que outra gravação reutilize a unidade.

## 2. Checksum detecta, mas não recupera

O sistema calcula um valor a partir dos dados e compara com o valor registrado. Se forem diferentes, há evidência de alteração. Mas o checksum não sabe qual era o conteúdo correto e não reconstrói os bytes perdidos.

## 3. Falha no meio da atualização

Imagine que uma operação reserve uma unidade e depois registre essa unidade no arquivo. Se a energia acabar entre as etapas, uma estrutura pode ser atualizada e a outra não.

## 4. O journal registra o trabalho

O journal guarda informações sobre alterações e ajuda a decidir o que fazer após uma interrupção. Dependendo do formato, a recuperação pode repetir ou desfazer uma operação. As garantias dependem da ordem e da persistência dos registros.

## 5. Cache e persistência

Dados podem estar apenas na memória, em trânsito, em cache do dispositivo ou persistidos em mídia não volátil. O sistema precisa conhecer as garantias da interface e usar mecanismos de sincronização quando necessário.

## 6. Backup resolve outro problema

Journal ajuda com operações interrompidas. Backup mantém outra cópia dos dados. Se o dispositivo inteiro quebrar, o journal armazenado nele também pode ser perdido.

## 7. Quando não corrigir automaticamente?

Se duas versões de metadados discordarem e não houver informação suficiente para escolher a correta, uma correção arbitrária pode descartar dados válidos. Em alguns casos, o sistema deve preservar evidências e impedir novas gravações.

## 8. Perguntas de fixação

1. Um checksum diferente revela qual byte está correto?
2. Por que duas estruturas podem ficar inconsistentes após uma queda de energia?
3. O que o journal ajuda a fazer?
4. O journal substitui backup?
5. Por que uma gravação enviada pode ainda não estar persistida?
6. Quando uma correção automática pode causar mais danos?
