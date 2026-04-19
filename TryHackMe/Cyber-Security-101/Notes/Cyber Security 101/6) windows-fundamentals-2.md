# 🪟 Windows Fundamentals 2

> **Plataforma:** TryHackMe  
> **Caminho:** Cyber Security 101  
> **Estado:** ✅ Concluído  
> **Tags:** #windows #thm #cybersecurity101 #fundamentos #cmd #powershell #segurança #firewall

---

## 📌 Resumo do Módulo

Continuação do estudo do Windows, com foco em ferramentas de linha de comandos (**CMD** e **PowerShell**), **gestão de utilizadores**, **Event Viewer**, **Windows Update**, **Windows Security** e ferramentas de proteção integradas como o **Windows Defender** e o **Firewall**. O módulo prepara para entender como o Windows se defende — e como pode ser atacado.

---

## ⌨️ Command Prompt (CMD)

O **CMD** é o interpretador de comandos clássico do Windows, herdado do MS-DOS.

```
Executar → cmd
```

### Comandos Essenciais

#### 🔍 Navegação e Ficheiros

|Comando|Descrição|Exemplo|
|---|---|---|
|`dir`|Lista ficheiros e pastas|`dir /a` (inclui ocultos)|
|`cd`|Muda de diretório|`cd C:\Users`|
|`tree`|Mostra estrutura em árvore|`tree C:\`|
|`cls`|Limpa o ecrã|`cls`|
|`type`|Mostra conteúdo de ficheiro|`type ficheiro.txt`|
|`copy`|Copia ficheiros|`copy a.txt b.txt`|
|`move`|Move/renomeia ficheiros|`move a.txt C:\temp\`|
|`del`|Apaga ficheiros|`del ficheiro.txt`|
|`mkdir`|Cria diretório|`mkdir pasta`|
|`rmdir`|Remove diretório|`rmdir /s /q pasta`|

#### 🌐 Rede

|Comando|Descrição|
|---|---|
|`ipconfig`|Ver IPs, gateway, DNS|
|`ipconfig /all`|Informação completa de rede|
|`ipconfig /flushdns`|Limpar cache DNS|
|`ping host`|Testar conectividade|
|`tracert host`|Traçar rota até ao destino|
|`nslookup dominio`|Consultar DNS|
|`netstat -ano`|Conexões ativas e portas abertas|
|`arp -a`|Tabela ARP (IPs ↔ MACs)|

#### 👤 Utilizadores e Sistema

|Comando|Descrição|
|---|---|
|`whoami`|Utilizador atual|
|`whoami /priv`|Privilégios do utilizador|
|`net user`|Lista utilizadores locais|
|`net user nome`|Detalhes de um utilizador|
|`net localgroup`|Lista grupos locais|
|`systeminfo`|Info detalhada do sistema|
|`hostname`|Nome da máquina|
|`tasklist`|Processos em execução|
|`taskkill /PID x /F`|Terminar processo pelo PID|

```bash
# Ver todos os serviços
sc query

# Ver estado de um serviço específico
sc query wuauserv

# Iniciar/parar serviço
net start NomeServico
net stop NomeServico
```

> [!tip] Elevar privilégios no CMD Clica com o botão direito no CMD → **"Run as administrator"** para abrir com privilégios de administrador. Muitos comandos requerem isto.

---

## 💙 PowerShell

O **PowerShell** é o shell moderno da Microsoft — muito mais poderoso que o CMD. Usa **cmdlets** no formato `Verbo-Substantivo`.

```
Executar → powershell
```

### Cmdlets Fundamentais

|Cmdlet|Equivalente Linux|Descrição|
|---|---|---|
|`Get-ChildItem` (`ls`, `dir`)|`ls`|Lista ficheiros|
|`Set-Location` (`cd`)|`cd`|Muda de diretório|
|`Get-Content` (`cat`)|`cat`|Lê ficheiro|
|`Copy-Item` (`cp`)|`cp`|Copia ficheiro|
|`Move-Item` (`mv`)|`mv`|Move ficheiro|
|`Remove-Item` (`rm`)|`rm`|Remove ficheiro|
|`New-Item`|`touch` / `mkdir`|Cria ficheiro ou pasta|
|`Get-Process`|`ps aux`|Lista processos|
|`Stop-Process`|`kill`|Termina processo|
|`Get-Service`|`systemctl`|Lista serviços|
|`Get-Help`|`man`|Ajuda de um cmdlet|

```powershell
# Exemplos práticos
Get-ChildItem -Hidden           # mostra ficheiros ocultos
Get-Content C:\Windows\System32\drivers\etc\hosts
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
Get-Service | Where-Object {$_.Status -eq "Running"}

