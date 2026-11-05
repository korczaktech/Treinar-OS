# Blocos Defeituosos, Saúde e Confiabilidade

## Objetivo

Dispositivos de armazenamento podem apresentar erros permanentes ou temporários. Em SSDs, o controlador gerencia blocos NAND defeituosos e pode remapear endereços. Nesta aula vamos distinguir erros reportados ao host, remapeamento interno, indicadores de saúde e limites do diagnóstico.

## 1. O que é um bloco defeituoso?

É uma região que não pode ser usada de forma confiável segundo os critérios do dispositivo. Em mídia magnética, podem existir setores problemáticos. Em NAND, blocos podem ser considerados defeituosos desde a fabricação ou tornar-se inadequados durante o uso.

O host nem sempre enxerga a unidade física defeituosa. O controlador pode ocultá-la por remapeamento.

## 2. Remapeamento

Quando uma região interna não é mais confiável, o controlador pode substituir seu uso por outra região disponível e atualizar o mapeamento lógico-físico.

Esse processo é interno ao dispositivo. O sistema operacional continua usando os LBAs apresentados, salvo quando o dispositivo reporta erro ou alteração de capacidade.

## 3. Erro irrecuperável

Se o dispositivo não consegue ler um bloco e não possui cópia recuperável, pode reportar erro ao host. O sistema operacional deve propagar o erro corretamente e evitar fingir que os dados foram lidos com sucesso.

Dados não recuperáveis exigem restauração a partir de backup ou outra fonte válida.

## 4. Indicadores de saúde

Alguns dispositivos oferecem atributos de saúde, contadores de erros, temperatura, tempo ligado, desgaste estimado e alertas. Os campos variam por protocolo e fabricante.

Não trate um único número como previsão exata de falha. Indicadores ajudam a avaliar tendências, mas não garantem que o dispositivo continuará funcionando.

## 5. Monitoramento e política

O sistema pode registrar alertas, avisar o usuário, reduzir operações arriscadas ou recomendar substituição. A política deve distinguir aviso preventivo de falha confirmada.

Evite monitoramento que gere gravações excessivas ou consultas contínuas sem necessidade.

## 6. Integridade dos dados

Um dispositivo saudável ainda pode perder dados por falhas de software, energia, controlador ou erro humano. Saúde do hardware não substitui checksum, verificação de consistência e backup.

Da mesma forma, um checksum correto não prova que o hardware não vai falhar amanhã.

## 7. Aplicação no ZenithOS

O driver deve traduzir códigos do dispositivo em erros compreensíveis. O serviço de monitoramento reúne indicadores sem assumir que são universais. A camada de armazenamento propaga falhas de leitura e gravação sem converter erro em sucesso.

## 8. Perguntas de compreensão

1. O host sempre enxerga um bloco NAND defeituoso?
2. O que é remapeamento?
3. Como o sistema deve tratar uma leitura irrecuperável?
4. Indicadores de saúde garantem previsão de falha?
5. Por que dispositivo saudável não substitui backup?
6. Qual a diferença entre alerta preventivo e falha confirmada?

## 9. Exercícios de código

- EXN1A18.nbx — traduzir códigos de erro de dispositivo em categorias do sistema.
- EXN2A18.nbx — interpretar indicadores fictícios de saúde sem produzir previsões absolutas.


## Método de estudo e exemplo guiado
Considere um dispositivo que apresenta aumento de erros corrigidos e um alerta de desgaste, mas ainda conclui leituras. Classifique isso como sinal de saúde, não como falha definitiva. Depois simule uma leitura irrecuperável: o driver deve propagar erro, não preencher o buffer com conteúdo inventado. Por fim, explique como backup e verificação de integridade complementam o monitoramento do hardware.

## Metadados da aula
- Dificuldade: Média
- Duração: 45 minutos
