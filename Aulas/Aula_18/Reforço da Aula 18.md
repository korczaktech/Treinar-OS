# Reforço da Aula 18 — Blocos Defeituosos e Saúde

## 1. O defeito pode ficar escondido

O controlador pode remapear uma região interna e continuar apresentando os mesmos LBAs ao sistema operacional.

## 2. Remapeamento

Uma região interna problemática deixa de ser usada e outra assume seu lugar, conforme os recursos do dispositivo.

## 3. Falha de leitura

Se o dispositivo não consegue recuperar os dados, o sistema deve informar erro. Não deve preencher o buffer com conteúdo inventado e declarar sucesso.

## 4. Saúde não é garantia

Temperatura, desgaste e contadores ajudam no monitoramento. Não são uma previsão infalível. Backup continua necessário.

## 5. Fixação

1. Por que um bloco defeituoso pode não aparecer como LBA inválido?
2. O que o remapeamento altera?
3. Como tratar uma leitura irrecuperável?
4. Um indicador de saúde baixo prova que a falha ocorrerá hoje?
5. Por que checksum e backup têm funções diferentes?
