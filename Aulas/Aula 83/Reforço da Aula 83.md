# Reforço da Aula 83 — Índices e busca em diretórios: funcionamento interno e fluxo de execução

## Ideia central

Diretório precisa localizar entrada pelo nome. Lista simples é fácil, mas busca cresce linearmente. Hash tables e árvores aceleram consultas, porém exigem regras de colisão, atualização e recuperação.

## Pontos para memorizar

- Tema: Índices e busca em diretórios.
- Foco: árvores, hashing, colisões e ordenação.
- Regra de segurança: validar entradas, limites e referências antes de alterar estado persistente.
- No ZenithOS: separar domínio, persistência e acesso ao dispositivo.

## Exemplo de revisão

Normalize nome; calcule chave/hash; procure candidatos; compare nome completo; valide referência; ao inserir, verifique duplicidade e atualize índice e dados de forma consistente.

## Perguntas de revisão

1. Explique o foco da aula sem consultar o material.
2. Cite dois invariantes e diga quando são verificados.
3. Descreva um caso inválido e o resultado esperado.
4. Relacione o tema com uma camada vizinha do ZenithOS.
5. Proponha um teste que aumentaria sua confiança na implementação.

## Revisão ativa

Feche o material e reconstrua o modelo ou fluxo em uma folha. Compare com a aula, marque as lacunas e refaça apenas os pontos que não conseguiu explicar. Avance quando conseguir justificar decisões, não apenas repetir definições.
