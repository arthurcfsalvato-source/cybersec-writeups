
  TRYHACKME 

Pre Security Path 

Introduction to Cyber Security 

Notas Completas de Estudo 

Módulos abordados: 

Offensive Security  •  Defensive Security  •  Tipos de Hackers 

Carreiras em Cybersecurity  •  Conceitos Fundamentais 

Elaborado com base no conteúdo do TryHackMe 

📋  Visão Geral do Módulo 

O módulo Introduction to Cyber Security é o ponto de partida do Pre Security Path no TryHackMe. O objetivo é apresentar os fundamentos da cibersegurança: o que é, como funciona, quem são os profissionais da área e quais as principais áreas de atuação. 

Este módulo é dividido em três grandes secções: 

- Offensive Security — atacar sistemas de forma ética para descobrir vulnerabilidades 
    

- Defensive Security — defender sistemas, detetar intrusos e responder a incidentes 
    

- Careers in Cyber — explorar as diferentes carreiras dentro da cibersegurança 
    

📖  Glossário Fundamental 

Antes de mergulhar nos conceitos técnicos, é essencial conhecer os termos básicos que aparecem em todo o módulo: 

|   |   |
|---|---|
|Termo|Definição|
|Cybersecurity|Conjunto de práticas, tecnologias e processos para proteger sistemas, redes e dados contra ataques digitais.|
|Hacker|Pessoa com conhecimentos técnicos avançados. Pode ser ético (White Hat), malicioso (Black Hat) ou intermédio (Grey Hat).|
|Vulnerability|Falha ou fraqueza num sistema que pode ser explorada por um atacante.|
|Exploit|Código ou técnica que aproveita uma vulnerabilidade para executar ações não autorizadas.|
|Malware|Software malicioso criado para danificar, roubar dados ou obter acesso não autorizado a sistemas.|
|Threat|Qualquer circunstância ou evento com potencial para causar dano a um sistema ou organização.|
|Risk|Probabilidade de uma ameaça explorar uma vulnerabilidade e o impacto resultante.|
|Asset|Qualquer recurso de valor para uma organização: dados, hardware, software, pessoas.|
|Payload|Parte do ataque que executa a ação maliciosa (ex: código que apaga ficheiros).|
|Social Engineering|Técnica que manipula pessoas para revelar informação confidencial ou executar ações prejudiciais.|
|Phishing|Tipo de ataque de engenharia social via email/mensagem, fingindo ser entidade legítima.|
|Patch|Atualização de software que corrige vulnerabilidades ou bugs.|
|Zero-Day|Vulnerabilidade desconhecida pelo fabricante, sem patch disponível, explorada por atacantes.|
|CIA Triad|Confidentiality, Integrity, Availability — os três pilares da segurança da informação.|

⚔️  Offensive Security (Segurança Ofensiva) 

O que é Offensive Security? 

A segurança ofensiva consiste em pensar como um atacante — tentar invadir sistemas, redes e aplicações antes que atores maliciosos o façam. O objetivo é encontrar vulnerabilidades para que possam ser corrigidas. 

💡 Princípio-Chave 

Para vencer um hacker, tens de pensar como um hacker. A segurança ofensiva usa as mesmas ferramentas e técnicas dos criminosos, mas com permissão legal e propósito ético. 

Tipos de Hackers (Hat Colors) 

🎩 White Hat (Chapéu Branco): Hackers éticos com autorização explícita. Trabalham para empresas e governos para melhorar a segurança. 

🎩 Black Hat (Chapéu Preto): Hackers maliciosos que atacam sistemas sem permissão. Motivados por lucro, ideologia ou simples vandalismo. 

🎩 Grey Hat (Chapéu Cinzento): Intermédio — podem invadir sistemas sem permissão mas sem intenção maliciosa, geralmente para reportar falhas. 

Penetration Testing (Pentest) 

O Penetration Testing (ou pentest) é um ataque simulado e controlado a um sistema, com o objetivo de identificar vulnerabilidades que um atacante real poderia explorar. É o trabalho principal de um hacker ético. 

Fases do Penetration Testing 

- 1. Reconnaissance (Reconhecimento) 
    

- Recolha de informação sobre o alvo: domínios, IPs, tecnologias usadas, funcionários. 
    

- Tipos: Passive Recon (sem contato direto) e Active Recon (interação direta com o alvo). 
    

- 2. Scanning & Enumeration 
    

- Varredura de portas e serviços ativos (ex: Nmap). Identificação de versões de software. 
    

- 3. Exploitation (Exploração) 
    

