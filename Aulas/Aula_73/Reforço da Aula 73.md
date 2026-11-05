# Reforço da Aula 73 — Mapas de espaço livre: funcionamento interno e fluxo de execução

## Ideia central

O mapa de espaço livre responde quais unidades podem ser alocadas. Bitmap usa um bit por unidade; listas encadeiam unidades; árvores ou grupos aceleram buscas por intervalos. A escolha depende do tamanho e do padrão de uso.

## Pontos para memorizar

- Tema: Mapas de espaço livre.
- Foco: bitmap, listas livres, busca e atualização.
- Regra de segurança: validar entradas, limites e referências antes de alterar estado persistente.
- No ZenithOS: separar domínio, persistência e acesso ao dispositivo.

## Exemplo de revisão

Localize candidatos; valide faixa; marque reserva; atualize contadores; persista metadados; ao liberar, confirme pertencimento ao volume e que o bloco ainda está ocupado.

## Perguntas de revisão

1. Explique o foco da aula sem consultar o material.
2. Cite dois invariantes e diga quando são verificados.
3. Descreva um caso inválido e o resultado esperado.
4. Relacione o tema com uma camada vizinha do ZenithOS.
5. Proponha um teste que aumentaria sua confiança na implementação.

## Revisão ativa

Feche o material e reconstrua o modelo ou fluxo em uma folha. Compare com a aula, marque as lacunas e refaça apenas os pontos que não conseguiu explicar. Avance quando conseguir justificar decisões, não apenas repetir definições.
