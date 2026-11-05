# Reforço da Aula 21 — Arquitetura Integrada

## 1. Cada camada tem uma responsabilidade

O sistema de arquivos organiza arquivos. Partições delimitam regiões. O cache mantém cópias. A camada de blocos valida operações. Drivers conhecem interfaces específicas. O controlador e o dispositivo executam transferências.

## 2. Leitura em sequência

O sistema de arquivos localiza os blocos; o cache verifica se já possui os dados; a camada de blocos valida o pedido; o driver prepara a operação; o dispositivo transfere; a conclusão retorna até o solicitante.

## 3. Gravação e persistência

Uma gravação pode atualizar dados e metadados. A ordem importa. Cache, flush e barreiras precisam respeitar o contrato de durabilidade.

## 4. Contratos

Toda interface deve definir parâmetros, unidades, limites, buffer, estados, erros, cancelamento e garantias.

## 5. Testes progressivos

Comece com funções puras, avance para dispositivo em RAM, simule falhas, teste integração e só então valide em hardware real.

## 6. Invariantes

Nenhuma faixa fora dos limites; nenhum buffer usado depois de liberado; nenhuma entrada suja descartada silenciosamente; nenhuma falha convertida em sucesso; nenhuma partição sobreposta indevidamente.

## 7. Fixação

1. Qual camada organiza arquivos?
2. Qual camada conversa com o protocolo específico do dispositivo?
3. Por que o dispositivo em RAM é útil?
4. Cite três regras que devem ser verificadas automaticamente.
5. Por que uma gravação concluída não significa sempre que os dados estão persistidos?
6. O que o ZBL precisa fazer antes de o kernel assumir o controle?
