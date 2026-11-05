# Treinar-OS

## Plano geral de formação — 500 aulas

Este repositório organiza uma formação progressiva em arquitetura e desenvolvimento de sistemas operacionais, com foco na construção do **ZenithOS**. O curso está dividido em 10 etapas de 50 aulas, totalizando 500 aulas.

Esta página é o **mapa completo do curso**. Ela define a sequência e o tema central de cada aula; não significa que todas as aulas já estejam escritas. O conteúdo será desenvolvido gradualmente, respeitando os pré-requisitos.

## Estrutura prevista de cada aula

- **Aula principal:** explicação original e detalhada do tema central, conceitos, funcionamento, exemplos e relação com o ZenithOS.
- **Reforço:** revisão dos conceitos essenciais, esclarecimento dos pontos difíceis e exemplos adicionais.
- **Exercícios:** incluídos quando agregarem valor. Podem existir vários, com limite de 10 por aula. Nem toda aula precisa ter exercício.
- **Nebula (.nbx):** utilizada quando a atividade exigir implementação ou raciocínio executável. Os enunciados não devem entregar a solução.
- **Validação:** os exercícios poderão ser verificados posteriormente pelo compilador, testes automatizados e CI. Criar um exercício não significa que ele foi compilado ou executado.

## Visão geral das etapas

- **Etapa 1 — Armazenamento e dispositivos (1–50):** Dispositivos, blocos, endereçamento, operações, partições e volumes.
- **Etapa 2 — Sistemas de arquivos (51–100):** Arquivos, diretórios, metadados, alocação, montagem e consistência.
- **Etapa 3 — Memória (101–150):** Memória física e virtual, alocação, paginação e proteção.
- **Etapa 4 — Processos e threads (151–200):** Execução de programas, processos, threads e chamadas de sistema.
- **Etapa 5 — Concorrência e temporização (201–250):** Sincronização, atomicidade, deadlocks, relógios e escalonamento.
- **Etapa 6 — Hardware e drivers (251–300):** Barramentos, interrupções, DMA, descoberta e drivers.
- **Etapa 7 — Boot e kernel (301–350):** Firmware, ZBL, carregamento do kernel e serviços essenciais.
- **Etapa 8 — Entrada, saída e gráficos (351–400):** Console, entrada humana, vídeo, GPU e renderização.
- **Etapa 9 — Segurança (401–450):** Identidade, privilégios, isolamento, criptografia e confiança.
- **Etapa 10 — Rede e integração (451–500):** Protocolos, serviços de rede, integração, testes e projeto final.

## As 500 aulas

### Etapa 1 — Armazenamento e dispositivos

Dispositivos, blocos, endereçamento, operações, partições e volumes.

| Aula | Tema central |
|---:|---|
| 1 | Fundamentos do armazenamento |
| 2 | Organização física e lógica do armazenamento |
| 3 | Identificação e endereçamento do armazenamento |
| 4 | Intervalos e validação de operações de armazenamento |
| 5 | Unidades, capacidades e conversões |
| 6 | Geometria lógica e organização de blocos |
| 7 | Dispositivos, controladores e comunicação |
| 8 | Leitura e escrita de blocos |
| 9 | Erros e limites de endereçamento |
| 10 | Camadas do subsistema de armazenamento |
| 11 | Cache de armazenamento e coerência |
| 12 | Sincronização, flush e barreiras |
| 13 | Operações assíncronas e filas |
| 14 | Interrupções, polling e conclusão |
| 15 | DMA e acesso do dispositivo à memória |
| 16 | Timeouts, erros e recuperação |
| 17 | Arquitetura de SSDs e memória NAND |
| 18 | Blocos defeituosos e confiabilidade |
| 19 | Dispositivos virtuais e abstração de blocos |
| 20 | Segurança do armazenamento |
| 21 | Arquitetura integrada de armazenamento |
| 22 | Particionamento e tabelas de partição |
| 23 | Leitura e validação de GPT |
| 24 | Compatibilidade e leitura de MBR |
| 25 | Descoberta e identificação de dispositivos |
| 26 | Volumes e regiões reservadas |
| 27 | Alinhamento e limites de partições |
| 28 | Montagem e desmontagem de volumes |
| 29 | Metadados e estruturas de armazenamento |
| 30 | Validação defensiva de metadados |
| 31 | Integridade e recuperação de tabelas |
| 32 | Discos removíveis e hot-plug |
| 33 | Capacidades dos dispositivos |
| 34 | Setores lógicos e físicos avançados |
| 35 | Operações de múltiplos blocos |
| 36 | Leitura e escrita parcial |
| 37 | Atomicidade de operações |
| 38 | Ordenação de requisições |
| 39 | Agrupamento e divisão de requisições |
| 40 | Despacho de I/O |
| 41 | Diagnóstico de desempenho |
| 42 | Dispositivos compostos |
| 43 | Volumes distribuídos e espelhados |
| 44 | Conceitos de RAID |
| 45 | Reconstrução de RAID |
| 46 | Falhas em conjuntos RAID |
| 47 | Snapshots em nível de bloco |
| 48 | Clonagem de volumes |
| 49 | TRIM e descarte de blocos |
| 50 | Projeto do gerenciador de volumes |

