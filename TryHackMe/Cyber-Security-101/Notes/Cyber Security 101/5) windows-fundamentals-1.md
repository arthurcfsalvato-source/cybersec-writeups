# 🪟 Windows Fundamentals 1

> **Plataforma:** TryHackMe  
> **Caminho:** Cyber Security 101  
> **Estado:** ✅ Concluído  
> **Tags:** #windows #thm #cybersecurity101 #fundamentos #sistema-operativo #gui

---

## 📌 Resumo do Módulo

Introdução ao sistema operativo **Windows** — o mais utilizado em ambientes empresariais e desktops domésticos. Este módulo cobre a **interface gráfica**, a **estrutura do sistema de ficheiros**, o **painel de controlo**, as **definições do sistema** e ferramentas essenciais de administração como o **Task Manager** e o **Registry**.

---

## 🏛️ Edições do Windows

O Windows existe em várias edições, cada uma direcionada para um público diferente:

|Edição|Público-alvo|
|---|---|
|**Home**|Utilizadores domésticos|
|**Pro**|Profissionais e pequenas empresas|
|**Pro for Workstations**|Estações de trabalho de alto desempenho|
|**Enterprise**|Grandes organizações (licença volumétrica)|
|**Education**|Instituições de ensino|
|**Server**|Servidores e infraestrutura de rede|

> [!important] Windows em Cibersegurança A edição **Pro** e **Enterprise** incluem funcionalidades de segurança avançadas como **BitLocker**, **Group Policy**, **Remote Desktop** e **Windows Defender Credential Guard** — ausentes na edição Home.

---

## 🖥️ Interface Gráfica (GUI)

### Componentes principais do Desktop

```
┌─────────────────────────────────────────────────┐
│  Desktop — área de trabalho principal            │
│                                                  │
│   [Ícones]   [Atalhos]   [Pastas]               │
│                                                  │
│                                                  │
├──────────────────────────────────────────────────┤
│ 🪟 Start │ 🔍 Search │ [Apps abertas] │ ... │ 🕐 │
│          Taskbar (Barra de Tarefas)               │
└─────────────────────────────────────────────────┘
```

|Componente|Função|
|---|---|
|**Desktop**|Área de trabalho principal|
|**Taskbar**|Barra inferior com apps abertas e sistema|
|**Start Menu**|Acesso a apps, definições e power options|
|**System Tray**|Ícones de sistema (rede, volume, hora)|
|**File Explorer**|Gestor de ficheiros gráfico|
|**Action Center**|Notificações e definições rápidas|

---

## 📂 Sistema de Ficheiros — NTFS

O Windows usa o sistema de ficheiros **NTFS (New Technology File System)** como padrão desde o Windows XP.

### Vantagens do NTFS sobre FAT32

|Funcionalidade|NTFS|FAT32|
|---|---|---|
|Tamanho máximo de ficheiro|**Sem limite prático**|4 GB|
|Permissões de ficheiros|✅ Sim|❌ Não|
|Encriptação (EFS)|✅ Sim|❌ Não|
|Compressão|✅ Sim|❌ Não|
|Journaling (recuperação)|✅ Sim|❌ Não|

### Permissões NTFS

```
Permissões aplicadas a ficheiros e pastas:

✅ Full Control     → Ler, escrever, apagar, alterar permissões
✅ Modify           → Ler, escrever, apagar (sem alterar permissões)
✅ Read & Execute   → Ver e executar ficheiros
✅ List Folder      → Ver conteúdo da pasta (apenas pastas)
✅ Read             → Ver conteúdo de ficheiros
✅ Write            → Criar e modificar ficheiros
```

> [!tip] Herança de Permissões Por defeito, as permissões de uma pasta são **herdadas** pelas subpastas e ficheiros dentro dela. Podes desativar esta herança manualmente nas propriedades da pasta.

---

## 🗂️ Estrutura de Diretórios do Windows

```
C:\
├── Windows\           → Ficheiros do sistema operativo
│   ├── System32\      → DLLs e executáveis críticos do sistema (64-bit)
│   ├── SysWOW64\      → Compatibilidade com apps 32-bit em sistemas 64-bit
│   └── Temp\          → Ficheiros temporários do sistema
│
├── Program Files\     → Aplicações instaladas (64-bit)
├── Program Files (x86)\ → Aplicações instaladas (32-bit)
│
├── Users\             → Perfis dos utilizadores
│   ├── Public\        → Partilhado entre todos os utilizadores
│   └── NomeUtilizador\
│       ├── Desktop\
│       ├── Documents\
│       ├── Downloads\
│       ├── AppData\   → Dados das aplicações (oculto)
│       │   ├── Local\
│       │   ├── LocalLow\
│       │   └── Roaming\
│       └── ...
│
└── ProgramData\       → Dados de apps partilhados (oculto)
```

> [!warning] `System32` — Nunca apagar! A pasta `System32` contém ficheiros críticos do sistema. Apagar ou modificar o seu conteúdo pode tornar o Windows inoperacional.

---

## 👤 Contas de Utilizador e Grupos

### Tipos de conta

