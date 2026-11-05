# Descoberta e identificação de dispositivos

## Objetivo

Nesta aula, você estudará descoberta e identificação de dispositivos e entenderá como esse assunto participa da arquitetura de armazenamento. Ao final, deverá explicar o conceito, reconhecer seus limites e relacioná-lo ao ZenithOS.

## 1. Conceito central

A descoberta enumera controladores e dispositivos, identifica interfaces reconhecidas e consulta capacidades como quantidade de blocos, tamanho lógico, limites de transferência e comandos disponíveis. Identidade física, caminho de conexão e identificador interno são conceitos distintos.

## 2. Exemplo de funcionamento

Um dispositivo pode receber um número interno durante o boot, mas esse número pode mudar após reinicialização. Se o hardware for removido e outro ocupar o mesmo endereço, referências antigas não podem passar a representar o novo dispositivo.

## 3. Validação e segurança

Tratar respostas incompletas, capacidades absurdas, timeouts e remoção durante descoberta. Não assumir que um endereço de barramento é identidade permanente. Validar capacidades antes de registrar o dispositivo.

Dados lidos do dispositivo e capacidades anunciadas por hardware devem ser tratados como entradas externas. Valide limites, tamanhos, referências e estados antes de usá-los para acessar memória ou encaminhar operações.

## 4. Aplicação no ZenithOS

O ZenithOS deve registrar dispositivos em uma estrutura comum com identificador, estado, capacidades e driver responsável. As camadas superiores não devem depender de endereços específicos do barramento.

Mantenha as responsabilidades separadas: o gerenciador oferece abstrações comuns; drivers conhecem protocolos e controladores; o dispositivo executa as operações.

## 5. Perguntas de compreensão

1. Qual é a diferença entre descobrir um dispositivo e inicializá-lo?
2. Por que um endereço de barramento não é uma identidade permanente?
3. Que informações mínimas o ZenithOS deve registrar sobre uma unidade?
4. O que pode acontecer se uma referência antiga for reutilizada após remoção e reconexão?
5. Por que as capacidades anunciadas precisam ser validadas?
6. Como distinguir um dispositivo descoberto de um dispositivo operacional?

## 6. Etapas de descoberta
A descoberta normalmente começa com a enumeração do barramento e dos controladores conhecidos. O sistema identifica uma função ou dispositivo, associa um driver compatível, inicializa a interface e consulta informações como capacidade, tamanho lógico, limites de transferência e recursos opcionais.

Nem todo dispositivo encontrado está pronto para receber operações. Descoberto, inicializado e operacional são estados diferentes.

## 7. Identidade não é endereço físico
Um endereço no barramento descreve onde o dispositivo foi encontrado naquele momento. Um número de série pode ajudar a identificar a unidade física, mas pode estar ausente, duplicado ou ser fornecido incorretamente. O ZenithOS deve manter um identificador interno e controlar o ciclo de vida da referência.

Uma referência antiga não pode passar a apontar para um novo dispositivo só porque ele ocupou o mesmo endereço do barramento. Um contador de geração ou mecanismo equivalente ajuda a detectar referências obsoletas.

## 8. Exemplo guiado
Durante o boot, o sistema encontra uma unidade, atribui um identificador interno e registra suas capacidades. Depois a unidade é removida. O registro muda para indisponível e as operações pendentes são tratadas. Se outra unidade aparecer no mesmo endereço, ela recebe uma nova identidade operacional.

## 9. Método de aprendizagem
Separe o processo em quatro perguntas: onde o dispositivo foi encontrado? qual driver pode operá-lo? quais capacidades ele declarou? em que estado está? Não misture descoberta com autorização para executar operações.

## 11. Critério de conclusão

Você concluiu a aula quando conseguir explicar o conceito com suas palavras, resolver um exemplo novo e justificar pelo menos duas validações necessárias antes de integrar esse recurso ao ZenithOS.

> - **Dificuldade:** Muito difícil
> - **Duração:** 50 minutos
