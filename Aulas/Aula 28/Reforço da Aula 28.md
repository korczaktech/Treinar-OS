# Reforço da Aula 28 — Montagem e desmontagem de volumes

## Montagem
Identifique o formato, valide metadados, prepare estruturas em memória e publique o ponto de montagem somente quando estiver consistente. Um volume que falhou na validação não deve aparecer parcialmente montado.

## Desmontagem
Impeça novas operações, trate referências abertas, conclua ou cancele operações conforme o contrato, sincronize dados quando possível e só então libere estruturas. Se o dispositivo foi removido, a persistência pode não ser possível.

## Exemplo
Um arquivo está aberto e possui gravação pendente. Liberar imediatamente o volume deixaria referências apontando para objetos inválidos. A desmontagem precisa coordenar o ciclo de vida desses recursos.

## Perguntas
1. Por que a montagem precisa validar metadados?
2. O que impede uma desmontagem normal?
3. Qual o risco de liberar estruturas com I/O pendente?
4. O que muda quando o dispositivo é removido inesperadamente?
5. Por que desmontagem forçada não garante persistência?
