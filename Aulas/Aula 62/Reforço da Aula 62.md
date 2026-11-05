# Reforço da Aula 62 — Metadados, atributos e timestamps: estruturas de dados e representação

## Ideia central

Metadados descrevem um objeto sem serem seu conteúdo principal: tipo, tamanho, proprietário, permissões, tempos, referências e localização dos blocos. O formato precisa definir largura, unidade, validade e compatibilidade de cada campo.

## Pontos para memorizar

- Tema: Metadados, atributos e timestamps.
- Foco: identificadores, tamanho, permissões e datas.
- Regra de segurança: validar entradas, limites e referências antes de alterar estado persistente.
- No ZenithOS: separar domínio, persistência e acesso ao dispositivo.

## Exemplo de revisão

Use tipos de largura explícita. Timestamps precisam de época, unidade e precisão documentadas. Campos reservados devem ser inicializados e validados. Não interprete bytes de disco como estrutura nativa sem decodificação.

## Perguntas de revisão

1. Explique o foco da aula sem consultar o material.
2. Cite dois invariantes e diga quando são verificados.
3. Descreva um caso inválido e o resultado esperado.
4. Relacione o tema com uma camada vizinha do ZenithOS.
5. Proponha um teste que aumentaria sua confiança na implementação.

## Revisão ativa

Feche o material e reconstrua o modelo ou fluxo em uma folha. Compare com a aula, marque as lacunas e refaça apenas os pontos que não conseguiu explicar. Avance quando conseguir justificar decisões, não apenas repetir definições.