### Etapa 2 — Sistemas de arquivos

Arquivos, diretórios, metadados, alocação, montagem e consistência.

| Aula | Tema central |
|---:|---|
| 51 | Fundamentos e conceitos de conceitos e responsabilidades |
| 52 | Arquitetura e estruturas de conceitos e responsabilidades |
| 53 | Funcionamento interno de conceitos e responsabilidades |
| 54 | Implementação no ZenithOS de conceitos e responsabilidades |
| 55 | Validação, falhas e integração de conceitos e responsabilidades |
| 56 | Fundamentos e conceitos de arquivos, diretórios e caminhos |
| 57 | Arquitetura e estruturas de arquivos, diretórios e caminhos |
| 58 | Funcionamento interno de arquivos, diretórios e caminhos |
| 59 | Implementação no ZenithOS de arquivos, diretórios e caminhos |
| 60 | Validação, falhas e integração de arquivos, diretórios e caminhos |
| 61 | Fundamentos e conceitos de metadados e atributos |
| 62 | Arquitetura e estruturas de metadados e atributos |
| 63 | Funcionamento interno de metadados e atributos |
| 64 | Implementação no ZenithOS de metadados e atributos |
| 65 | Validação, falhas e integração de metadados e atributos |
| 66 | Fundamentos e conceitos de alocação de espaço |
| 67 | Arquitetura e estruturas de alocação de espaço |
| 68 | Funcionamento interno de alocação de espaço |
| 69 | Implementação no ZenithOS de alocação de espaço |
| 70 | Validação, falhas e integração de alocação de espaço |
| 71 | Fundamentos e conceitos de mapas de espaço livre |
| 72 | Arquitetura e estruturas de mapas de espaço livre |
| 73 | Funcionamento interno de mapas de espaço livre |
| 74 | Implementação no ZenithOS de mapas de espaço livre |
| 75 | Validação, falhas e integração de mapas de espaço livre |
| 76 | Fundamentos e conceitos de inodes e estruturas equivalentes |
| 77 | Arquitetura e estruturas de inodes e estruturas equivalentes |
| 78 | Funcionamento interno de inodes e estruturas equivalentes |
| 79 | Implementação no ZenithOS de inodes e estruturas equivalentes |
| 80 | Validação, falhas e integração de inodes e estruturas equivalentes |
| 81 | Fundamentos e conceitos de índices de diretório |
| 82 | Arquitetura e estruturas de índices de diretório |
| 83 | Funcionamento interno de índices de diretório |
| 84 | Implementação no ZenithOS de índices de diretório |
| 85 | Validação, falhas e integração de índices de diretório |
| 86 | Fundamentos e conceitos de criação, abertura e remoção |
| 87 | Arquitetura e estruturas de criação, abertura e remoção |
| 88 | Funcionamento interno de criação, abertura e remoção |
| 89 | Implementação no ZenithOS de criação, abertura e remoção |
| 90 | Validação, falhas e integração de criação, abertura e remoção |
| 91 | Fundamentos e conceitos de leitura, escrita e truncamento |
| 92 | Arquitetura e estruturas de leitura, escrita e truncamento |
| 93 | Funcionamento interno de leitura, escrita e truncamento |
| 94 | Implementação no ZenithOS de leitura, escrita e truncamento |
| 95 | Validação, falhas e integração de leitura, escrita e truncamento |
| 96 | Fundamentos e conceitos de links e referências |
| 97 | Arquitetura e estruturas de links e referências |
| 98 | Funcionamento interno de links e referências |
| 99 | Implementação no ZenithOS de links e referências |
| 100 | Validação, falhas e integração de links e referências |

### Etapa 3 — Memória

Memória física e virtual, alocação, paginação e proteção.

