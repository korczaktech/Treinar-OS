# Reforço da Aula 7 — Controladores e comunicação

## Caminho resumido
Camada de blocos → driver → protocolo/controlador → dispositivo. A resposta percorre o caminho inverso, levando sucesso, erro e informações de conclusão.

## Funções
- A camada de blocos valida uma solicitação genérica.
- O driver traduz a solicitação para o protocolo.
- O controlador recebe comandos e coordena o dispositivo.
- O dispositivo executa a operação de armazenamento.

## Protocolos
SATA/AHCI e NVMe são interfaces/protocolos diferentes. O kernel não deve supor que um comando de um protocolo funcione em outro.

## Exemplo
Uma leitura do LBA 20 chega à camada de blocos. Depois da validação, o driver prepara o comando apropriado. O controlador executa a solicitação e reporta conclusão. Se ocorrer erro de mídia, o driver não deve transformar o resultado em sucesso.

## Perguntas de fixação
1. Quem traduz a solicitação genérica para o protocolo?
2. O controlador é o mesmo que o dispositivo?
3. Por que a inicialização precisa terminar antes de aceitar pedidos?
4. O que muda entre um driver NVMe e um driver SATA?
5. Por que a camada superior deve receber uma interface comum?
