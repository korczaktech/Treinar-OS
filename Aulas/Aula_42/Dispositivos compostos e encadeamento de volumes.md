# Dispositivos compostos e encadeamento de volumes

## Objetivo

Nesta aula, você estudará dispositivos compostos e encadeamento de volumes e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Um dispositivo composto apresenta interface própria, mas encaminha operações para dispositivos inferiores. Pode representar uma faixa, concatenação ou camada de transformação.

## 2. Exemplo de funcionamento

O mapeamento valida a faixa na entrada e traduz segmentos para a camada inferior. Pedidos que cruzam fronteiras podem ser divididos. O grafo de dependências não pode conter ciclos.

## 3. Validação e segurança

Propague falhas inferiores e remoções para todos os volumes dependentes. Controle referências e operações pendentes para evitar uso de objetos liberados.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

No ZenithOS, dispositivos compostos declaram dependências e capacidades derivadas. A capacidade publicada nunca excede a região respaldada.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. O que é um dispositivo composto?
2. Qual é a diferença entre concatenação e espelhamento?
3. Como dividir uma requisição que cruza a fronteira entre dois membros?
4. Por que um grafo de dependências não pode conter ciclos?
5. O que acontece com um volume composto quando um membro é removido?
6. Por que a capacidade publicada não pode exceder o espaço respaldado pelos membros?

## 6. Tipos de composição
- **Concatenação:** regiões de dispositivos diferentes são apresentadas em sequência. A capacidade lógica soma as capacidades utilizáveis, mas a falha de um membro pode afetar parte do espaço.
- **Mapeamento de faixa:** uma região lógica é traduzida para uma região inferior.
- **Camada de transformação:** pode criptografar, comprimir ou redirecionar operações, desde que o contrato deixe claro quais capacidades são mantidas.

Composição não implica redundância. Um volume que combina dois discos pode aumentar capacidade sem tolerar falhas.

## 7. Tradução e operações que cruzam fronteiras
Se uma requisição começa perto do fim de uma região e continua na seguinte, a camada composta pode precisar dividi-la. Cada parte é traduzida para o dispositivo inferior correto. A soma deve preservar a faixa original e o resultado precisa agregar falhas.

## 8. Grafo de dependências
Dispositivos compostos formam um grafo: um volume pode depender de outros volumes ou dispositivos. Ciclos precisam ser rejeitados, pois poderiam causar encaminhamento infinito. A remoção de um membro deve propagar indisponibilidade para as camadas dependentes.

## 9. Exemplo guiado
Um volume concatena 1.000 blocos do dispositivo A e 2.000 do B. A faixa lógica 990–1.009 cruza a fronteira: os primeiros 10 blocos vêm de A e os próximos 10 de B. A camada precisa dividir e traduzir os dois segmentos corretamente.

## 10. Método de aprendizagem
Desenhe o volume lógico e suas regiões inferiores. Escolha pedidos que ficam dentro de uma região e pedidos que cruzam fronteiras. Verifique tradução, limites e propagação de falha.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 60 minutos
