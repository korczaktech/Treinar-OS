# Reforço da Aula 7 — Descritores e Metadados do Dispositivo

## 1. O dispositivo precisa se apresentar

Antes de usar uma unidade, o ZenithOS precisa saber com qual dispositivo está trabalhando e quais operações ele suporta. O descritor é como um cadastro técnico: não contém arquivos, mas informações para usar a unidade corretamente.

## 2. Capacidade

Um dispositivo com 500 blocos possui LBAs de 0 a 499. O LBA 500 está fora do espaço apresentado.

O tamanho em bytes depende do tamanho de cada bloco. Dois dispositivos com a mesma quantidade de blocos podem ter capacidades em bytes diferentes.

## 3. Identificador interno

O ZenithOS pode atribuir um identificador para localizar a entrada no registro de dispositivos. Ele não precisa ser igual ao número de série físico.

Quando a unidade é removida, a referência deve ser invalidada conforme as regras do sistema.

## 4. Dois grupos de metadados

Metadados do dispositivo descrevem a unidade. Metadados do sistema de arquivos descrevem arquivos e diretórios. Saber a capacidade do disco não informa quais arquivos estão nele.

## 5. Não confie cegamente nos valores

Tamanho de bloco zero impede calcular transferências. Capacidade zero não oferece blocos válidos. Identificadores duplicados podem apontar para a unidade errada. Os valores devem ser verificados antes do registro.

## 6. Perguntas de fixação

1. O que o descritor de dispositivo descreve?
2. Quantos blocos existem entre LBA 0 e 499, incluindo ambos?
3. Por que dispositivos com a mesma quantidade de blocos podem ter capacidade em bytes diferente?
4. O número de série precisa ser o identificador interno?
5. O descritor informa os nomes dos arquivos?
6. Por que tamanho de bloco zero deve ser rejeitado?
