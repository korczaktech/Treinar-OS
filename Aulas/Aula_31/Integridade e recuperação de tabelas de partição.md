# Integridade e recuperação de tabelas de partição

## Objetivo

Nesta aula, você estudará integridade e recuperação de tabelas de partição e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Tabelas podem ser corrompidas por desligamento, falha de gravação, defeito ou ferramenta incorreta. GPT possui cópias principal e de backup e CRCs; MBR clássico não oferece a mesma redundância.

## 2. Exemplo de funcionamento

O diagnóstico verifica cada cópia, compara posições e entradas e identifica divergências. Uma cópia válida pode estar desatualizada; não basta escolher automaticamente a que passou no CRC.

## 3. Validação e segurança

CRC não prova autenticidade. Reparar modifica dados persistentes: preserve uma imagem quando possível, explique a origem dos dados recuperados e não invente entradas quando não houver evidência suficiente.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

A primeira versão do ZenithOS deve diagnosticar sem reparar. Um futuro reparador deverá ser explícito, gerar plano verificável e exigir autorização antes de escrever.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Quais estruturas redundantes a GPT mantém?
2. Por que passar no CRC não garante que uma tabela seja semanticamente válida?
3. Por que não é seguro escolher automaticamente a primeira cópia que passa no CRC?
4. Qual é a limitação do MBR clássico em comparação à GPT para recuperação?
5. Quais passos devem ocorrer antes de gravar uma tabela recuperada?
6. Por que a primeira versão do ZenithOS pode preferir diagnosticar sem reparar?

## 6. Diagnóstico das cópias GPT
A GPT mantém estruturas principal e de backup. O diagnóstico deve ler cada cópia separadamente, validar seus cabeçalhos, posições, dimensões e CRCs e comparar os resultados. Uma cópia pode passar no CRC e ainda conter entradas que não fazem sentido para o dispositivo.

O parser também precisa confirmar que a localização declarada para o backup corresponde à região esperada e que as partições cabem no disco.

## 7. Por que não escolher automaticamente?
Imagine que a cópia principal esteja íntegra, mas antiga, enquanto a cópia de backup foi atualizada e também está íntegra. Escolher a primeira cópia válida pode descartar alterações legítimas. A decisão exige comparar campos, posições e contexto do dano.

No MBR clássico, não existe uma cópia redundante equivalente da tabela principal. A recuperação pode depender de backup externo, imagem anterior ou reconstrução manual com evidências.

## 8. Processo de recuperação conservador
1. interromper operações que possam sobrescrever a região danificada;
2. coletar diagnóstico e preservar os dados disponíveis;
3. validar todas as cópias candidatas;
4. comparar consistência e contexto;
5. apresentar a origem e as consequências da recuperação;
6. só escrever após uma decisão explícita e plano verificável;
7. verificar novamente a estrutura após a gravação.

## 9. Exemplo guiado
Se a GPT principal falhar no CRC e a cópia de backup passar nas verificações, o sistema pode indicar que existe uma fonte candidata para recuperação. Isso não autoriza reparo silencioso. O usuário ou política administrativa deve aprovar a escrita e o sistema deve preservar evidências quando possível.

## 10. Método de aprendizagem
Separe três resultados: estrutura válida, estrutura inválida e estrutura recuperável com evidência. “Recuperável” não é sinônimo de “já reparada”.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
