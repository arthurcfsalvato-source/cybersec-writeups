# 🌐 How The Web Works — Pre Security Path (TryHackMe)

> **Caminho:** Pre Security → How The Web Works  
> **Objetivo:** Entender como funciona a Web por baixo dos panos — desde o que acontece quando escreves um URL até como os servidores respondem.

---

## 🔗 Navegação Inteligente

### Sequencial
- **← Anterior:** 2) Network Fundamentals (OSI, TCP/IP, Portas)
- **Próximo →:** 4) Computer Fundamentals (CPU, RAM, Storage, Hardware)
- **Depois:** 5) Operating Systems Basics (Windows, Linux, CLI)
- **Final:** 7) Attacks and Defenses (Segurança avançada)

### Tópicos Relacionados Nesta Nota
- **DNS em profundidade:** Ver também em 2) Network Fundamentals — DNS
- **HTTP/HTTPS Protocolos:** Ver também em 2) Network Fundamentals — Portas e Protocolos
- **Segurança Web:** Ver em 7) Attacks and Defenses — SQL Injection e XSS
- **Criptografia HTTPS:** Ver em 7) Attacks and Defenses — Criptografia
- **Firewalls & WAF:** Ver em 5) Operating Systems Basics — Defesas

### Referencias Rapidas
- **⚡ Quick Reference** — Protocolos HTTP, DNS, códigos de estado
- **🔑 Conceitos-Chave** — Mapa tematico (web, segurança)

---

## 📚 Índice

- #DNS — Como os nomes viram IPs
- #HTTP e HTTPS — A linguagem da Web
- #Como Funciona um Website
- #Outros Componentes da Web

---

## 🔍 DNS — Como os nomes viram IPs

### O que é o DNS?

Quando escreves `www.google.com` no browser, o teu computador não sabe onde esse site está. Ele precisa de descobrir o **endereço IP** do servidor onde o site está hospedado.

O **DNS (Domain Name System)** é o sistema que faz essa tradução:

```
www.google.com  →  142.250.74.46
```

Pensa no DNS como a **agenda de contactos do telemóvel** — em vez de memorizares números (IPs), memorizas nomes (domínios).

---

### 🏗️ Hierarquia de Domínios

Um domínio tem uma estrutura hierárquica, lida da direita para a esquerda:

```
         subdomínio . domínio . TLD
              www  . google  . com
```

|Parte|Nome|Explicação|
|---|---|---|
|`.com`|TLD (Top-Level Domain)|O nível mais alto. Pode ser genérico (.com, .net, .org) ou por país (.pt, .uk, .de)|
|`google`|Domínio de segundo nível|O nome que a empresa/pessoa regista|
|`www`|Subdomínio|Uma divisão dentro do domínio principal|

**Exemplos de subdomínios:**

- `mail.google.com` → serviço de email
- `drive.google.com` → serviço de armazenamento
- `admin.tryhackme.com` → painel de administração

> ⚠️ Em cibersegurança, **subdomínios** são alvos frequentes em reconnaissance — podem revelar serviços escondidos ou painéis de admin.

---

### 📋 Tipos de Registos DNS

Quando o DNS responde a uma consulta, devolve um **registo**. Existem vários tipos:

---

#### Registo A

- Associa um domínio a um **endereço IPv4**
- Exemplo: `tryhackme.com → 104.22.55.228`

---

#### Registo AAAA

- Associa um domínio a um **endereço IPv6**
- Exemplo: `tryhackme.com → 2606:4700::6816:37e4`

---

#### Registo CNAME (Canonical Name)

- Aponta um domínio para **outro domínio** (alias/apelido)
- Exemplo: `shop.tryhackme.com → stores.shopify.com`
- Útil quando o serviço real está noutro servidor

---

#### Registo MX (Mail Exchange)

- Indica qual o servidor responsável pelo **email** do domínio
- Tem prioridade — o número mais baixo tem prioridade maior
- Exemplo: `tryhackme.com → alt1.aspmx.l.google.com` (prioridade 5)

---

#### Registo TXT

