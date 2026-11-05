# Reforço da Aula 15 — DMA e Memória

## 1. DMA reduz cópias pela CPU

O dispositivo transfere dados envolvendo a RAM usando um mecanismo próprio. A CPU ainda prepara e acompanha a operação.

## 2. Endereços não são intercambiáveis

Endereço virtual de processo, endereço físico e endereço DMA podem ser diferentes. O driver usa os serviços de mapeamento do kernel.

## 3. IOMMU

Ajuda a restringir quais regiões um dispositivo pode acessar. Não substitui validação de tamanho, direção e vida útil.

## 4. Buffer protegido

O dispositivo pode continuar acessando o buffer até a conclusão real. Não libere a memória só porque o solicitante pediu cancelamento.

## 5. Fixação

1. O que o DMA evita que a CPU faça byte a byte?
2. Por que um ponteiro virtual não basta?
3. Qual é o papel da IOMMU?
4. Em leitura, quem escreve no buffer?
5. Quando o buffer pode ser liberado?
