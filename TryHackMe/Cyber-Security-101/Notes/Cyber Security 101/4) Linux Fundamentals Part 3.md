# 🐧 Linux Fundamentals 3

> **Plataforma:** TryHackMe  
> **Caminho:** Cyber Security 101  
> **Estado:** ✅ Concluído  
> **Tags:** #linux #thm #cybersecurity101 #fundamentos #terminal #automação #logs #serviços

---

## 📌 Resumo do Módulo

O módulo final da série Linux Fundamentals aprofunda temas essenciais para administração de sistemas e cibersegurança: **editores de texto**, **utilitários gerais**, **automatização com cron jobs**, **gestão de pacotes**, **logs do sistema** e **serviços/daemons**. Aqui o Linux começa a parecer uma ferramenta real de trabalho.

---

## 📝 Editores de Texto — Nano vs Vim

### Nano (recomendado para iniciantes)

```bash
nano ficheiro.txt
```

|Atalho|Ação|
|---|---|
|`Ctrl + O`|Guardar ficheiro|
|`Ctrl + X`|Sair|
|`Ctrl + W`|Pesquisar texto|
|`Ctrl + K`|Cortar linha|
|`Ctrl + U`|Colar linha|
|`Ctrl + G`|Ajuda|

### Vim (poderoso, curva de aprendizagem maior)

```bash
vim ficheiro.txt
```

|Modo|Como entrar|Para quê|
|---|---|---|
|**Normal**|`Esc`|Navegar, copiar, apagar|
|**Insert**|`i`|Escrever texto|
|**Visual**|`v`|Selecionar texto|
|**Command**|`:`|Guardar, sair, pesquisar|

```bash
# Comandos essenciais no modo Command (:)
:w        # guardar
:q        # sair
:wq       # guardar e sair
:q!       # sair sem guardar (forçado)
:/palavra # pesquisar
```

> [!tip] Saída de emergência do Vim Se ficares preso no Vim, prime `Esc` várias vezes e depois escreve `:q!` + Enter.

---

## 🛠️ Utilitários Gerais Úteis

### Descarregar e transferir ficheiros

```bash
# Descarregar da internet
wget https://exemplo.com/ficheiro.zip
curl https://exemplo.com/ficheiro.zip -o ficheiro.zip

# Diferença:
# wget → simples, ideal para downloads diretos
# curl → mais flexível, suporta APIs, headers, métodos HTTP
```

### Verificar conectividade e rede

```bash
ping google.com          # testa conectividade
ifconfig                 # ver interfaces de rede (IPs)
ip a                     # alternativa moderna ao ifconfig
netstat -tulpn           # portas abertas e serviços a escutar
ss -tulpn                # alternativa moderna ao netstat
```

### Informações do sistema

```bash
uname -a          # info do kernel e sistema
hostname          # nome da máquina
uptime            # há quanto tempo está ligada
df -h             # espaço em disco
du -sh pasta/     # tamanho de uma pasta
free -h           # memória RAM disponível
```

---

## ⚙️ Gestão de Pacotes (APT)

O **APT (Advanced Package Tool)** é o gestor de pacotes das distribuições baseadas em Debian/Ubuntu.

```bash
# Atualizar lista de pacotes disponíveis
sudo apt update

# Atualizar pacotes instalados
sudo apt upgrade

# Instalar um pacote
sudo apt install nome_do_pacote

# Remover um pacote
sudo apt remove nome_do_pacote

# Remover + ficheiros de configuração
sudo apt purge nome_do_pacote

# Pesquisar um pacote
apt search nome_do_pacote

# Ver info de um pacote
apt show nome_do_pacote
```

> [!important] `update` vs `upgrade`
> 
> - `apt update` → apenas atualiza a **lista** de pacotes disponíveis
> - `apt upgrade` → efetivamente **instala as atualizações** Faz sempre `update` antes de `upgrade` ou de instalar qualquer coisa.

### Repositórios

Os pacotes vêm de **repositórios** definidos em:

```
/etc/apt/sources.list
/etc/apt/sources.list.d/
```

---

## ⏰ Automatização com Cron Jobs

O **cron** é o agendador de tarefas do Linux. Permite executar comandos ou scripts automaticamente em horários definidos.

```bash
# Editar as cron jobs do utilizador atual
crontab -e

# Ver as cron jobs ativas
crontab -l

# Remover todas as cron jobs
crontab -r
```

### Sintaxe do Crontab

```
*  *  *  *  *  comando_a_executar
│  │  │  │  │
│  │  │  │  └── Dia da semana (0=Dom, 1=Seg, ..., 6=Sáb)
│  │  │  └───── Mês (1-12)
│  │  └──────── Dia do mês (1-31)
│  └─────────── Hora (0-23)
└────────────── Minuto (0-59)
```

### Exemplos práticos