- Contém **texto livre** — usado para vários fins
- Verificação de propriedade do domínio (Google, Microsoft)
- Configurações de email anti-spam (SPF, DKIM)
- Exemplo: `"v=spf1 include:_spf.google.com ~all"`

---

### 🔄 Como Funciona uma Consulta DNS (Passo a Passo)

Quando escreves `www.tryhackme.com`:

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                   │
│  1. O teu PC verifica a cache local — já sabe o IP?              │
│     → Sim: usa diretamente                                        │
│     → Não: continua...                                            │
│                                                                   │
│  2. Pergunta ao DNS Resolver (normalmente do teu ISP ou 8.8.8.8) │
│     → Tem em cache? Usa e responde                                │
│     → Não tem: continua...                                        │
│                                                                   │
│  3. O Resolver pergunta ao Root DNS Server                        │
│     → "Quem sabe sobre .com?"                                     │
│     → Root responde: "Fala com o TLD Server do .com"             │
│                                                                   │
│  4. O Resolver pergunta ao TLD Server (.com)                      │
│     → "Quem sabe sobre tryhackme.com?"                           │
│     → TLD responde: "Fala com o Authoritative Name Server"       │
│                                                                   │
│  5. O Resolver pergunta ao Authoritative Name Server              │
│     → "Qual é o IP de www.tryhackme.com?"                        │
│     → Responde: "104.22.55.228" (registo A)                      │
│                                                                   │
│  6. O Resolver devolve o IP ao teu PC                             │
│                                                                   │
│  7. O teu PC conecta ao IP 104.22.55.228                          │
│                                                                   │
└─────────────────────────────────────────────────────────────────┘
```

---

### ⏱️ TTL — Time To Live no DNS

- Cada registo DNS tem um **TTL** (em segundos)
- Indica quanto tempo o registo pode ficar em **cache**
- TTL baixo (ex: 300s = 5 min) → mudanças propagam rápido
- TTL alto (ex: 86400s = 24h) → menos consultas, mas mudanças demoram a propagar

---

### 🛠️ Comandos DNS Úteis

```bash
# Consultar o IP de um domínio
nslookup tryhackme.com

# Consulta avançada (Linux/Mac)
dig tryhackme.com
dig tryhackme.com MX        # ver registos MX
dig tryhackme.com TXT       # ver registos TXT
dig tryhackme.com ANY       # ver todos os registos

# Limpar cache DNS
ipconfig /flushdns           # Windows
sudo systemd-resolve --flush-caches  # Linux
```

---

## 🌐 HTTP e HTTPS — A Linguagem da Web

### O que é HTTP?

**HTTP (HyperText Transfer Protocol)** é o protocolo que define como o teu browser **pede** recursos ao servidor e como o servidor **responde**.

É uma linguagem comum entre o browser e o servidor web.

**HTTPS** = HTTP com **encriptação TLS/SSL** — os dados viajam cifrados, protegidos de interceção.

> 💡 Sempre que vês o 🔒 no browser, estás a usar HTTPS. Nunca introduzas passwords em sites HTTP!

---

### 🏗️ Anatomia de um URL

Um **URL (Uniform Resource Locator)** é o endereço completo de um recurso na web:

```
https://www.exemplo.com:443/pagina/sobre?nome=pedro&idade=25#secção
  │         │            │      │               │              │
  │         │            │      │               │              └─ Fragmento (âncora na página)
  │         │            │      │               └─ Query String (parâmetros)
  │         │            │      └─ Path (caminho/página)
  │         │            └─ Porta (opcional, 443 é o default do HTTPS)
  │         └─ Domínio
  └─ Esquema/Protocolo (http ou https)
```

|Parte|Exemplo|Explicação|
|---|---|---|
|**Esquema**|`https://`|Protocolo a usar|
|**Domínio**|`www.exemplo.com`|Servidor a contactar|
|**Porta**|`:443`|Porta (80=HTTP, 443=HTTPS)|
|**Path**|`/pagina/sobre`|Caminho para o recurso|
|**Query String**|`?nome=pedro&idade=25`|Parâmetros enviados ao servidor|
|**Fragmento**|`#secção`|Âncora na página (só no browser)|

---

### 📤 Métodos HTTP (Verbos)

