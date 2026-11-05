# Reforço da Aula 132 — TLB e tradução de endereços

## Ideia central

Explicar o cache de traduções do processador e manter coerência quando o kernel altera mapeamentos. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

Translation Lookaside Buffer; hit/miss; page walk; contexto de endereço; ASID/PCID quando suportado; invalidação local e remota; custo de flush.

## Exemplo comentado

Se virtual X apontava para quadro A e passa a apontar para quadro B, uma entrada antiga no TLB pode continuar direcionando acessos para A até a invalidação apropriada.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** centralizar mudanças de mapeamento; escolher invalidação específica ou ampla conforme arquitetura; considerar CPUs múltiplas e identificadores de contexto
- **Fluxo:** acesso consulta TLB; em miss percorre tabelas; registra tradução; alteração de mapeamento atualiza tabelas e invalida entradas relevantes antes de reutilizar recursos
- **Riscos:** usar tradução antiga após liberar quadro; invalidar apenas uma CPU; confundir flush de cache de dados com TLB; assumir que toda arquitetura oferece ASID
- **Validação:** hit; miss; substituição; alteração de mapeamento; invalidação de uma página; troca de contexto; quadro liberado; múltiplos processadores simulados

## Perguntas para revisão ativa

1. Quais estruturas representam o componente?
2. Qual é a unidade de cada campo: bytes, páginas, identificadores ou estados?
3. Quais campos podem ser derivados e quais precisam ser armazenados?
4. Como representar ausência, erro e recurso reservado?
5. Quais invariantes devem permanecer verdadeiros?
6. Como evitar overflow, duplicidade e referências pendentes?

## Exercício rápido de recuperação

Sem olhar a aula principal, desenhe um modelo de dados anotado com campos, unidades, invariantes e estados inválidos. Depois compare seu desenho com as estruturas, fluxo e invariantes descritos na aula. Corrija o que estiver incompleto e explique em voz alta por que cada etapa existe.

## Quando revisar novamente

Faça uma revisão curta no dia seguinte e outra alguns dias depois. Em cada revisão, tente reconstruir o fluxo sem reler o texto primeiro. Consulte o material apenas para corrigir lacunas.
