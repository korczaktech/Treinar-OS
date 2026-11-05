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

1. Qual problema esta aula procura resolver?
2. Quais informações precisam ser conhecidas antes de executar a operação estudada?
3. Que dado inválido poderia causar acesso fora dos limites ou perda de consistência?
4. Qual responsabilidade pertence ao ZenithOS e qual pertence ao driver?
5. Que teste automatizado ajudaria a detectar uma implementação incorreta?

## 6. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 60 minutos