```bash
# Executar todos os dias à meia-noite
0 0 * * * /home/user/backup.sh

# Executar de 5 em 5 minutos
*/5 * * * * /home/user/script.sh

# Executar às 9h de segunda a sexta
0 9 * * 1-5 /home/user/relatorio.sh

# Executar uma vez por mês, dia 1, à meia-noite
0 0 1 * * /home/user/mensal.sh
```

> [!tip] Gerador visual de cron Usa [crontab.guru](https://crontab.guru/) para construir e validar expressões cron facilmente.

---

## 📋 Logs do Sistema

Os logs são fundamentais em cibersegurança — guardam registo de tudo o que acontece no sistema.

### Localização dos logs

```
/var/log/
├── syslog         → log geral do sistema
├── auth.log       → autenticações, sudo, SSH logins
├── kern.log       → mensagens do kernel
├── dpkg.log       → pacotes instalados/removidos
├── apache2/       → logs do servidor web Apache
│   ├── access.log → pedidos HTTP recebidos
│   └── error.log  → erros do Apache
└── mysql/         → logs do MySQL
```

### Comandos para analisar logs

```bash
# Ver logs em tempo real
tail -f /var/log/syslog
tail -f /var/log/auth.log

# Pesquisar por tentativas de login falhadas
grep "Failed password" /var/log/auth.log

# Pesquisar por logins com sucesso via SSH
grep "Accepted password" /var/log/auth.log

# Ver últimos logins do sistema
last

# Ver logins falhados
lastb
```

> [!warning] Logs em Cibersegurança Durante um incidente, os logs são **evidência**. Em pentest, os atacantes tentam apagar os logs para cobrir os rastos. Como defensor, monitoriza-os com ferramentas como **Splunk**, **ELK Stack** ou **Wazuh**.

---

## 🔧 Serviços e Daemons (Systemd)

Os **serviços** (ou daemons) são processos que correm em background — servidores web, SSH, bases de dados, etc.

O gestor de serviços moderno no Linux é o **systemd**.

```bash
# Ver estado de um serviço
sudo systemctl status ssh

# Iniciar um serviço
sudo systemctl start ssh

# Parar um serviço
sudo systemctl stop ssh

# Reiniciar um serviço
sudo systemctl restart ssh

# Ativar serviço no arranque
sudo systemctl enable ssh

# Desativar serviço no arranque
sudo systemctl disable ssh

# Listar todos os serviços ativos
systemctl list-units --type=service --state=running
```

### Serviços comuns em servidores

|Serviço|Comando|Função|
|---|---|---|
|SSH|`ssh` / `sshd`|Acesso remoto seguro|
|Apache|`apache2`|Servidor web|
|Nginx|`nginx`|Servidor web alternativo|
|MySQL|`mysql`|Base de dados|
|Cron|`cron`|Agendador de tarefas|
|UFW|`ufw`|Firewall simples|

---

## 🔒 Firewall com UFW

O **UFW (Uncomplicated Firewall)** é a interface simplificada para gerir o `iptables`.

```bash
# Ativar/desativar firewall
sudo ufw enable
sudo ufw disable

# Ver estado e regras
sudo ufw status verbose

# Permitir uma porta
sudo ufw allow 22       # SSH
sudo ufw allow 80       # HTTP
sudo ufw allow 443      # HTTPS

# Bloquear uma porta
sudo ufw deny 23        # Telnet

# Apagar uma regra
sudo ufw delete allow 80

# Permitir de um IP específico
sudo ufw allow from 192.168.1.100
```

> [!important] Boas práticas de Firewall
> 
> - Bloqueia tudo por defeito, permite só o necessário (**default deny**)
> - Nunca bloquear a porta 22 sem ter acesso alternativo — ficas sem acesso remoto!

---

## 🏁 Rooms / Tarefas Completadas

- [x] Task 1 — Introdução ao módulo
- [x] Task 2 — Editores de texto (Nano e Vim)
- [x] Task 3 — Utilitários gerais (wget, curl, rede)
- [x] Task 4 — Gestão de pacotes com APT
- [x] Task 5 — Logs do sistema
- [x] Task 6 — Cron Jobs e automatização
- [x] Task 7 — Serviços e Systemd
- [x] Task 8 — Conclusão

---

## 🔗 Navegação

- [[THM - Linux Fundamentals 1]] ← Módulo 1
- [[THM - Linux Fundamentals 2]] ← Módulo anterior
- [ ] Próximo: explorar [[THM - Bash Scripting]] ou [[THM - Network Fundamentals]]

---

## 📚 Recursos Úteis

- [TryHackMe — Linux Fundamentals 3](https://tryhackme.com/room/linuxfundamentalspart3)
- [Crontab Guru](https://crontab.guru/) — validar expressões cron
- [ExplainShell](https://explainshell.com/) — explicar comandos
- [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/) — prática de Linux em CTF

---

_Nota criada após conclusão do módulo · TryHackMe · Cyber Security 101_