| Aula | Tema central |
|---:|---|
| 101 | Fundamentos e conceitos de mapa físico e descoberta de memória |
| 102 | Arquitetura e estruturas de mapa físico e descoberta de memória |
| 103 | Funcionamento interno de mapa físico e descoberta de memória |
| 104 | Implementação no ZenithOS de mapa físico e descoberta de memória |
| 105 | Validação, falhas e integração de mapa físico e descoberta de memória |
| 106 | Fundamentos e conceitos de quadros e páginas físicas |
| 107 | Arquitetura e estruturas de quadros e páginas físicas |
| 108 | Funcionamento interno de quadros e páginas físicas |
| 109 | Implementação no ZenithOS de quadros e páginas físicas |
| 110 | Validação, falhas e integração de quadros e páginas físicas |
| 111 | Fundamentos e conceitos de alocadores de memória |
| 112 | Arquitetura e estruturas de alocadores de memória |
| 113 | Funcionamento interno de alocadores de memória |
| 114 | Implementação no ZenithOS de alocadores de memória |
| 115 | Validação, falhas e integração de alocadores de memória |
| 116 | Fundamentos e conceitos de fragmentação e compactação |
| 117 | Arquitetura e estruturas de fragmentação e compactação |
| 118 | Funcionamento interno de fragmentação e compactação |
| 119 | Implementação no ZenithOS de fragmentação e compactação |
| 120 | Validação, falhas e integração de fragmentação e compactação |
| 121 | Fundamentos e conceitos de memória virtual e endereços |
| 122 | Arquitetura e estruturas de memória virtual e endereços |
| 123 | Funcionamento interno de memória virtual e endereços |
| 124 | Implementação no ZenithOS de memória virtual e endereços |
| 125 | Validação, falhas e integração de memória virtual e endereços |
| 126 | Fundamentos e conceitos de tabelas de páginas |
| 127 | Arquitetura e estruturas de tabelas de páginas |
| 128 | Funcionamento interno de tabelas de páginas |
| 129 | Implementação no ZenithOS de tabelas de páginas |
| 130 | Validação, falhas e integração de tabelas de páginas |
| 131 | Fundamentos e conceitos de tlb e tradução |
| 132 | Arquitetura e estruturas de tlb e tradução |
| 133 | Funcionamento interno de tlb e tradução |
| 134 | Implementação no ZenithOS de tlb e tradução |
| 135 | Validação, falhas e integração de tlb e tradução |
| 136 | Fundamentos e conceitos de falhas de página |
| 137 | Arquitetura e estruturas de falhas de página |
| 138 | Funcionamento interno de falhas de página |
| 139 | Implementação no ZenithOS de falhas de página |
| 140 | Validação, falhas e integração de falhas de página |
| 141 | Fundamentos e conceitos de heap, pilha e mapeamentos |
| 142 | Arquitetura e estruturas de heap, pilha e mapeamentos |
| 143 | Funcionamento interno de heap, pilha e mapeamentos |
| 144 | Implementação no ZenithOS de heap, pilha e mapeamentos |
| 145 | Validação, falhas e integração de heap, pilha e mapeamentos |
| 146 | Fundamentos e conceitos de permissões e proteção |
| 147 | Arquitetura e estruturas de permissões e proteção |
| 148 | Funcionamento interno de permissões e proteção |
| 149 | Implementação no ZenithOS de permissões e proteção |
| 150 | Validação, falhas e integração de permissões e proteção |

### Etapa 4 — Processos e threads

Execução de programas, processos, threads e chamadas de sistema.

| Aula | Tema central |
|---:|---|
| 151 | Fundamentos e conceitos de programa e processo |
| 152 | Arquitetura e estruturas de programa e processo |
| 153 | Funcionamento interno de programa e processo |
| 154 | Implementação no ZenithOS de programa e processo |
| 155 | Validação, falhas e integração de programa e processo |
| 156 | Fundamentos e conceitos de estados e ciclo de vida |
| 157 | Arquitetura e estruturas de estados e ciclo de vida |
| 158 | Funcionamento interno de estados e ciclo de vida |
| 159 | Implementação no ZenithOS de estados e ciclo de vida |
| 160 | Validação, falhas e integração de estados e ciclo de vida |
| 161 | Fundamentos e conceitos de criação e término |
| 162 | Arquitetura e estruturas de criação e término |
| 163 | Funcionamento interno de criação e término |
| 164 | Implementação no ZenithOS de criação e término |
| 165 | Validação, falhas e integração de criação e término |
| 166 | Fundamentos e conceitos de contexto e troca de contexto |
| 167 | Arquitetura e estruturas de contexto e troca de contexto |
| 168 | Funcionamento interno de contexto e troca de contexto |
| 169 | Implementação no ZenithOS de contexto e troca de contexto |
| 170 | Validação, falhas e integração de contexto e troca de contexto |
| 171 | Fundamentos e conceitos de modo usuário e kernel |
| 172 | Arquitetura e estruturas de modo usuário e kernel |
| 173 | Funcionamento interno de modo usuário e kernel |
| 174 | Implementação no ZenithOS de modo usuário e kernel |
| 175 | Validação, falhas e integração de modo usuário e kernel |
| 176 | Fundamentos e conceitos de chamadas de sistema |
| 177 | Arquitetura e estruturas de chamadas de sistema |
| 178 | Funcionamento interno de chamadas de sistema |
| 179 | Implementação no ZenithOS de chamadas de sistema |
| 180 | Validação, falhas e integração de chamadas de sistema |
| 181 | Fundamentos e conceitos de carregamento de executáveis |
| 182 | Arquitetura e estruturas de carregamento de executáveis |
| 183 | Funcionamento interno de carregamento de executáveis |
| 184 | Implementação no ZenithOS de carregamento de executáveis |
| 185 | Validação, falhas e integração de carregamento de executáveis |
| 186 | Fundamentos e conceitos de formato e segmentos |
| 187 | Arquitetura e estruturas de formato e segmentos |
| 188 | Funcionamento interno de formato e segmentos |
| 189 | Implementação no ZenithOS de formato e segmentos |
| 190 | Validação, falhas e integração de formato e segmentos |
| 191 | Fundamentos e conceitos de pilha e ambiente inicial |
| 192 | Arquitetura e estruturas de pilha e ambiente inicial |
| 193 | Funcionamento interno de pilha e ambiente inicial |
| 194 | Implementação no ZenithOS de pilha e ambiente inicial |
| 195 | Validação, falhas e integração de pilha e ambiente inicial |
| 196 | Fundamentos e conceitos de threads e execução |
| 197 | Arquitetura e estruturas de threads e execução |
| 198 | Funcionamento interno de threads e execução |
| 199 | Implementação no ZenithOS de threads e execução |
| 200 | Validação, falhas e integração de threads e execução |

