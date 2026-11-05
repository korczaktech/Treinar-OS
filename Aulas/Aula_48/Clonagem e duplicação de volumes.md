# Clonagem e duplicação de volumes

## Objetivo

Nesta aula, você estudará clonagem e duplicação de volumes e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

Cópia física transfere blocos; clone lógico pode compartilhar dados e copiar somente quando houver alteração. Clonar um volume não é igual a copiar arquivos, pois pode incluir metadados e espaço não alocado.

## 2. Exemplo de funcionamento

Antes da cópia, valide capacidade, tamanho de bloco, sobreposição e estado. Origem ativa pode mudar durante a operação; consistência exige snapshot, congelamento ou coordenação.

## 3. Validação e segurança

Duplicar identificadores únicos pode gerar conflito quando origem e clone ficam conectados simultaneamente. Interrupção deve deixar destino marcado como incompleto, não como volume válido.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve distinguir cópia bruta, clone consistente e clone copy-on-write. Publique destino somente após validação final.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Qual problema esta aula procura resolver?
2. Quais informações precisam ser conhecidas antes de executar a operação estudada?
3. Que dado inválido poderia causar acesso fora dos limites ou perda de consistência?
4. Qual responsabilidade pertence ao ZenithOS e qual pertence ao driver?
5. Que teste automatizado ajudaria a detectar uma implementação incorreta?

## 6. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 65 minutos
