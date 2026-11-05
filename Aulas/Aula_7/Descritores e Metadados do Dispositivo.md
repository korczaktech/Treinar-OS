# Descritores e Metadados do Dispositivo

## Objetivo

A camada de armazenamento precisa trabalhar com dispositivos diferentes sem presumir que todos possuem a mesma capacidade ou geometria. Para isso, o ZenithOS mantém informações que descrevem cada unidade. Nesta aula estudaremos descritores e metadados do dispositivo.

Ao final, você deverá explicar o que um descritor representa, distinguir identidade de capacidade e entender como os metadados operacionais são validados.

## 1. Por que descrever o dispositivo?

Imagine duas unidades: uma possui 200 blocos lógicos de 512 bytes; outra possui um milhão de blocos de 4096 bytes. Se o ZenithOS tratar ambas como se tivessem o mesmo tamanho de bloco, fará cálculos errados.

Antes de enviar operações, o sistema precisa conhecer as propriedades que a interface do dispositivo disponibiliza. Essas informações podem ser reunidas em um descritor.

O descritor não contém arquivos. Ele descreve a unidade e suas capacidades operacionais.

## 2. Identidade interna

O sistema precisa distinguir uma unidade das demais. O ZenithOS pode atribuir um identificador interno durante a descoberta.

Esse identificador é uma chave de organização do kernel. Não precisa ser igual ao número de série físico, nome comercial, letra de unidade de outro sistema ou endereço usado pelo controlador.

Dispositivos podem ser removidos. Uma referência antiga não deve continuar sendo considerada válida depois que a unidade deixa de existir.

## 3. Capacidade lógica

A capacidade indica quantos blocos lógicos são apresentados ao sistema. Se há N blocos numerados a partir de zero, os endereços válidos vão de 0 até N-1.

Com 500 blocos:
- primeiro LBA: 0;
- último LBA: 499;
- limite exclusivo: 500.

A capacidade em bytes depende também do tamanho do bloco. Não confunda capacidade lógica apresentada com a quantidade física de células NAND. O controlador pode reservar e gerenciar espaço interno que não é exposto ao sistema.

## 4. Geometria e recursos

Um descritor pode reunir:
- quantidade total de blocos;
- tamanho do bloco lógico;
- limites máximos de transferência;
- requisitos de alinhamento;
- recursos suportados;
- estado operacional;
- identificador interno.

O sistema não deve inventar um tamanho padrão quando uma informação essencial está ausente. Se o tamanho do bloco for zero ou a capacidade for inválida, a unidade não pode ser registrada como operacional.

## 5. Metadados do dispositivo e do arquivo

Metadados do dispositivo descrevem a unidade: capacidade, tamanho de bloco, recursos e estado.

Metadados do sistema de arquivos descrevem arquivos e diretórios: nomes, tamanhos, permissões, datas e referências ao conteúdo.

Saber que um dispositivo possui um milhão de blocos não informa qual arquivo está no LBA 500. Essa relação pertence ao sistema de arquivos.

## 6. Descoberta e registro

Um fluxo conceitual:
1. o mecanismo de inicialização ou barramento identifica um dispositivo;
2. o driver obtém informações da interface;
3. o driver verifica se consegue operar com a unidade;
4. o ZenithOS valida os dados essenciais;
5. a camada registra o descritor;
6. outros componentes passam a solicitar operações pela identificação interna.

Se a descoberta falhar, o sistema não deve criar um descritor funcional com valores inventados.

## 7. Estado e ciclo de vida

Uma unidade pode estar descoberta, inicializada, disponível, ocupada, com falha ou removida. Os estados precisam ter significado e regras de transição.

Uma unidade removida deve deixar de aceitar novas operações. Operações em andamento precisam ser tratadas conforme o contrato do driver e as capacidades do dispositivo.

## 8. Validando informações recebidas

Capacidade zero não permite operações normais. Tamanho de bloco zero impede calcular o tamanho da transferência. Identificador duplicado pode direcionar uma solicitação à unidade errada. Requisito de alinhamento inválido pode tornar buffers incompatíveis.

Informações vindas do hardware ainda precisam ser validadas. A origem do dado não o torna automaticamente seguro.

## 9. Aplicação no ZenithOS

O ZenithOS deverá manter um registro centralizado de dispositivos. Cada entrada representa uma unidade identificada e suas propriedades operacionais. A camada consulta o registro para validar pedidos; o driver continua responsável pela comunicação específica.

Um dispositivo simulado pode ser registrado com capacidade e tamanho conhecidos, permitindo testar a camada sem hardware real.

## 10. Perguntas de compreensão

1. Por que o tamanho do bloco deve ser conhecido para cada dispositivo?
2. Qual é a diferença entre identificador interno e número de série físico?
3. Quais são os LBAs válidos em um dispositivo com 500 blocos?
4. Por que capacidade lógica não equivale necessariamente à quantidade de células NAND?
5. Qual é a diferença entre metadados do dispositivo e metadados do sistema de arquivos?
6. O que fazer se o tamanho de bloco informado for zero?

## 11. Exercício de código

- EXN1A7.nbx — validar se as propriedades de um descritor são consistentes e suficientes para registrar uma unidade operacional.

## Critério de conclusão

Você deve explicar por que o descritor existe, quais informações reúne e como a camada usa esses dados sem confundi-los com os metadados dos arquivos.