- Uso de exploits para tirar partido das vulnerabilidades encontradas. 
    

- 4. Post-Exploitation 
    

- Manter acesso, escalar privilégios, mover-se lateralmente na rede, exfiltrar dados. 
    

- 5. Reporting (Relatório) 
    

- Documentar todas as descobertas, impacto e recomendações de remediação. 
    

Bug Bounty Programs 

Programas onde empresas pagam recompensas a investigadores que encontrem e reportem vulnerabilidades de forma responsável. Exemplos: HackerOne, Bugcrowd, programas da Google, Microsoft, Facebook. 

🏆 Exemplo Prático no TryHackMe 

No exercício do módulo, usas o Gobuster — uma ferramenta de line command — para fazer brute-force a diretórios escondidos de um site web, simulando o trabalho de reconhecimento de um pentester. 

Ferramentas Comuns em Offensive Security 

|   |   |   |
|---|---|---|
|Ferramenta|Categoria|Uso|
|Nmap|Scanning|Varredura de portas e serviços numa rede.|
|Gobuster|Web Enumeration|Brute-force de diretórios e ficheiros web ocultos.|
|Metasploit|Exploitation|Framework para desenvolvimento e execução de exploits.|
|Burp Suite|Web Testing|Proxy para interceptar e modificar tráfego HTTP/HTTPS.|
|Nikto|Web Scanning|Scanner de vulnerabilidades em servidores web.|
|SQLMap|Injection|Automatiza a deteção e exploração de SQL Injection.|
|John the Ripper|Password Cracking|Quebra de passwords via dicionário ou força bruta.|
|Hydra|Password Cracking|Brute-force de autenticação em vários protocolos.|

🛡️  Defensive Security (Segurança Defensiva) 

O que é Defensive Security? 

A segurança defensiva é a outra face da moeda — enquanto a ofensiva ataca, a defensiva protege. Envolve prevenir intrusões, detetar atividades suspeitas, responder a incidentes e recuperar de ataques. 

🎯 Objetivo Principal 

Garantir que sistemas e dados estão protegidos, disponíveis e íntegros. Quando um ataque ocorre, a equipa defensiva tem de detetá-lo o mais rápido possível e minimizar o dano. 

Áreas Principais da Segurança Defensiva 

1. SOC — Security Operations Center 

Um SOC é uma equipa (e infraestrutura) responsável por monitorizar, detetar e responder a ameaças de segurança 24/7. É o 'quartel general' da segurança defensiva de uma organização. 

- Monitorização contínua de logs, tráfego de rede e eventos de segurança 
    

- Análise de alertas gerados por ferramentas como SIEM e IDS/IPS 
    

- Resposta a incidentes de segurança e contenção de ataques 
    

- Threat hunting — busca proativa por ameaças ocultas na rede 
    

- Criação e manutenção de regras de deteção 
    

2. Threat Intelligence (Inteligência de Ameaças) 

Processo de recolher, analisar e partilhar informação sobre ameaças existentes e emergentes. Permite às organizações antecipar e preparar-se para ataques. 

Fontes de Threat Intelligence: feeds de OSINT, relatórios de empresas de segurança (CrowdStrike, Mandiant), dark web, partilha entre organizações (ISACs). 

IOC (Indicators of Compromise): Evidências de que um sistema foi comprometido: IPs maliciosos, hashes de malware, domínios suspeitos, padrões de comportamento. 

3. DFIR — Digital Forensics and Incident Response 

Combinação de duas disciplinas críticas: 

Digital Forensics: Investigação de crimes digitais. Análise de discos, memória, logs e artefactos digitais para reconstruir o que aconteceu. 

Incident Response (IR): Processo estruturado de resposta a incidentes de segurança. 

Fases do Incident Response 

|   |   |   |
|---|---|---|
|Fase|Nome|Descrição|
|1|Preparation|Criar políticas, formar a equipa, preparar ferramentas antes de um incidente ocorrer.|
|2|Identification|Detetar que um incidente está a ocorrer através de alertas, logs ou denúncias.|
|3|Containment|Limitar o impacto — isolar sistemas afetados, bloquear IPs maliciosos.|
|4|Eradication|Remover o malware, fechar backdoors, eliminar a causa raiz do problema.|
|5|Recovery|Restaurar sistemas ao normal, monitorizar de perto para garantir que o ataque não recomeçou.|
|6|Lessons Learned|Documentar o incidente, o que correu mal e melhorar os processos para o futuro.|

4. Malware Analysis 