### Etapa 5 — Concorrência e temporização

Sincronização, atomicidade, deadlocks, relógios e escalonamento.

| Aula | Tema central |
|---:|---|
| 201 | Fundamentos e conceitos de concorrência e paralelismo |
| 202 | Arquitetura e estruturas de concorrência e paralelismo |
| 203 | Funcionamento interno de concorrência e paralelismo |
| 204 | Implementação no ZenithOS de concorrência e paralelismo |
| 205 | Validação, falhas e integração de concorrência e paralelismo |
| 206 | Fundamentos e conceitos de condições de corrida |
| 207 | Arquitetura e estruturas de condições de corrida |
| 208 | Funcionamento interno de condições de corrida |
| 209 | Implementação no ZenithOS de condições de corrida |
| 210 | Validação, falhas e integração de condições de corrida |
| 211 | Fundamentos e conceitos de seções críticas |
| 212 | Arquitetura e estruturas de seções críticas |
| 213 | Funcionamento interno de seções críticas |
| 214 | Implementação no ZenithOS de seções críticas |
| 215 | Validação, falhas e integração de seções críticas |
| 216 | Fundamentos e conceitos de operações atômicas |
| 217 | Arquitetura e estruturas de operações atômicas |
| 218 | Funcionamento interno de operações atômicas |
| 219 | Implementação no ZenithOS de operações atômicas |
| 220 | Validação, falhas e integração de operações atômicas |
| 221 | Fundamentos e conceitos de modelo de memória |
| 222 | Arquitetura e estruturas de modelo de memória |
| 223 | Funcionamento interno de modelo de memória |
| 224 | Implementação no ZenithOS de modelo de memória |
| 225 | Validação, falhas e integração de modelo de memória |
| 226 | Fundamentos e conceitos de mutexes e spinlocks |
| 227 | Arquitetura e estruturas de mutexes e spinlocks |
| 228 | Funcionamento interno de mutexes e spinlocks |
| 229 | Implementação no ZenithOS de mutexes e spinlocks |
| 230 | Validação, falhas e integração de mutexes e spinlocks |
| 231 | Fundamentos e conceitos de semáforos e eventos |
| 232 | Arquitetura e estruturas de semáforos e eventos |
| 233 | Funcionamento interno de semáforos e eventos |
| 234 | Implementação no ZenithOS de semáforos e eventos |
| 235 | Validação, falhas e integração de semáforos e eventos |
| 236 | Fundamentos e conceitos de deadlocks e prevenção |
| 237 | Arquitetura e estruturas de deadlocks e prevenção |
| 238 | Funcionamento interno de deadlocks e prevenção |
| 239 | Implementação no ZenithOS de deadlocks e prevenção |
| 240 | Validação, falhas e integração de deadlocks e prevenção |
| 241 | Fundamentos e conceitos de temporizadores e relógios |
| 242 | Arquitetura e estruturas de temporizadores e relógios |
| 243 | Funcionamento interno de temporizadores e relógios |
| 244 | Implementação no ZenithOS de temporizadores e relógios |
| 245 | Validação, falhas e integração de temporizadores e relógios |
| 246 | Fundamentos e conceitos de escalonamento em tempo real |
| 247 | Arquitetura e estruturas de escalonamento em tempo real |
| 248 | Funcionamento interno de escalonamento em tempo real |
| 249 | Implementação no ZenithOS de escalonamento em tempo real |
| 250 | Validação, falhas e integração de escalonamento em tempo real |

