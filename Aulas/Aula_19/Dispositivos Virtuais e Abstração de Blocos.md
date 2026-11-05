# Dispositivos Virtuais e Abstração de Blocos

## Objetivo

Nem toda unidade apresentada ao sistema precisa corresponder diretamente a um dispositivo físico. Sistemas operacionais podem oferecer discos em RAM, volumes compostos, dispositivos de teste e camadas que redirecionam operações. Nesta aula vamos entender dispositivos virtuais e por que uma interface uniforme facilita o projeto do ZenithOS.

## 1. O que é um dispositivo virtual?

É uma unidade apresentada por software que oferece operações semelhantes às de um dispositivo de blocos. Ela pode armazenar dados em RAM, encaminhar operações para outro dispositivo ou combinar regiões de diferentes fontes.

O sistema de arquivos pode usar a interface de blocos sem precisar conhecer todos os detalhes internos da implementação.

## 2. Disco em RAM

Um disco em RAM reserva uma região de memória e a apresenta como uma sequência de blocos. É rápido e útil para testes, ambientes temporários e sistemas de inicialização.

Porém, seu conteúdo normalmente desaparece quando a memória é perdida, como ao desligar a máquina. Não deve ser confundido com armazenamento persistente.

## 3. Dispositivo de teste

Um dispositivo simulado pode responder leituras e gravações sem hardware físico. Também pode gerar erros controlados, atrasos e remoção simulada.

Isso permite testar validação de intervalos, filas, timeouts, estados e recuperação de forma repetível.

## 4. Camada de abstração

Uma interface comum pode oferecer descobrir capacidade, ler blocos, gravar blocos, sincronizar, descartar regiões e consultar estado. Nem todo dispositivo suporta todas as operações; o descritor deve indicar capacidades.

A camada superior consulta os recursos antes de solicitar uma função opcional.

## 5. Encadeamento de dispositivos

Um dispositivo virtual pode usar outro como base. Por exemplo, um volume lógico pode mapear uma faixa para um dispositivo físico. Isso cria camadas, mas também exige cuidado com ciclos, limites e propagação de erros.

Uma cadeia de dispositivos deve ter direção clara e não pode encaminhar operações indefinidamente.

## 6. Identidade e ciclo de vida

Cada dispositivo virtual precisa de identidade própria. Se dois dispositivos encaminham para o mesmo armazenamento, suas identidades ainda podem ser diferentes porque representam interfaces e políticas distintas.

Ao remover uma camada, operações dependentes precisam ser encerradas ou invalidadas.

## 7. Limites da abstração

Uma interface uniforme não deve esconder diferenças importantes. Alinhamento, tamanho máximo de transferência, flush, discard e comportamento de erro podem variar. O contrato comum expõe capacidades e requisitos sem exigir que todos os dispositivos finjam suportar tudo.

## 8. Aplicação no ZenithOS

O ZenithOS deve implementar primeiro uma interface de dispositivo de blocos e um dispositivo em RAM para testes. Drivers físicos e dispositivos virtuais devem cumprir o mesmo contrato básico. Isso permite testar o sistema de arquivos antes de ter suporte completo a hardware real.

## 9. Perguntas de compreensão

1. O que torna um dispositivo virtual?
2. Por que um disco em RAM normalmente não é persistente?
3. Como um dispositivo simulado ajuda nos testes?
4. Por que nem todos os dispositivos suportam as mesmas operações?
5. Qual risco existe em encadear dispositivos virtuais?
6. Por que uma interface comum não deve esconder capacidades diferentes?

## 10. Exercícios de código

- EXN1A19.nbx — implementar um dispositivo de blocos em memória com limites.
- EXN2A19.nbx — criar uma camada de dispositivo virtual que encaminha operações para uma faixa de outro dispositivo.