Os métodos definem **o que o browser quer fazer**:

|Método|Uso|Exemplo|
|---|---|---|
|**GET**|Pedir/obter um recurso|Abrir uma página web|
|**POST**|Enviar dados para o servidor|Submeter um formulário de login|
|**PUT**|Criar ou substituir um recurso|Fazer upload de um ficheiro|
|**DELETE**|Apagar um recurso|Apagar uma conta|
|**PATCH**|Atualizar parte de um recurso|Mudar só o email do perfil|

> 💡 Em **pentest**, os métodos PUT e DELETE mal configurados podem ser vulnerabilidades sérias!

---

### 📨 Pedido HTTP (Request)

Quando o teu browser acede a um site, envia um **pedido HTTP**. Tem esta estrutura:

```http
GET /page HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 (Windows NT 10.0) Chrome/120.0.0.0
Accept-Language: pt-PT,pt;q=0.9
Accept: text/html,application/xhtml+xml
Connection: keep-alive
```

|Linha/Campo|Explicação|
|---|---|
|`GET /page HTTP/1.1`|Método + caminho + versão do protocolo|
|`Host`|O domínio que estamos a contactar|
|`User-Agent`|Identifica o browser e sistema operativo|
|`Accept-Language`|Idioma preferido para a resposta|
|`Accept`|Tipos de conteúdo aceites|
|`Connection: keep-alive`|Manter a ligação aberta para mais pedidos|

> ⚠️ O **User-Agent** pode ser falsificado! É uma das formas de fazer **web scraping** ou contornar restrições.

---

### 📩 Resposta HTTP (Response)

O servidor responde com:

```http
HTTP/1.1 200 OK
Server: nginx/1.18.0
Date: Sun, 29 Mar 2026 12:00:00 GMT
Content-Type: text/html; charset=utf-8
Content-Length: 4532
Set-Cookie: SessionId=abc123; Secure; HttpOnly

<!DOCTYPE html>
<html>
  <head><title>TryHackMe</title></head>
  <body>...</body>
</html>
```

|Campo|Explicação|
|---|---|
|`HTTP/1.1 200 OK`|Versão + código de status|
|`Server`|Software do servidor web|
|`Content-Type`|Tipo de conteúdo enviado|
|`Content-Length`|Tamanho em bytes|
|`Set-Cookie`|Define um cookie no browser|

---

### 🔢 Códigos de Estado HTTP

Os códigos dizem o que aconteceu com o pedido:

#### ✅ 2xx — Sucesso

|Código|Significado|
|---|---|
|**200 OK**|Tudo correu bem, aqui está o que pediste|
|**201 Created**|Recurso criado com sucesso|

#### ↪️ 3xx — Redirecionamentos

|Código|Significado|
|---|---|
|**301 Moved Permanently**|A página mudou de endereço permanentemente|
|**302 Found**|Redirecionamento temporário|

#### ❌ 4xx — Erros do Cliente

|Código|Significado|
|---|---|
|**400 Bad Request**|O pedido está mal formado|
|**401 Unauthorized**|Precisas de fazer login|
|**403 Forbidden**|Estás logado mas não tens permissão|
|**404 Not Found**|A página não existe|
|**405 Method Not Allowed**|Método não permitido (ex: DELETE numa API que não o suporta)|

#### 💥 5xx — Erros do Servidor

|Código|Significado|
|---|---|
|**500 Internal Server Error**|Erro genérico no servidor|
|**503 Service Unavailable**|Servidor sobrecarregado ou em manutenção|

> 💡 Em **bug bounty e pentest**, erros 500 podem indicar vulnerabilidades no servidor!

---

### 🍪 Cookies

Os **cookies** são pequenos ficheiros que o servidor envia ao browser para **guardar informação** entre sessões.

**Porquê existem?** O HTTP é **stateless** (sem estado) — cada pedido é independente. Os cookies permitem que o servidor "lembre" quem és.

**Exemplos de uso:**

- Manter a sessão de login
- Guardar preferências (idioma, tema)
- Tracking de comportamento

**Flags de segurança importantes:**