# Histórico de comandos
Get-History

# Ajuda detalhada
Get-Help Get-Process -Full
Get-Help Get-Process -Examples
```

### Pipeline no PowerShell

Tal como no Linux, o PowerShell usa `|` para encadear comandos:

```powershell
# Top 5 processos que mais consomem CPU
Get-Process | Sort-Object CPU -Descending | Select-Object -First 5

# Serviços parados
Get-Service | Where-Object {$_.Status -eq "Stopped"}

# Exportar para CSV
Get-Process | Export-Csv processos.csv
```

> [!important] PowerShell vs CMD O PowerShell trabalha com **objetos** (não texto), o que permite filtrar, ordenar e manipular dados de forma muito mais poderosa. É a ferramenta preferida de administradores de sistemas e atacantes modernos.

---

## 📋 Event Viewer

O **Event Viewer** regista todos os eventos importantes do sistema — essencial para análise forense e deteção de intrusões.

```
Executar → eventvwr.msc
```

### Categorias de Logs

```
Event Viewer
├── Windows Logs
│   ├── Application   → Eventos de aplicações
│   ├── Security      → Logins, acessos, auditorias ⭐
│   ├── Setup         → Instalação do SO
│   ├── System        → Eventos do kernel e drivers
│   └── Forwarded     → Eventos de outras máquinas
│
└── Applications and Services Logs
    ├── Microsoft
    ├── Windows
    └── (logs específicos de aplicações)
```

### Níveis de Severidade

|Nível|Ícone|Significado|
|---|---|---|
|**Information**|ℹ️|Evento normal|
|**Warning**|⚠️|Algo pode estar errado|
|**Error**|❌|Falha que não afeta o sistema|
|**Critical**|🔴|Falha grave do sistema|
|**Audit Success**|✅|Ação de segurança bem-sucedida|
|**Audit Failure**|🔒|Tentativa de acesso negada|

### Event IDs Importantes para Cibersegurança

|Event ID|Descrição|
|---|---|
|`4624`|Login bem-sucedido|
|`4625`|Login falhado ⚠️|
|`4648`|Login com credenciais explícitas|
|`4720`|Conta de utilizador criada|
|`4726`|Conta de utilizador apagada|
|`4732`|Utilizador adicionado a grupo privilegiado|
|`4688`|Novo processo criado|
|`7045`|Novo serviço instalado|

> [!warning] Monitorização de Segurança Múltiplos eventos `4625` seguidos podem indicar um **ataque de força bruta**. O Event ID `7045` é frequentemente usado por malware para instalar persistência como serviço.

---

## 🔄 Windows Update

O **Windows Update** é o sistema de atualização automática do Windows — crítico para manter o sistema seguro.

```
Definições → Windows Update
```

### Tipos de Atualizações

|Tipo|Frequência|Conteúdo|
|---|---|---|
|**Quality Updates**|Mensal (Patch Tuesday)|Correções de segurança e bugs|
|**Feature Updates**|Semestral|Novas funcionalidades do SO|
|**Driver Updates**|Variável|Atualizações de hardware|
|**Definition Updates**|Diária|Bases de dados do Defender|

> [!important] Patch Tuesday A Microsoft lança atualizações de segurança na **segunda terça-feira de cada mês**. Em ambientes empresariais, estas atualizações são testadas antes de serem implementadas usando ferramentas como o **WSUS (Windows Server Update Services)**.

> [!warning] CVEs e Patches Muitos ataques exploram **vulnerabilidades conhecidas** para as quais já existem patches. Manter o sistema atualizado é uma das defesas mais eficazes contra ransomware e exploits.

---

## 🛡️ Windows Security

O **Windows Security** é o centro de segurança integrado no Windows — acesso rápido a todas as proteções do sistema.

```
Definições → Windows Security
ou
Executar → windowsdefender:
```

### Áreas de Proteção

|Área|Função|
|---|---|
|**Virus & Threat Protection**|Antivírus e scans|
|**Account Protection**|Windows Hello, conta Microsoft|
|**Firewall & Network Protection**|Gestão da firewall|
|**App & Browser Control**|SmartScreen, proteção de exploits|
|**Device Security**|TPM, Secure Boot, Core Isolation|
|**Device Performance & Health**|Saúde geral do dispositivo|
|**Family Options**|Controlo parental|

---

## 🦠 Windows Defender Antivirus

O **Windows Defender** é o antivírus integrado no Windows — competitivo com soluções de terceiros.

### Tipos de Scan

```powershell
# Scan rápido via PowerShell
Start-MpScan -ScanType QuickScan

