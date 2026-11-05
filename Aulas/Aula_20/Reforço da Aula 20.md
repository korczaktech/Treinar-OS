# Reforço da Aula 20 — Segurança do Armazenamento

## 1. Permissão antes da operação

O sistema precisa verificar quem solicita a leitura ou gravação e se possui autorização. Um processo não deve poder alterar qualquer bloco do disco sem controle.

## 2. Buffer isolado

O dispositivo só pode acessar a região mapeada para sua operação. Memória antiga não inicializada não deve ser devolvida ao usuário.

## 3. Criptografia em repouso

Protege dados armazenados quando não estão desbloqueados. A chave precisa ser protegida e recuperável conforme a política definida.

## 4. Apagar não é simples

Excluir arquivo, sobrescrever LBA e executar sanitize são operações diferentes. Em SSDs, remapeamento interno impede presumir que uma escrita apagou todas as cópias físicas.

## 5. Logs

Registre o tipo e o contexto do erro, mas não exponha senhas, chaves ou conteúdo sensível.

## 6. Fixação

1. Por que permissões precisam ser verificadas?
2. O que a criptografia em repouso protege?
3. O que acontece se a chave for perdida?
4. Por que sobrescrever um LBA pode não apagar páginas antigas?
5. Quais informações não devem aparecer em logs?
