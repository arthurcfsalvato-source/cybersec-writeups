---
tags:
  - tryhackme
  - pre-security
  - osint
  - linux
  - cybersecurity
aliases:
  - Search Skills
  - THM Search Skills
date: 2026-04-16
path: Pre Security Path
status: completo
---

# THM — Pre Security Path — Search Skills

> [!info] Visão Geral do Módulo
> Este módulo foca em **encontrar informação de forma eficaz** — desde avaliar a qualidade das fontes até usar ferramentas especializadas de OSINT. O objetivo é desenvolver sentido crítico antes de confiar em qualquer ferramenta ou recurso de segurança.

---

## 📋 Módulos abordados

- Módulo 1 — Avaliação de Fontes & Comando `ss`
- Módulo 2 — Pesquisa Avançada no Google
- Módulo 3 — Ferramentas OSINT Especializadas
- Módulo 4 — CVE & Exploit Database
- Módulo 5 — Documentação Técnica (Linux & Windows)
- Módulo 6 — Redes Sociais como Fonte de Informação

---

## Módulo 1 — Avaliação de Fontes & Ferramentas Criptográficas

O primeiro passo antes de usar qualquer ferramenta de segurança é **avaliar bem a sua fonte**. É aqui que entra o conceito de ==Snake Oil==.

> [!warning] Snake Oil[^1]
> Termo usado na criptografia para descrever produtos que se apresentam como seguros mas que na prática são fracos, mal implementados ou deliberadamente enganosos. Analogia com os charlatões do século XIX que vendiam "óleo de cobra" como remédio milagroso.

Para não cair em snake oil, avaliar sempre pelos critérios:
- **Fonte** — quem escreveu? tem credibilidade?
- **Evidências** — há testes independentes? auditorias públicas?
- **Objetividade** — a comunicação é honesta ou exagerada?
- **Transparência** — o algoritmo é aberto para revisão por pares?

---

### Comando `ss` (Socket Statistics)

O ==ss== é o comando moderno que **substitui o `netstat`** em sistemas Linux. Faz parte do pacote `iproute2` e é mais rápido e completo que o `netstat` (pacote `net-tools`, hoje considerado obsoleto).

**O que ele mostra:**

- Conexões TCP/UDP ativas
- Portas abertas e em escuta (listening)
- Endereços IP locais e remotos conectados
- Estado das conexões (`ESTABLISHED`, `LISTEN`, `TIME-WAIT`, etc.)

**Exemplos de uso comuns:**

```bash
ss -tuln      # mostra portas TCP/UDP abertas (sem resolver nomes)
ss -ta        # todas as conexões TCP
ss -s         # resumo estatístico das conexões
ss -p         # mostra qual processo está usando cada conexão
```

**Na prática, serve para:**

- Ver se um serviço está realmente a escutar numa porta
- Detetar conexões suspeitas (útil em segurança)
- Diagnosticar problemas de rede
- Ver quais programas estão a usar a rede

---

## Módulo 2 — Pesquisa Avançada no Google

Usar operadores de pesquisa permite filtrar resultados de forma muito mais precisa — habilidade essencial para **reconhecimento passivo (OSINT)**.

| Operador | Exemplo | O que faz |
|---|---|---|
| `"termo"` | `"hacker ético"` | Pesquisa a frase exata |
| `site:` | `site:tryhackme.com falha` | Pesquisa apenas naquele domínio |
| `filetype:` | `filetype:ppt cyber security` | Filtra por tipo de ficheiro |
| `-` | `segurança -windows` | Exclui o termo dos resultados |
| `OR` | `hacker OR pentester` | Mostra resultados com um ou outro |

