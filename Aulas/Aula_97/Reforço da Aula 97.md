# Reforço da Aula 97 — Links, referências e montagem: estruturas de dados e representação

## Ideia central

Hard links criam mais de um nome para a mesma identidade; links simbólicos guardam caminho a resolver. Montagem conecta árvore de diretórios a outra instância. Essas relações afetam resolução, ciclo de vida e segurança.

## Pontos para memorizar

- Tema: Links, referências e montagem.
- Foco: hard links, links simbólicos, pontos de montagem e desmontagem.
- Regra de segurança: validar entradas, limites e referências antes de alterar estado persistente.
- No ZenithOS: separar domínio, persistência e acesso ao dispositivo.

## Exemplo de revisão

Hard link aponta ao mesmo inode e altera contagem de links. Link simbólico é objeto cujo conteúdo representa destino. Ponto de montagem associa diretório de cobertura à raiz montada.

## Perguntas de revisão

1. Explique o foco da aula sem consultar o material.
2. Cite dois invariantes e diga quando são verificados.
3. Descreva um caso inválido e o resultado esperado.
4. Relacione o tema com uma camada vizinha do ZenithOS.
5. Proponha um teste que aumentaria sua confiança na implementação.

## Revisão ativa

Feche o material e reconstrua o modelo ou fluxo em uma folha. Compare com a aula, marque as lacunas e refaça apenas os pontos que não conseguiu explicar. Avance quando conseguir justificar decisões, não apenas repetir definições.
