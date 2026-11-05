# Falhas parciais e degradação de conjuntos RAID

## Objetivo

Nesta aula, você estudará falhas parciais e degradação de conjuntos raid e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Conjunto degradado perdeu membro ou redundância, mas ainda pode disponibilizar alguns dados. O comportamento depende do nível, da posição e da quantidade de falhas.

## 2. Exemplo de funcionamento

Gravações podem alcançar alguns membros e falhar em outros. O sistema registra divergência; leituras podem exigir paridade ou escolha de cópia válida. Erros silenciosos exigem verificação.

## 3. Validação e segurança

Em estado degradado, outra falha pode ser fatal. O sistema pode limitar operações, sinalizar urgência e impedir alterações administrativas perigosas. Não apresente o estado como normal.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS expõe saúde por membro e saúde geral do conjunto. Cada operação consulta o estado e aplica a política de leitura, gravação e recuperação.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. O que significa um conjunto RAID estar degradado?
2. Por que o sistema não deve apresentar um conjunto degradado como saudável?
3. Como tratar uma gravação que concluiu em alguns membros e falhou em outros?
4. Por que uma resposta sem erro não garante que os dados estejam corretos?
5. Quando um membro que voltou a responder pode ser considerado sincronizado?
6. Quais informações o ZenithOS deve expor sobre a saúde dos membros?

## 6. Estado degradado
Um conjunto está degradado quando perdeu um membro ou parte da redundância, mas ainda consegue oferecer determinadas operações. O que continua acessível depende do nível RAID, da localização das falhas e da quantidade de membros restantes.

Degradado não significa saudável. O sistema precisa informar a condição e pode aplicar políticas mais conservadoras.

## 7. Escrita parcial e divergência
Uma gravação pode alcançar alguns membros e falhar em outros. O conjunto precisa registrar quais membros concluíram, quais falharam e se a operação pode ser repetida com segurança. Não pode marcar todos como sincronizados quando houve sucesso parcial.

## 8. Erros silenciosos e leitura
Um membro pode responder sem erro, mas entregar conteúdo incorreto. Checksums ou comparações entre cópias/paridade podem ajudar a detectar divergências. Se não houver informação suficiente para decidir qual cópia é correta, o sistema deve preservar o estado de incerteza em vez de escolher arbitrariamente.

## 9. Exemplo guiado
Em um espelho de dois membros, A responde corretamente e B apresenta erro. O conjunto pode continuar lendo de A, mas precisa marcar B como falho ou desatualizado. Se B voltar, não deve ser tratado como sincronizado sem reconstrução ou verificação.

## 10. Método de aprendizagem
Monte uma tabela de membros com estado, última operação concluída e possibilidade de leitura. Simule uma falha durante gravação e determine o estado geral do conjunto e as operações permitidas.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 60 minutos
