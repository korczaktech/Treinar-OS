# Leitura e escrita parcial de blocos

## Objetivo

Nesta aula, você estudará leitura e escrita parcial de blocos e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

A interface de blocos normalmente transfere setores completos, mas arquivos e aplicações podem alterar poucos bytes. A camada superior localiza o setor, lê, modifica a região e grava o setor completo quando não há escrita parcial nativa.

## 2. Exemplo de funcionamento

Para offset em bytes, a divisão pelo tamanho do setor fornece LBA relativo e resto interno. Uma operação pode atravessar vários setores e exige tratar o primeiro, os intermediários e o último.

## 3. Validação e segurança

Leitura-modificação-escrita pode perder atualizações concorrentes se duas operações alterarem regiões diferentes do mesmo setor. Falhas entre leitura e gravação também precisam de política explícita.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

No ZenithOS, operações parciais ficam acima da interface de blocos. Locks ou serialização protegem setores compartilhados quando a camada promete consistência.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Como encontrar o LBA relativo a partir de um offset em bytes?
2. O que representa o resto da divisão pelo tamanho do setor?
3. Com setores de 512 bytes, em qual LBA relativo está o offset 1.300 e qual é o deslocamento interno?
4. Uma alteração de 20 bytes começa no offset 500. Quantos bytes afetam o primeiro e o segundo setor?
5. Por que leitura-modificação-escrita pode perder atualizações concorrentes?
6. Por que a gravação parcial não deve ser considerada automaticamente atômica?

## 6. Converter offset em LBA e deslocamento interno
Para uma posição em bytes, divida o offset pelo tamanho do setor lógico. O quociente indica o LBA relativo e o resto indica a posição dentro do setor.

Exemplo: setor lógico de 512 bytes e offset 1.300:
- 1.300 / 512 = 2, com resto 276;
- LBA relativo = 2;
- deslocamento interno = 276 bytes.

Se a operação atravessar o fim do setor, será necessário acessar o próximo LBA.

## 7. Leitura-modificação-escrita
Quando o dispositivo só aceita setores completos, uma gravação parcial pode exigir ler o setor, modificar os bytes desejados e gravar o setor inteiro. Essa sequência não é automaticamente atômica.

Se duas threads modificarem regiões diferentes do mesmo setor ao mesmo tempo, uma gravação pode sobrescrever a alteração da outra. A camada precisa serializar ou coordenar operações que compartilham o setor.

## 8. Exemplo guiado
Alterar 20 bytes a partir do offset 500 em um setor de 512 bytes afeta 12 bytes do primeiro setor e 8 bytes do seguinte. A implementação precisa ler e preservar as partes não alteradas de ambos os setores.

## 9. Método de aprendizagem
Divida a operação em três partes: bytes antes da região alterada, bytes modificados e bytes depois. Marque em quais setores cada parte está localizada e determine quais leituras e gravações são necessárias.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
