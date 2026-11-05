# Aula 101 — Mapa físico e descoberta de memória: fundamentos, finalidade e limites

## Objetivo

Compreender como firmware e plataforma descrevem a memória física disponível, por que nem toda região pode ser usada pelo kernel e como transformar o mapa recebido em uma visão segura para o ZenithOS.

## Pré-requisitos

Aulas 1 a 100, especialmente endereçamento, intervalos, metadados e validação defensiva.

## 1. O que é memória física

Memória física é o conjunto de endereços que a plataforma apresenta ao processador e aos dispositivos. Ela não é necessariamente contínua nem está inteiramente livre para o sistema operacional. Parte pode estar ocupada por firmware, dispositivos mapeados em memória, regiões reservadas ou estruturas necessárias durante a inicialização.

O mapa físico descreve regiões e seus tipos. Ele não concede ao kernel autorização irrestrita para usar qualquer endereço.

## 2. Quem fornece o mapa

Durante a inicialização, firmware ou bootloader pode fornecer informações sobre regiões utilizáveis e reservadas. O formato depende da plataforma e do protocolo de boot. O kernel deve tratar esses dados como entrada externa: verificar tamanho, alinhamento, tipos conhecidos e limites antes de incorporá-los ao gerenciador de memória.

Não presuma que o mapa esteja ordenado, sem lacunas, sem sobreposição ou completo. Essas propriedades precisam ser verificadas.

## 3. Regiões utilizáveis e reservadas

Uma região utilizável pode ser candidata à alocação depois que o kernel descontar suas próprias áreas e demais reservas. Uma região reservada não deve ser entregue ao alocador geral. Regiões de firmware, ACPI, memória persistente e dispositivos podem exigir políticas específicas.

O significado de cada tipo deve vir da especificação da plataforma. Não transforme um tipo desconhecido em memória livre por conveniência.

## 4. Intervalos e limites

Represente regiões como início e tamanho, ou início e limite exclusivo. A forma com limite exclusivo facilita verificar sobreposições. Antes de calcular início + tamanho, detecte overflow. Verifique também se o intervalo cabe no espaço de endereçamento suportado.

Exemplo: uma região começa em 0x100000 e possui 0x300000 bytes. Seu limite exclusivo é 0x400000. A região inclui 0x100000, mas não inclui 0x400000. Uma solicitação que termina exatamente nesse limite pode caber; uma que ultrapassa não cabe.

## 5. Alinhamento e páginas

O mapa pode descrever regiões em granularidade diferente daquela usada pelo alocador de páginas. Ao disponibilizar páginas, o kernel não deve incluir uma página parcialmente reservada. Arredondar o início para cima e o limite para baixo reduz o conjunto utilizável, mas evita entregar bytes pertencentes a outra finalidade.

Página física e quadro de página são unidades do gerenciador; não confunda tamanho de página com bloco de armazenamento.

## 6. Aplicação no ZenithOS

Preserve o mapa original recebido para diagnóstico e produza uma lista normalizada separada para o alocador. Valide regiões e classifique tipos; depois subtraia kernel, bootloader, estruturas de inicialização, framebuffer e demais reservas conhecidas. Só então publique quadros livres.

Mantenha o parser do mapa independente do alocador físico. Assim, testes podem fornecer mapas artificiais sem depender de firmware ou máquina real.

## 7. Método de aprendizagem

1. Desenhe uma linha de endereços e marque regiões utilizáveis e reservadas.
2. Identifique lacunas e sobreposições.
3. Converta intervalos em páginas completas.
4. Simule endereço inicial próximo ao limite máximo e verifique overflow.
5. Explique por que regiões desconhecidas não devem ser consideradas livres.

## 8. Exercícios de compreensão

1. Por que o mapa físico não significa que toda a memória listada está disponível?
2. Qual a diferença entre região utilizável e reservada?
3. Por que limite exclusivo simplifica a verificação de intervalos?
4. Como tratar um tipo de região desconhecido?
5. Por que arredondar início para cima e fim para baixo ao converter em páginas?
6. Quais áreas do boot precisam ser preservadas até não serem mais utilizadas?
7. Como testar o parser sem firmware real?

## 9. Exercício .nbx (opcional)

Modele uma lista pequena de regiões com valores fictícios. Classifique cada intervalo, identifique sobreposições e determine quais páginas completas poderiam ser candidatas à alocação. Não implemente acesso físico à memória.

## 10. Critério de conclusão

Você concluiu quando conseguir interpretar um mapa simples, identificar regiões que não podem ser usadas, validar limites sem overflow e explicar como o ZenithOS transforma o mapa recebido em uma lista segura para o alocador.

> **Dificuldade:** Média  
> **Duração estimada:** 45 minutos