### Etapa 6 — Hardware e drivers

Barramentos, interrupções, DMA, descoberta e drivers.

| Aula | Tema central |
|---:|---|
| 251 | Fundamentos e conceitos de descoberta e enumeração de hardware |
| 252 | Arquitetura e estruturas de descoberta e enumeração de hardware |
| 253 | Funcionamento interno de descoberta e enumeração de hardware |
| 254 | Implementação no ZenithOS de descoberta e enumeração de hardware |
| 255 | Validação, falhas e integração de descoberta e enumeração de hardware |
| 256 | Fundamentos e conceitos de barramentos e pcie |
| 257 | Arquitetura e estruturas de barramentos e pcie |
| 258 | Funcionamento interno de barramentos e pcie |
| 259 | Implementação no ZenithOS de barramentos e pcie |
| 260 | Validação, falhas e integração de barramentos e pcie |
| 261 | Fundamentos e conceitos de configuração e bars |
| 262 | Arquitetura e estruturas de configuração e bars |
| 263 | Funcionamento interno de configuração e bars |
| 264 | Implementação no ZenithOS de configuração e bars |
| 265 | Validação, falhas e integração de configuração e bars |
| 266 | Fundamentos e conceitos de mmio e registradores |
| 267 | Arquitetura e estruturas de mmio e registradores |
| 268 | Funcionamento interno de mmio e registradores |
| 269 | Implementação no ZenithOS de mmio e registradores |
| 270 | Validação, falhas e integração de mmio e registradores |
| 271 | Fundamentos e conceitos de controladores de interrupção |
| 272 | Arquitetura e estruturas de controladores de interrupção |
| 273 | Funcionamento interno de controladores de interrupção |
| 274 | Implementação no ZenithOS de controladores de interrupção |
| 275 | Validação, falhas e integração de controladores de interrupção |
| 276 | Fundamentos e conceitos de vetores e roteamento irq |
| 277 | Arquitetura e estruturas de vetores e roteamento irq |
| 278 | Funcionamento interno de vetores e roteamento irq |
| 279 | Implementação no ZenithOS de vetores e roteamento irq |
| 280 | Validação, falhas e integração de vetores e roteamento irq |
| 281 | Fundamentos e conceitos de msi e msi-x |
| 282 | Arquitetura e estruturas de msi e msi-x |
| 283 | Funcionamento interno de msi e msi-x |
| 284 | Implementação no ZenithOS de msi e msi-x |
| 285 | Validação, falhas e integração de msi e msi-x |
| 286 | Fundamentos e conceitos de ciclo de vida de drivers |
| 287 | Arquitetura e estruturas de ciclo de vida de drivers |
| 288 | Funcionamento interno de ciclo de vida de drivers |
| 289 | Implementação no ZenithOS de ciclo de vida de drivers |
| 290 | Validação, falhas e integração de ciclo de vida de drivers |
| 291 | Fundamentos e conceitos de dma e descritores |
| 292 | Arquitetura e estruturas de dma e descritores |
| 293 | Funcionamento interno de dma e descritores |
| 294 | Implementação no ZenithOS de dma e descritores |
| 295 | Validação, falhas e integração de dma e descritores |
| 296 | Fundamentos e conceitos de isolamento e testes de drivers |
| 297 | Arquitetura e estruturas de isolamento e testes de drivers |
| 298 | Funcionamento interno de isolamento e testes de drivers |
| 299 | Implementação no ZenithOS de isolamento e testes de drivers |
| 300 | Validação, falhas e integração de isolamento e testes de drivers |

### Etapa 7 — Boot e kernel

Firmware, ZBL, carregamento do kernel e serviços essenciais.

