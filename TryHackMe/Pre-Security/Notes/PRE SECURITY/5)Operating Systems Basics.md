# Operating Systems Basics

---

## 🔗 Navegação Inteligente

### Sequencial
- **← Anterior:** 4) Computer Fundamentals (CPU, RAM, Arquitetura)
- **Próximo →:** 6) Software Basics (Python, JavaScript, SQL)
- **Depois:** 7) Attacks and Defenses (Segurança avançada)
- **Início:** 1) Introduction to Cyber Security (Conceitos básicos)

### Tópicos Relacionados Nesta Nota
- **Kernel & Privilégios:** Ver em 7) Attacks and Defenses — Privilege Escalation
- **Firewall & IDS/IPS:** Ver em 2) Network Fundamentals — Firewalls
- **SSH & Criptografia:** Ver em 3) How The Web Works — Segurança Web
- **Autenticação & Controlo de Acesso:** Ver em 1) Introduction to Cyber Security — Controlo de Acesso
- **Forense Digital:** Ver em 1) Introduction to Cyber Security — DFIR

### Referencias Rapidas
- **⚡ Quick Reference** — Comandos Linux, PowerShell, permissões
- **🔑 Conceitos-Chave** — Mapa tematico (SO, segurança)

---

## Índice
1. [Introdução aos Sistemas Operacionais](#introdução)
2. [O que é um Sistema Operacional?](#o-que-é-um-so)
3. [Kernel e Espaço de Usuário](#kernel)
4. [Processos vs Threads](#processos-vs-threads)
5. [Windows: Conceitos Fundamentais](#windows)
6. [Linux: Conceitos Fundamentais](#linux)
7. [Interface de Linha de Comando (CLI)](#cli)
8. [Segurança do Sistema Operacional](#segurança-so)
9. [Conceitos-Chave para Lembrar](#conceitos-chave)

---

## <a name="introdução"></a>Introdução aos Sistemas Operacionais

Um Sistema Operacional (SO) é o software fundamental que permite a comunicação entre o usuário e o hardware do computador. Ele gerencia todos os recursos disponíveis e coordena a execução de programas.

**Funções Principais:**
- Gerenciamento de memória
- Escalonamento de processos
- Gerenciamento de arquivos
- Controle de dispositivos periféricos
- Interface com o usuário
- Segurança e controle de acesso

Os sistemas operacionais mais populares incluem:
- **Windows** (Microsoft)
- **macOS** (Apple)
- **Linux** (Open-source)
- **Unix** (Sistema base)

---

## <a name="o-que-é-um-so"></a>O que é um Sistema Operacional?

### Visão Geral da Arquitetura

```
┌──────────────────────────────────────────┐
│        Aplicações do Usuário             │
├──────────────────────────────────────────┤
│      Serviços do Sistema Operacional     │
│  - Gerenciamento de Memória              │
│  - Escalonamento de Processos            │
│  - Sistema de Arquivos                   │
│  - I/O de Dispositivos                   │
├──────────────────────────────────────────┤
│           Kernel (Núcleo)                │
├──────────────────────────────────────────┤
│      Hardware (CPU, RAM, Disco)          │
└──────────────────────────────────────────┘
```

### Responsabilidades Principais

| Responsabilidade | Descrição |
|---|---|
| **Gerenciamento de Recursos** | Aloca CPU, memória, disco para processos |
| **Escalonamento** | Determina qual processo usa a CPU e quando |
| **Sistema de Arquivos** | Organiza e gerencia dados no armazenamento |
| **Gerenciamento de I/O** | Controla comunicação com periféricos |
| **Segurança** | Protege dados e recursos contra acessos não autorizados |
| **Interface com Usuário** | GUI ou CLI para interação |

---

## <a name="kernel"></a>Kernel e Espaço de Usuário

### O que é o Kernel?

O **Kernel** é o núcleo do sistema operacional - o programa mais privilegiado que executa em modo protegido do processador. Ele tem acesso direto ao hardware.

### Modo Kernel vs Modo Usuário

```
┌─────────────────────────────────────┐
│     MODO KERNEL (Ring 0)            │
│  - Acesso total ao hardware         │
│  - Instruções privilegiadas         │
│  - Gerencia interrupções            │
│  - Máximo de privilégio             │
└─────────────────────────────────────┘
           ↑↓ Troca de Contexto
┌─────────────────────────────────────┐
│     MODO USUÁRIO (Ring 3)           │
│  - Acesso restrito                  │
│  - Instrução através de syscalls    │
│  - Isolamento de processos          │
│  - Mínimo de privilégio             │
└─────────────────────────────────────┘
```

### Chamadas de Sistema (Syscalls)

Quando um programa precisa acessar um recurso protegido (como ler um arquivo), ele faz uma **syscall**:

```
Aplicação (Modo Usuário)
    ↓
    Syscall: read("/etc/passwd", buffer, 1024)
    ↓
Kernel (Modo Kernel)
    ↓
    - Valida permissões
    - Acessa disco
    - Retorna dados
    ↓
Aplicação retorna (Modo Usuário)
```

### Exemplos de Syscalls Comuns

| Syscall | Propósito |
|---|---|
| `open()` | Abre arquivo |
| `read()` | Lê de arquivo ou dispositivo |
| `write()` | Escreve em arquivo ou dispositivo |
| `fork()` | Cria novo processo |
| `exit()` | Termina processo |
| `exec()` | Executa novo programa |
| `chmod()` | Muda permissões |

---

## <a name="processos-vs-threads"></a>Processos vs Threads

### O que é um Processo?

Um **processo** é uma instância de um programa em execução. Cada processo tem seus próprios recursos isolados.

**Características:**
- PID (Process ID) único
- Espaço de memória isolado
- Variáveis de ambiente próprias
- Descritores de arquivo independentes
- Estado próprio (executando, suspenso, etc.)

### O que é uma Thread?

Uma **thread** (thread de execução) é a menor unidade de processamento dentro de um processo. Múltiplas threads podem existir dentro de um único processo e compartilham recursos.

**Características:**
- TID (Thread ID) único
- Compartilha memória com outras threads
- Compartilha descritores de arquivo
- Tem seu próprio stack
- Executa sequências de instruções independentes

### Comparação Detalhada

| Aspecto | Processo | Thread |
|---|---|---|
| **Isolamento de Memória** | Espaço separado | Compartilhado |
| **Comunicação Inter** | IPC (complexo) | Memória compartilhada (fácil) |
| **Overhead de Criação** | Alto | Baixo |
| **Segurança** | Alto (isolado) | Menor (compartilhado) |
| **Sincronização** | Sistema operacional | Código da aplicação |
| **Exemplo de Uso** | Navegador (tab independente) | Navegador (mesmo tab, múltiplas threads) |

### Diagrama de Relação

```
┌─────────────────────────────────────────┐
│         PROCESSO A (Firefox)            │
├─────────────────────────────────────────┤
│  Thread 1 (Renderização)                │
│  Thread 2 (I/O de Rede)                 │
│  Thread 3 (Processamento DOM)           │
│  Memória Compartilhada (Heap)           │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│         PROCESSO B (Notepad)            │
├─────────────────────────────────────────┤
│  Thread 1 (Interface)                   │
│  Memória Compartilhada (Heap)           │
└─────────────────────────────────────────┘
```

### Exemplo em Python

```python
# Processo: Cada execução é independente
import subprocess

# Cria novo processo
p1 = subprocess.Popen(['python', 'script.py'])
p2 = subprocess.Popen(['python', 'script.py'])
# p1 e p2 têm PIDs diferentes, memória isolada

# Thread: Compartilha memória
import threading

shared_data = {'counter': 0}

def increment():
    shared_data['counter'] += 1  # Compartilhado!

t1 = threading.Thread(target=increment)
t2 = threading.Thread(target=increment)
# t1 e t2 acessam mesmo dicionário
```

---

## <a name="windows"></a>Windows: Conceitos Fundamentais

### Estrutura do Sistema de Arquivos

Windows utiliza o **NTFS** (New Technology File System) como principal sistema de arquivos moderno.

```
C:\
├── Users\
│   ├── Username\
│   │   ├── Desktop\
│   │   ├── Documents\
│   │   ├── Downloads\
│   │   ├── Pictures\
│   │   └── AppData\
│   │       ├── Local\
│   │       ├── LocalLow\
│   │       └── Roaming\
├── Windows\
│   ├── System32\
│   ├── SysWOW64\
│   ├── Temp\
│   └── Drivers\
├── Program Files\
├── Program Files (x86)\
└── ProgramData\
```

**Importantes:**
- `C:\Users\Username\AppData\` - Dados de aplicações (escondido)
- `C:\Windows\System32\` - Arquivos críticos do sistema
- `C:\Program Files\` - Programas instalados
- `C:\Windows\Temp\` - Arquivos temporários

### Task Manager (Gerenciador de Tarefas)

O **Task Manager** permite visualizar e gerenciar processos, serviços e performance.

```
┌──────────────────────────────────┐
│    Windows Task Manager          │
├──────────────────────────────────┤
│ Abas:                            │
│ • Processos - PIDs, Memória      │
│ • Performance - CPU, RAM, Disco  │
│ • Inicialização - Programas      │
│ • Serviços - Serviços do Windows │
│ • Detalhes - Informações avançadas
└──────────────────────────────────┘
```

**Como abrir:**
- `Ctrl+Shift+Esc` (direto)
- `Ctrl+Alt+Delete` → Task Manager
- Botão direito na barra de tarefas

### Windows Registry

O **Registry** é um banco de dados hierárquico que armazena configurações do Windows e aplicações.

```
HKEY_LOCAL_MACHINE (HKLM)
├── SOFTWARE
│   ├── Microsoft\Windows\
│   └── [Vendors]\[Applications]\
├── SYSTEM
│   ├── CurrentControlSet\Services\
│   └── ...
├── HARDWARE
└── SECURITY

HKEY_CURRENT_USER (HKCU)
├── Software
│   └── [Applications]\
├── Control Panel
└── ...
```

**Estrutura:**
- **Chave (Key)** - Pasta/Diretório
- **Valor (Value)** - Par chave-valor
- **Tipo de Dados** - REG_SZ (string), REG_DWORD (inteiro), etc.

**Acesso ao Registry:**
```powershell
# PowerShell
Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows"

# cmd (não recomendado)
regedit.exe
```

### Usuários e Permissões no Windows

#### Tipos de Contas

| Tipo | Privilégios | Uso |
|---|---|---|
| **Administrator** | Total | Configuração do sistema |
| **Standard User** | Limitado | Uso diário seguro |
| **Service Account** | Específicos | Serviços do sistema |
| **Guest** | Muito limitado | Acesso temporário |

#### ACL (Access Control List)

Windows usa **ACLs** para controlar acesso a arquivos e pastas:

```
┌──────────────────────────┐
│  C:\Users\Alice\Secret\  │
├──────────────────────────┤
│ ACL:                     │
│ • Alice: Full Control    │
│ • Admin: Full Control    │
│ • Bob: Nenhum acesso     │
└──────────────────────────┘
```

**Permissões Básicas:**
- Read (Ler)
- Write (Escrever)
- Modify (Modificar)
- Full Control (Controle Total)

**Visualizar permissões:**
```
Botão direito → Propriedades → Segurança → Editar
```

### UAC (User Account Control)

O **UAC** protege o sistema solicitando confirmação para operações que requerem privilégios elevados.

```
┌─────────────────────────┐
│ Deseja executar esta    │
│ aplicação como admin?   │
│ [Sim] [Não]             │
└─────────────────────────┘
```

---

## <a name="linux"></a>Linux: Conceitos Fundamentais

### Estrutura do Sistema de Arquivos

Linux segue a **Filesystem Hierarchy Standard (FHS)**.

```
/
├── bin/              # Executáveis essenciais
├── sbin/             # Executáveis para admin
├── etc/              # Arquivos de configuração
├── home/             # Diretórios dos usuários
│   ├── alice/
│   └── bob/
├── root/             # Diretório do root
├── tmp/              # Arquivos temporários
├── var/              # Dados variáveis (logs, caches)
├── opt/              # Programas opcionais
├── usr/              # Programas e dados do usuário
│   ├── bin/
│   ├── sbin/
│   ├── local/        # Software instalado localmente
│   └── share/
├── lib/              # Bibliotecas essenciais
├── dev/              # Arquivos de dispositivo
├── proc/             # Informações do processo
└── sys/              # Informações do sistema
```

### Usuários e Permissões em Linux

#### Estrutura de Permissões

```bash
-rwxr-xr-x  1  alice  users  1234  Jan 15 10:30  documento.txt
│││││││││   │   │     │      │     │             │
├┤││││││││   │   │     │      │     │             └─ Nome do arquivo
│ │││││││││   │   │     │      │     └─ Data/hora
│ │││││││││   │   │     │      └─ Tamanho (bytes)
│ │││││││││   │   │     └─ Grupo propietário
│ │││││││││   │   └─ Usuário proprietário
│ │││││││││   └─ Número de links
│ └┴┴┴┴┴┴┴┴─ Permissões (9 bits)
└─ Tipo de arquivo (- = arquivo regular)
```

#### Permissões Detalhadas

| Símbolo | Tipo | Significado |
|---|---|---|
| `-` | Arquivo regular | Arquivo comum |
| `d` | Diretório | Pasta/diretório |
| `l` | Link simbólico | Atalho para arquivo |
| `r` (read) | 4 | Ler arquivo/listar diretório |
| `w` (write) | 2 | Escrever/deletar do diretório |
| `x` (execute) | 1 | Executar arquivo/acessar diretório |

**Exemplo:**
```
-rw-r--r--  (644 em octal)
  └─ Dono: read + write (6)
     └─ Grupo: read (4)
        └─ Outros: read (4)
```

#### Usuários Especiais

| Usuário | UID | Propósito |
|---|---|---|
| **root** | 0 | Superusuário (privilégios totais) |
| **www-data** | 33 | Servidor web |
| **postgres** | 107 | Banco de dados |
| **nobody** | 65534 | Conta sem privilégios |

### Comandos Linux Essenciais

#### Navegação e Listagem

```bash
# Diretório atual
pwd                    # Print working directory

# Listar arquivos
ls                     # Listagem simples
ls -la                 # Listagem longa com ocultos
ls -lh                 # Tamanhos legíveis
ls -lt                 # Ordenado por tempo
ls -lS                 # Ordenado por tamanho

# Mudar diretório
cd /path/to/dir        # Navegar para caminho
cd ..                  # Subir um nível
cd ~                   # Ir para home
cd -                   # Ir para anterior
```

#### Manipulação de Arquivos

```bash
# Criar
touch filename.txt     # Cria arquivo vazio
mkdir dirname          # Cria diretório
mkdir -p a/b/c         # Cria recursivamente

# Copiar
cp arquivo.txt cópia.txt
cp -r diretorio/ cópia/

# Mover/Renomear
mv arquivo.txt novo_nome.txt
mv arquivo.txt /path/to/

# Deletar
rm arquivo.txt         # Remove arquivo
rm -r diretorio/       # Remove diretório recursivamente
rm -f arquivo          # Force remove (sem confirmação)

# Visualizar
cat arquivo.txt        # Exibe conteúdo completo
head -n 20 arquivo.txt # Primeiras 20 linhas
tail -n 10 arquivo.txt # Últimas 10 linhas
less arquivo.txt       # Visualizador paginado
grep "texto" arquivo.txt # Busca por padrão
```

#### Permissões

```bash
# Modificar permissões (octal)
chmod 644 arquivo.txt  # rw-r--r--
chmod 755 script.sh    # rwxr-xr-x
chmod +x programa      # Adiciona execute para todos

# Modificar permissões (simbólico)
chmod u+rwx arquivo    # User (dono) + read/write/execute
chmod g-w arquivo      # Group - write
chmod o= arquivo       # Others nenhuma permissão

# Mudar proprietário
chown alice arquivo    # Muda dono para alice
chown alice:users arquivo  # Muda dono e grupo
chown -R alice dir/    # Recursivamente
```

#### Informações do Sistema

```bash
# Usuário e privilégios
whoami                 # Usuário atual
id                     # UID, GID e grupos
groups                 # Grupos do usuário
sudo -l                # Comandos com sudo

# Sistema
uname -a               # Informações do kernel
hostnamectl            # Nome do host
uptime                 # Tempo ligado
df -h                  # Espaço em disco
du -sh *               # Uso de espaço por item
free -h                # Memória disponível
ps aux                 # Processos em execução
top                    # Monitor em tempo real
netstat -tlnp          # Conexões de rede
```

#### Busca

```bash
# find: Busca por arquivo
find /home -name "*.txt"     # Por nome
find /home -type f -size +1M # Arquivos maiores que 1MB
find /home -user alice       # De um usuário
find /home -perm 644         # Com permissão específica
find /home -exec rm {} \;    # Executa comando para cada

# locate: Banco de dados rápido
locate filename        # Busca em índice

# grep: Busca em conteúdo
grep "erro" log.txt    # Busca simples
grep -i "ERROR" log    # Insensível a maiúsculas
grep -r "texto" ./     # Recursivo
grep -n "texto" log    # Com número de linha
```

---

## <a name="cli"></a>Interface de Linha de Comando (CLI)

### Windows: CMD vs PowerShell

#### Command Prompt (CMD)

O **cmd.exe** é o shell tradicional do Windows (obsoleto).

```batch
REM Comandos básicos
dir                    REM Lista arquivos
cd C:\Users           REM Muda diretório
copy arquivo.txt cópia.txt  REM Copia
del arquivo.txt       REM Deleta
type arquivo.txt      REM Exibe conteúdo
echo Hello World      REM Imprime
```

**Limitações:**
- Sintaxe limitada e confusa
- Sem suporte a objetos
- Sem scripting avançado
- Legado, em desuso

#### PowerShell

O **PowerShell** é o shell moderno do Windows, baseado em objetos.

```powershell
# Comandos básicos (cmdlets)
Get-ChildItem                    # Lista arquivos
Get-ChildItem -Path C:\Users    # Com parâmetros
Set-Location C:\Users           # Muda diretório
Copy-Item arquivo.txt -Destination cópia.txt
Remove-Item arquivo.txt
Get-Content arquivo.txt          # Exibe conteúdo
Write-Host "Hello World"        # Imprime

# Objetos e pipeline
Get-Process | Where-Object {$_.WorkingSet -gt 100MB}
Get-ChildItem | Sort-Object -Property Length -Descending

# Variáveis
$nome = "Alice"
$idade = 30
$lista = @(1, 2, 3, 4, 5)

# Funções
function Saudacao {
    param([string]$nome)
    Write-Host "Olá, $nome!"
}
Saudacao -nome "Bob"

# Condicional
if ($idade -gt 18) {
    Write-Host "Maior de idade"
}

# Loop
foreach ($item in $lista) {
    Write-Host $item
}
```

**Vantagens:**
- Orientado a objetos
- Scripting poderoso
- Integração com .NET
- Suporte a automação
- Multiplataforma (PowerShell Core)

---

## <a name="segurança-so"></a>Segurança do Sistema Operacional

### Autenticação e Autorização

#### Autenticação em Windows

```
Usuário insere senha
        ↓
    Windows executa hash
        ↓
    Compara com SAM ou Active Directory
        ↓
    Se corresponder → Cria token de acesso
        ↓
    Token contém SID e grupos
```

**SAM (Security Account Manager):**
- Banco de dados local do Windows
- Localização: `C:\Windows\System32\config\SAM`
- Armazona hashes de senhas (NTLM)
- Apenas legível pelo SYSTEM

#### Autenticação em Linux

```bash
# /etc/passwd - Informações de usuário
alice:x:1000:1000:Alice Smith:/home/alice:/bin/bash
│     │  │    │    │            │              │
│     │  │    │    │            │              └─ Shell
│     │  │    │    │            └─ Diretório home
│     │  │    │    └─ GECOS (nome, telefone)
│     │  │    └─ GID (grupo primário)
│     │  └─ UID
│     └─ x = senha em /etc/shadow
└─ Usuário

# /etc/shadow - Hashes de senha (apenas root pode ler)
alice:$6$rounds=656000$hash...:18000:0:99999:7:3::
  │    │                       │     │   │    │ │ └─ Dias após passw inativo
  │    │                       │     │   │    └─ Período de aviso
  │    │                       │     │   └─ Máx dias para mudar
  │    │                       │     └─ Min dias para mudar
  │    │                       └─ Dias desde 01/01/1970
  │    └─ Hash da senha (SHA-512)
  └─ Usuário
```

### Firewall

#### Windows Firewall

```powershell
# Verificar status
Get-NetFirewallProfile

# Habilitar firewall
Set-NetFirewallProfile -Profile Domain,Public,Private -Enabled $true

# Criar regra (permitir)
New-NetFirewallRule -DisplayName "Permitir SSH" `
    -Direction Inbound `
    -Action Allow `
    -Protocol TCP `
    -LocalPort 22

# Remover regra
Remove-NetFirewallRule -DisplayName "Permitir SSH"
```

#### Linux Firewall (UFW/iptables)

```bash
# UFW (Uncomplicated Firewall)
sudo ufw enable          # Habilitar
sudo ufw disable         # Desabilitar
sudo ufw allow 22        # Permitir porta 22
sudo ufw deny 3000       # Bloquear porta 3000
sudo ufw status          # Verificar status

# iptables (nível inferior)
sudo iptables -L                    # Listar regras
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
sudo iptables -A INPUT -j DROP      # Drop padrão
```

### Antivírus e Proteção em Tempo Real

#### Windows Defender

```powershell
# Verificar status
Get-MpPreference

# Executar scan
Start-MpScan -ScanType Full    # Scan completo
Start-MpScan -ScanType Quick   # Scan rápido

# Atualizar assinaturas
Update-MpSignature
```

#### Linux (ClamAV)

```bash
# Instalar
sudo apt-get install clamav

# Atualizar banco de dados
sudo freshclam

# Escanear
clamscan -r /home/        # Recursivo
clamscan -i /home/        # Mostrar apenas infecções
clamscan --remove /home/  # Remover malware
```

### Princípio do Menor Privilégio

O **princípio do menor privilégio** significa que usuários e processos devem ter apenas as permissões mínimas necessárias.

#### Boas Práticas

```
❌ Usar conta admin para tarefas diárias
✓  Usar conta de usuário padrão

❌ Executar serviços como root
✓  Criar usuário específico com mínimas permissões

❌ Dar permissão 777 (rwxrwxrwx) em tudo
✓  Usar permissões específicas (ex: 755, 644)

❌ Armazenar credenciais em código
✓  Usar variáveis de ambiente ou gerenciadores de secrets
```

#### Sudo em Linux

O **sudo** permite executar comandos como outro usuário (geralmente root) com controle granular.

```bash
# Arquivo de configuração: /etc/sudoers
alice ALL=(ALL) ALL              # alice pode tudo como root
bob ALL=(www-data) NOPASSWD: /usr/bin/nginx  # bob sem senha apenas nginx

# Uso
sudo apt-get update              # Solicita senha
sudo -u www-data ls /var/www     # Executa como www-data
sudo -l                          # Lista permissões
sudo visudo                      # Edita /etc/sudoers seguramente
```

### Auditoria e Logging

#### Windows Event Viewer

```
Tipos de logs:
• Application - Eventos de aplicações
• Security - Tentativas de logon, mudanças de permissão
• System - Eventos do kernel e serviços
```

**Exemplo de event de logon bem-sucedido:**
```
Tipo: Success Audit
ID de Evento: 4624 (Logon bem-sucedido)
Usuário: DOMAIN\alice
Hora: 2024-01-15 10:30:45
Tipo de Logon: 3 (Rede)
Conta de Origem: 192.168.1.100
```

#### Linux Audit

```bash
# Instalar auditctl
sudo apt-get install auditd

# Monitorar acesso a arquivo
sudo auditctl -w /etc/passwd -p wa -k passwd_change

# Monitorar chamadas de sistema
sudo auditctl -a always,exit -F arch=b64 -S adjtimex -F key=time_change

# Ver logs
sudo ausearch -k passwd_change
sudo aureport                    # Relatório
```

### SSH (Secure Shell)

#### Configuração Segura

```bash
# ~/.ssh/config
Host servidor
    HostName 192.168.1.10
    User alice
    Port 22
    IdentityFile ~/.ssh/id_rsa
    StrictHostKeyChecking accept-new

# Usar SSH
ssh alice@servidor.com
ssh -i /path/to/key alice@servidor.com

# Copiar arquivos
scp arquivo.txt alice@servidor.com:/home/alice/
scp -r diretorio/ alice@servidor.com:/home/alice/

# Tunel SSH (Port Forwarding)
ssh -L 8080:localhost:3000 alice@servidor.com
# Acessa localhost:8080 → servidor.com:3000
```

**Configuração do servidor (/etc/ssh/sshd_config):**
```bash
Port 2222                    # Muda porta padrão
PermitRootLogin no          # Proíbe login direto como root
PasswordAuthentication no   # Apenas chaves públicas
PubkeyAuthentication yes
MaxAuthTries 3              # Máximo tentativas
LoginGraceTime 30s          # Tempo para autenticar
X11Forwarding no            # Desabilita X11
```

---

## <a name="conceitos-chave"></a>Conceitos-Chave para Lembrar

### Fundamentos
- Um **Sistema Operacional** gerencia hardware e fornece serviços a aplicações
- O **Kernel** é o núcleo privilegiado; aplicações rodam em espaço de usuário protegido
- **Processos** são instâncias independentes; **threads** compartilham memória dentro de um processo

### Windows
- **NTFS** é o sistema de arquivos moderno do Windows
- **Task Manager** monitora processos e recursos
- **Registry** armazena configurações em HKEY_LOCAL_MACHINE e HKEY_CURRENT_USER
- **ACLs** controlam acesso a arquivos e pastas
- **UAC** protege contra alterações não autorizadas do sistema

### Linux
- **Hierarquia de diretórios** segue FHS: /, /home, /etc, /usr, /var, etc.
- **Permissões** são representadas em octal (644, 755) ou simbólico (rwxr-xr-x)
- Usuários têm **UID**, grupos têm **GID**, **root** tem UID 0
- **/etc/passwd** e **/etc/shadow** armazenam dados de usuários
- **Sudo** permite executar comandos com privilégios elevados

### CLI
- **PowerShell** é moderno e orientado a objetos; **CMD** é legado
- PowerShell usa cmdlets e pipeline de objetos
- Linux CLI oferece ferramentas poderosas como grep, find, chmod, chown

### Segurança
- **Princípio do Menor Privilégio** limita acessos desnecessários
- **Firewall** controla tráfego de rede
- **Antivírus** detecta malware
- **SSH** oferece acesso remoto seguro com autenticação por chave
- **Auditoria** registra eventos importantes para investigação
- **Autenticação** verifica identidade; **autorização** verifica permissões

---

## 🚀 Próximos Passos no Pre Security Path

### Sequência de Aprendizagem
1. **Dominar CLI:** Praticar comandos Linux e PowerShell — habilidades essenciais para segurança
2. **Entender Segurança do SO:** Consolidar conceitos de permissões, firewall e auditoria
3. **Avançar para Software:** Software Basics — aprender linguagens e SQL
4. **Estudar Ataques:** Attacks and Defenses — explorar privilege escalation e defesas

### Prática Recomendada
- **Criar usuários e gerenciar permissões:** Praticar `adduser`, `chmod`, `chown` em Linux
- **Explorar o Registry:** Usar `regedit` no Windows para entender configurações
- **Configurar Firewall:** Usar `iptables` (Linux) ou `netsh` (Windows)
- **Análise de Logs:** Usar `Event Viewer` (Windows) ou `journalctl` (Linux)
- **Exercícios TryHackMe:** Fazer as tarefas práticas de SO

### Tópicos de Interesse Posterior
- **Privilege Escalation:** Técnicas de exploração para elevar privilégios
- **Rootkits:** Malware que se esconde ao nível do kernel
- **Container Security:** Docker e segurança de containers
- **Hardening:** Endurecer sistemas operativos contra ataques
- **Incident Response:** Responder a incidentes ao nível do SO

---

## 🔖 Tags

#cybersecurity #operatingsystems #presecurity #tryhackme #linux #windows #powershell #security #kernel #permissions #firewall #ssh #auditoria

---

_Notas criadas para o TryHackMe Pre Security Path — Operating Systems Basics_  
_Formatado para Obsidian_
