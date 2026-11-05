# Reforço da Aula 70 — Alocação de espaço em disco: falhas, validação e testes

## Ideia central

O sistema de arquivos relaciona o espaço lógico de um arquivo às regiões físicas do volume. Alocação contígua favorece leitura sequencial; encadeada facilita crescimento, mas pode exigir várias leituras; indexada usa estruturas intermediárias para localizar extensões.

## Pontos para memorizar

- Tema: Alocação de espaço em disco.
- Foco: alocação contígua, encadeada e indexada.
- Regra de segurança: validar entradas, limites e referências antes de alterar estado persistente.
- No ZenithOS: separar domínio, persistência e acesso ao dispositivo.

## Exemplo de revisão

Riscos principais: Dupla alocação, vazamento de blocos, extensão fora do volume, fragmentação, overflow e metadados divergentes.

## Perguntas de revisão

1. Explique o foco da aula sem consultar o material.
2. Cite dois invariantes e diga quando são verificados.
3. Descreva um caso inválido e o resultado esperado.
4. Relacione o tema com uma camada vizinha do ZenithOS.
5. Proponha um teste que aumentaria sua confiança na implementação.

## Revisão ativa

Feche o material e reconstrua o modelo ou fluxo em uma folha. Compare com a aula, marque as lacunas e refaça apenas os pontos que não conseguiu explicar. Avance quando conseguir justificar decisões, não apenas repetir definições.