|Flag|O que faz|
|---|---|
|**Secure**|Cookie só é enviado em HTTPS|
|**HttpOnly**|JavaScript não pode aceder ao cookie (protege contra XSS)|
|**SameSite**|Protege contra ataques CSRF|

```http
Set-Cookie: SessionId=abc123; Secure; HttpOnly; SameSite=Strict; Path=/; Expires=...
```

> ⚠️ Cookies sem **HttpOnly** podem ser roubados por ataques **XSS (Cross-Site Scripting)**!

---

### 🔒 Headers de Segurança HTTP

O servidor pode enviar **headers especiais** para proteger o site:

|Header|Proteção|
|---|---|
|`Strict-Transport-Security`|Força HTTPS|
|`Content-Security-Policy`|Controla de onde scripts/imagens podem ser carregados|
|`X-Frame-Options`|Impede o site de ser carregado em iframes (protege contra Clickjacking)|
|`X-Content-Type-Options`|Impede o browser de adivinhar o tipo de ficheiro|

---

## 🖥️ Como Funciona um Website

### O que é um Website?

Um website é composto por dois lados:

```
┌──────────────────────────────────────────────────────────┐
│                                                            │
│   FRONTEND (o que vês)       BACKEND (o que não vês)      │
│                                                            │
│   HTML  → estrutura          Servidor Web (nginx/apache)  │
│   CSS   → aparência          Linguagem: PHP, Python, Node │
│   JS    → comportamento      Base de Dados: MySQL, Mongo  │
│                                                            │
└──────────────────────────────────────────────────────────┘
```

---

### 🏗️ Frontend — HTML, CSS e JavaScript

#### HTML (HyperText Markup Language)

Define a **estrutura** da página — o esqueleto.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>O Meu Site</title>
  </head>
  <body>
    <h1>Olá Mundo!</h1>
    <p>Este é um parágrafo.</p>
    <a href="https://google.com">Ir para o Google</a>
    <img src="imagem.jpg" alt="Uma imagem">
  </body>
</html>
```

**Tags HTML importantes:**

|Tag|Para que serve|
|---|---|
|`<h1>` a `<h6>`|Títulos (h1 = maior, h6 = menor)|
|`<p>`|Parágrafo|
|`<a href="...">`|Link/hiperligação|
|`<img src="...">`|Imagem|
|`<form>`|Formulário|
|`<input>`|Campo de texto, checkbox, etc.|
|`<div>`|Contentor genérico|
|`<script>`|Código JavaScript|
|`<link>`|Ligar CSS externo|

---

#### CSS (Cascading Style Sheets)

Define a **aparência** — cores, fontes, layout.

```css
body {
  background-color: #1a1a2e;
  font-family: Arial, sans-serif;
}

h1 {
  color: #e94560;
  font-size: 32px;
}
```

---

#### JavaScript

Adiciona **comportamento interativo** à página — animações, validação de formulários, pedidos sem recarregar a página.

```javascript
document.getElementById("btn").addEventListener("click", function() {
  alert("Clicaste no botão!");
});
```

> ⚠️ JavaScript corre no **browser do utilizador** (client-side). Isso significa que pode ser visto e manipulado. Nunca guardes informação sensível no JS!

---

### 🖥️ Backend — O Servidor

O **backend** é o código que corre no servidor. Não é visível para o utilizador diretamente.

Responsabilidades:

- Processar pedidos do browser
- Interagir com a base de dados
- Autenticar utilizadores
- Devolver a resposta correta

**Tecnologias comuns:**

- **PHP** — muito usado em WordPress
- **Python** (Django/Flask)
- **Node.js** (JavaScript no servidor)
- **Ruby on Rails**
- **Java** (Spring)

---

### 🗄️ Bases de Dados

O backend guarda e recupera dados de uma **base de dados**:

|Tipo|Exemplos|Quando usar|
|---|---|---|
|**SQL (Relacional)**|MySQL, PostgreSQL, SQLite|Dados estruturados, relações entre tabelas|
|**NoSQL**|MongoDB, Redis|Dados flexíveis, grande escala|

> ⚠️ **SQL Injection** é uma das vulnerabilidades mais comuns e perigosas — acontece quando o input do utilizador é inserido diretamente numa query SQL sem validação.

---

### ⚙️ Como o Site é Servido — Static vs Dynamic

#### Site Estático

- O servidor devolve **sempre os mesmos ficheiros** (HTML, CSS, JS)
- Não há processamento no servidor
- Exemplo: uma página de apresentação simples
- Rápido e seguro

#### Site Dinâmico

- O servidor **gera o HTML na hora** consoante o utilizador e os dados
- Usa linguagem de backend + base de dados
- Exemplo: Facebook, Gmail, TryHackMe
- Mais complexo, mais vulnerabilidades potenciais

```
Estático:   Browser → Servidor → Ficheiro HTML fixo → Browser
Dinâmico:   Browser → Servidor → Código PHP/Python → Base de Dados → HTML gerado → Browser
```

---

## 🧩 Outros Componentes da Web

### 🔀 Load Balancer (Balanceador de Carga)

Quando um site tem milhões de visitantes, um único servidor não chega. O **load balancer** distribui o tráfego por **vários servidores**.

```
                    ┌─────────────┐