| Aula | Tema central |
|---:|---|
| 301 | Fundamentos e conceitos de firmware e processo de boot |
| 302 | Arquitetura e estruturas de firmware e processo de boot |
| 303 | Funcionamento interno de firmware e processo de boot |
| 304 | Implementação no ZenithOS de firmware e processo de boot |
| 305 | Validação, falhas e integração de firmware e processo de boot |
| 306 | Fundamentos e conceitos de uefi e contratos |
| 307 | Arquitetura e estruturas de uefi e contratos |
| 308 | Funcionamento interno de uefi e contratos |
| 309 | Implementação no ZenithOS de uefi e contratos |
| 310 | Validação, falhas e integração de uefi e contratos |
| 311 | Fundamentos e conceitos de bootloader próprio zbl |
| 312 | Arquitetura e estruturas de bootloader próprio zbl |
| 313 | Funcionamento interno de bootloader próprio zbl |
| 314 | Implementação no ZenithOS de bootloader próprio zbl |
| 315 | Validação, falhas e integração de bootloader próprio zbl |
| 316 | Fundamentos e conceitos de carregamento do kernel |
| 317 | Arquitetura e estruturas de carregamento do kernel |
| 318 | Funcionamento interno de carregamento do kernel |
| 319 | Implementação no ZenithOS de carregamento do kernel |
| 320 | Validação, falhas e integração de carregamento do kernel |
| 321 | Fundamentos e conceitos de mapa de memória inicial |
| 322 | Arquitetura e estruturas de mapa de memória inicial |
| 323 | Funcionamento interno de mapa de memória inicial |
| 324 | Implementação no ZenithOS de mapa de memória inicial |
| 325 | Validação, falhas e integração de mapa de memória inicial |
| 326 | Fundamentos e conceitos de inicialização de cpu |
| 327 | Arquitetura e estruturas de inicialização de cpu |
| 328 | Funcionamento interno de inicialização de cpu |
| 329 | Implementação no ZenithOS de inicialização de cpu |
| 330 | Validação, falhas e integração de inicialização de cpu |
| 331 | Fundamentos e conceitos de gdt, idt e exceções |
| 332 | Arquitetura e estruturas de gdt, idt e exceções |
| 333 | Funcionamento interno de gdt, idt e exceções |
| 334 | Implementação no ZenithOS de gdt, idt e exceções |
| 335 | Validação, falhas e integração de gdt, idt e exceções |
| 336 | Fundamentos e conceitos de temporizador e interrupções |
| 337 | Arquitetura e estruturas de temporizador e interrupções |
| 338 | Funcionamento interno de temporizador e interrupções |
| 339 | Implementação no ZenithOS de temporizador e interrupções |
| 340 | Validação, falhas e integração de temporizador e interrupções |
| 341 | Fundamentos e conceitos de heap do kernel |
| 342 | Arquitetura e estruturas de heap do kernel |
| 343 | Funcionamento interno de heap do kernel |
| 344 | Implementação no ZenithOS de heap do kernel |
| 345 | Validação, falhas e integração de heap do kernel |
| 346 | Fundamentos e conceitos de montagem do volume raiz |
| 347 | Arquitetura e estruturas de montagem do volume raiz |
| 348 | Funcionamento interno de montagem do volume raiz |
| 349 | Implementação no ZenithOS de montagem do volume raiz |
| 350 | Validação, falhas e integração de montagem do volume raiz |

### Etapa 8 — Entrada, saída e gráficos

Console, entrada humana, vídeo, GPU e renderização.

| Aula | Tema central |
|---:|---|
| 351 | Fundamentos e conceitos de modelo de entrada e saída |
| 352 | Arquitetura e estruturas de modelo de entrada e saída |
| 353 | Funcionamento interno de modelo de entrada e saída |
| 354 | Implementação no ZenithOS de modelo de entrada e saída |
| 355 | Validação, falhas e integração de modelo de entrada e saída |
| 356 | Fundamentos e conceitos de console e terminal |
| 357 | Arquitetura e estruturas de console e terminal |
| 358 | Funcionamento interno de console e terminal |
| 359 | Implementação no ZenithOS de console e terminal |
| 360 | Validação, falhas e integração de console e terminal |
| 361 | Fundamentos e conceitos de framebuffer e pixels |
| 362 | Arquitetura e estruturas de framebuffer e pixels |
| 363 | Funcionamento interno de framebuffer e pixels |
| 364 | Implementação no ZenithOS de framebuffer e pixels |
| 365 | Validação, falhas e integração de framebuffer e pixels |
| 366 | Fundamentos e conceitos de modos de vídeo |
| 367 | Arquitetura e estruturas de modos de vídeo |
| 368 | Funcionamento interno de modos de vídeo |
| 369 | Implementação no ZenithOS de modos de vídeo |
| 370 | Validação, falhas e integração de modos de vídeo |
| 371 | Fundamentos e conceitos de fontes e texto |
| 372 | Arquitetura e estruturas de fontes e texto |
| 373 | Funcionamento interno de fontes e texto |
| 374 | Implementação no ZenithOS de fontes e texto |
| 375 | Validação, falhas e integração de fontes e texto |
| 376 | Fundamentos e conceitos de eventos de teclado |
| 377 | Arquitetura e estruturas de eventos de teclado |
| 378 | Funcionamento interno de eventos de teclado |
| 379 | Implementação no ZenithOS de eventos de teclado |
| 380 | Validação, falhas e integração de eventos de teclado |
| 381 | Fundamentos e conceitos de layouts e caracteres |
| 382 | Arquitetura e estruturas de layouts e caracteres |
| 383 | Funcionamento interno de layouts e caracteres |
| 384 | Implementação no ZenithOS de layouts e caracteres |
| 385 | Validação, falhas e integração de layouts e caracteres |
| 386 | Fundamentos e conceitos de mouse e toque |
| 387 | Arquitetura e estruturas de mouse e toque |
| 388 | Funcionamento interno de mouse e toque |
| 389 | Implementação no ZenithOS de mouse e toque |
| 390 | Validação, falhas e integração de mouse e toque |
| 391 | Fundamentos e conceitos de composição de janelas |
| 392 | Arquitetura e estruturas de composição de janelas |
| 393 | Funcionamento interno de composição de janelas |
| 394 | Implementação no ZenithOS de composição de janelas |
| 395 | Validação, falhas e integração de composição de janelas |
| 396 | Fundamentos e conceitos de gpu e renderização |
| 397 | Arquitetura e estruturas de gpu e renderização |
| 398 | Funcionamento interno de gpu e renderização |
| 399 | Implementação no ZenithOS de gpu e renderização |
| 400 | Validação, falhas e integração de gpu e renderização |

