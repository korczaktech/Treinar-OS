# Reforço da Aula 161 — Criação e encerramento de processos

## Ideia central

Entender como recursos são preparados para uma nova execução e como são recolhidos com segurança ao finalizar. O ponto que você precisa guardar é que o componente deve operar dentro de limites explícitos e manter seus invariantes mesmo quando a entrada ou a operação falhar.

## Revisão dos conceitos

alocação de PID; descritor; espaço virtual; herança ou criação de recursos; falha parcial; rollback; código de saída; limpeza; processo órfão/zumbi conforme modelo.

## Exemplo comentado

Se a criação reservou PID e espaço virtual, mas falhou ao carregar o executável, deve desfazer as reservas antes de devolver erro e não deixar um processo incompleto visível ao escalonador.

Ao resolver um cenário semelhante, siga esta ordem: identifique entradas e unidades; confira limites e permissões; represente o estado antes da operação; execute a transformação; confira o estado depois; só então aceite o resultado.

## Pontos que merecem atenção

- **Responsabilidade:** usar criação transacional ou rollback por etapas; tornar a publicação o ponto de visibilidade; impedir vazamento quando qualquer fase falhar
- **Fluxo:** validar pedido; reservar identidade; alocar estruturas; criar espaço; carregar imagem; montar contexto; publicar processo apenas quando consistente; no término recolher recursos
- **Riscos:** processo parcialmente publicado; PID perdido; memória não liberada; recurso fechado duas vezes; referência pendente; término enquanto outro componente ainda usa o processo
- **Validação:** falha em cada etapa; criação completa; encerramento normal; limpeza repetida; PID reutilizado; referência pendente

## Perguntas para revisão ativa

1. Qual problema este componente resolve no sistema operacional?
2. Quais responsabilidades pertencem a ele e quais pertencem a outro subsistema?
3. Que premissas precisam ser verdadeiras para seu funcionamento?
4. Quais limites de hardware, memória ou privilégio afetam a solução?
5. O que deve acontecer quando o recurso solicitado não existe?
6. Que risco aparece se o kernel confiar cegamente nos dados recebidos?

## Exercício rápido de recuperação

Sem olhar a aula principal, desenhe um diagrama conceitual que mostre entradas, saídas, responsabilidades e limites do componente. Depois compare seu desenho com as estruturas, fluxo e invariantes descritos na aula. Corrija o que estiver incompleto e explique em voz alta por que cada etapa existe.

## Quando revisar novamente

Faça uma revisão curta no dia seguinte e outra alguns dias depois. Em cada revisão, tente reconstruir o fluxo sem reler o texto primeiro. Consulte o material apenas para corrigir lacunas.
