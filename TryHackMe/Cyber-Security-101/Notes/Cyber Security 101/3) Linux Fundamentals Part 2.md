# 🐧 Linux Fundamentals 2

> **Plataforma:** TryHackMe  
> **Caminho:** Cyber Security 101  
> **Estado:** ✅ Concluído  
> **Tags:** #linux #thm #cybersecurity101 #fundamentos #terminal #ssh #permissões

---

## 📌 Resumo do Módulo

Continuação do estudo do Linux, com foco em **acesso remoto via SSH**, **flags e switches de comandos**, **sistema de permissões**, **variáveis de ambiente** e **utilitários comuns**. Este módulo aprofunda a interação com o sistema e prepara para a administração real de servidores.

---

## 🔐 Acesso Remoto com SSH

O **SSH (Secure Shell)** é o protocolo padrão para acesso remoto seguro a máquinas Linux.

```bash
ssh utilizador@IP_da_maquina
# Exemplo:
ssh tryhackme@10.10.10.10
```

- Comunicação **encriptada** (substituiu o Telnet)
- Usa a porta **22** por defeito
- Pode autenticar com **password** ou **chave SSH (mais seguro)**

> [!tip] Chaves SSH Em vez de password, podes usar um par de chaves pública/privada com `ssh-keygen`. A chave pública fica no servidor (`~/.ssh/authorized_keys`) e a privada fica contigo.

---

## 🚩 Flags e Switches

Os comandos Linux aceitam **flags** (modificadores) que alteram o seu comportamento.

```bash
ls        # listagem simples
ls -a     # inclui ficheiros ocultos
ls -l     # formato longo com detalhes
ls -la    # combinação de ambos
ls -lh    # tamanhos legíveis (KB, MB)
ls -t     # ordena por data de modificação
```

### Como descobrir flags disponíveis

```bash
# Opção 1 — Manual completo
man ls

# Opção 2 — Ajuda rápida
ls --help

# Navegar no man: usa as setas, 'q' para sair, '/' para pesquisar
```

> [!important] Páginas `man` As páginas de manual (`man`) são a documentação oficial de cada comando. São essenciais para trabalhar de forma autónoma no Linux.

---

## 👤 Utilizadores e Grupos

O Linux é um sistema **multi-utilizador**. Cada utilizador pertence a um ou mais grupos.

### Ficheiros importantes

|Ficheiro|Conteúdo|
|---|---|
|`/etc/passwd`|Lista de todos os utilizadores do sistema|
|`/etc/shadow`|Passwords encriptadas (só root acede)|
|`/etc/group`|Lista de grupos e os seus membros|

```bash
# Ver utilizador atual
whoami

# Ver a que grupos pertenço
id

# Mudar para outro utilizador
su outro_utilizador

# Mudar para root
sudo su
```

---

## 🔑 Permissões em Detalhe

### Estrutura completa

```
-  r w x  r w x  r w x
↑  ↑↑↑↑  ↑↑↑↑  ↑↑↑↑
│  Dono   Grupo  Outros
│
└── Tipo: - ficheiro | d diretório | l link simbólico
```

### Valores numéricos (Octal)

|Permissão|Valor|
|---|---|
|`r` (read)|**4**|
|`w` (write)|**2**|
|`x` (execute)|**1**|
|Sem permissão|**0**|

```bash
# Exemplos comuns
chmod 777 ficheiro   # rwxrwxrwx — todos têm tudo (⚠️ inseguro)
chmod 755 ficheiro   # rwxr-xr-x — dono tem tudo, resto só lê/executa
chmod 644 ficheiro   # rw-r--r-- — dono lê/escreve, resto só lê
chmod 600 ficheiro   # rw------- — só o dono acede (chaves SSH!)
```

### Alterar dono e grupo

```bash
chown utilizador ficheiro          # muda o dono
chown utilizador:grupo ficheiro    # muda dono e grupo
chgrp grupo ficheiro               # muda só o grupo
```

---

## 🌐 Variáveis de Ambiente

