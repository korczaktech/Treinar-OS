# Reforço da Aula 46 — Falhas parciais e degradação RAID

## Estado degradado
O conjunto perdeu um membro ou parte da redundância, mas ainda pode oferecer algumas operações. Não deve ser apresentado como saudável.

## Exemplo
Em um espelho, A responde e B falha. Leituras podem continuar em A, mas B precisa ser marcado como indisponível ou desatualizado. Se voltar, não é automaticamente confiável: precisa de verificação ou reconstrução.

## Escrita parcial
Se alguns membros concluírem e outros falharem, registre o resultado de cada membro. Não declare sincronização completa. Erros silenciosos também podem exigir checksums ou comparação de cópias/paridade.

## Perguntas
1. O que significa RAID degradado?
2. Por que uma gravação parcial exige registrar cada membro?
3. Como tratar um membro que voltou a responder?
4. O que é erro silencioso?
5. Por que o estado degradado aumenta o risco de perda?
