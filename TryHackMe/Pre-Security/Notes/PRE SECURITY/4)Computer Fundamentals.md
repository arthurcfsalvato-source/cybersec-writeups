# 4) Computer Fundamentals

---

## 🔗 Navegação Inteligente

### Sequencial
- **← Anterior:** 3) How The Web Works (DNS, HTTP, Web Components)
- **Próximo →:** 5) Operating Systems Basics (Windows, Linux, Segurança do SO)
- **Depois:** 6) Software Basics (Programação, SQL)
- **Final:** 7) Attacks and Defenses (Segurança avançada)

### Tópicos Relacionados Nesta Nota
- **Memória e Forense:** Ver em 5) Operating Systems Basics — Memória
- **Firmware & BIOS:** Ver em 5) Operating Systems Basics — Segurança do SO
- **Ataques de Hardware:** Ver em 7) Attacks and Defenses — Side-Channel Attacks
- **Criptografia de Disco:** Ver em 7) Attacks and Defenses — Criptografia
- **Redes & Periféricos:** Ver em 2) Network Fundamentals — Interfaces

### Referencias Rapidas
- **⚡ Quick Reference** — Arquitetura, componentes, especificações
- **🔑 Conceitos-Chave** — Mapa tematico (hardware, segurança)

---

## Índice
1. [Introdução](#introdução)
2. [Arquitetura de Computadores](#arquitetura-de-computadores)
3. [Componentes de Hardware Essenciais](#componentes-de-hardware-essenciais)
4. [Sistema Binário e Dados Digitais](#sistema-binário-e-dados-digitais)
5. [Processamento de Dados](#processamento-de-dados)
6. [Memória e Armazenamento](#memória-e-armazenamento)
7. [Periféricos e Interfaces](#periféricos-e-interfaces)
8. [Energia e Termodinâmica](#energia-e-termodinâmica)
9. [Segurança em Hardware](#segurança-em-hardware)
10. [Conceitos-Chave para Lembrar](#conceitos-chave-para-lembrar)

---

## Introdução

Um computador é uma máquina eletrônica programável capaz de processar dados e executar operações lógicas. A compreensão dos fundamentos de computadores é essencial para qualquer profissional de segurança cibernética, pois entender como o hardware funciona permite identificar vulnerabilidades físicas e lógicas.

### Por que aprender Computer Fundamentals em Cybersecurity?

- **Vulnerabilidades de Hardware**: Explorar fraquezas físicas em dispositivos
- **Análise de Malware**: Entender como malware interage com hardware
- **Forense Digital**: Recuperar dados de dispositivos comprometidos
- **Segurança Física**: Proteger infraestrutura contra acesso não autorizado
- **Troubleshooting**: Diagnosticar e resolver problemas de segurança

---

## Arquitetura de Computadores

### Modelo de Von Neumann

A maioria dos computadores modernos segue a arquitetura de Von Neumann, proposta por John von Neumann em 1945.

```
┌─────────────────────────────────────────────┐
│          ARQUITETURA VON NEUMANN            │
├─────────────────────────────────────────────┤
│                                             │
│  ┌──────────┐    ┌──────────┐              │
│  │ Memória  │◄───┤   CPU    │              │
│  │          │    │          │              │
│  └──────────┘    └──────────┘              │
│        ▲              ▲                    │
│        └──────┬───────┘                    │
│               │                            │
│        ┌──────────────┐                    │
│        │ Dispositivos │                    │
│        │    E/S       │                    │
│        └──────────────┘                    │
│                                             │
└─────────────────────────────────────────────┘
```

### Componentes Principais

| Componente | Função | Importância em Segurança |
|-----------|--------|--------------------------|
| **CPU** | Executa instruções | Alvo para exploração de vulnerabilidades |
| **Memória RAM** | Armazena dados temporariamente | Análise de malware em tempo real |
| **Disco Rígido** | Armazenamento permanente | Recuperação de dados apagados |
| **Placa-Mãe** | Interconecta todos os componentes | Vulnerabilidades de firmware |
| **Fonte de Alimentação** | Fornece energia | Ataques side-channel |

### Ciclo de Execução (Fetch-Decode-Execute)

```
1. FETCH (Buscar)
   └─> CPU busca instrução da memória

2. DECODE (Decodificar)
   └─> CPU interpreta a instrução

3. EXECUTE (Executar)
   └─> CPU realiza a operação

4. STORE (Armazenar)
   └─> Resultado é armazenado na memória
```

---

## Componentes de Hardware Essenciais

### 1. CPU (Unidade Central de Processamento)

A CPU é o "cérebro" do computador, responsável por executar todas as operações.

**Características Técnicas:**

```
CPU
├── Núcleos (Cores)
│   ├── Processadores single-core
│   ├── Multi-core (2, 4, 8, 16+ núcleos)
│   └── Hyper-threading (threads virtuais)
│
├── Frequência (GHz)
│   ├── Base Clock (frequência padrão)
│   └── Boost Clock (frequência máxima)
│
├── Cache (Memória rápida)
│   ├── L1 Cache (2-64 KB por núcleo)
│   ├── L2 Cache (256 KB - 1 MB por núcleo)
│   └── L3 Cache (2-32 MB compartilhado)
│
└── Instruções
    ├── x86/x64 (Intel, AMD)
    ├── ARM (Mobile, Raspberry Pi)
    └── MIPS (Legacy systems)
```

**Fabricantes Principais:**
- Intel (Core i3/i5/i7/i9, Xeon)
- AMD (Ryzen, EPYC)
- ARM Holdings (Licenças para others)

### 2. Placa-Mãe (Motherboard)

A placa-mãe é o backbone que conecta todos os componentes.

**Componentes-Chave:**

| Componente | Descrição |
|-----------|-----------|
| **Chipset** | Controla comunicação entre CPU e outros componentes |
| **BIOS/UEFI** | Firmware que inicializa o computador |
| **Slots de RAM** | Conexões para módulos de memória |
| **Slots PCI/PCIe** | Extensões para placas adicionais |
| **Conectores SATA/NVMe** | Conexões para drives de armazenamento |
| **Conectores de Potência** | Recebem energia da fonte |

**Ameaças de Segurança:**
- Exploração de vulnerabilidades em BIOS/UEFI
- Rootkits de firmware
- Clonagem de BIOS por atacantes

### 3. RAM (Random Access Memory)

A RAM é a memória volátil (temporária) usada durante a execução.

**Características:**

```
RAM
├── Tipo
│   ├── DDR4 (2014-presente)
│   ├── DDR5 (2021+)
│   └── LPDDR (Low Power, para mobile)
│
├── Capacidade
│   ├── 4 GB (básico)
│   ├── 8 GB (padrão)
│   ├── 16 GB (recomendado para profissionais)
│   └── 32 GB+ (high-performance/servidores)
│
└── Velocidade
    ├── Medida em MHz/GHz
    ├── Latência (CAS Latency)
    └── Timing (exemplos: 16-18-18-38)
```

**Importância em Cybersecurity:**
- Análise de dumps de RAM para investigação forense
- Detecção de malware em memória
- Side-channel attacks explorando cache

### 4. Armazenamento (Storage)

**Disco Rígido (HDD):**
```
HDD
├── Mecanismo
│   ├── Pratos magnéticos
│   ├── Cabeçote de leitura/escrita
│   └── Motor
│
├── Velocidade
│   ├── 5,400 RPM (notebooks)
│   └── 7,200 RPM (desktops)
│
└── Capacidade: 1 TB - 16 TB
```

**Unidade de Estado Sólido (SSD):**
```
SSD
├── Tipo
│   ├── SATA (2.5", até 550 MB/s)
│   ├── NVMe (M.2, até 7.4 GB/s)
│   └── PCIe 4.0/5.0 (extremamente rápido)
│
├── Vantagens
│   ├── Sem partes móveis
│   ├── Mais rápido que HDD
│   └── Consome menos energia
│
└── Importância Forense
    ├── TRIM pode apagar dados
    ├── Wear-leveling afeta recuperação
    └── Criptografia integrada
```

---

## Sistema Binário e Dados Digitais

### Bits e Bytes

Um **bit** é a unidade fundamental de informação (0 ou 1). Um **byte** é composto de 8 bits.

**Conversão Rápida:**

| Unidade | Equivalente | Uso |
|--------|------------|-----|
| **Bit (b)** | 0 ou 1 | Unidade básica |
| **Byte (B)** | 8 bits | Armazena um caractere |
| **Kilobyte (KB)** | 1.024 B | Textos pequenos |
| **Megabyte (MB)** | 1.024 KB | Imagens, músicas curtas |
| **Gigabyte (GB)** | 1.024 MB | Filmes, aplicações |
| **Terabyte (TB)** | 1.024 GB | Grandes datasets |

### Sistema Binário

**Conversão de Decimal para Binário:**

```
Exemplo: 13 em decimal = ?

13 ÷ 2 = 6 resto 1
6 ÷ 2 = 3 resto 0
3 ÷ 2 = 1 resto 1
1 ÷ 2 = 0 resto 1

Lendo de baixo para cima: 1101 (binary)

Verificação: 1×8 + 1×4 + 0×2 + 1×1 = 13 ✓
```

**Conversão de Binário para Decimal:**

```
Exemplo: 11010 = ?

1×2⁴ + 1×2³ + 0×2² + 1×2¹ + 0×2⁰
= 1×16 + 1×8 + 0×4 + 1×2 + 0×1
= 16 + 8 + 2
= 26
```

### Sistema Hexadecimal

Hexadecimal (base 16) usa dígitos 0-9 e letras A-F.

**Conversão Hex para Decimal:**

```
Exemplo: 2F em hex = ?

2F₁₆ = 2×16¹ + 15×16⁰
     = 2×16 + 15×1
     = 32 + 15
     = 47 em decimal
```

**Tabela de Referência:**

| Decimal | Binário | Hexadecimal |
|---------|---------|-------------|
| 0 | 0000 | 0 |
| 10 | 1010 | A |
| 15 | 1111 | F |
| 16 | 10000 | 10 |
| 255 | 11111111 | FF |

### Representação de Dados

**Texto (ASCII):**
```
Letra 'A' = 65 em decimal = 01000001 em binário = 41 em hex

Exemplo de string "Hi":
H = 72 = 01001000
i = 105 = 01101001
```

**Imagens (Pixels):**
```
Cada pixel armazena informações de cor
RGB (Red, Green, Blue) - 3 bytes por pixel
Exemplo: Vermelho puro = RGB(255, 0, 0) = FF0000 em hex
```

---

## Processamento de Dados

### Operações Lógicas (Operadores Booleanos)

A CPU executa operações usando lógica booleana.

**AND (E):**
```
0 AND 0 = 0
0 AND 1 = 0
1 AND 0 = 0
1 AND 1 = 1
```

**OR (OU):**
```
0 OR 0 = 0
0 OR 1 = 1
1 OR 0 = 1
1 OR 1 = 1
```

**NOT (NÃO):**
```
NOT 0 = 1
NOT 1 = 0
```

**XOR (OU Exclusivo):**
```
0 XOR 0 = 0
0 XOR 1 = 1
1 XOR 0 = 1
1 XOR 1 = 0
```

### Tabela de Verdade Completa

| A | B | AND | OR | XOR | NOT A |
|---|---|-----|----|----|-------|
| 0 | 0 | 0 | 0 | 0 | 1 |
| 0 | 1 | 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 1 | 1 | 0 |
| 1 | 1 | 1 | 1 | 0 | 0 |

### Unidades de Processamento

**Fluxograma de Processamento:**

```
┌──────────────┐
│   Entrada    │
│  (Mouse,     │
│  Teclado)    │
└──────┬───────┘
       │
       ▼
┌──────────────────────┐
│   Processamento      │
│   (CPU executa       │
│   instruções)        │
└──────┬───────────────┘
       │
       ▼
┌──────────────┐
│   Saída      │
│  (Monitor,   │
│  Impressora) │
└──────────────┘
```

---

## Memória e Armazenamento

### Hierarquia de Memória

```
     VELOCIDADE ▲
                │
         1 ns   │  ┌─────────────────┐
                │  │  Registradores  │  (CPU)
         2 ns   │  │  (64-512 bytes)  │
                │  └─────────────────┘
       10-100 ns│  ┌─────────────────┐
                │  │   Cache L1/L2   │  (CPU)
     1-10 μs    │  │  (32 KB-8 MB)    │
                │  └─────────────────┘
    50-100 μs   │  ┌─────────────────┐
                │  │    RAM (DDR)     │  (Volátil)
        1 ms    │  │  (4-64 GB)       │
                │  └─────────────────┘
      10-100 ms │  ┌─────────────────┐
                │  │   SSD/HDD        │  (Permanente)
       1-10 s   │  │  (256 GB-16 TB)  │
                │  └─────────────────┘
                │
                └───────────────────► CAPACIDADE
```

### Diferenças Principais

| Aspecto | RAM | SSD | HDD |
|--------|-----|-----|-----|
| **Volatilidade** | Volátil (apaga com desligamento) | Não-volátil | Não-volátil |
| **Velocidade** | ~10 ns | ~100 μs | ~10 ms |
| **Capacidade Típica** | 8-64 GB | 256 GB-2 TB | 1-16 TB |
| **Custo por GB** | Caro | Médio | Barato |
| **Forense** | Difícil (apaga rapidamente) | Possível (TRIM complicado) | Mais fácil |

### BIOS vs UEFI

**BIOS (Basic Input/Output System):**
- Legado, lançado em 1981
- Limite de 2 TB por partição
- Inicialização mais lenta
- 16-bit

**UEFI (Unified Extensible Firmware Interface):**
- Moderno, lançado em 2005
- Suporta discos > 2 TB
- Inicialização mais rápida
- 32-bit / 64-bit
- Secure Boot para prevenir malware

---

## Periféricos e Interfaces

### Conectores Comuns

**USB (Universal Serial Bus):**
```
USB
├── USB 2.0 (480 Mbps)
├── USB 3.0 (5 Gbps)
├── USB 3.1 (10 Gbps)
└── USB-C (reversível, crescente adoção)

Riscos de Segurança:
├── BadUSB (malware em controladores)
├── USB drops (disposivos plantados em locais públicos)
└── Exfiltração de dados via USB não autorizado
```

**DisplayPort / HDMI:**
- Transferência de vídeo
- Recente: suporte a criptografia (HDCP)

**Ethernet (RJ45):**
- Conexão de rede com fio
- 10/100/1000 Mbps / 10 Gbps

**Áudio:**
- Jack 3.5mm (analógico)
- Conectores XLR (profissional)

### Dispositivos de Entrada

| Dispositivo | Função | Aplicação Forense |
|------------|--------|------------------|
| **Teclado** | Entrada de texto | Keystroke logging |
| **Mouse** | Movimento/click | Rastreamento de atividade |
| **Scanner** | Digitalização | Detecção de documentos |
| **Câmera** | Captura de vídeo | Vigilância, malware |

### Dispositivos de Saída

| Dispositivo | Função | Risco de Segurança |
|------------|--------|-------------------|
| **Monitor** | Exibição visual | Screen capture (malware) |
| **Impressora** | Impressão em papel | Memory (Hard disk) contém cópias |
| **Alto-falante** | Saída de áudio | Malware com síntese de fala |
| **Projetor** | Apresentações | Não recomendado para dados sensíveis |

---

## Energia e Termodinâmica

### Fonte de Alimentação (Power Supply Unit - PSU)

**Características:**

```
PSU
├── Wattagem
│   ├── Mínima: 300W (office basic)
│   ├── Padrão: 650W (desktop gamer)
│   └── Máxima: 1500W+ (servidores)
│
├── Eficiência
│   ├── Bronze (80%)
│   ├── Silver (85%)
│   ├── Gold (90%)
│   └── Platinum (92%+)
│
└── Conectores
    ├── ATX 24-pin (placa-mãe)
    ├── 8-pin/4-pin (CPU)
    └── SATA/PCIe 6-pin (periféricos)
```

### Gerenciamento Térmico

**Componentes Quentes:**

```
CPU
├── Operação Normal: 30-60°C
├── Sob Carga: 60-85°C
└── Limite Crítico: 100°C+ (throttling)

GPU
├── Operação Normal: 40-60°C
├── Sob Carga: 75-90°C
└── Limite Crítico: 95°C+ (desligamento)
```

**Métodos de Resfriamento:**

| Método | Descrição | Eficácia |
|--------|-----------|---------|
| **Ar Passivo** | Sem ventilação ativa | Baixa |
| **Ar Ativo** | Ventiladores | Média |
| **Líquido** | Refrigeração a água | Alta |
| **Peltier** | Módulo termoelétrico | Muito alta (cara) |

### Segurança em Energia

**Ataques side-channel:** Análise de consumo de energia pode revelar informações criptográficas.

**Power Analysis Attack:**
```
Monitorar corrente elétrica durante operações
┌─────────────────────────────────┐
│ Bit 0 processado = pico menor   │
│ Bit 1 processado = pico maior   │
└─────────────────────────────────┘

Analisando padrões, atacantes podem deduzir chaves
```

---

## Segurança em Hardware

### Vulnerabilidades Comuns

**1. Rootkits de Firmware:**
```
BIOS/UEFI Rootkit
└─> Persiste através de reinicializações
└─> Difícil de detectar
└─> Acesso de kernel
```

**2. Cold Boot Attack:**
```
Procedimento:
1. Sistema ligado, RAM contém dados sensíveis
2. Atacante desliga abruptamente
3. RAM retém dados por alguns segundos
4. Dados são transferidos para outro sistema
5. Informações como senhas/chaves podem ser recuperadas

Proteção: Criptografia de disco, DRAM scrambling
```

**3. Side-Channel Attacks:**
```
Tipos:
├── Timing attacks
├── Power analysis
├── Electromagnetic emanation
└── Acoustic cryptanalysis
```

### Mitigações

**Secure Boot:**
- Valida integridade de bootloader
- Previne execução de código não autorizado

**TPM (Trusted Platform Module):**
- Chip dedicado a segurança
- Armazena chaves de criptografia
- Suporta BitLocker e FileVault

**Encriptação de Hardware:**
- SSD com criptografia integrada
- Requer apenas senha

**Isolamento de Segurança:**
- Intel SGX
- AMD SEV
- ARM TrustZone

---

## Conceitos-Chave para Lembrar

1. **Arquitetura Von Neumann**: CPU, Memória e Dispositivos E/S
2. **CPU**: Responsável por todas computações; medida em cores, frequência e cache
3. **RAM**: Memória temporária, volátil e essencial para forense
4. **SSD vs HDD**: SSDs mais rápidos; HDDs maior capacidade
5. **Sistema Binário**: Todos dados são sequências de 0s e 1s
6. **Operações Lógicas**: AND, OR, NOT, XOR formam base do processamento
7. **Hierarquia de Memória**: Registradores > Cache > RAM > SSD/HDD em velocidade
8. **BIOS/UEFI**: Firmware essencial; vulnerabilidades levam a rootkits
9. **Periféricos**: USB, Ethernet, etc.; pontos de entrada para malware
10. **Gerenciamento Térmico**: Temperatura crítica afeta performance
11. **Side-Channel Attacks**: Consumo de energia, timing revelam informações
12. **TPM**: Chip de segurança essencial para criptografia de disco
13. **Cold Boot Attack**: Dados em RAM recuperáveis após desligamento
14. **Supply Chain Security**: Hardware malicioso pode ser inserido durante fabricação
15. **Defesa em Profundidade**: Múltiplas camadas (firmware, SO, aplicação) necessárias

---

## 🚀 Próximos Passos no Pre Security Path

### Sequência de Aprendizagem
1. **Consolidar Hardware:** Revisa os conceitos de CPU, RAM e armazenamento — fundamentais para entender o SO
2. **Aprender Sistemas Operativos:** Operating Systems Basics — como o hardware é gerenciado pelo SO
3. **Explorar Software:** Software Basics — entender linguagens de programação e SQL
4. **Estudar Segurança Avançada:** Attacks and Defenses — aplicar conhecimento a vulnerabilidades reais

### Prática Recomendada
- **Inspeção de Hardware:** Usar `CPU-Z`, `GPU-Z`, ou `hwinfo` para analisar especificações do teu computador
- **Análise de Memória:** Ferramentas como `Rammap` para ver alocação de RAM
- **Monitorização Térmica:** Usar `HWMonitor` para verificar temperaturas dos componentes
- **Exercícios TryHackMe:** Fazer os testes de conhecimento de hardware

### Tópicos de Interesse Posterior
- **Advanced Micro Architecture:** Exploração de side-channels (Spectre, Meltdown)
- **Firmware Security:** UEFI rootkits e ataques de firmware
- **Physical Security:** Ataques físicos a componentes
- **Reverse Engineering:** Análise de componentes eletrônicos

---

## 🔖 Tags

#cybersecurity #hardware #presecurity #tryhackme #cpu #ram #storage #firmware #bios #security #ssd #hdd #vulnerabilities

---

_Notas criadas para o TryHackMe Pre Security Path — Computer Fundamentals_  
_Formatado para Obsidian_
