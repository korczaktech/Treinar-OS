# Reforço da Aula 58 — Arquivos, diretórios e caminhos: funcionamento interno e fluxo de execução

## Ideia central

Arquivo é um objeto que guarda dados ou representa um recurso; diretório associa nomes a objetos. Um caminho é uma sequência de componentes usada para atravessar essa hierarquia. O nome visível não precisa ser a identidade interna.

## Pontos para memorizar

- Tema: Arquivos, diretórios e caminhos.
- Foco: nomes, hierarquia, caminhos absolutos e relativos.
- Regra de segurança: validar entradas, limites e referências antes de alterar estado persistente.
- No ZenithOS: separar domínio, persistência e acesso ao dispositivo.

## Exemplo de revisão

Divida o caminho em componentes; escolha raiz ou diretório inicial; procure cada nome; confirme que componentes intermediários são diretórios; trate . e ..; aplique pontos de montagem; retorne objeto ou erro.

## Perguntas de revisão

1. Explique o foco da aula sem consultar o material.
2. Cite dois invariantes e diga quando são verificados.
3. Descreva um caso inválido e o resultado esperado.
4. Relacione o tema com uma camada vizinha do ZenithOS.
5. Proponha um teste que aumentaria sua confiança na implementação.

## Revisão ativa

Feche o material e reconstrua o modelo ou fluxo em uma folha. Compare com a aula, marque as lacunas e refaça apenas os pontos que não conseguiu explicar. Avance quando conseguir justificar decisões, não apenas repetir definições.
