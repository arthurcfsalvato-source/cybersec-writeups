# 🌐 Network Fundamentals — Pre Security Path (TryHackMe)

> **Caminho:** Pre Security → Network Fundamentals  
> **Objetivo:** Entender como as redes funcionam, desde o básico até os protocolos que usamos todos os dias.

---

## 📚 Índice

- #O que é uma Rede?
- #O que é a Internet?
- #Identificando Dispositivos na Rede
- #Ping — Testando a Conexão
- #Introdução ao LAN
- #Topologias de Rede
- #Subnetting
- #O Modelo OSI
- #O Modelo TCP/IP
- #Pacotes e Frames
- #UDP vs TCP
- #Portas e Protocolos
- #Como funciona a Internet — DNS, HTTP, etc.

---

## 🔗 Navegação Inteligente

### Sequencial
- **← Anterior:** 1) Introduction to Cyber Security (Fundamentos, Carreiras)
- **Próximo →:** 3) How The Web Works (DNS e HTTP detalhado)






---

## 🔌 O que é uma Rede?

Uma **rede** é simplesmente um conjunto de dispositivos conectados entre si para poderem **comunicar e partilhar recursos**.

Pensa assim: quando o teu telemóvel se liga ao Wi-Fi de casa, ele entra numa rede. Quando abres o browser e acedes a um site, o teu telemóvel está a comunicar com um servidor que está noutra rede — algures no mundo.

### Exemplos de redes no dia a dia:

- A rede de casa (router + telemóvel + PC + smart TV)
- A rede da escola ou empresa
- A própria Internet (uma rede de redes gigante)

---

## 🌍 O que é a Internet?

A **Internet** não é uma coisa física num único lugar — é uma **rede de redes** interligadas por todo o mundo.

Existem dois tipos principais de redes:

|Tipo|Nome completo|O que é|
|---|---|---|
|**LAN**|Local Area Network|Rede pequena — a tua casa, escritório, escola|
|**WAN**|Wide Area Network|Rede grande — liga várias LANs; a Internet é o maior exemplo de WAN|

### Como surgiu a Internet?

A Internet nasceu nos anos 60 como **ARPANET**, um projeto do governo americano para conectar computadores de universidades. Com o tempo, cresceu e tornou-se a Internet que conhecemos hoje.

---

## 🪪 Identificando Dispositivos na Rede

Para que os dispositivos numa rede comuniquem, cada um precisa de ter um **endereço único** — tal como uma morada de casa.

Existem dois tipos principais de endereços:

---

### 🔷 Endereço IP (Internet Protocol)

O **IP** é como a morada temporária de um dispositivo na rede. Pode mudar.

Existem duas versões:

#### IPv4

- Formato: **4 grupos de números separados por pontos**
- Exemplo: `192.168.1.1`
- Cada grupo vai de 0 a 255
- Total de endereços possíveis: ~4,3 mil milhões (já estão quase todos usados!)

#### IPv6