### Etapa 9 — Segurança

Identidade, privilégios, isolamento, criptografia e confiança.

| Aula | Tema central |
|---:|---|
| 401 | Fundamentos e conceitos de princípios e modelo de ameaças |
| 402 | Arquitetura e estruturas de princípios e modelo de ameaças |
| 403 | Funcionamento interno de princípios e modelo de ameaças |
| 404 | Implementação no ZenithOS de princípios e modelo de ameaças |
| 405 | Validação, falhas e integração de princípios e modelo de ameaças |
| 406 | Fundamentos e conceitos de privilégios e confiança |
| 407 | Arquitetura e estruturas de privilégios e confiança |
| 408 | Funcionamento interno de privilégios e confiança |
| 409 | Implementação no ZenithOS de privilégios e confiança |
| 410 | Validação, falhas e integração de privilégios e confiança |
| 411 | Fundamentos e conceitos de identidades e autenticação |
| 412 | Arquitetura e estruturas de identidades e autenticação |
| 413 | Funcionamento interno de identidades e autenticação |
| 414 | Implementação no ZenithOS de identidades e autenticação |
| 415 | Validação, falhas e integração de identidades e autenticação |
| 416 | Fundamentos e conceitos de autorização e controle de acesso |
| 417 | Arquitetura e estruturas de autorização e controle de acesso |
| 418 | Funcionamento interno de autorização e controle de acesso |
| 419 | Implementação no ZenithOS de autorização e controle de acesso |
| 420 | Validação, falhas e integração de autorização e controle de acesso |
| 421 | Fundamentos e conceitos de permissões e acls |
| 422 | Arquitetura e estruturas de permissões e acls |
| 423 | Funcionamento interno de permissões e acls |
| 424 | Implementação no ZenithOS de permissões e acls |
| 425 | Validação, falhas e integração de permissões e acls |
| 426 | Fundamentos e conceitos de capacidades e privilégio mínimo |
| 427 | Arquitetura e estruturas de capacidades e privilégio mínimo |
| 428 | Funcionamento interno de capacidades e privilégio mínimo |
| 429 | Implementação no ZenithOS de capacidades e privilégio mínimo |
| 430 | Validação, falhas e integração de capacidades e privilégio mínimo |
| 431 | Fundamentos e conceitos de validação de entradas |
| 432 | Arquitetura e estruturas de validação de entradas |
| 433 | Funcionamento interno de validação de entradas |
| 434 | Implementação no ZenithOS de validação de entradas |
| 435 | Validação, falhas e integração de validação de entradas |
| 436 | Fundamentos e conceitos de proteção de memória |
| 437 | Arquitetura e estruturas de proteção de memória |
| 438 | Funcionamento interno de proteção de memória |
| 439 | Implementação no ZenithOS de proteção de memória |
| 440 | Validação, falhas e integração de proteção de memória |
| 441 | Fundamentos e conceitos de secure boot |
| 442 | Arquitetura e estruturas de secure boot |
| 443 | Funcionamento interno de secure boot |
| 444 | Implementação no ZenithOS de secure boot |
| 445 | Validação, falhas e integração de secure boot |
| 446 | Fundamentos e conceitos de criptografia e chaves |
| 447 | Arquitetura e estruturas de criptografia e chaves |
| 448 | Funcionamento interno de criptografia e chaves |
| 449 | Implementação no ZenithOS de criptografia e chaves |
| 450 | Validação, falhas e integração de criptografia e chaves |

