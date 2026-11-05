# Volumes distribuídos e espelhados

## Objetivo

Nesta aula, você estudará volumes distribuídos e espelhados e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Distribuição divide dados entre dispositivos para capacidade ou paralelismo; espelhamento mantém cópias equivalentes para tolerar certas falhas. Cada estratégia possui custo e comportamento distintos.

## 2. Exemplo de funcionamento

No espelhamento, defina quando uma gravação é considerada concluída e como escolher cópia saudável para leitura. Em distribuição, perda de um membro pode tornar faixas inacessíveis.

## 3. Validação e segurança

Redundância não substitui backup: exclusão, corrupção lógica e malware podem ser replicados. Falhas simultâneas e erros silenciosos também podem comprometer o conjunto.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve expor estado de cada membro, divergências e capacidade útil. Não prometa proteção absoluta nem disponibilidade além das garantias reais.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Como a distribuição organiza os dados entre membros?
2. Por que distribuição sem redundância não tolera a perda de um membro?
3. Como o espelhamento difere da distribuição?
4. Quando uma gravação em espelho pode ser considerada concluída?
5. Por que uma divergência entre membros precisa ser registrada?
6. Por que espelhamento não substitui backup?

## 6. Distribuição (striping)
Na distribuição, faixas ou blocos são espalhados entre vários membros. Isso pode aumentar paralelismo e capacidade agregada, mas não cria uma cópia completa dos dados. Se um membro necessário falhar, parte do volume pode ficar inacessível.

O tamanho da faixa (stripe/chunk) influencia o mapeamento. O sistema precisa saber em qual membro e posição interna cada LBA lógico está localizado.

## 7. Espelhamento
No espelhamento, os mesmos dados são mantidos em mais de um membro. Uma leitura pode escolher uma cópia válida. Uma gravação precisa coordenar os membros e definir quando o pedido é considerado concluído: depois de todos os membros, depois de um quorum ou segundo outra política explícita.

Uma cópia atrasada ou divergente não pode ser escolhida sem verificar o estado e as garantias.

## 8. Redundância não é backup
Espelhamento pode tolerar a falha de um membro, mas também replica exclusões, corrupção lógica e ataques. Se o usuário remove um arquivo, a remoção pode ser propagada a todas as cópias.

## 9. Exemplo guiado
Em um espelho de dois membros, A conclui a gravação e B falha. O conjunto precisa registrar divergência e entrar em estado degradado ou inconsistente conforme a política. Não deve afirmar que ambas as cópias estão sincronizadas.

## 10. Método de aprendizagem
Compare distribuição e espelhamento em três critérios: capacidade útil, desempenho e tolerância a falhas. Depois simule falha de um membro e identifique quais dados continuam disponíveis.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 60 minutos
