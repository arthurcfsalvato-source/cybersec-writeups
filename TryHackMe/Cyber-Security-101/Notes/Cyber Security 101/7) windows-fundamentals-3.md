# 🪟 Windows Fundamentals 3

> **Plataforma:** TryHackMe  
> **Caminho:** Cyber Security 101  
> **Estado:** ✅ Concluído  
> **Tags:** #windows #thm #cybersecurity101 #fundamentos #bitlocker #active-directory #segurança #vss

---

## 📌 Resumo do Módulo

O módulo final da série Windows Fundamentals aprofunda temas avançados de segurança e administração: **Microsoft Security Center**, **BitLocker**, **VSS (Volume Shadow Copy)**, **proteção avançada contra ameaças**, e uma introdução ao conceito de **Active Directory**. Este módulo liga os fundamentos do Windows ao mundo real da cibersegurança empresarial.

---

## 🛡️ Microsoft Security Center & Práticas de Segurança

A segurança no Windows assenta em três pilares fundamentais:

```
┌─────────────────────────────────────────────┐
│           Segurança no Windows              │
│                                             │
│  🔐 Confidencialidade  →  BitLocker, EFS   │
│  ✅ Integridade        →  Windows Defender  │
│  🟢 Disponibilidade    →  VSS, Backups      │
└─────────────────────────────────────────────┘
```

### CIA Triad aplicada ao Windows

|Pilar|Ferramenta Windows|Função|
|---|---|---|
|**Confidentiality**|BitLocker, EFS|Encriptação de dados|
|**Integrity**|Windows Defender, SmartScreen|Deteção de alterações maliciosas|
|**Availability**|VSS, Backup, RAID|Recuperação de dados|

---

## 🔒 BitLocker — Encriptação de Disco

O **BitLocker** é a solução de encriptação de disco completo integrada no Windows. Protege os dados em caso de roubo ou acesso físico não autorizado.

> [!important] Disponibilidade O BitLocker está disponível nas edições **Pro**, **Enterprise** e **Education**. **Não está disponível na edição Home.**

### Como funciona

```
Disco sem BitLocker:
[Dados legíveis por qualquer um com acesso físico]

Disco com BitLocker:
[Dados encriptados com AES-128 ou AES-256]
         ↓
    Só acessíveis com:
    ✅ PIN / Password
    ✅ Chave de recuperação (Recovery Key)
    ✅ Chip TPM (Trusted Platform Module)
```

### TPM — Trusted Platform Module

O **TPM** é um chip de segurança integrado na motherboard que armazena as chaves de encriptação do BitLocker de forma segura.

|Cenário|O que acontece|
|---|---|
|Boot normal com TPM|Windows desencripta automaticamente|
|Disco removido para outra máquina|Dados inacessíveis — sem o TPM|
|TPM + PIN|Dupla autenticação no arranque|
|Sem TPM|Usa password ou USB com chave|

```
Gerir BitLocker:
Painel de Controlo → System and Security → BitLocker Drive Encryption
ou
Executar → manage-bde (linha de comandos)
```

```powershell
# Ver estado do BitLocker em todos os volumes
manage-bde -status

# Ativar BitLocker numa drive
manage-bde -on C: -recoverypassword

# Ver a Recovery Key
manage-bde -protectors -get C:
```

> [!warning] Recovery Key — Guarda com cuidado! A **chave de recuperação** é o único backup se perderes acesso ao BitLocker. Guarda-a numa conta Microsoft, num USB separado ou imprime. Sem ela, os dados são irrecuperáveis.

---

## 📸 VSS — Volume Shadow Copy Service

O **VSS** cria "fotografias" (snapshots) do sistema de ficheiros num determinado momento — essencial para recuperação de dados e análise forense.

```
O que é um Shadow Copy?
─────────────────────────────────────────
  Estado do disco às 09:00 ──→ [Snapshot A]
  Estado do disco às 12:00 ──→ [Snapshot B]
  Estado do disco às 15:00 ──→ [Snapshot C]
  
  Se um ficheiro for apagado ou corrompido às 14:00,
  podes restaurá-lo a partir do [Snapshot B]
```

### Gerir Shadow Copies