Utilizadores ──────►│Load Balancer│──► Servidor 1
                    │             │──► Servidor 2
                    └─────────────┘──► Servidor 3
```

**Benefícios:**

- **Escalabilidade** — adicionar mais servidores facilmente
- **Alta disponibilidade** — se um servidor cai, os outros continuam
- **Performance** — cada servidor recebe menos carga

**Algoritmos de balanceamento:**

- **Round Robin** — cada pedido vai para o próximo servidor na fila
- **Weighted** — servidores mais potentes recebem mais tráfego
- **Least Connections** — vai para o servidor com menos conexões ativas

O load balancer também faz **health checks** — verifica periodicamente se os servidores estão a funcionar.

---

### 💾 CDN — Content Delivery Network

Uma **CDN** é uma rede de servidores distribuídos pelo mundo que guardam **cópias** dos ficheiros estáticos do site (imagens, CSS, JS, vídeos).

```
Utilizador em Lisboa ──► Servidor CDN em Lisboa (rápido! ⚡)
Utilizador em Tóquio ──► Servidor CDN em Tóquio (rápido! ⚡)

Sem CDN:
Utilizador em Tóquio ──► Servidor nos EUA (lento... 🐢)
```

**Benefícios:**

- Muito mais rápido para utilizadores longe do servidor principal
- Reduz a carga no servidor de origem
- Proteção contra ataques DDoS

---

### 🗄️ Web Application Firewall (WAF)

O **WAF** é uma camada de segurança que filtra o tráfego HTTP/HTTPS **antes** de chegar ao servidor.

```
Internet → WAF → Servidor Web
```

**O que o WAF bloqueia:**

- SQL Injection
- XSS (Cross-Site Scripting)
- Tentativas de acesso a ficheiros sensíveis
- Bots e scanners automáticos
- Ataques DDoS

> 💡 Em pentest, identificar e contornar WAFs é uma skill importante. Ferramentas como `wafw00f` detetam WAFs ativos.

---

### 🔄 Proxy vs Reverse Proxy

#### Proxy (Forward Proxy)

Fica entre o **utilizador e a Internet**. O utilizador pede ao proxy, e o proxy pede ao site.

```
Utilizador → Proxy → Internet → Site
```

**Usos:**

- Anonimato (o site vê o IP do proxy, não o teu)
- Filtrar conteúdo (redes empresariais/escolares)
- Contornar restrições geográficas

---

#### Reverse Proxy

Fica entre a **Internet e o servidor**. Os utilizadores falam com o reverse proxy, que encaminha para o servidor real.

```
Internet → Reverse Proxy → Servidor
```

**Usos:**

- Load balancing
- SSL termination (decifrar HTTPS e repassar HTTP internamente)
- Esconder a infraestrutura real
- Cache

**Exemplos de software:** Nginx, Apache, HAProxy, Cloudflare

---

### 🗃️ Cache do Servidor

O servidor pode guardar em **cache** respostas a pedidos frequentes, para não ter de processar tudo de novo.

```
1ª vez:  Pedido → Processa → Guarda em Cache → Responde
2ª vez:  Pedido → Encontra em Cache → Responde (muito mais rápido!)
```

**Tipos de cache:**

- **Browser Cache** — o teu browser guarda ficheiros localmente
- **CDN Cache** — servidores CDN guardam cópias
- **Server Cache** — o servidor guarda respostas geradas

---

## 🔐 Resumo de Segurança Web (Conceitos Base)

> [!warning] Vulnerabilidades Web mais Comuns
> 
> |Vulnerabilidade|O que é|
> |---|---|
> |**SQL Injection**|Inserir código SQL malicioso em campos de input|
> |**XSS**|Injetar JavaScript malicioso numa página web|
> |**CSRF**|Forçar um utilizador autenticado a fazer ações indesejadas|
> |**Path Traversal**|Aceder a ficheiros fora do diretório web (`../../../etc/passwd`)|
> |**IDOR**|Aceder a recursos de outros utilizadores mudando um ID|

---

## 🗝️ Conceitos Chave para Lembrar

> [!important] Resumo dos Conceitos Mais Importantes
> 
> - **DNS** = Converte nomes de domínio em IPs
> - **Registos DNS**: A (IPv4), AAAA (IPv6), CNAME (alias), MX (email), TXT (texto)
> - **HTTP** = protocolo de comunicação web | **HTTPS** = HTTP + encriptação
> - **URL** = esquema + domínio + porta + path + query string
> - **Métodos HTTP**: GET (pedir), POST (enviar), PUT (criar/substituir), DELETE (apagar)
> - **Códigos de estado**: 2xx (sucesso), 3xx (redirecionamento), 4xx (erro cliente), 5xx (erro servidor)
> - **Cookies** = guardam estado no browser | flags importantes: Secure, HttpOnly
> - **Frontend** = HTML + CSS + JS (o que o utilizador vê)
> - **Backend** = código no servidor + base de dados (o que processa tudo)
> - **Load Balancer** = distribui tráfego por múltiplos servidores
> - **CDN** = servidores espalhados pelo mundo para entregar conteúdo mais rápido
> - **WAF** = firewall para aplicações web — filtra pedidos maliciosos
> - **Reverse Proxy** = intermediário entre a Internet e o servidor real

---

## 🔗 Tags

#cybersecurity #web #presecurity #tryhackme #dns #http #https #html #css #javascript #backend #frontend #cdn #waf #cookies #loadbalancer

---

_Notas criadas para o TryHackMe Pre Security Path — How The Web Works_  
_Formatado para Obsidian_

---

## 🚀 Próximos Passos no Pre Security Path

### Sequência de Aprendizagem
1. **Consolidar conhecimento de Redes:** Revisa Network Fundamentals — compreender DNS e TCP/IP é essencial para a Web
2. **Avançar para Hardware:** Computer Fundamentals — entender CPU, RAM e storage ajuda a perceber performance
3. **Aprender o Sistema Operativo:** Operating Systems Basics — Windows e Linux são a base dos servidores web
4. **Estudar Ataques e Defesas:** Attacks and Defenses — aplicar conhecimento de web security (SQL Injection, XSS, CSRF)

### Prática Recomendada
- **Teste de segurança web:** Usar ferramentas como Burp Suite para interceptar e modificar pedidos HTTP
- **Análise de DNS:** Usar `nslookup` ou `dig` para ver registos DNS e compreender a resolução
- **Inspetor do browser:** F12 para ver requests HTTP, cookies, localStorage
- **Exercícios TryHackMe:** Fazer as tarefas práticas de web security

### Tópicos de Interesse Posterior
- **APIs REST:** Como a web moderna comunica programaticamente
- **OAuth 2.0 e OpenID Connect:** Autenticação moderna na web
- **OWASP Top 10:** As 10 vulnerabilidades web mais perigosas
- **Penetration Testing em Web Apps:** Ferramentas e técnicas de pentesting web

---

## 🔖 Tags

#cybersecurity #web #presecurity #tryhackme #dns #http #https #html #css #javascript #backend #frontend #cdn #waf #cookies #loadbalancer #security

---

_Notas criadas para o TryHackMe Pre Security Path — How The Web Works_  
_Formatado para Obsidian_