Análise de software malicioso para perceber como funciona, o que faz e como pode ser detetado ou removido. 

Static Analysis: Examinar o código sem o executar. Uso de ferramentas como Ghidra, IDA Pro, strings, file. 

Dynamic Analysis: Executar o malware num ambiente controlado (sandbox) e observar o seu comportamento: chamadas ao sistema, tráfego de rede, ficheiros criados. 

Ferramentas Essenciais em Defensive Security 

SIEM — Security Information and Event Management 

Sistema que agrega e correlaciona logs de múltiplas fontes (firewalls, endpoints, servidores) para identificar padrões suspeitos e gerar alertas. 

- Exemplos: Splunk, IBM QRadar, Microsoft Sentinel, ELK Stack (Elasticsearch + Logstash + Kibana) 
    

- Funciona com regras de correlação e análise comportamental 
    

- Permite investigar incidentes históricos e criar dashboards de segurança 
    

IDS/IPS — Intrusion Detection/Prevention System 

IDS (Detection): Monitoriza o tráfego e alerta quando deteta algo suspeito. Não bloqueia — só avisa. 

IPS (Prevention): Tal como o IDS, mas tem capacidade de bloquear automaticamente o tráfego malicioso. 

- Baseados em assinaturas: comparam com padrões conhecidos de ataques 
    

- Baseados em anomalias: detetam desvios do comportamento normal da rede 
    

Firewall 

Sistema que filtra o tráfego de rede com base em regras definidas. É a primeira linha de defesa. 

- Stateless Firewall: examina pacotes individualmente, sem contexto de sessão 
    

- Stateful Firewall: mantém registo do estado das conexões ativas 
    

- Next-Generation Firewall (NGFW): combina firewall tradicional com inspeção profunda de pacotes, controlo de aplicações e inteligência de ameaças 
    

🔑  Conceitos Fundamentais de Cibersegurança 

A Tríade CIA 

🔒 Os Três Pilares da Segurança da Informação 

Confidentiality (Confidencialidade)  •  Integrity (Integridade)  •  Availability (Disponibilidade) 

|   |   |   |
|---|---|---|
|🔒 Confidentiality|✅ Integrity|⚡ Availability|
|Apenas quem tem autorização pode aceder à informação. Protegemos dados sensíveis contra acesso não autorizado.|Os dados não foram alterados de forma não autorizada. A informação é precisa e fiável.|Os sistemas e dados estão acessíveis quando necessário. Ataques DDoS são uma ameaça direta a este pilar.|
|Exemplo: Encriptação de dados, controlo de acesso (ACL), autenticação forte (MFA).|Exemplo: Hashing de ficheiros (MD5, SHA-256), assinaturas digitais, controlo de versões.|Exemplo: Redundância de servidores, backups, proteção contra DDoS, SLAs de uptime.|

Tipos de Ataques Comuns 

Malware 

- Vírus: código malicioso que se anexa a ficheiros legítimos e se propaga. 
    

- Worm: propaga-se automaticamente pela rede sem necessitar de ficheiro hospedeiro. 
    

- Trojan (Cavalo de Troia): disfarça-se de software legítimo. Quando executado, abre backdoors. 
    

- Ransomware: encripta os ficheiros da vítima e exige resgate (geralmente em criptomoeda). 
    

- Spyware: monitoriza e exfiltra atividade do utilizador sem o seu conhecimento. 
    

- Rootkit: esconde a presença de malware no sistema, operando ao nível do kernel. 
    

- Keylogger: regista todas as teclas premidas pelo utilizador para roubar credenciais. 
    

Ataques de Rede 

- DoS/DDoS: sobrecarrega um servidor com tráfego para torná-lo inacessível. 
    

- Man-in-the-Middle (MitM): intercepta comunicação entre duas partes sem que o saibam. 
    

- Packet Sniffing: captura e analisa tráfego de rede (Wireshark é a ferramenta mais conhecida). 
    

- Port Scanning: identifica portas abertas e serviços a correr num host. 
    

- ARP Poisoning: associa o MAC do atacante ao IP legítimo para intercetar tráfego na rede local. 
    

Ataques a Aplicações Web 

- SQL Injection (SQLi): injeta código SQL em campos de input para manipular a base de dados. 
    

- Cross-Site Scripting (XSS): injeta scripts maliciosos em páginas web visitadas por outros utilizadores. 
    

- Command Injection: executa comandos do sistema operativo através de inputs mal sanitizados. 
    

- Directory Traversal: acede a ficheiros fora do diretório web usando sequências como ../ 
    