- Criado porque os endereços IPv4 acabaram
- Formato: **8 grupos de 4 caracteres hexadecimais separados por dois pontos**
- Exemplo: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`
- Total de endereços: praticamente ilimitados

#### Tipos de endereço IP:

- **IP Público** — o endereço que o mundo vê. É o endereço do teu router na Internet. É único no mundo.
- **IP Privado** — o endereço interno da tua rede. Só existe dentro da tua LAN. Pode repetir em redes diferentes.

**Exemplos de IPs privados (reservados):**

```
10.0.0.0    – 10.255.255.255
172.16.0.0  – 172.31.255.255
192.168.0.0 – 192.168.255.255
```

> 💡 Quando acedes a um site, o site vê o teu **IP público** (do router), não o teu IP privado.

---

### 🔶 Endereço MAC (Media Access Control)

O **MAC** é como o número de série físico de uma placa de rede. É permanente (ou quase).

- Formato: **6 pares de caracteres hexadecimais separados por dois pontos**
- Exemplo: `a4:c3:f0:85:ac:2d`
- Os **primeiros 3 pares** identificam o fabricante (ex: Apple, Samsung, Intel)
- Os **últimos 3 pares** identificam o dispositivo específico

> ⚠️ O endereço MAC pode ser falsificado (spoofed) por software — é uma técnica usada em ataques de rede.

**Diferença simples entre IP e MAC:**

|Característica|IP|MAC|
|---|---|---|
|Permanência|Temporário (pode mudar)|Permanente (hardware)|
|Scope|Local ou global|Só na rede local|
|Camada OSI|Camada 3 (Rede)|Camada 2 (Enlace)|

---

## 📡 Ping — Testando a Conexão

O **ping** é uma das ferramentas mais simples e úteis em redes. Serve para verificar se um dispositivo está **acessível** e medir o **tempo de resposta**.

### Como funciona?

O ping envia pacotes **ICMP Echo Request** para um destino. Se o destino estiver ativo, responde com **ICMP Echo Reply**.

### Uso básico:

```bash
ping google.com
ping 192.168.1.1
```

### O que o output significa:

```
PING google.com (142.250.74.46): 56 bytes de dados
64 bytes de 142.250.74.46: icmp_seq=0 ttl=118 time=14.2 ms
```

|Campo|Significado|
|---|---|
|`bytes`|Tamanho do pacote enviado|
|`icmp_seq`|Número de sequência do pacote|
|`ttl`|Time To Live — quantos "saltos" o pacote ainda pode dar|
|`time`|Tempo de resposta em milissegundos (ms)|

> 💡 Quanto menor o `time`, mais rápida é a conexão com aquele destino.

---

## 🏠 Introdução ao LAN

**LAN = Local Area Network** = Rede Local

É a rede que existe dentro de um espaço físico limitado — a tua casa, um escritório, uma escola.

### Componentes típicos de uma LAN:

#### 🔁 Switch

- Liga **múltiplos dispositivos** dentro da mesma rede
- É mais inteligente que um hub — sabe para qual dispositivo enviar cada pacote (usando a tabela MAC)
- Opera na **Camada 2** do modelo OSI
- Exemplo: o switch de rede num escritório que liga 20 computadores

#### 📡 Router

- Liga **redes diferentes** entre si (ex: a tua LAN com a Internet)
- Decide o melhor caminho para os pacotes chegarem ao destino (**routing**)
- Opera na **Camada 3** do modelo OSI
- Tem um IP público (para a Internet) e um IP privado (para a LAN)

> **Switch** = liga dispositivos dentro da mesma rede  
> **Router** = liga redes diferentes entre si

---

## 🗺️ Topologias de Rede

A **topologia** é a forma como os dispositivos estão organizados e conectados na rede.

---

### ⭐ Topologia em Estrela (Star)

```
     PC1
      |
PC2—Switch—PC3
      |
     PC4
