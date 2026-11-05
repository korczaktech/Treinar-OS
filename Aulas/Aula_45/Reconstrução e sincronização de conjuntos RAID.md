# Reconstrução e sincronização de conjuntos RAID

## Objetivo

Nesta aula, você estudará reconstrução e sincronização de conjuntos raid e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Reconstrução repõe dados em um membro substituído usando membros restantes e, conforme o nível, dados e paridade. Sincronização também ocorre ao criar ou verificar um conjunto.

## 2. Exemplo de funcionamento

Acompanhe progresso por faixa, erros de leitura e gravação e estado persistente para retomar após reinicialização. Escritas concorrentes precisam ser coordenadas com a faixa em reconstrução.

## 3. Validação e segurança

Uma segunda falha durante reconstrução pode ser fatal, dependendo do nível. A leitura completa pode revelar setores irrecuperáveis. A prioridade equilibra tempo de recuperação e responsividade.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

No ZenithOS, reconstrução é tarefa controlada, cancelável e monitorável. Estados reconstruindo, sincronizado, degradado e falha devem ser explícitos.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Qual é a diferença entre reconstrução e verificação de paridade?
2. Por que a reconstrução reduz o desempenho?
3. Por que o conjunto fica mais vulnerável durante a reconstrução?
4. Que informação de progresso deve ser persistida?
5. Como tratar uma gravação concorrente em uma faixa que está sendo reconstruída?
6. O que pode acontecer se um segundo membro falhar durante a reconstrução?

## 6. Reconstrução após substituição
Quando um membro falha e é substituído, o conjunto precisa reconstruir nele os dados ou a paridade correspondentes. O processo percorre regiões do volume, lê os membros restantes, calcula o conteúdo necessário e grava o novo membro.

A reconstrução consome leitura, escrita e largura de banda. Pode reduzir o desempenho das operações normais e aumenta o período em que o conjunto permanece vulnerável.

## 7. Sincronização inicial e verificação
Ao criar um conjunto, os membros podem precisar ser inicializados para que dados e paridade estejam coerentes. Uma verificação posterior pode ler regiões e comparar paridade ou cópias. Verificar não é o mesmo que reconstruir: a verificação detecta divergências; a reconstrução produz conteúdo para um membro ausente ou inválido.

## 8. Progresso e reinício
O sistema precisa registrar progresso de forma consistente para retomar após reinicialização. Se o processo for interrompido, o estado salvo não pode afirmar que regiões ainda não processadas já foram reconstruídas. Escritas normais concorrentes precisam ser coordenadas com a região em reconstrução.

## 9. Exemplo guiado
Em um RAID 1, o membro A permanece saudável e B foi substituído. O sistema copia faixas de A para B e registra progresso. Se houver nova gravação na faixa que está sendo copiada, a política precisa garantir que a cópia final reflita a versão mais recente.

## 10. Método de aprendizagem
Represente o conjunto como faixas. Marque as faixas concluídas, pendentes e com erro. Simule reinício e gravação concorrente para verificar se o estado pode ser retomado sem declarar dados incorretos como válidos.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 60 minutos