```powershell
# Ver shadow copies existentes
vssadmin list shadows

# Ver espaço usado pelo VSS
vssadmin list shadowstorage

# Criar um shadow copy manualmente
wmic shadowcopy call create Volume='C:\'
```

### Aceder a versões anteriores

```
Botão direito numa pasta → Properties → Previous Versions
```

> [!warning] VSS e Ransomware O ransomware moderno frequentemente **apaga os shadow copies** antes de encriptar os ficheiros, eliminando a possibilidade de recuperação. Comando usado por atacantes:
> 
> ```
> vssadmin delete shadows /all /quiet
> ```
> 
> Isto é um **indicador de comprometimento (IOC)** crítico — monitoriza este comando!

---

## 🧱 Windows Defender SmartScreen

O **SmartScreen** protege contra sites maliciosos, downloads perigosos e aplicações não reconhecidas.

### Como funciona

```
Utilizador tenta abrir ficheiro descarregado
              ↓
    SmartScreen verifica a reputação
              ↓
    ┌─────────────────────────────────┐
    │  Reputação boa → Abre normal   │
    │  Reputação má  → Bloqueia ⛔  │
    │  Desconhecido  → Aviso ⚠️     │
    └─────────────────────────────────┘
```

### Configuração

```
Windows Security → App & Browser Control → SmartScreen
```

|Opção|Comportamento|
|---|---|
|**Block**|Bloqueia automaticamente|
|**Warn**|Avisa mas permite continuar|
|**Off**|Desativado (não recomendado)|

> [!tip] Mark of the Web (MotW) Quando descarregas um ficheiro da internet, o Windows adiciona uma flag invisível chamada **Zone Identifier** (Mark of the Web). O SmartScreen usa isto para identificar ficheiros externos. Atacantes usam técnicas para contornar o MotW (ex: ficheiros `.iso`, `.vhd`).

---

## 🔐 Credential Guard & Core Isolation

### Core Isolation e Memory Integrity

Funcionalidades de segurança baseadas em **virtualização (VBS — Virtualization Based Security)**:

```
Windows Security → Device Security → Core Isolation
```

|Funcionalidade|Proteção|
|---|---|
|**Memory Integrity**|Impede injeção de código malicioso no kernel|
|**Credential Guard**|Isola credenciais NTLM/Kerberos em ambiente virtualizado|
|**Hypervisor-Protected Code Integrity (HVCI)**|Garante integridade dos drivers|

> [!important] Credential Guard O **Credential Guard** é uma das defesas mais importantes contra ataques **Pass-the-Hash** e **Pass-the-Ticket** — técnicas comuns em pós-exploração de redes Windows. Disponível apenas nas edições **Enterprise** e **Education**.

---

## 🏢 Introdução ao Active Directory

O **Active Directory (AD)** é o serviço de diretório da Microsoft para gerir identidades e recursos em redes empresariais.

```
Ambiente doméstico:         Ambiente empresarial:
─────────────────           ──────────────────────
PC standalone               Domínio Windows
Contas locais               Active Directory
Sem gestão centralizada     Gestão centralizada
```

### Conceitos Fundamentais

|Conceito|Descrição|
|---|---|
|**Domain**|Grupo lógico de computadores geridos centralmente|
|**Domain Controller (DC)**|Servidor que gere o AD|
|**Domain Admin**|Conta com controlo total sobre o domínio|
|**OU (Organizational Unit)**|Contentor para organizar objetos no AD|
|**GPO (Group Policy Object)**|Políticas aplicadas a utilizadores/computadores|
|**LDAP**|Protocolo usado para consultar o AD|
|**Kerberos**|Protocolo de autenticação padrão do AD|

### Estrutura do Active Directory

```
Forest (floresta)
└── Domain: empresa.com
    ├── Domain Controller (DC01)
    ├── Organizational Units (OUs)
    │   ├── IT
    │   │   ├── Utilizadores
    │   │   └── Computadores
    │   ├── RH
    │   └── Financeiro
    ├── Group Policy Objects (GPOs)
    └── Security Groups
```

> [!important] AD em Cibersegurança O **Active Directory** é um alvo primário em ataques a redes empresariais. Comprometer o **Domain Controller** dá controlo total sobre toda a organização. Ataques comuns incluem: **Kerberoasting**, **Pass-the-Hash**, **DCSync**, **Golden Ticket**.

---

## 📋 Group Policy (GPO)

