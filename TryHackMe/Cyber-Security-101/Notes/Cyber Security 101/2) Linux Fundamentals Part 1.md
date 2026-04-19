# 🐧 Linux Fundamentals 1

> **Plataforma:** TryHackMe  
> **Caminho:** Cyber Security 101  
> **Estado:** ✅ Concluído  
> **Tags:** #linux #thm #cybersecurity101 #fundamentos #terminal

---

## 📌 Resumo do Módulo

Introdução ao sistema operativo **Linux** — o sistema mais utilizado em servidores, dispositivos embebidos e ambientes de cibersegurança. Este módulo cobre a navegação básica, interação com o sistema de ficheiros e execução de comandos fundamentais na linha de comandos.

---

## 🖥️ Porquê Linux em Cibersegurança?

- A maioria dos servidores web e infraestruturas correm Linux
- Ferramentas de segurança como **Metasploit**, **Nmap**, **Wireshark** são nativas em Linux
- Distribuições como **Kali Linux** e **Parrot OS** são baseadas nele
- Conhecimento de Linux é essencial para pentesters, analistas SOC e sysadmins

---

## 📂 Sistema de Ficheiros Linux

```
/
├── bin/       → Binários essenciais do sistema
├── etc/       → Ficheiros de configuração
├── home/      → Diretórios dos utilizadores
├── var/       → Dados variáveis (logs, etc.)
├── tmp/       → Ficheiros temporários
├── usr/       → Programas e utilitários do utilizador
└── root/      → Diretório home do utilizador root
```

> 💡 **Nota:** No Linux, **tudo é um ficheiro** — dispositivos, processos e sockets são representados como ficheiros.

---

## ⌨️ Comandos Essenciais

### 🔍 Navegação e Exploração

|Comando|Descrição|Exemplo|
|---|---|---|
|`pwd`|Mostra o diretório atual|`pwd` → `/home/user`|
|`ls`|Lista ficheiros e pastas|`ls -la`|
|`cd`|Muda de diretório|`cd /etc`|
|`file`|Identifica o tipo de ficheiro|`file nota.txt`|
|`find`|Procura ficheiros no sistema|`find / -name "*.txt"`|

### 📄 Visualização de Ficheiros

|Comando|Descrição|Exemplo|
|---|---|---|
|`cat`|Mostra o conteúdo de um ficheiro|`cat /etc/passwd`|
|`less`|Visualização paginada|`less ficheiro.txt`|
|`head`|Primeiras 10 linhas|`head -n 5 ficheiro.txt`|
|`tail`|Últimas 10 linhas|`tail -n 5 ficheiro.txt`|

### 🔎 Pesquisa e Filtros

|Comando|Descrição|Exemplo|
|---|---|---|
|`grep`|Filtra linhas por padrão|`grep "root" /etc/passwd`|
|`wc`|Conta linhas/palavras/caracteres|`wc -l ficheiro.txt`|
|`sort`|Ordena o output|`sort nomes.txt`|
|`uniq`|Remove duplicados|`sort \| uniq`|

### 📁 Manipulação de Ficheiros

|Comando|Descrição|Exemplo|
|---|---|---|
|`touch`|Cria um ficheiro vazio|`touch nota.txt`|
|`mkdir`|Cria um diretório|`mkdir pasta`|
|`cp`|Copia ficheiros|`cp a.txt b.txt`|
|`mv`|Move / Renomeia|`mv a.txt /tmp/`|
|`rm`|Remove ficheiros|`rm -rf pasta/`|

---

## 🔗 Operadores de Shell

|Operador|Função|Exemplo|
|---|---|---|
|`&`|Executa em background|`sleep 10 &`|
|`&&`|Executa o 2º se o 1º tiver sucesso|`mkdir test && cd test`|
|`>`|Redireciona output (substitui)|`echo "ola" > ficheiro.txt`|
|`>>`|Redireciona output (acrescenta)|`echo "mais" >> ficheiro.txt`|
|`\|`|Pipe — passa output para o próximo|`cat ficheiro \| grep "root"`|

---

## 👤 Utilizadores e Permissões (Introdução)

- **`whoami`** → mostra o utilizador atual
- **`su`** → muda de utilizador
- **`sudo`** → executa comando como superutilizador

### Estrutura de Permissões

```
-rwxr-xr-- 1 user group 1234 Jan 1 ficheiro.txt
 ↑↑↑ ↑↑↑ ↑↑↑
 │   │   └── Outros
 │   └─────── Grupo
 └─────────── Dono
```

|Símbolo|Significado|
|---|---|
|`r`|Leitura (read)|
|`w`|Escrita (write)|
|`x`|Execução (execute)|
|`-`|Sem permissão|

---

## 📝 Conceitos-Chave para Lembrar

> [!important] Flag `-la` no `ls` `ls -la` mostra **todos os ficheiros** (incluindo ocultos com `.`) com detalhes de permissões, dono, tamanho e data.

> [!tip] Ficheiros ocultos no Linux Qualquer ficheiro que começa com `.` está oculto. Ex: `.bashrc`, `.ssh/`

> [!warning] Cuidado com `rm -rf` Este comando apaga recursivamente **sem confirmação**. Não há "Recycle Bin" no Linux.

---

## 🏁 Rooms / Tarefas Completadas

- [x] Task 1 — Introdução ao Linux
- [x] Task 2 — Acesso à máquina (SSH / Browser)
- [x] Task 3 — Comandos básicos (`echo`, `whoami`)
- [x] Task 4 — Interagir com o sistema de ficheiros
- [x] Task 5 — Procura de ficheiros (`find`, `grep`)
- [x] Task 6 — Shell Operators
- [x] Task 7 — Conclusão

---

## 🔗 Próximos Passos

- [ ] [[THM - Linux Fundamentals 2]] → Permissões, variáveis de ambiente, processos
- [ ] [[THM - Linux Fundamentals 3]] → Automatização, tarefas, logs
- [ ] Praticar comandos num terminal Linux real (WSL / VM / VPS)

---

## 📚 Recursos Úteis

- [TryHackMe — Linux Fundamentals 1](https://tryhackme.com/room/linuxfundamentalspart1)
- [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/) — prática de comandos Linux
- [ExplainShell](https://explainshell.com/) — explica qualquer comando Linux

---

_Nota criada após conclusão do módulo · TryHackMe · Cyber Security 101_