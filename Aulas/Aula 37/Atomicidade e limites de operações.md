# Atomicidade e limites de operações

## Objetivo

Nesta aula, você estudará atomicidade e limites de operações e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Atomicidade significa que uma atualização é observada como unidade indivisível segundo um contrato. Não é sinônimo de durabilidade: uma operação pode ser atômica durante execução e ainda não estar persistida após falta de energia.

## 2. Exemplo de funcionamento

Dispositivos podem anunciar limites de escrita atômica, com tamanho, alinhamento e condições específicas. Sem garantia explícita, uma gravação que cruza setores pode ser parcialmente aplicada.

## 3. Validação e segurança

Journal, copy-on-write e ordenação são mecanismos usados por sistemas de arquivos para consistência. Flush ordena persistência conforme contrato, mas não transforma várias gravações em uma transação indivisível.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve separar conclusão, atomicidade e durabilidade nas interfaces. Quando o hardware não garante atomicidade suficiente, a camada superior usa mecanismo próprio.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Qual é a diferença entre atomicidade e durabilidade?
2. Uma gravação de 8 KiB é automaticamente atômica se o dispositivo garante atomicidade de 4 KiB?
3. Por que flush não transforma várias gravações em uma transação indivisível?
4. Qual é o papel de journal ou copy-on-write quando o hardware não oferece atomicidade suficiente?
5. Como distinguir conclusão, consistência e persistência?
6. Por que o ZenithOS deve consultar os limites de atomicidade anunciados?

## 6. Atomicidade, consistência e durabilidade
Esses três conceitos não são sinônimos:
- **Atomicidade:** a operação é observada como uma unidade conforme o contrato; não aparece parcialmente aplicada.
- **Consistência:** as regras e invariantes do formato continuam verdadeiras.
- **Durabilidade:** depois da confirmação definida pelo contrato, a alteração sobrevive às falhas cobertas pela garantia.

Uma gravação pode ser atômica, mas ainda estar em cache volátil e não ser durável. Uma sequência de várias gravações pode ser durável individualmente e ainda deixar estruturas inconsistentes se a ordem estiver errada.

## 7. Limites de atomicidade
O dispositivo pode anunciar limites de escrita atômica, tamanho máximo, alinhamento e condições específicas. Essas garantias normalmente se aplicam a determinadas unidades e circunstâncias, não a qualquer sequência arbitrária de comandos.

Sem garantia explícita, o kernel deve considerar que uma gravação pode ser interrompida parcialmente.

## 8. Exemplo guiado
Um sistema precisa atualizar um registro de 8 KiB, mas o dispositivo só garante atomicidade de 4 KiB sob alinhamento específico. Não é correto assumir que duas gravações de 4 KiB formam automaticamente uma operação atômica de 8 KiB. A camada superior precisa de journal, copy-on-write ou outro mecanismo para preservar consistência.

## 9. Método de aprendizagem
Para cada cenário, pergunte: a operação pode aparecer parcialmente? as invariantes continuam válidas? a alteração sobrevive à falta de energia? Responda separadamente.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