```

- Todos os dispositivos ligam a um ponto central (switch ou hub)
- **Vantagem:** Se um cabo falha, só aquele dispositivo é afetado
- **Desvantagem:** Se o switch central falha, toda a rede cai
- É a topologia **mais comum** em redes modernas

---

### 🚌 Topologia em Barramento (Bus)

```
PC1—PC2—PC3—PC4—PC5
```

- Todos os dispositivos partilham o mesmo cabo (backbone)
- **Vantagem:** Fácil e barata de instalar
- **Desvantagem:** Se o cabo principal falha, tudo para; muito lenta com muitos dispositivos
- Pouco usada hoje em dia

---

### 💍 Topologia em Anel (Ring)

```
PC1 → PC2 → PC3 → PC4 → PC1
```

- Os dados circulam num único sentido, passando por cada dispositivo
- **Vantagem:** Previsível e fácil de identificar falhas
- **Desvantagem:** Se um dispositivo falha, pode quebrar o anel todo

---

### 🕸️ Topologia em Malha (Mesh)

- Cada dispositivo está ligado a **vários outros** diretamente
- **Vantagem:** Muito redundante — se uma ligação cai, existem outras rotas
- **Desvantagem:** Cara e complexa de instalar
- Usada em infraestruturas críticas e na backbone da Internet

---

## 🧮 Subnetting

**Subnetting** = dividir uma rede grande em sub-redes menores.

### Porquê fazer subnetting?

- Organizar a rede (ex: separar o departamento de RH do de TI)
- Melhorar a segurança (isolar grupos de dispositivos)
- Usar os IPs de forma mais eficiente

### Conceitos fundamentais:

#### Máscara de Sub-rede (Subnet Mask)

A máscara indica qual parte do IP é a **rede** e qual é o **host** (dispositivo).

|Máscara|CIDR|Hosts disponíveis|
|---|---|---|
|255.255.255.0|/24|254 hosts|
|255.255.0.0|/16|65.534 hosts|
|255.0.0.0|/8|16.777.214 hosts|
|255.255.255.128|/25|126 hosts|

#### Exemplo prático:

- IP: `192.168.1.0/24`
- Máscara: `255.255.255.0`
- Endereço de rede: `192.168.1.0` (não se atribui a dispositivos)
- Endereço de broadcast: `192.168.1.255` (não se atribui a dispositivos)
- Hosts disponíveis: `192.168.1.1` até `192.168.1.254` = **254 dispositivos**

#### Notação CIDR

Em vez de escrever a máscara completa, usa-se uma barra com o número de bits da rede:

- `/24` = 255.255.255.0 (os primeiros 24 bits são da rede)
- `/16` = 255.255.0.0
- `/8` = 255.0.0.0

---

## 📦 O Modelo OSI

O **modelo OSI** (Open Systems Interconnection) é um modelo conceptual que divide a comunicação em rede em **7 camadas**. Cada camada tem uma função específica.

> 💡 **Mnemónica para lembrar as camadas (de baixo para cima):**  
> **P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way  
> Physical → Data Link → Network → Transport → Session → Presentation → Application

---

### Camada 7 — Aplicação (Application)

- É a camada com que os **utilizadores interagem diretamente**
- Fornece serviços de rede às aplicações
- **Exemplos:** HTTP (web), FTP (transferência de ficheiros), SMTP (email), DNS

---

### Camada 6 — Apresentação (Presentation)

- **Traduz** os dados para um formato que a aplicação consiga entender
- Trata de **encriptação, compressão e formatação**
- Exemplos: SSL/TLS (encriptação HTTPS), JPEG, MP4

---

### Camada 5 — Sessão (Session)

- **Gere as sessões** de comunicação entre dispositivos
- Abre, mantém e fecha ligações
- Exemplo: quando fazes login num site, é a camada de sessão que mantém a tua sessão ativa enquanto navegas

---

### Camada 4 — Transporte (Transport)

- Responsável pela **entrega de dados** entre aplicações
- Divide os dados em **segmentos**
- Escolhe o protocolo: **TCP** (fiável) ou **UDP** (rápido)
- Usa **portas** para identificar a aplicação destino (ex: porta 80 para HTTP)

---

### Camada 3 — Rede (Network)

- Responsável pelo **endereçamento lógico** e **routing**
- Usa **endereços IP** para determinar o caminho dos pacotes
- Dispositivo desta camada: **Router**
- Protocolo principal: **IP (Internet Protocol)**

---

### Camada 2 — Enlace de Dados (Data Link)

- Responsável pela **transmissão entre dispositivos na mesma rede**
- Usa **endereços MAC** para identificar dispositivos
- Divide os dados em **frames**
- Dispositivo desta camada: **Switch**
- Deteta erros na transmissão

---

### Camada 1 — Física (Physical)

- É o **hardware físico** — cabos, sinais elétricos, ondas de rádio
- Transmite **bits (0s e 1s)** pelo meio físico
- Exemplos: cabo Ethernet, fibra ótica, Wi-Fi (ondas de rádio)

---

### Resumo Visual do Modelo OSI:

```
┌─────────────────────────────────────────────────────┐
│  7. Aplicação     │ HTTP, FTP, DNS, SMTP            │
├─────────────────────────────────────────────────────┤
│  6. Apresentação  │ SSL/TLS, JPEG, encriptação      │
├─────────────────────────────────────────────────────┤
│  5. Sessão        │ Gestão de sessões               │
├─────────────────────────────────────────────────────┤
│  4. Transporte    │ TCP, UDP, Portas                │
├─────────────────────────────────────────────────────┤
│  3. Rede          │ IP, Routing, Routers            │
├─────────────────────────────────────────────────────┤
│  2. Enlace        │ MAC, Frames, Switches           │
├─────────────────────────────────────────────────────┤
│  1. Física        │ Cabos, sinais, bits             │
└─────────────────────────────────────────────────────┘
```

> 💡 Quando os dados **saem** do teu computador, descem do nível 7 para o 1. Quando **chegam** a outro computador, sobem do nível 1 para o 7.

---

### Encapsulamento e Desencapsulamento

**Encapsulamento** = cada camada **adiciona o seu cabeçalho** aos dados ao descerem as camadas.

```
Dados → Segmento (+ cabeçalho Transporte) → Pacote (+ cabeçalho Rede) → Frame (+ cabeçalho Enlace) → Bits
```

**Desencapsulamento** = o processo inverso — cada camada **remove o seu cabeçalho** ao receberem os dados.

---

## 🌐 O Modelo TCP/IP

O modelo **TCP/IP** é o modelo **prático** usado na Internet real. É mais simples que o OSI — tem apenas **4 camadas**.

|Camada TCP/IP|Equivalente OSI|Protocolos|
|---|---|---|
|Aplicação|5, 6, 7|HTTP, FTP, DNS, SMTP|
|Transporte|4|TCP, UDP|
|Internet|3|IP, ICMP|
|Acesso à Rede|1, 2|Ethernet, Wi-Fi|

> 💡 Na prática, o modelo TCP/IP é o que realmente é usado. O OSI é mais usado para **aprender e entender conceitos**.

---

## 📬 Pacotes e Frames

### O que é um Pacote?

Um **pacote** é uma unidade de dados que viaja pela rede. Quando envias uma mensagem ou acedes a um site, os dados são divididos em pacotes pequenos, enviados separadamente e remontados no destino.

**Estrutura de um pacote IP:**

```
┌──────────────────────────────────────┐
│ Cabeçalho IP                         │
│  - IP de origem                      │
│  - IP de destino                     │
│  - TTL (Time To Live)                │
│  - Protocolo (TCP/UDP)               │
├──────────────────────────────────────┤
│ Dados (payload)                      │
└──────────────────────────────────────┘
```

### O que é um Frame?

Um **frame** é o pacote já "embrulhado" com informação da **Camada 2** (endereços MAC) para ser transmitido na rede local.

```
┌──────────────┬───────────┬──────────────────┬──────────┐
│ MAC destino  │ MAC origem│ Pacote IP (dados) │ Checksum │
└──────────────┴───────────┴──────────────────┴──────────┘
```

### TTL (Time To Live)

- O **TTL** é um número que indica quantos **routers** (saltos/hops) o pacote ainda pode atravessar
- Cada vez que passa por um router, o TTL é **decrementado em 1**
- Quando chega a 0, o pacote é **descartado** (para evitar loops infinitos)
- Valores típicos: Linux = 64, Windows = 128, Cisco = 255

---

## ⚡ UDP vs TCP

São os dois protocolos principais da camada de Transporte. Têm propósitos diferentes.

---

### 🔵 TCP (Transmission Control Protocol)

O TCP é **fiável** — garante que todos os dados chegam, na ordem correta.

**Características:**

- Orientado à ligação (é preciso estabelecer ligação antes de enviar dados)
- Garante entrega dos dados
- Verifica erros
- Reordena pacotes que chegam fora de ordem
- Mais lento que UDP

**Quando usar TCP:**

- Download de ficheiros
- Email
- Páginas web (HTTP/HTTPS)
- Qualquer coisa onde perder dados seria problemático

#### O Three-Way Handshake (Aperto de Mão de 3 Vias)

Antes de transmitir dados, o TCP estabelece a ligação com 3 passos:

```
Cliente                    Servidor
   |                           |
   |──── SYN ─────────────────►|  "Posso conectar?"
   |                           |
   |◄─── SYN-ACK ─────────────|  "Sim, podes!"
   |                           |
   |──── ACK ─────────────────►|  "Ótimo, ligado!"
   |                           |
   |====== Dados ============= |  Agora trocam dados
