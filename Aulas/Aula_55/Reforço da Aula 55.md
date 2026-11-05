# Reforço da Aula 55 — Conceitos e responsabilidades de um sistema de arquivos: falhas, validação e testes

## Ideia central

O sistema de arquivos transforma blocos em objetos nomeados e organiza conteúdo, diretórios e metadados. O dispositivo fornece operações de bloco; o sistema de arquivos define como esses blocos representam objetos persistentes. A montagem conecta uma instância a uma árvore de diretórios, mas não altera por si só o conteúdo físico.

## Pontos para memorizar

- Tema: Conceitos e responsabilidades de um sistema de arquivos.
- Foco: abstração de arquivo, volume, persistência, interface e limites.
- Regra de segurança: validar entradas, limites e referências antes de alterar estado persistente.
- No ZenithOS: separar domínio, persistência e acesso ao dispositivo.

## Exemplo de revisão

Riscos principais: Confundir volume com sistema de arquivos, aceitar metadados não validados, publicar montagem incompleta e misturar política de nomes com I/O.

## Perguntas de revisão

1. Explique o foco da aula sem consultar o material.
2. Cite dois invariantes e diga quando são verificados.
3. Descreva um caso inválido e o resultado esperado.
4. Relacione o tema com uma camada vizinha do ZenithOS.
5. Proponha um teste que aumentaria sua confiança na implementação.

## Revisão ativa

Feche o material e reconstrua o modelo ou fluxo em uma folha. Compare com a aula, marque as lacunas e refaça apenas os pontos que não conseguiu explicar. Avance quando conseguir justificar decisões, não apenas repetir definições.
