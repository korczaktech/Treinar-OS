# Reforço da Aula 10 — Camadas do subsistema de armazenamento

## Visão em sequência
Aplicação → sistema de arquivos → volume/partição → cache de blocos → camada de blocos → gerenciador de dispositivos → driver → controlador/dispositivo. O subsistema de memória participa fornecendo buffers e mapeamentos.

## Exemplo de leitura
A aplicação pede um arquivo. O sistema de arquivos encontra os blocos. A camada de blocos valida a faixa. O driver traduz o pedido. O dispositivo transfere os dados. A conclusão retorna às camadas superiores.

## Responsabilidades
- Sistema de arquivos: nomes, diretórios e alocação.
- Gerenciador de volumes: partições, limites e volumes.
- Camada de blocos: requisições genéricas e validação.
- Gerenciador de dispositivos: identidade, capacidades e estado.
- Driver: protocolo específico.

## Como estudar
Escolha uma operação e percorra a arquitetura em ambas as direções. Para cada camada, identifique entrada, validação, transformação e resultado.

## Perguntas de fixação
1. Qual camada entende nomes de arquivos?
2. Qual camada valida uma faixa de LBAs?
3. Qual camada conhece o protocolo NVMe?
4. Por que um erro precisa ser propagado até a aplicação?
5. Como um dispositivo em RAM ajuda a testar a arquitetura?