# Scan completo
Start-MpScan -ScanType FullScan

# Scan de um caminho específico
Start-MpScan -ScanType CustomScan -ScanPath "C:\Users\Downloads"

# Atualizar definições
Update-MpSignature
```

### Exclusões (usado em pentest / administração)

> [!warning] Exclusões do Defender Adicionar exclusões reduz a proteção. Em pentest, atacantes frequentemente adicionam exclusões para evitar deteção. Monitoriza alterações às exclusões do Defender!

---

## 🔥 Windows Firewall

O **Windows Defender Firewall** controla o tráfego de rede de entrada e saída.

```
Executar → wf.msc          (interface avançada)
Executar → firewall.cpl    (interface simples)
```

### Perfis de Rede

|Perfil|Quando se aplica|
|---|---|
|**Domain**|Ligado ao domínio da empresa|
|**Private**|Rede doméstica ou de confiança|
|**Public**|Redes públicas (café, aeroporto) — mais restritivo|

### Gestão via CMD/PowerShell

```powershell
# Ver estado da firewall
Get-NetFirewallProfile

# Desativar firewall (⚠️ não recomendado)
Set-NetFirewallProfile -Profile Domain,Public,Private -Enabled False

# Criar regra para permitir porta
New-NetFirewallRule -DisplayName "Permitir HTTP" -Direction Inbound -Protocol TCP -LocalPort 80 -Action Allow

# Bloquear uma porta
New-NetFirewallRule -DisplayName "Bloquear Telnet" -Direction Inbound -Protocol TCP -LocalPort 23 -Action Block

# Ver todas as regras ativas
Get-NetFirewallRule | Where-Object {$_.Enabled -eq "True"}
```

---

## 🔍 Ferramentas Adicionais

### Resource Monitor (`resmon`)

Monitorização em tempo real de CPU, memória, disco e rede por processo.

### Performance Monitor (`perfmon`)

Análise detalhada de performance com contadores e logs históricos.

### Reliability Monitor

```
Control Panel → Security and Maintenance → Reliability Monitor
```

Histórico visual de erros e falhas do sistema — útil para troubleshooting.

---

## 🏁 Rooms / Tarefas Completadas

- [x] Task 1 — Introdução ao módulo
- [x] Task 2 — Command Prompt (CMD)
- [x] Task 3 — PowerShell
- [x] Task 4 — Event Viewer
- [x] Task 5 — Windows Update
- [x] Task 6 — Windows Security Center
- [x] Task 7 — Windows Defender Antivirus
- [x] Task 8 — Windows Firewall
- [x] Task 9 — Ferramentas adicionais
- [x] Task 10 — Conclusão

---

## 🔗 Navegação

- [[THM - Windows Fundamentals 1]] ← Módulo anterior
- [ ] [[THM - Windows Fundamentals 3]] → Active Directory, BitLocker, ferramentas avançadas

---

## 📚 Recursos Úteis

- [TryHackMe — Windows Fundamentals 2](https://tryhackme.com/room/windowsfundamentals2x0x)
- [Microsoft Docs — PowerShell](https://docs.microsoft.com/en-us/powershell/)
- [Windows Event IDs — Referência Completa](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/)
- [HackTricks — Windows](https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation)

---

_Nota criada após conclusão do módulo · TryHackMe · Cyber Security 101_