As variáveis de ambiente guardam informação do sistema e do utilizador.

```bash
# Ver todas as variáveis
env

# Ver uma variável específica
echo $HOME
echo $USER
echo $PATH
echo $SHELL
```

### Variáveis mais importantes

|Variável|Descrição|
|---|---|
|`$HOME`|Diretório home do utilizador (`/home/user`)|
|`$USER`|Nome do utilizador atual|
|`$PATH`|Diretórios onde o shell procura executáveis|
|`$SHELL`|Shell em uso (ex: `/bin/bash`)|
|`$PWD`|Diretório atual (mesmo que `pwd`)|

```bash
# Definir uma variável temporária
export MINHA_VAR="valor"

# Torná-la permanente — adiciona ao ficheiro:
echo 'export MINHA_VAR="valor"' >> ~/.bashrc
source ~/.bashrc
```

---

## 🛠️ Utilitários Comuns

### Editar ficheiros de texto

```bash
nano ficheiro.txt    # editor simples, amigo de iniciantes
vim ficheiro.txt     # editor poderoso, curva de aprendizagem maior
```

> [!tip] Nano — Atalhos básicos
> 
> - `Ctrl + O` → Guardar
> - `Ctrl + X` → Sair
> - `Ctrl + W` → Pesquisar

### Transferência de ficheiros

```bash
# Descarregar ficheiro da internet
wget https://exemplo.com/ficheiro.zip

# Cópia segura entre máquinas (via SSH)
scp ficheiro.txt user@10.10.10.10:/home/user/
scp user@10.10.10.10:/home/user/ficheiro.txt .
```

### Processos

```bash
ps aux            # lista todos os processos em execução
top               # monitor de processos em tempo real (como Task Manager)
kill PID          # termina processo pelo ID
kill -9 PID       # força terminar processo
```

---

## 📁 Diretórios Importantes do Sistema

|Diretório|Função|
|---|---|
|`/etc`|Configurações do sistema e serviços|
|`/var/log`|Logs do sistema (`auth.log`, `syslog`, etc.)|
|`/tmp`|Ficheiros temporários (limpos no reboot)|
|`/proc`|Info sobre processos e hardware (virtual)|
|`/dev`|Dispositivos de hardware como ficheiros|
|`~` ou `$HOME`|Diretório pessoal do utilizador|

> [!warning] `/tmp` em Pentest O diretório `/tmp` é frequentemente usado em exploits e pós-exploração porque qualquer utilizador pode escrever nele.

---

## 🔗 Ligações (Links)

```bash
# Link simbólico (como um atalho)
ln -s /caminho/original /caminho/link

# Link físico (hard link)
ln /caminho/original /caminho/link
```

|Tipo|Característica|
|---|---|
|**Simbólico**|Aponta para o caminho — quebra se o original for apagado|
|**Hard Link**|Aponta para os dados — persiste mesmo sem o original|

---

## 🏁 Rooms / Tarefas Completadas

- [x] Task 1 — Introdução ao módulo
- [x] Task 2 — Acesso remoto com SSH
- [x] Task 3 — Flags, switches e páginas `man`
- [x] Task 4 — Ficheiros e permissões do sistema
- [x] Task 5 — Variáveis de ambiente
- [x] Task 6 — Utilitários comuns (nano, wget, scp)
- [x] Task 7 — Processos
- [x] Task 8 — Conclusão

---

## 🔗 Navegação

- [[THM - Linux Fundamentals 1]] ← Módulo anterior
- [ ] [[THM - Linux Fundamentals 3]] → Automatização, cron jobs, logs, serviços

---

## 📚 Recursos Úteis

- [TryHackMe — Linux Fundamentals 2](https://tryhackme.com/room/linuxfundamentalspart2)
- [ExplainShell](https://explainshell.com/) — explica qualquer comando
- [SS64 — Referência de comandos Linux](https://ss64.com/bash/)
- [LinuxCommand.org](https://linuxcommand.org/) — guia completo para iniciantes

---

_Nota criada após conclusão do módulo · TryHackMe · Cyber Security 101_