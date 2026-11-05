# Níveis RAID e tolerância a falhas

## Objetivo

Nesta aula, você estudará níveis raid e tolerância a falhas e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

RAID 0 distribui sem redundância; RAID 1 espelha; RAID 5 usa paridade simples; RAID 6 usa paridade dupla; RAID 10 combina espelhamento e distribuição.

## 2. Exemplo de funcionamento

Para N discos iguais de capacidade C: RAID 0 ≈ N×C; RAID 5 ≈ (N−1)×C; RAID 6 ≈ (N−2)×C; RAID 10 ≈ (N/2)×C. RAID 1 de dois membros oferece aproximadamente C de capacidade útil.

## 3. Validação e segurança

RAID 5 tolera uma falha de membro e RAID 6 duas, sob suas hipóteses. RAID 10 pode tolerar várias falhas se não atingirem o mesmo par espelhado. RAID não protege contra exclusão acidental.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve definir nível, geometria, estado e política de reconstrução. Deve rejeitar conjuntos incompletos e comunicar a tolerância real.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Qual é a diferença entre RAID 0 e RAID 1?
2. Quantas falhas de membro RAID 5 e RAID 6 toleram sob suas hipóteses?
3. Quatro discos de 2 TB oferecem aproximadamente quanto de capacidade útil em RAID 5?
4. Por que RAID 10 pode tolerar mais de uma falha em alguns cenários, mas não em todos?
5. Por que RAID não substitui backup?
6. Qual informação precisa ser conhecida para determinar se um conjunto RAID ainda consegue operar?

## 6. Comparação das estratégias
- **RAID 0:** distribui dados; oferece capacidade agregada e paralelismo, mas não tolera falha de membro.
- **RAID 1:** mantém cópias espelhadas; capacidade útil aproximada de um membro em um espelho de dois discos.
- **RAID 5:** distribui dados e paridade; tolera uma falha de membro, mas reconstruções podem ser intensas.
- **RAID 6:** usa paridade dupla; tolera duas falhas de membro dentro das hipóteses do conjunto.
- **RAID 10:** combina espelhamento e distribuição; tolerância depende de quais membros falham em cada par.

## 7. Capacidade útil
Para N discos iguais de capacidade C, RAID 0 oferece aproximadamente N×C; RAID 5, (N−1)×C; RAID 6, (N−2)×C; RAID 10, aproximadamente (N/2)×C quando N é par e os pares são espelhados. RAID 1 com dois membros oferece aproximadamente C. Metadados, reservas e diferenças de capacidade podem reduzir os valores efetivos.

## 8. Paridade em termos simples
A paridade é informação adicional calculada a partir dos dados. Em RAID 5, uma paridade distribuída permite reconstruir os dados de um membro ausente, sob as hipóteses do nível. RAID 6 mantém informação suficiente para tolerar duas falhas. O cálculo e a distribuição exatos precisam seguir a geometria do nível.

## 9. Exemplo guiado
Quatro discos de 2 TB: RAID 0 ≈ 8 TB; RAID 5 ≈ 6 TB; RAID 6 ≈ 4 TB; RAID 10 ≈ 4 TB. Os valores são aproximados e não significam que todos os níveis ofereçam a mesma tolerância ou desempenho.

## 10. Método de aprendizagem
Para cada nível, desenhe onde ficam dados, cópias ou paridade. Em seguida retire um membro hipotético e verifique se os dados podem ser reconstruídos. Não memorize apenas a fórmula de capacidade.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 60 minutos
