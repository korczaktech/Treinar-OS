# Reforço da Aula 89 — Criação, abertura e remoção de arquivos: implementação prática no zenithos

## Ideia central

Criar associa nome a objeto; abrir obtém referência operacional; remover elimina associação. Remover nome não precisa destruir conteúdo se ainda houver descritores abertos ou outras referências.

## Pontos para memorizar

- Tema: Criação, abertura e remoção de arquivos.
- Foco: descritores, referências abertas e remoção segura.
- Regra de segurança: validar entradas, limites e referências antes de alterar estado persistente.
- No ZenithOS: separar domínio, persistência e acesso ao dispositivo.

## Exemplo de revisão

Implemente primeiro operações em memória e tabela de descritores. Teste abertura repetida, remoção com arquivo aberto, fechamento duplo e falha entre alocação e inserção.

## Perguntas de revisão

1. Explique o foco da aula sem consultar o material.
2. Cite dois invariantes e diga quando são verificados.
3. Descreva um caso inválido e o resultado esperado.
4. Relacione o tema com uma camada vizinha do ZenithOS.
5. Proponha um teste que aumentaria sua confiança na implementação.

## Revisão ativa

Feche o material e reconstrua o modelo ou fluxo em uma folha. Compare com a aula, marque as lacunas e refaça apenas os pontos que não conseguiu explicar. Avance quando conseguir justificar decisões, não apenas repetir definições.
