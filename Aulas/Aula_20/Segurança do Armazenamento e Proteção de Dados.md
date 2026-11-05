# Segurança do Armazenamento e Proteção de Dados

## Objetivo

Armazenamento contém dados pessoais, credenciais, configurações e arquivos essenciais ao sistema. Nesta aula vamos estudar como proteger operações, impedir acessos indevidos, reduzir exposição de dados e compreender criptografia e descarte seguro sem confundir esses mecanismos.

## 1. Segurança em camadas

A proteção começa antes da leitura do bloco. O sistema precisa validar quem solicita a operação, qual objeto pode acessar e se a faixa está dentro dos limites. O driver também deve validar parâmetros recebidos da camada superior.

Não confie em dados de entrada apenas porque vieram de outro componente do próprio kernel: erros internos também podem causar corrupção.

## 2. Controle de acesso

Permissões definem quais usuários ou componentes podem ler, gravar ou executar operações. O sistema de arquivos normalmente aplica permissões sobre arquivos e diretórios. A camada de armazenamento aplica controles mais baixos sobre dispositivos e operações privilegiadas.

Um processo comum não deve conseguir escrever diretamente em qualquer LBA do disco do sistema.

## 3. Isolamento de buffers

Buffers pertencem a um contexto e possuem uma vida útil. O kernel deve impedir que um dispositivo ou componente acesse memória fora da região autorizada. Mapeamentos DMA e IOMMU podem ajudar, mas não substituem validação.

Ao devolver um buffer ao usuário, não exponha bytes antigos de memória que não foram inicializados.

## 4. Criptografia em repouso

Criptografia de armazenamento protege dados quando a mídia está desligada ou é acessada sem a chave apropriada. Os dados são transformados usando uma chave; sem a chave correta, o conteúdo não deve ser interpretável.

A segurança depende do algoritmo, implementação, gestão de chaves, modo de operação e proteção contra vazamento. Não invente algoritmo próprio.

## 5. Gestão de chaves

A chave não deve ficar armazenada em texto puro junto com os dados que protege. O sistema precisa definir como desbloquear, guardar, derivar, rotacionar e revogar chaves.

Perder a chave pode tornar os dados inacessíveis. Uma cópia de segurança da chave deve ser protegida com o mesmo cuidado que os dados.

## 6. Apagamento lógico e físico

Remover um arquivo pode apenas liberar suas referências. Sobrescrever um LBA não garante que todas as versões físicas anteriores sejam apagadas em SSD, por causa do FTL e remapeamento.

Comandos de sanitize ou secure erase dependem do dispositivo e do protocolo. O sistema deve verificar suporte e resultado; não deve prometer apagamento seguro apenas porque removeu um arquivo ou escreveu zeros.

## 7. Dados sensíveis em logs e erros

Logs devem registrar o necessário para diagnóstico, sem copiar senhas, chaves ou conteúdo de buffers. Mensagens de erro também não devem revelar dados protegidos a usuários sem permissão.

## 8. Ameaças e limites

Criptografia em repouso não protege automaticamente um sistema já desbloqueado contra malware com privilégios. Permissões não corrigem firmware malicioso. Checksums não autenticam dados contra adulteração intencional, a menos que façam parte de um mecanismo criptográfico apropriado.

Cada controle protege contra uma classe de ameaça.

## 9. Aplicação no ZenithOS

O ZenithOS deve usar primitivas criptográficas consolidadas, separar chaves dos dados, validar permissões em cada camada apropriada, proteger buffers e documentar exatamente o que significa apagar ou sincronizar.

## 10. Perguntas de compreensão

1. Por que um processo comum não deve escrever diretamente em qualquer LBA?
2. Qual é a função do isolamento de buffers?
3. O que a criptografia em repouso protege?
4. Por que perder a chave pode significar perder acesso aos dados?
5. Por que sobrescrever um LBA não garante apagar todas as páginas NAND antigas?
6. Por que logs não devem conter chaves e conteúdo sensível?
7. Criptografia em repouso protege automaticamente contra malware após desbloqueio?

## 11. Exercícios de código

- EXN1A20.nbx — validar permissões de leitura, gravação e operação privilegiada.
- EXN2A20.nbx — classificar pedidos de descarte conforme as capacidades declaradas, sem afirmar apagamento garantido.