```

- **SYN** = Synchronize (pedido de ligação)
- **ACK** = Acknowledge (confirmação)

#### Encerramento da ligação (Four-Way):

```
Cliente ──── FIN ────► Servidor    "Quero terminar"
Cliente ◄─── ACK ──── Servidor    "Ok, recebi"
Cliente ◄─── FIN ──── Servidor    "Eu também termino"
Cliente ──── ACK ────► Servidor   "Confirmado, adeus"
```

---

### 🔴 UDP (User Datagram Protocol)

O UDP é **rápido mas não fiável** — envia dados sem verificar se chegaram.

**Características:**

- Sem ligação (envia sem estabelecer conexão prévia)
- Não garante entrega
- Sem verificação de ordem
- Muito mais rápido que TCP

**Quando usar UDP:**

- Streaming de vídeo/música (um frame perdido não importa muito)
- Jogos online (velocidade é mais importante que perfeição)
- DNS (perguntas rápidas e simples)
- VoIP (chamadas de voz)

---

### Comparação TCP vs UDP:

|Característica|TCP|UDP|
|---|---|---|
|Fiabilidade|✅ Garantida|❌ Não garantida|
|Velocidade|🐢 Mais lento|🐇 Mais rápido|
|Ligação|Orientado à ligação|Sem ligação|
|Ordem dos pacotes|✅ Garantida|❌ Não garantida|
|Uso típico|Web, Email, FTP|Streaming, Jogos, DNS|

---

## 🚪 Portas e Protocolos

As **portas** são como "portas de entrada" num computador. Permitem que um computador tenha **múltiplos serviços** a funcionar ao mesmo tempo, identificando para qual serviço cada pacote deve ir.

- Intervalo total: **0 a 65535**
- **Portas 0–1023**: Portas conhecidas (Well-Known) — reservadas para serviços padrão
- **Portas 1024–49151**: Registadas — usadas por aplicações específicas
- **Portas 49152–65535**: Dinâmicas/Privadas — usadas temporariamente pelo sistema

### Portas Mais Importantes (obrigatório saber! 🧠):

|Porta|Protocolo|Serviço|Para que serve|
|---|---|---|---|
|21|TCP|FTP|Transferência de ficheiros|
|22|TCP|SSH|Acesso remoto seguro|
|23|TCP|Telnet|Acesso remoto (inseguro, não usar)|
|25|TCP|SMTP|Envio de email|
|53|TCP/UDP|DNS|Resolução de nomes de domínio|
|80|TCP|HTTP|Páginas web (sem encriptação)|
|110|TCP|POP3|Receber email|
|143|TCP|IMAP|Receber email (mais avançado)|
|443|TCP|HTTPS|Páginas web (com encriptação SSL/TLS)|
|3306|TCP|MySQL|Base de dados MySQL|
|3389|TCP|RDP|Ambiente de trabalho remoto (Windows)|

> 💡 Em cibersegurança, saber as portas de cor é essencial — ferramentas como o `nmap` usam este conhecimento para descobrir serviços ativos num servidor.

---

## 🌍 Como Funciona a Internet (DNS, HTTP, etc.)

### 🔍 DNS — Domain Name System

O **DNS** é como a "agenda telefónica" da Internet. Traduz nomes de domínio (legíveis por humanos) em endereços IP (legíveis por máquinas).

**Exemplo:**

```
Escreves:  www.google.com
DNS diz:   142.250.74.46
Browser usa: 142.250.74.46
```

#### Como funciona uma consulta DNS:

```
1. Escreves "tryhackme.com" no browser
2. O teu PC pergunta ao DNS Resolver (normalmente o teu ISP)
3. O Resolver pergunta ao Root Name Server (sabe quem gere ".com")
4. Root Server aponta para o TLD Server (.com)
5. TLD Server aponta para o Authoritative Server (sabe o IP de tryhackme.com)
6. Resposta volta: "tryhackme.com = 104.22.55.228"
7. O teu browser conecta ao IP 104.22.55.228
```

#### Tipos de registos DNS:

|Tipo|Para que serve|Exemplo|
|---|---|---|
|**A**|Mapeia domínio → IPv4|`tryhackme.com → 104.22.55.228`|
|**AAAA**|Mapeia domínio → IPv6|`tryhackme.com → 2606:4700::...`|
|**CNAME**|Alias (aponta para outro domínio)|`www → tryhackme.com`|
|**MX**|Servidor de email|`mail.tryhackme.com`|
|**TXT**|Texto genérico|Verificação de domínio, SPF|

#### Cache DNS:

- Para ser mais rápido, o teu PC **guarda temporariamente** as respostas DNS
- O tempo que ficam guardadas chama-se **TTL** (Time To Live)
- Podes limpar a cache DNS:
    - Windows: `ipconfig /flushdns`
    - Linux/Mac: `sudo systemd-resolve --flush-caches`

---

### 🌐 HTTP e HTTPS

**HTTP** (HyperText Transfer Protocol) é o protocolo que o browser usa para **pedir e receber páginas web**.

**HTTPS** = HTTP + **SSL/TLS** (encriptação) → os dados viajam cifrados, ninguém no meio pode ler.

#### Métodos HTTP (como o browser "fala" com o servidor):

|Método|Uso|
|---|---|
|**GET**|Pedir um recurso (abrir uma página)|
|**POST**|Enviar dados (preencher um formulário, fazer login)|
|**PUT**|Atualizar um recurso|
|**DELETE**|Apagar um recurso|

#### Códigos de Resposta HTTP:

|Código|Significado|
|---|---|
|**200**|OK — tudo correu bem|
|**301**|Redirect Permanente — a página mudou de endereço|
|**302**|Redirect Temporário|
|**404**|Not Found — a página não existe|
|**403**|Forbidden — não tens permissão|
|**500**|Internal Server Error — erro no servidor|

---

### 🔒 DHCP — Dynamic Host Configuration Protocol

O **DHCP** é o protocolo que **atribui automaticamente** um endereço IP ao teu dispositivo quando entras numa rede.

**Processo DORA:**

```
1. Discover  — O teu PC grita "Há algum servidor DHCP aqui?"
2. Offer     — O servidor responde "Sim! Podes usar o IP 192.168.1.50"
3. Request   — O teu PC diz "Obrigado, quero esse IP"
4. Acknowledge — O servidor confirma "É teu! Por 24 horas."
```

Sem DHCP, terias de configurar manualmente o IP de cada dispositivo na rede.

---

### 🛤️ ARP — Address Resolution Protocol

O **ARP** resolve um problema: tens o IP de destino, mas precisas do MAC para enviar o frame na rede local.

**Como funciona:**

```
PC A (192.168.1.10) quer falar com PC B (192.168.1.20)

