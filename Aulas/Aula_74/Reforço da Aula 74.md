# Reforço da Aula 74 — Mapas de espaço livre: implementação prática no zenithos

## Ideia central

O mapa de espaço livre responde quais unidades podem ser alocadas. Bitmap usa um bit por unidade; listas encadeiam unidades; árvores ou grupos aceleram buscas por intervalos. A escolha depende do tamanho e do padrão de uso.

## Pontos para memorizar

- Tema: Mapas de espaço livre.
- Foco: bitmap, listas livres, busca e atualização.
- Regra de segurança: validar entradas, limites e referências antes de alterar estado persistente.
- No ZenithOS: separar domínio, persistência e acesso ao dispositivo.

## Exemplo de revisão

Comece com bitmap em memória e operações reservar/liberar. Teste índices 0, último bloco e tamanhos não múltiplos de 8. Depois adicione busca por sequências contíguas.

## Perguntas de revisão

1. Explique o foco da aula sem consultar o material.
2. Cite dois invariantes e diga quando são verificados.
3. Descreva um caso inválido e o resultado esperado.
4. Relacione o tema com uma camada vizinha do ZenithOS.
5. Proponha um teste que aumentaria sua confiança na implementação.

## Revisão ativa

Feche o material e reconstrua o modelo ou fluxo em uma folha. Compare com a aula, marque as lacunas e refaça apenas os pontos que não conseguiu explicar. Avance quando conseguir justificar decisões, não apenas repetir definições.