|Tipo|Descrição|
|---|---|
|**Administrator**|Controlo total do sistema|
|**Standard User**|Uso normal, sem instalar software ou alterar sistema|
|**Guest**|Acesso muito limitado e temporário|

### Contas de sistema importantes

|Conta|Função|
|---|---|
|`SYSTEM`|A conta com mais privilégios — usada internamente pelo Windows|
|`Local Service`|Serviços com privilégios mínimos|
|`Network Service`|Serviços com acesso à rede|
|`Administrator`|Conta admin local (frequentemente desativada por segurança)|

> [!important] UAC — User Account Control O **UAC** é o prompt que aparece quando uma ação requer privilégios elevados. É uma camada de segurança que impede que malware faça alterações silenciosas no sistema. Nunca deves desativar o UAC.

---

## ⚙️ Ferramentas de Administração do Sistema

### System Configuration (`msconfig`)

```
Executar → msconfig
```

Permite gerir:

- **Boot** — opções de arranque do sistema
- **Services** — serviços que iniciam com o Windows
- **Startup** → redireciona para o Task Manager
- **Tools** → atalhos para ferramentas administrativas

### Computer Management (`compmgmt.msc`)

```
Executar → compmgmt.msc
```

Inclui três secções principais:

```
Computer Management
├── System Tools
│   ├── Task Scheduler       → Agendar tarefas automáticas
│   ├── Event Viewer         → Logs de eventos do sistema
│   ├── Shared Folders       → Pastas partilhadas na rede
│   ├── Local Users & Groups → Gerir utilizadores e grupos
│   └── Device Manager       → Gerir hardware e drivers
│
├── Storage
│   └── Disk Management      → Gerir partições e discos
│
└── Services and Applications
    └── Services             → Gerir serviços do Windows
```

### System Information (`msinfo32`)

```
Executar → msinfo32
```

Mostra informação detalhada sobre o hardware e software do sistema:

- Versão do SO e build
- Processador, RAM, arquitetura
- Drivers instalados
- Variáveis de ambiente

---

## 🗝️ Windows Registry

O **Registry** é uma base de dados hierárquica que armazena configurações do sistema operativo, hardware e aplicações.

```
Executar → regedit
```

### Estrutura das Hives (raízes)

|Hive|Abreviatura|Conteúdo|
|---|---|---|
|`HKEY_LOCAL_MACHINE`|`HKLM`|Configurações do sistema (todos os utilizadores)|
|`HKEY_CURRENT_USER`|`HKCU`|Configurações do utilizador atual|
|`HKEY_CLASSES_ROOT`|`HKCR`|Associações de ficheiros e COM objects|
|`HKEY_USERS`|`HKU`|Perfis de todos os utilizadores carregados|
|`HKEY_CURRENT_CONFIG`|`HKCC`|Perfil de hardware atual|

> [!warning] Registry — Cuidado Redobrado Alterações incorretas no Registry podem impedir o arranque do Windows. Faz sempre um backup antes de editar: `Ficheiro → Exportar`.

> [!tip] Registry em Cibersegurança O Registry é um alvo frequente de **malware** para garantir persistência. Chaves como `HKCU\Software\Microsoft\Windows\CurrentVersion\Run` executam programas automaticamente no login — verifica-as se suspeitares de infeção.

---

## 🔍 Ferramentas Rápidas — Executar (`Win + R`)

|Comando|Abre|
|---|---|
|`msconfig`|System Configuration|
|`compmgmt.msc`|Computer Management|
|`msinfo32`|System Information|
|`regedit`|Registry Editor|
|`cmd`|Command Prompt|
|`powershell`|PowerShell|
|`control`|Painel de Controlo|
|`taskmgr`|Task Manager|
|`devmgmt.msc`|Device Manager|
|`services.msc`|Services|
|`eventvwr.msc`|Event Viewer|
|`diskmgmt.msc`|Disk Management|
|`mstsc`|Remote Desktop|
|`calc`|Calculadora|
|`notepad`|Bloco de Notas|

---

## 🏁 Rooms / Tarefas Completadas

- [x] Task 1 — Introdução ao Windows
- [x] Task 2 — Interface gráfica e Desktop
- [x] Task 3 — Sistema de ficheiros NTFS
- [x] Task 4 — Estrutura de diretórios
- [x] Task 5 — Contas de utilizador e UAC
- [x] Task 6 — System Configuration (msconfig)
- [x] Task 7 — Computer Management
- [x] Task 8 — System Information
- [x] Task 9 — Windows Registry
- [x] Task 10 — Conclusão

---

## 🔗 Navegação

- [[THM - Linux Fundamentals 3]] ← Módulo anterior
- [ ] [[THM - Windows Fundamentals 2]] → Command Line, PowerShell, ferramentas de segurança

---

## 📚 Recursos Úteis

- [TryHackMe — Windows Fundamentals 1](https://tryhackme.com/room/windowsfundamentals1xbx)
- [Microsoft Docs — Windows Architecture](https://docs.microsoft.com/en-us/windows-hardware/drivers/kernel/windows-kernel-mode-object-manager)
- [HackTricks — Windows](https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation) — referência para pentest Windows

---

_Nota criada após conclusão do módulo · TryHackMe · Cyber Security 101_