- IDOR (Insecure Direct Object Reference): acede a recursos de outros utilizadores por manipulação de IDs. 
    

Criptografia — Fundamentos 

Tipos de Encriptação 

Simétrica: Mesma chave para encriptar e desencriptar. Rápida mas o problema é partilhar a chave de forma segura. Exemplos: AES, DES. 

Assimétrica: Par de chaves: pública (para encriptar) e privada (para desencriptar). Mais lenta mas resolve o problema de distribuição de chaves. Exemplos: RSA, ECC. 

Hashing: Função unidirecional — transforma dados em string de comprimento fixo. Não é possível reverter. Exemplos: MD5, SHA-1, SHA-256. Usado para verificar integridade. 

Autenticação e Controlo de Acesso 

- Autenticação: verificar que o utilizador é quem diz ser (passwords, biometria, tokens). 
    

- Autorização: definir o que o utilizador autenticado tem permissão de fazer. 
    

- MFA (Multi-Factor Authentication): combina dois ou mais fatores — algo que sabes (password), algo que tens (token), algo que és (impressão digital). 
    

- Princípio do Menor Privilégio: cada utilizador/sistema só deve ter o mínimo de permissões necessárias para a sua função. 
    

- Role-Based Access Control (RBAC): permissões atribuídas com base no papel/função do utilizador. 
    

💼  Carreiras em Cibersegurança 

A cibersegurança oferece uma vasta gama de carreiras, tanto no lado ofensivo como no defensivo. Aqui estão os principais papéis abordados no módulo: 

Carreiras Ofensivas (Red Team) 

|   |   |
|---|---|
|Cargo|Responsabilidades|
|Penetration Tester|Simula ataques a sistemas com permissão para encontrar vulnerabilidades antes dos atacantes. Produz relatórios detalhados com recomendações.|
|Red Team Operator|Simula ataques avançados e persistentes (APTs) para testar a capacidade de deteção e resposta da equipa defensiva.|
|Vulnerability Researcher|Descobre novas vulnerabilidades em software e hardware. Pode trabalhar para empresas de segurança ou no mercado de bug bounty.|
|Exploit Developer|Desenvolve código de exploração para vulnerabilidades descobertas. Trabalho altamente especializado e técnico.|
|Malware Analyst (Ofensivo)|Cria ou analisa malware para perceber técnicas de ataque. Frequentemente trabalha para empresas de inteligência ou defesa.|

Carreiras Defensivas (Blue Team) 

|   |   |
|---|---|
|Cargo|Responsabilidades|
|SOC Analyst (Tier 1-3)|Monitoriza alertas de segurança, investiga eventos, escala incidentes. Tier 1 trata alertas básicos, Tier 3 investiga ameaças avançadas.|
|Security Engineer|Implementa e mantém ferramentas de segurança: firewalls, SIEM, IDS/IPS. Faz hardening de sistemas.|
|Incident Responder|Responde a incidentes de segurança em tempo real. Contém ameaças, investiga causas e restaura sistemas.|
|Digital Forensics Investigator|Recolhe e analisa evidências digitais de crimes ou incidentes. Trabalha com imagens de disco, memória e logs.|
|Malware Analyst (Defensivo)|Analisa amostras de malware encontradas em incidentes para perceber como funciona e criar deteções.|
|Threat Hunter|Busca proativa por ameaças ocultas na rede que não foram detetadas por ferramentas automáticas.|
|Security Architect|Define a estratégia de segurança de longo prazo e a arquitetura de sistemas seguros na organização.|

Certificações Relevantes 

O TryHackMe referencia estas certificações como marcos importantes na carreira em cibersegurança: 

- CompTIA Security+: certificação de entrada amplamente reconhecida. Cobre conceitos fundamentais de segurança. 
    

- CompTIA Network+: essencial para perceber redes antes de avançar para a segurança. 
    

- CEH (Certified Ethical Hacker): focada em técnicas de hacking ético e penetration testing. 
    

- OSCP (Offensive Security Certified Professional): certificação prática e muito respeitada em pentesting ofensivo. 
    

- eJPT (eLearnSecurity Junior Penetration Tester): boa certificação de entrada para pentesting. 
    

- CySA+ (CompTIA Cybersecurity Analyst): focada em análise de segurança e trabalho em SOC. 
    

- CISM / CISSP: certificações de gestão de segurança para profissionais seniores. 
    

🧪  Exercícios Práticos do Módulo 

Tarefa: Gobuster — Web Enumeration 

Este é o exercício hands-on do módulo de Offensive Security. O objetivo é usar o Gobuster para descobrir páginas ou diretórios escondidos num site. 