> [!tip] Recurso útil
> [Lista completa de operadores de pesquisa avançada](https://github.com/cipher387/Advanced-search-operators-list) — tem todos os operadores para Google, Bing, GitHub, Shodan, etc.

---

## Módulo 3 — Ferramentas OSINT Especializadas

Ferramentas mais poderosas que os motores de busca convencionais, cada uma com um foco específico.

---

### 🔍 Shodan

[Shodan](https://www.shodan.io/) é um motor de busca para **dispositivos conectados à Internet**. Ao contrário do Google, que indexa páginas web, o Shodan indexa **banners de serviços e metadados de dispositivos** expostos — servidores, routers, webcams, sistemas industriais (ICS/SCADA) e dispositivos IoT.

**Exemplo de uso:**

```
apache 2.4.1
```

Retorna todos os servidores que ainda correm essa versão, com distribuição por país.

> [!tip] Links úteis
> - [Exemplos de consultas Shodan](https://www.shodan.io/search/examples)
> - [Shodan Trends](https://trends.shodan.io/) — dados históricos (requer subscrição)

---

### 🔍 Censys

[Censys](https://search.censys.io/) parece semelhante ao Shodan, mas o foco é diferente:

| | Shodan | Censys |
|---|---|---|
| **Foco** | Dispositivos e sistemas (IoT, routers, webcams) | Hosts, websites, certificados TLS/SSL |
| **Uso típico** | Detetar dispositivos expostos | Auditar portas, enumerar domínios, descobrir ativos não autorizados |

> [!tip] Documentação
> [Casos de Uso Introdutórios do Censys](https://docs.censys.com/docs/ls-introductory-use-cases#/)

---

### 🦠 VirusTotal

[VirusTotal](https://www.virustotal.com/) verifica **ficheiros, URLs e hashes** através de múltiplos motores antivírus em simultâneo (67+). 

**O que aceita:**
- Upload de ficheiros
- URLs para verificar
- Hashes de ficheiros (para verificar resultados de uploads anteriores)

> [!note] Falsos Positivos
> Um ficheiro legítimo pode ser sinalizado incorretamente. Os **comentários da comunidade** são úteis para esclarecer esses casos.

---

### 🔓 Have I Been Pwned (HIBP)

[Have I Been Pwned](https://haveibeenpwned.com/) faz uma coisa: **verifica se um e-mail apareceu num vazamento de dados**.

- Se o e-mail estiver comprometido → as credenciais associadas foram expostas
- Risco agravado por **reutilização de passwords** em múltiplas plataformas
- As passwords costumam estar em formato criptografado, mas muitas são fracas e recuperáveis via ataques de dicionário

---

## Módulo 4 — CVE & Bases de Dados de Vulnerabilidades

### CVE — Common Vulnerabilities and Exposures[^2]

O programa CVE funciona como um **dicionário padronizado de vulnerabilidades**. Cada vulnerabilidade recebe um identificador único no formato:

```
CVE-[ANO]-[NÚMERO]
```

**Exemplo:** `CVE-2024-29988`

Esse ID garante que investigadores, fornecedores e profissionais de TI estejam todos a falar da mesma vulnerabilidade.

**Fontes oficiais de consulta:**

| Recurso | URL | O que oferece |
|---|---|---|
| CVE Program | [cve.org](https://www.cve.org/) | Base oficial de CVEs |
| NVD (NIST) | [nvd.nist.gov](https://nvd.nist.gov/) | Inclui pontuação CVSS e detalhes técnicos |

> [!example] Exemplo histórico
> `CVE-2014-0160` — também conhecido como **Heartbleed**, uma das vulnerabilidades mais críticas já descobertas, afetando a biblioteca OpenSSL.

---

### Exploit Database

O [Exploit Database](https://www.exploit-db.com/) lista **códigos de exploração** para vulnerabilidades conhecidas. Alguns exploits estão marcados como **verificados** — foram testados e confirmados.

Útil para:
- Pesquisa durante pentests
- Compreender como uma vulnerabilidade é explorada na prática
- Usar com `searchsploit` localmente via linha de comandos

---

## Módulo 5 — Documentação Técnica

### Linux — Páginas de Manual (man pages)

Muito antes da internet, a forma de obter ajuda num sistema Linux/Unix era consultar a **man page** do comando. Hoje continua a ser a referência mais completa e fiável.

```bash
man ip        # manual do comando ip
man ss        # manual do comando ss
man 8 ip      # secção 8 (comandos de administração)
```

As man pages estão organizadas em secções:

| Secção | Conteúdo |
|---|---|
| 1 | Comandos do utilizador |
| 2 | Chamadas ao sistema |
| 3 | Funções de biblioteca C |
| 5 | Formatos de ficheiros |
| 8 | Comandos de administração |

> [!tip] Online
> Pesquisar `man ip` no browser também funciona — [linux.die.net](https://linux.die.net/man/8/ip) costuma estar no topo dos resultados.

---

### Windows — Documentação Microsoft

A Microsoft centraliza toda a documentação técnica oficial em [learn.microsoft.com](https://learn.microsoft.com/) — referência para comandos, PowerShell, APIs e administração de sistemas Windows.

---

### Princípio Geral

> [!important]
> Consultar **sempre a documentação oficial** como primeira fonte. É a mais atualizada, completa e fiável — independentemente da plataforma.

---

## Módulo 6 — Redes Sociais & OSINT Humano

As redes sociais são uma fonte rica de informação para profissionais de cibersegurança — tanto para proteger organizações como para recolher informação em reconhecimento passivo.

### Aplicações em Cibersegurança

- Avaliar o excesso de partilha de informação por colaboradores
- Descobrir respostas a **perguntas de segurança** (ex.: escola de infância, cidade natal)
- Mapear a estrutura de uma organização
- Manter-se atualizado sobre tendências e ameaças

### Plataformas e Casos de Uso

| Plataforma | Uso em OSINT |
|---|---|
| **LinkedIn** | Competências técnicas, cargos, percurso profissional — identificar targets |
| **Facebook** | Informação pessoal: escola, localização, família — útil para engenharia social |
| **Twitter / X** | Declarações públicas, posicionamentos técnicos, informação partilhada |
| **GitHub** | Repositórios públicos com credenciais, tokens de API ou código sensível expostos |

> [!example] Exercício do módulo
> - **"Qual rede social usarias para saber o conhecimento técnico de um funcionário?"** → **LinkedIn**
> - **"Qual rede para descobrir a escola de infância de alguém?"** → **Facebook**

### Boas Práticas de Investigação

- Explorar plataformas desconhecidas com um **e-mail temporário**
- Encerrar contas criadas apenas para investigação após concluir
- Nunca usar contas pessoais para investigar alvos
- Seguir canais e grupos especializados para atualização técnica contínua

---

## ⚡ Conceitos-Chave para Memorizar

> [!summary] Revisão Rápida
> - **Snake Oil** = produto criptográfico que parece seguro mas não é — sempre verificar fonte e evidências
> - **`ss`** substitui `netstat` — Socket Statistics, parte do `iproute2`
> - **`site:`, `filetype:`, `""`** — operadores essenciais de pesquisa avançada
> - **Shodan** = dispositivos IoT/servidores expostos | **Censys** = hosts, certificados, domínios
> - **VirusTotal** = verificar ficheiros/URLs com 67+ antivírus
> - **HIBP** = verificar se um e-mail foi exposto em vazamentos
> - **CVE** = identificador padronizado para vulnerabilidades (`CVE-ANO-NÚMERO`)
> - **NVD** = base do NIST com pontuação CVSS por CVE
> - **Exploit DB** = códigos de exploração para vulnerabilidades conhecidas
> - **man pages** = documentação oficial de comandos Linux
> - **LinkedIn** = info técnica/profissional | **Facebook** = info pessoal

---

## 🔗 Próximos Passos

### Sequencial

- **→** [[Network Fundamentals — Pre Security Path]]
- **→** How The Web Works (HTTP, HTTPS, DNS, Cookies)
- **→** Linux Fundamentals (CLI, permissões, bash)
- **→** Windows Fundamentals (Active Directory, PowerShell)

### Tópicos Relacionados

- **Reconhecimento passivo aprofundado:** [[OSINT — Técnicas Avançadas]]
- **CVE e exploits na prática:** [[Vulnerability Assessment]]
- **Engenharia Social:** [[Social Engineering — Técnicas]]

### Ferramentas Mencionadas

- [Shodan](https://www.shodan.io/)
- [Censys](https://search.censys.io/)
- [VirusTotal](https://www.virustotal.com/)
- [Have I Been Pwned](https://haveibeenpwned.com/)
- [CVE Program](https://www.cve.org/)
- [NVD — NIST](https://nvd.nist.gov/)
- [Exploit Database](https://www.exploit-db.com/)
- [Operadores de Pesquisa Avançada](https://github.com/cipher387/Advanced-search-operators-list)

---

[^1]: **Snake Oil** — é o termo usado na criptografia para descrever métodos, algoritmos ou produtos que se apresentam como seguros mas que na prática são fracos, mal implementados ou deliberadamente enganosos. A analogia vem dos charlatões do século XIX que vendiam "óleo de cobra" como remédio milagroso.

[^2]: **CVE (Common Vulnerabilities and Exposures)** — sistema padronizado de identificação de vulnerabilidades divulgadas publicamente. Mantido pela MITRE Corporation.