### Etapa 10 — Rede e integração

Protocolos, serviços de rede, integração, testes e projeto final.

| Aula | Tema central |
|---:|---|
| 451 | Fundamentos e conceitos de camadas e encapsulamento |
| 452 | Arquitetura e estruturas de camadas e encapsulamento |
| 453 | Funcionamento interno de camadas e encapsulamento |
| 454 | Implementação no ZenithOS de camadas e encapsulamento |
| 455 | Validação, falhas e integração de camadas e encapsulamento |
| 456 | Fundamentos e conceitos de ethernet e mac |
| 457 | Arquitetura e estruturas de ethernet e mac |
| 458 | Funcionamento interno de ethernet e mac |
| 459 | Implementação no ZenithOS de ethernet e mac |
| 460 | Validação, falhas e integração de ethernet e mac |
| 461 | Fundamentos e conceitos de ipv4, ipv6 e roteamento |
| 462 | Arquitetura e estruturas de ipv4, ipv6 e roteamento |
| 463 | Funcionamento interno de ipv4, ipv6 e roteamento |
| 464 | Implementação no ZenithOS de ipv4, ipv6 e roteamento |
| 465 | Validação, falhas e integração de ipv4, ipv6 e roteamento |
| 466 | Fundamentos e conceitos de icmp e diagnóstico |
| 467 | Arquitetura e estruturas de icmp e diagnóstico |
| 468 | Funcionamento interno de icmp e diagnóstico |
| 469 | Implementação no ZenithOS de icmp e diagnóstico |
| 470 | Validação, falhas e integração de icmp e diagnóstico |
| 471 | Fundamentos e conceitos de udp e datagramas |
| 472 | Arquitetura e estruturas de udp e datagramas |
| 473 | Funcionamento interno de udp e datagramas |
| 474 | Implementação no ZenithOS de udp e datagramas |
| 475 | Validação, falhas e integração de udp e datagramas |
| 476 | Fundamentos e conceitos de tcp e conexões |
| 477 | Arquitetura e estruturas de tcp e conexões |
| 478 | Funcionamento interno de tcp e conexões |
| 479 | Implementação no ZenithOS de tcp e conexões |
| 480 | Validação, falhas e integração de tcp e conexões |
| 481 | Fundamentos e conceitos de api de sockets |
| 482 | Arquitetura e estruturas de api de sockets |
| 483 | Funcionamento interno de api de sockets |
| 484 | Implementação no ZenithOS de api de sockets |
| 485 | Validação, falhas e integração de api de sockets |
| 486 | Fundamentos e conceitos de dns e configuração |
| 487 | Arquitetura e estruturas de dns e configuração |
| 488 | Funcionamento interno de dns e configuração |
| 489 | Implementação no ZenithOS de dns e configuração |
| 490 | Validação, falhas e integração de dns e configuração |
| 491 | Fundamentos e conceitos de pilha e driver de rede |
| 492 | Arquitetura e estruturas de pilha e driver de rede |
| 493 | Funcionamento interno de pilha e driver de rede |
| 494 | Implementação no ZenithOS de pilha e driver de rede |
| 495 | Validação, falhas e integração de pilha e driver de rede |
| 496 | Fundamentos e conceitos de projeto final integrado |
| 497 | Arquitetura e estruturas de projeto final integrado |
| 498 | Funcionamento interno de projeto final integrado |
| 499 | Implementação no ZenithOS de projeto final integrado |
| 500 | Validação, falhas e integração de projeto final integrado |

## Critérios pedagógicos e técnicos

1. A numeração representa a ordem planejada. Não é necessário avançar sem compreender os fundamentos.
2. Cada aula deve explicar o problema que o conceito resolve, seu funcionamento, seus limites e sua relação com outros subsistemas.
3. Conceitos necessários devem aparecer antes de implementações que dependam deles.
4. Exemplos devem distinguir abstração, implementação e comportamento real do hardware.
5. Decisões próprias do ZenithOS devem ser justificadas e comparadas com padrões consolidados quando isso for útil.
6. Não afirmar desempenho, compatibilidade ou segurança sem evidências e testes adequados.
7. Exercícios devem avaliar o que foi realmente ensinado na aula ou em aulas anteriores.
8. O plano poderá receber ajustes técnicos, desde que a progressão seja preservada e as mudanças sejam justificadas.

## Objetivo final

Ao concluir as 500 aulas, o estudante terá percorrido os fundamentos necessários para projetar, implementar, integrar, testar e manter os principais subsistemas de um sistema operacional. O objetivo é desenvolver capacidade de tomar decisões arquiteturais, justificar escolhas, identificar falhas e construir o ZenithOS incrementalmente.
