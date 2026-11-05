# Reforço da Aula 91 — Leitura, escrita e truncamento de arquivos: fundamentos, finalidade e limites

## Ideia central

Leitura e escrita operam sobre intervalos de bytes, nem sempre alinhados a blocos. Offset indica posição lógica. Uma operação pode transferir menos bytes que o solicitado e deve informar o resultado real.

## Pontos para memorizar

- Tema: Leitura, escrita e truncamento de arquivos.
- Foco: offset, tamanho, extensão e operações parciais.
- Regra de segurança: validar entradas, limites e referências antes de alterar estado persistente.
- No ZenithOS: separar domínio, persistência e acesso ao dispositivo.

## Exemplo de revisão

Identifique quem possui a informação, quem pode alterá-la e qual camada rejeita um pedido inválido.

## Perguntas de revisão

1. Explique o foco da aula sem consultar o material.
2. Cite dois invariantes e diga quando são verificados.
3. Descreva um caso inválido e o resultado esperado.
4. Relacione o tema com uma camada vizinha do ZenithOS.
5. Proponha um teste que aumentaria sua confiança na implementação.

## Revisão ativa

Feche o material e reconstrua o modelo ou fluxo em uma folha. Compare com a aula, marque as lacunas e refaça apenas os pontos que não conseguiu explicar. Avance quando conseguir justificar decisões, não apenas repetir definições.
