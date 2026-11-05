# Reforço da Aula 80 — Inodes e identificação de arquivos: falhas, validação e testes

## Ideia central

Em sistemas no estilo Unix, inode representa identidade e metadados; nomes ficam em entradas de diretório. Um inode pode ter vários nomes e seu identificador pode ser reutilizado depois da liberação.

## Pontos para memorizar

- Tema: Inodes e identificação de arquivos.
- Foco: números de inode, referências e atributos.
- Regra de segurança: validar entradas, limites e referências antes de alterar estado persistente.
- No ZenithOS: separar domínio, persistência e acesso ao dispositivo.

## Exemplo de revisão

Riscos principais: Reutilização prematura, contagem negativa, inode órfão, ponteiro de bloco corrompido e inconsistência entre diretório e inode.

## Perguntas de revisão

1. Explique o foco da aula sem consultar o material.
2. Cite dois invariantes e diga quando são verificados.
3. Descreva um caso inválido e o resultado esperado.
4. Relacione o tema com uma camada vizinha do ZenithOS.
5. Proponha um teste que aumentaria sua confiança na implementação.

## Revisão ativa

Feche o material e reconstrua o modelo ou fluxo em uma folha. Compare com a aula, marque as lacunas e refaça apenas os pontos que não conseguiu explicar. Avance quando conseguir justificar decisões, não apenas repetir definições.