1. PC A faz broadcast: "Quem tem o IP 192.168.1.20? Diz-me o teu MAC!"
2. PC B responde: "Sou eu! O meu MAC é aa:bb:cc:dd:ee:ff"
3. PC A guarda na ARP Cache e envia o frame
```

**Ver a ARP Cache:**

```bash
arp -a        # Windows/Linux/Mac
```

---

## 🧰 Comandos Úteis de Rede

```bash
# Ver o teu IP
ipconfig                 # Windows
ip a                     # Linux

# Testar conectividade
ping google.com

# Ver a rota dos pacotes até um destino
tracert google.com       # Windows
traceroute google.com    # Linux

# Consultar DNS
nslookup tryhackme.com
dig tryhackme.com

# Ver portas abertas e conexões ativas
netstat -an

# Ver a tabela ARP
arp -a

# Limpar cache DNS (Windows)
ipconfig /flushdns
```

---

## 🗝️ Conceitos Chave para Lembrar

> [!important] Resumo dos Conceitos Mais Importantes
> 
> - **IP** = endereço lógico (pode mudar) | **MAC** = endereço físico (permanente)
> - **Switch** = liga dispositivos na mesma rede | **Router** = liga redes diferentes
> - **TCP** = fiável e lento | **UDP** = rápido mas sem garantias
> - **DNS** = converte nomes em IPs
> - **DHCP** = distribui IPs automaticamente
> - **ARP** = descobre o MAC a partir do IP
> - **HTTP porta 80** | **HTTPS porta 443** | **SSH porta 22** | **FTP porta 21**
> - Modelo OSI tem **7 camadas** | Modelo TCP/IP tem **4 camadas**
> - **Three-Way Handshake TCP**: SYN → SYN-ACK → ACK

---

## 🚀 Proximos Passos

**Aprendizado Sequencial:**
1. **Revise esta nota** — Foque em OSI e TCP/UDP
2

**Pratica Sugerida:**
- Use `ping` em diferentes hosts
- Teste `traceroute` para ver rota de pacotes
- Experimente `nslookup` com domínios
- Analise com `netstat -an` as conexões ativas

---

## 🔗 Tags

#cybersecurity #networking #presecurity #tryhackme #fundamentals #tcp-ip #osi #dns #http #subnetting #protoclos #portas

---

_Notas criadas para o TryHackMe Pre Security Path — Network Fundamentals_  
_Formatado para Obsidian_ 🗒️