As **Group Policy Objects** permitem configurar e forçar definições em todos os computadores e utilizadores do domínio de forma centralizada.

```
Gerir GPOs:
Executar → gpedit.msc     (política local — máquina individual)
Executar → gpmc.msc       (consola de gestão — domínio completo)
```

### Exemplos de GPOs comuns

```
Segurança:
✅ Forçar complexidade de passwords
✅ Bloquear USB drives
✅ Desativar Command Prompt para utilizadores normais
✅ Forçar screensaver com password
✅ Restringir instalação de software

Configuração:
✅ Mapear drives de rede automaticamente
✅ Instalar software em todos os PCs
✅ Configurar fundo de ecrã corporativo
✅ Definir proxies e definições de rede
```

```powershell
# Forçar atualização de GPOs no cliente
gpupdate /force

# Ver GPOs aplicadas ao utilizador/computador atual
gpresult /r

# Relatório HTML detalhado das GPOs
gpresult /h C:\relatorio-gpo.html
```

---

## 🔍 Sysinternals Suite

A **Sysinternals Suite** é um conjunto de ferramentas avançadas da Microsoft para administração e análise do Windows — essenciais em cibersegurança.

```
Download: https://docs.microsoft.com/sysinternals
Ou usar diretamente: \\live.sysinternals.com\tools
```

### Ferramentas mais importantes

|Ferramenta|Função|
|---|---|
|**Process Explorer**|Task Manager avançado — mostra processos pai/filho, DLLs carregadas|
|**Autoruns**|Tudo o que executa no arranque — usado para encontrar malware persistente|
|**Process Monitor**|Registo em tempo real de ficheiros, registry e rede por processo|
|**TCPView**|Conexões de rede ativas por processo (como `netstat` mas visual)|
|**PsExec**|Executar processos remotamente|
|**Strings**|Extrai texto legível de binários|
|**Sigcheck**|Verifica assinaturas digitais de ficheiros|
|**Sysmon**|Logging avançado de eventos de segurança|

> [!tip] Autoruns em Incident Response O **Autoruns** é frequentemente a primeira ferramenta a correr numa máquina suspeita — mostra todos os pontos de persistência onde malware pode estar escondido: Registry, serviços, scheduled tasks, drivers, browser extensions, etc.

---

## 🔐 Protocolos de Autenticação Windows

|Protocolo|Descrição|Segurança|
|---|---|---|
|**NTLM**|Hash challenge-response|⚠️ Legacy — vulnerável a Pass-the-Hash|
|**Kerberos**|Tickets de autenticação|✅ Padrão em domínios AD|
|**LDAP**|Consulta de diretório|Usado pelo AD para pesquisas|
|**RADIUS**|Autenticação de rede|Usado em VPNs e Wi-Fi empresarial|

---

## 🏁 Rooms / Tarefas Completadas

- [x] Task 1 — Introdução ao módulo
- [x] Task 2 — Windows Updates & Segurança
- [x] Task 3 — BitLocker e TPM
- [x] Task 4 — Volume Shadow Copy Service (VSS)
- [x] Task 5 — SmartScreen e proteção de apps
- [x] Task 6 — Core Isolation e Credential Guard
- [x] Task 7 — Introdução ao Active Directory
- [x] Task 8 — Group Policy (GPO)
- [x] Task 9 — Sysinternals Suite
- [x] Task 10 — Conclusão

---

## 🔗 Navegação

- [[THM - Windows Fundamentals 1]] ← Módulo 1
- [[THM - Windows Fundamentals 2]] ← Módulo anterior
- [ ] Próximo: [[THM - Active Directory Basics]] ou [[THM - Network Fundamentals]]

---

## 📚 Recursos Úteis

- [TryHackMe — Windows Fundamentals 3](https://tryhackme.com/room/windowsfundamentals3xzx)
- [Microsoft Sysinternals](https://docs.microsoft.com/en-us/sysinternals/)
- [HackTricks — Active Directory](https://book.hacktricks.xyz/windows-hardening/active-directory-methodology)
- [Windows Event IDs](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/)
- [ired.team — AD Attacks](https://www.ired.team/offensive-security-experiments/active-directory-kerberos-abuse)

---

_Nota criada após conclusão do módulo · TryHackMe · Cyber Security 101_