🖥️ Comando Usado 

gobuster dir -u http://fakebank.thm -w wordlist.txt  • dir = modo de enumeração de diretórios • -u = URL do alvo • -w = wordlist com palavras a tentar 

O Gobuster tenta aceder a cada palavra da wordlist como path no URL (ex: /admin, /login, /secret) e regista o código de resposta HTTP: 

- 200 OK: o diretório/página existe 
    

- 301/302: redirecionamento (também pode indicar existência) 
    

- 404 Not Found: não existe 
    

- 403 Forbidden: existe mas acesso negado 
    

Tarefa: SIEM — Análise de Logs 

No exercício de Defensive Security, usas uma interface de SIEM simplificada para analisar logs e identificar atividade maliciosa. O objetivo é aprender a: 

- Filtrar eventos por tipo, hora ou origem 
    

- Identificar tentativas de login falhadas em sequência (possível brute-force) 
    

- Localizar IPs suspeitos ou utilizadores com comportamento anómalo 
    

- Correlacionar eventos de diferentes fontes para perceber o que aconteceu 
    

⚡  Conceitos-Chave para Memorizar 

📌 Para o Exame / Revisão Rápida 

Estes são os pontos mais importantes que surgem frequentemente em CTFs e certificações relacionados com o conteúdo deste módulo. 

- CIA Triad = Confidentiality + Integrity + Availability — sempre lembrar os três pilares 
    

- White Hat = ético e legal | Black Hat = malicioso e ilegal | Grey Hat = ético mas sem autorização 
    

- Pentest segue: Recon → Scanning → Exploitation → Post-Exploitation → Reporting 
    

- Incident Response segue: Preparation → Identification → Containment → Eradication → Recovery → Lessons Learned 
    

- IDS alerta, IPS bloqueia — diferença crucial 
    

- SIEM agrega logs de múltiplas fontes e correlaciona eventos para gerar alertas 
    

- Zero-Day = vulnerabilidade sem patch ainda disponível — extremamente perigosa 
    

- Hashing é unidirecional (não dá para reverter), encriptação é bidirecional (dá para desencriptar) 
    

- Ransomware encripta dados e pede resgate | Trojan abre backdoors 
    

- Social Engineering explora o humano, não a tecnologia — o elo mais fraco da segurança 
    

- Principle of Least Privilege = só dar as permissões mínimas necessárias 
    

- MFA = algo que sabes + algo que tens + algo que és 
    

🚀  Próximos Passos no Pre Security Path 

Depois de completares este módulo de introdução, o Pre Security Path continua com: 

|   |   |
|---|---|
|Módulo|O que vais aprender|
|Network Fundamentals|Modelo OSI/TCP-IP, protocolos (HTTP, DNS, DHCP, ARP), subnetting, roteamento.|
|How The Web Works|DNS, HTTP/HTTPS, cookies, sessões, como os browsers comunicam com servidores.|
|Linux Fundamentals|Comandos básicos de Linux, sistema de ficheiros, permissões, scripts bash — essencial para cibersegurança.|
|Windows Fundamentals|Active Directory, registo do sistema, PowerShell, segurança em ambientes Windows.|

✅ Módulo Concluído 

Parabéns por teres completado o Introduction to Cyber Security! Tens agora a base conceptual para avançar nos módulos técnicos do Pre Security Path. Continua assim — a consistência é a chave no aprendizado de cibersegurança.

---

## Proximos Passos no Caminho

### Sequencial (Proximos 6 Modulos)
- **1 →** 2) [[2)Network Fundamentals — Pre Security Path]]
- **2 →** 3) How The Web Works (HTTP, HTTPS, Web Components)
- **3 →** 4) Computer Fundamentals (CPU, RAM, Storage, Security)
- **4 →** 5) Operating Systems Basics (Windows, Linux, CLI)
- **5 →** 6) Software Basics (Python, JavaScript, SQL)
- **6 →** 7) Attacks and Defenses (Criptografia, Defesas, IR)

### Topicos Relacionados Nesta Nota
- **CIA Triad detalhado:** 7) Attacks and Defenses — CIA Triad
- **Criptografia:** 7) Attacks and Defenses — Criptografia
- **IDS/IPS & Firewalls:** 5) Operating Systems Basics
- **Malware & Ataques:** 7) Attacks and Defenses

### Referencias Rapidas
- **Quick Reference** — Portas, ferramentas, conceitos
- **Conceitos-Chave** — Mapa tematico
- **Indice Principal**