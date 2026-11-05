# Reforço da Aula 59 — Arquivos, diretórios e caminhos: implementação prática no zenithos

## Ideia central

Arquivo é um objeto que guarda dados ou representa um recurso; diretório associa nomes a objetos. Um caminho é uma sequência de componentes usada para atravessar essa hierarquia. O nome visível não precisa ser a identidade interna.

## Pontos para memorizar

- Tema: Arquivos, diretórios e caminhos.
- Foco: nomes, hierarquia, caminhos absolutos e relativos.
- Regra de segurança: validar entradas, limites e referências antes de alterar estado persistente.
- No ZenithOS: separar domínio, persistência e acesso ao dispositivo.

## Exemplo de revisão

Defina regras de normalização e comparação antes de persistir diretórios. Implemente resolução em memória. Evite tratar concatenação de strings como resolução de caminhos.

## Perguntas de revisão

1. Explique o foco da aula sem consultar o material.
2. Cite dois invariantes e diga quando são verificados.
3. Descreva um caso inválido e o resultado esperado.
4. Relacione o tema com uma camada vizinha do ZenithOS.
5. Proponha um teste que aumentaria sua confiança na implementação.

## Revisão ativa

Feche o material e reconstrua o modelo ou fluxo em uma folha. Compare com a aula, marque as lacunas e refaça apenas os pontos que não conseguiu explicar. Avance quando conseguir justificar decisões, não apenas repetir definições.
