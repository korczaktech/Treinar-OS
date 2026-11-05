# Reforço da Aula 25 — Descoberta e identificação de dispositivos

## 1. Descoberta não é prontidão
Encontrar um dispositivo no barramento não significa que o driver já o inicializou. O sistema precisa identificar a interface, associar um driver, inicializar recursos e consultar capacidades.

## 2. Identidade
Endereço de barramento descreve uma localização de conexão. Identificador interno é a referência usada pelo ZenithOS. Número de série pode ajudar, mas não deve ser a única proteção contra referências obsoletas.

## 3. Exemplo de remoção e reconexão
Uma unidade é registrada e recebe uma identidade interna. Depois é removida. O sistema marca a referência como indisponível e trata pedidos pendentes. Outra unidade pode ocupar o mesmo endereço de barramento, mas não deve herdar os pedidos antigos.

## 4. Registro
Guarde identidade, estado, capacidades, tamanho lógico e driver responsável. Valide os valores antes de permitir operações.

## 5. Perguntas de revisão
1. Quais etapas existem entre descoberta e estado operacional?
2. Por que o endereço de barramento pode mudar?
3. Que risco existe em reutilizar uma referência antiga?
4. Quais capacidades devem ser consultadas?
5. Como o sistema deve reagir à remoção durante uma operação?
