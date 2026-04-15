# Software Basics

---

## 🔗 Navegação Inteligente

### Sequencial
- **← Anterior:** 5) Operating Systems Basics (Kernel, CLI, Segurança)
- **Próximo →:** 7) Attacks and Defenses (Criptografia, Exploração)
- **Depois:** Módulos avançados (Pentesting, CTFs)
- **Início:** 1) Introduction to Cyber Security (Fundamentos)

### Tópicos Relacionados Nesta Nota
- **SQL Injection:** Ver em 7) Attacks and Defenses — Ataques Web
- **Criptografia em Python:** Ver em 7) Attacks and Defenses — Criptografia
- **XSS em JavaScript:** Ver em 3) How The Web Works — Segurança Web
- **Reverse Engineering:** Ver em 1) Introduction to Cyber Security — Malware Analysis
- **CLI & Scripting:** Ver em 5) Operating Systems Basics — CLI

### Referencias Rapidas
- **⚡ Quick Reference** — Sintaxe Python, SQL, JavaScript
- **🔑 Conceitos-Chave** — Mapa tematico (programação, segurança)

---

## Índice
1. [Representação de Dados](#representação-dados)
2. [Codificação de Dados](#codificação)
3. [Python Basics](#python)
4. [JavaScript Basics](#javascript)
5. [SQL e Bancos de Dados](#sql)
6. [Conceitos-Chave para Lembrar](#conceitos-chave)

---

## <a name="representação-dados"></a>Representação de Dados

### Sistema Binário

O computador compreende apenas **0s e 1s**. Um **bit** (binary digit) é a unidade mínima de informação.

```
Um bit:           0 ou 1
Um byte:          8 bits = 00000000 a 11111111
Um kilobyte (KB): 1000 bytes (ou 1024 em alguns contextos)
Um megabyte (MB): 1000 KB
Um gigabyte (GB): 1000 MB
```

#### Conversão Binária para Decimal

```
Exemplo: 11010110 (binário) para decimal

Posição:  7 6 5 4 3 2 1 0
Bit:      1 1 0 1 0 1 1 0
Valor:    128+64+0+8+0+2+1+0 = 214 (decimal)

Fórmula: ∑(bit × 2^posição)
```

**Tabela de Conversão:**

| Binário | Decimal | Hexadecimal |
|---|---|---|
| 00000000 | 0 | 0x00 |
| 00001010 | 10 | 0x0A |
| 11111111 | 255 | 0xFF |
| 10000000 | 128 | 0x80 |
| 01111111 | 127 | 0x7F |

#### Operações Binárias

```
AND (E):           OR (OU):           XOR (Ou Exclusivo):
 1 AND 1 = 1        1 OR 1 = 1         1 XOR 1 = 0
 1 AND 0 = 0        1 OR 0 = 1         1 XOR 0 = 1
 0 AND 1 = 0        0 OR 1 = 1         0 XOR 1 = 1
 0 AND 0 = 0        0 OR 0 = 0         0 XOR 0 = 0

NOT (NÃO):
 NOT 1 = 0
 NOT 0 = 1

Exemplo com bytes:
 10110011 (decimal 179)
 AND
 11001100 (decimal 204)
 ─────────
 10000000 (decimal 128)
```

### Sistema Hexadecimal

O **hexadecimal** (base 16) usa dígitos 0-9 e letras A-F, compactando valores binários.

```
Hex Digit:  0  1  2  3  4  5  6  7  8  9  A  B  C  D  E  F
Decimal:    0  1  2  3  4  5  6  7  8  9  10 11 12 13 14 15
Binário:    0000 0001 0010 0011 0100 0101 0110 0111 
            1000 1001 1010 1011 1100 1101 1110 1111
```

#### Conversão Hexadecimal para Decimal

```
Exemplo: 0xA5 para decimal

Posição:  1  0
Dígito:   A  5
Valor:    (10 × 16¹) + (5 × 16⁰) = 160 + 5 = 165 (decimal)

Exemplo: 0xFF
(15 × 16¹) + (15 × 16⁰) = 240 + 15 = 255

Exemplo: 0x1A2B
(1 × 16³) + (10 × 16²) + (2 × 16¹) + (11 × 16⁰)
= 4096 + 2560 + 32 + 11
= 6699
```

**Uso comum:**
- **Cores:** #FF00AA (RGB em hex)
- **Memória:** Endereços em hex (0x7FFF)
- **Criptografia:** Hashes em hex

---

## <a name="codificação"></a>Codificação de Dados

### ASCII (American Standard Code for Information Interchange)

ASCII mapeia 128 caracteres para números (0-127).

```
Caractere | Decimal | Hex   | Binário
──────────────────────────────────────
NUL       | 0       | 0x00  | 00000000
SOH       | 1       | 0x01  | 00000001
...
Space     | 32      | 0x20  | 00100000
!         | 33      | 0x21  | 00100001
"         | 34      | 0x22  | 00100010
#         | 35      | 0x23  | 00100011
...
0         | 48      | 0x30  | 00110000
1         | 49      | 0x31  | 00110001
...
A         | 65      | 0x41  | 01000001
B         | 66      | 0x42  | 01000010
...
a         | 97      | 0x61  | 01100001
b         | 98      | 0x62  | 01100010
...
~         | 126     | 0x7E  | 01111110
DEL       | 127     | 0x7F  | 01111111
```

**Códigos de Controle ASCII (0-31):**
- `\0` (NUL) - Nulo
- `\n` (10) - Nova linha
- `\r` (13) - Retorno de carro
- `\t` (9) - Tabulação

### UTF-8 (Unicode Transformation Format)

UTF-8 é **compatível com ASCII** mas suporta qualquer caractere Unicode usando 1-4 bytes.

```
Intervalo Unicode    | Bytes UTF-8    | Exemplo
─────────────────────────────────────────────
U+0000 a U+007F      | 1 byte (ASCII) | A = 0x41
U+0080 a U+07FF      | 2 bytes        | é = 0xC3 0xA9
U+0800 a U+FFFF      | 3 bytes        | 中 (chinês)
U+10000 a U+10FFFF   | 4 bytes        | 😀 (emoji)
```

**Exemplo UTF-8:**
```
Caractere: "Ã" (A com til)
Unicode: U+00C3
UTF-8: 11000011 10000011 (0xC3 0x83 em hex)

Caractere: "é" (e com acento)
Unicode: U+00E9
UTF-8: 11001011 10101001 (0xC3 0xA9 em hex)
```

### Base64

Base64 codifica dados binários usando 64 caracteres imprimíveis, útil para transmissão.

```
Alfabeto Base64:
A-Z (26) + a-z (26) + 0-9 (10) + + e / (2) = 64 caracteres
Padding: = (quando necessário)

Exemplo: "Hello" em Base64

Binário:         01001000 01100101 01101100 01101100 01101111
                 H        e        l        l        o

Agrupar em 6:    010010 000110 010101 101100 011011 110110 1111
                 18     6      21     44     27     54     60
                 S      G      V      s      b      2      8

Base64: SGVsbG8=
```

**Comum em:**
- Encapsulamento de dados binários em JSON
- Codificação de imagens em HTML/CSS
- Autenticação HTTP Basic

```python
import base64

# Codificar
texto = "Hello World"
encoded = base64.b64encode(texto.encode()).decode()
print(encoded)  # SGVsbG8gV29ybGQ=

# Decodificar
decoded = base64.b64decode(encoded).decode()
print(decoded)  # Hello World
```

---

## <a name="python"></a>Python Basics

Python é uma linguagem de alto nível, legível e versátil.

### Variáveis e Tipos de Dados

```python
# Inteiros
idade = 30
negativo = -5
grande = 1000000

# Floats (números decimais)
altura = 1.75
pi = 3.14159

# Strings
nome = "Alice"
mensagem = 'Olá mundo'
multiline = """Texto em
múltiplas
linhas"""

# Booleans
ativo = True
descativo = False

# Listas (mutáveis, ordenadas)
numeros = [1, 2, 3, 4, 5]
misturado = [1, "texto", 3.14, True]
vazio = []

# Tuplas (imutáveis, ordenadas)
coordenadas = (10, 20)
dados = (1, 2, 3)
# dados[0] = 999  # ❌ Erro! Tuplas são imutáveis

# Dicionários (chave-valor)
usuario = {
    "nome": "Alice",
    "idade": 30,
    "email": "alice@example.com"
}

# Conjuntos (únicos, desordenados)
numeros_unicos = {1, 2, 3, 4, 5}
# numeros_unicos = {1, 1, 2}  -> {1, 2} (duplicatas removidas)

# Verificar tipo
print(type(idade))      # <class 'int'>
print(type(nome))       # <class 'str'>
print(type(numeros))    # <class 'list'>
```

### Operadores

```python
# Aritmética
resultado = 10 + 5      # 15
resultado = 10 - 3      # 7
resultado = 4 * 5       # 20
resultado = 20 / 4      # 5.0 (sempre float em Python 3)
resultado = 20 // 3     # 6 (divisão inteira)
resultado = 20 % 3      # 2 (modulo/resto)
resultado = 2 ** 8      # 256 (exponenciação)

# Comparação
10 > 5      # True
10 <= 5     # False
10 == 10    # True
10 != 5     # True
"abc" == "abc"  # True

# Lógica
True and True   # True
True and False  # False
True or False   # True
not True        # False

# Strings
mensagem = "Olá" + " " + "mundo"  # "Olá mundo"
texto = "abc" * 3                  # "abcabcabc"
"o" in "Olá"                      # True
len("Python")                      # 6
```

### Funções

```python
# Função simples
def saudacao(nome):
    return f"Olá, {nome}!"

print(saudacao("Alice"))  # Olá, Alice!

# Função com múltiplos parâmetros
def soma(a, b):
    return a + b

resultado = soma(10, 20)  # 30

# Função com valor padrão
def cumprimento(nome, saudacao="Oi"):
    return f"{saudacao}, {nome}!"

print(cumprimento("Bob"))              # Oi, Bob!
print(cumprimento("Bob", "Olá"))       # Olá, Bob!

# Função com múltiplos retornos
def divmod_custom(a, b):
    quociente = a // b
    resto = a % b
    return quociente, resto  # Tupla

q, r = divmod_custom(20, 3)
print(q, r)  # 6 3

# Função variádica (*args)
def soma_multipla(*numeros):
    return sum(numeros)

print(soma_multipla(1, 2, 3, 4, 5))  # 15

# Função com argumentos nomeados (**kwargs)
def criar_perfil(**dados):
    for chave, valor in dados.items():
        print(f"{chave}: {valor}")

criar_perfil(nome="Alice", idade=30, cidade="São Paulo")
```

### Controle de Fluxo

```python
# If/Elif/Else
idade = 20
if idade < 13:
    categoria = "criança"
elif idade < 18:
    categoria = "adolescente"
else:
    categoria = "adulto"

# While
contador = 0
while contador < 5:
    print(contador)
    contador += 1

# For
for i in range(5):  # 0, 1, 2, 3, 4
    print(i)

for item in ["a", "b", "c"]:
    print(item)

# List comprehension
numeros = [1, 2, 3, 4, 5]
pares = [n for n in numeros if n % 2 == 0]
print(pares)  # [2, 4]

# Tratamento de erros
try:
    resultado = 10 / 0
except ZeroDivisionError:
    print("Erro: divisão por zero")
except Exception as e:
    print(f"Erro: {e}")
finally:
    print("Sempre executado")
```

### Bibliotecas Importantes

```python
# Criptografia: cryptography
from cryptography.fernet import Fernet

chave = Fernet.generate_key()
cipher = Fernet(chave)
mensagem = b"Segredo"
criptografado = cipher.encrypt(mensagem)
descriptografado = cipher.decrypt(criptografado)

# Hashing: hashlib
import hashlib

texto = "senha123"
hash_sha256 = hashlib.sha256(texto.encode()).hexdigest()
print(hash_sha256)

# Requisições HTTP: requests
import requests

resposta = requests.get("https://api.example.com/users")
if resposta.status_code == 200:
    dados = resposta.json()
    print(dados)

# Manipulação de JSON
import json

dados = {"nome": "Alice", "idade": 30}
json_str = json.dumps(dados)  # Python → JSON
dados_recuperados = json.loads(json_str)  # JSON → Python

# Expressões regulares: re
import re

padrao = r"\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b"
email = "alice@example.com"
if re.match(padrao, email):
    print("Email válido")

# Data e hora: datetime
from datetime import datetime, timedelta

agora = datetime.now()
amanha = agora + timedelta(days=1)
print(f"Hoje: {agora.date()}")
print(f"Amanhã: {amanha.date()}")
```

---

## <a name="javascript"></a>JavaScript Basics

JavaScript é a linguagem da web, executada no navegador e em servidores (Node.js).

### Variáveis e Tipos

```javascript
// var (legado, escopo de função)
var contador = 0;

// let (escopo de bloco, pode ser reatribuído)
let nome = "Alice";
nome = "Bob";  // ✓ Permitido

// const (escopo de bloco, imutável)
const PI = 3.14159;
// PI = 3.14;  // ❌ Erro: assignment to constant variable

// Tipos de dados
let numero = 42;
let decimal = 3.14;
let texto = "Olá";
let booleano = true;
let nulo = null;        // Nulo intencional
let indefinido;         // Não inicializado
let objeto = {};
let array = [1, 2, 3];

// Verificar tipo
typeof numero;      // "number"
typeof texto;       // "string"
typeof booleano;    // "boolean"
typeof objeto;      // "object"
Array.isArray(array);  // true
```

### Objetos

```javascript
// Objeto literal
const usuario = {
    nome: "Alice",
    idade: 30,
    email: "alice@example.com",
    ativo: true,
    
    // Método
    apresentar: function() {
        return `Olá, meu nome é ${this.nome}`;
    }
};

// Acessar propriedades
console.log(usuario.nome);          // Alice
console.log(usuario["email"]);      // alice@example.com

// Chamar método
console.log(usuario.apresentar());  // Olá, meu nome é Alice

// Adicionar propriedade dinâmica
usuario.telefone = "1234567890";

// Deletar propriedade
delete usuario.ativo;

// Iterar propriedades
for (let chave in usuario) {
    console.log(`${chave}: ${usuario[chave]}`);
}

// Object.keys(), Object.values(), Object.entries()
Object.keys(usuario);      // ["nome", "idade", "email", ...]
Object.values(usuario);    // ["Alice", 30, "alice@example.com", ...]
```

### Funções

```javascript
// Função declarada
function saudacao(nome) {
    return `Olá, ${nome}!`;
}

// Função expressão
const multiplicar = function(a, b) {
    return a * b;
};

// Arrow function (sintaxe moderna)
const adicionar = (a, b) => a + b;
const quadrado = x => x * x;
const semParametro = () => "Sem parâmetro";

// Closure (função dentro de função)
function contar() {
    let contador = 0;
    return function() {
        contador++;
        return contador;
    };
}

const contador1 = contar();
console.log(contador1());  // 1
console.log(contador1());  // 2
console.log(contador1());  // 3
```

### DOM (Document Object Model)

O DOM representa a estrutura HTML como árvore de objetos.

```javascript
// Selecionar elementos
const elemento = document.getElementById("meuId");
const elementos = document.getElementsByClassName("minha-classe");
const inputs = document.querySelectorAll("input[type='text']");
const primeiro = document.querySelector(".minha-classe");  // Primeiro match

// Manipular conteúdo
elemento.textContent = "Novo texto";        // Apenas texto
elemento.innerHTML = "<b>Texto em bold</b>"; // Com HTML

// Manipular atributos
elemento.getAttribute("data-valor");
elemento.setAttribute("data-valor", "novo");
elemento.classList.add("ativa");
elemento.classList.remove("inativa");
elemento.classList.toggle("destacado");

// Manipular estilos
elemento.style.color = "red";
elemento.style.backgroundColor = "#f0f0f0";

// Eventos
elemento.addEventListener("click", function(evento) {
    console.log("Clicado!");
    console.log(evento.target);  // Elemento clicado
});

// Navegar no DOM
elemento.parentElement;      // Elemento pai
elemento.children;           // Filhos
elemento.nextElementSibling; // Próximo irmão
elemento.previousElementSibling;  // Irmão anterior
```

### Codificação Base64 em JavaScript

```javascript
// Codificar para Base64
const texto = "Hello World";
const encoded = btoa(texto);
console.log(encoded);  // SGVsbG8gV29ybGQ=

// Decodificar de Base64
const decoded = atob(encoded);
console.log(decoded);  // Hello World

// Com Unicode (UTF-8)
const textUnicode = "Olá Mundo";
const encodedUnicode = btoa(unescape(encodeURIComponent(textUnicode)));
const decodedUnicode = decodeURIComponent(escape(atob(encodedUnicode)));
```

---

## <a name="sql"></a>SQL e Bancos de Dados

SQL (Structured Query Language) é usada para interagir com bancos de dados relacionais.

### Conceitos Básicos

```
Banco de Dados
    └── Tabela (Relação)
        ├── Coluna (Atributo): Nome, Tipo, Restrições
        └── Linha (Registro): Dados específicos

Exemplo:
┌─────────────────────────────────────────┐
│          Tabela: Usuários               │
├─────────┬──────────┬───────┬────────────┤
│ id (PK) │  nome    │ idade │   email    │
├─────────┼──────────┼───────┼────────────┤
│ 1       │ Alice    │ 30    │ a@ex.com   │
│ 2       │ Bob      │ 25    │ b@ex.com   │
│ 3       │ Charlie  │ 35    │ c@ex.com   │
└─────────┴──────────┴───────┴────────────┘
```

### CRUD (Create, Read, Update, Delete)

#### CREATE (Inserir)

```sql
-- Inserir um registro
INSERT INTO usuarios (nome, idade, email) 
VALUES ('Alice', 30, 'alice@example.com');

-- Inserir múltiplos registros
INSERT INTO usuarios (nome, idade, email) 
VALUES 
    ('Bob', 25, 'bob@example.com'),
    ('Charlie', 35, 'charlie@example.com'),
    ('Diana', 28, 'diana@example.com');

-- Criar tabela
CREATE TABLE usuarios (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    idade INT CHECK (idade >= 0),
    email VARCHAR(100) UNIQUE,
    ativo BOOLEAN DEFAULT TRUE,
    criado_em TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### READ (Ler)

```sql
-- Selecionar todos
SELECT * FROM usuarios;

-- Selecionar colunas específicas
SELECT nome, email FROM usuarios;

-- Com WHERE (filtro)
SELECT * FROM usuarios WHERE idade > 25;
SELECT * FROM usuarios WHERE nome = 'Alice';
SELECT * FROM usuarios WHERE idade >= 25 AND ativo = TRUE;

-- Com operadores
SELECT * FROM usuarios WHERE idade BETWEEN 25 AND 35;
SELECT * FROM usuarios WHERE nome LIKE 'A%';  -- Começa com A
SELECT * FROM usuarios WHERE email LIKE '%@gmail.com';

-- Com ORDER BY (ordenação)
SELECT * FROM usuarios ORDER BY idade ASC;   -- Ascendente
SELECT * FROM usuarios ORDER BY idade DESC;  -- Descendente

-- Com LIMIT (limite de linhas)
SELECT * FROM usuarios LIMIT 10;
SELECT * FROM usuarios LIMIT 10 OFFSET 20;  -- Paginação

-- Agregação
SELECT COUNT(*) FROM usuarios;               -- Total
SELECT AVG(idade) FROM usuarios;             -- Média de idade
SELECT MAX(idade), MIN(idade) FROM usuarios; -- Máx e mín
SELECT SUM(idade) FROM usuarios;             -- Soma

-- GROUP BY (agrupamento)
SELECT idade, COUNT(*) as total FROM usuarios GROUP BY idade;

-- JOIN (combinar tabelas)
SELECT u.nome, p.titulo 
FROM usuarios u 
JOIN posts p ON u.id = p.usuario_id;
```

#### UPDATE (Atualizar)

```sql
-- Atualizar um registro
UPDATE usuarios SET idade = 31 WHERE id = 1;

-- Atualizar múltiplas colunas
UPDATE usuarios SET idade = 30, ativo = FALSE WHERE id = 1;

-- Atualizar múltiplos registros
UPDATE usuarios SET ativo = FALSE WHERE idade < 18;
```

#### DELETE (Deletar)

```sql
-- Deletar um registro
DELETE FROM usuarios WHERE id = 1;

-- Deletar múltiplos registros
DELETE FROM usuarios WHERE idade < 18;

-- ⚠️ Deletar todos (cuidado!)
DELETE FROM usuarios;
```

### Segurança: Proteção contra SQL Injection

**SQL Injection** é um ataque onde código SQL malicioso é inserido em inputs.

```sql
-- ❌ VULNERÁVEL (concatenação direta)
query = "SELECT * FROM usuarios WHERE nome = '" + nome_input + "'"
-- Se nome_input = "Alice' OR '1'='1"
-- Resultado: SELECT * FROM usuarios WHERE nome = 'Alice' OR '1'='1'
-- Retorna TODOS os usuários!

-- ✓ SEGURO (prepared statements / parametrizado)
-- Python
import sqlite3
conn = sqlite3.connect('database.db')
cursor = conn.cursor()
cursor.execute("SELECT * FROM usuarios WHERE nome = ?", (nome_input,))

-- PHP
$stmt = $pdo->prepare("SELECT * FROM usuarios WHERE nome = ?");
$stmt->execute([$nome_input]);

-- Node.js
connection.query("SELECT * FROM usuarios WHERE nome = ?", [nome_input], 
    (error, results) => { ... });

-- SQL Server / MySQL com placeholders
SELECT * FROM usuarios WHERE nome = @nome;  -- @nome é parametrizado
```

### Relacionamentos entre Tabelas

```sql
-- Tabela Users (Usuários)
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE
);

-- Tabela Posts (Postagens) - Foreign Key
CREATE TABLE posts (
    id INT PRIMARY KEY AUTO_INCREMENT,
    titulo VARCHAR(200) NOT NULL,
    conteudo TEXT,
    usuario_id INT,
    FOREIGN KEY (usuario_id) REFERENCES users(id)
);

-- Tabela Comments (Comentários)
CREATE TABLE comments (
    id INT PRIMARY KEY AUTO_INCREMENT,
    texto TEXT,
    post_id INT,
    usuario_id INT,
    FOREIGN KEY (post_id) REFERENCES posts(id),
    FOREIGN KEY (usuario_id) REFERENCES users(id)
);

-- Relação Many-to-Many: Users -> Roles
CREATE TABLE user_roles (
    user_id INT,
    role_id INT,
    PRIMARY KEY (user_id, role_id),
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (role_id) REFERENCES roles(id)
);

-- Query com múltiplos JOINs
SELECT 
    u.nome,
    p.titulo,
    c.texto
FROM users u
LEFT JOIN posts p ON u.id = p.usuario_id
LEFT JOIN comments c ON p.id = c.post_id
WHERE u.id = 1
ORDER BY p.id, c.id;
```

### Tipos de Dados Comuns

| Tipo | Descrição | Exemplo |
|---|---|---|
| INT | Inteiro | 42, -5, 1000000 |
| FLOAT, DOUBLE | Decimal | 3.14, -2.5 |
| VARCHAR(n) | String variável | 'Alice', 'email@ex.com' |
| TEXT | String longa | Conteúdo de artigo |
| BOOLEAN | Verdadeiro/Falso | TRUE, FALSE |
| DATE | Data | '2024-01-15' |
| TIMESTAMP | Data e hora | CURRENT_TIMESTAMP |
| BLOB | Dados binários | Imagens, arquivos |
| JSON | Dados JSON | '{"chave": "valor"}' |

---

## <a name="conceitos-chave"></a>Conceitos-Chave para Lembrar

### Representação de Dados
- **Binário** é o sistema fundamental (0s e 1s)
- **Hexadecimal** (base 16) compacta 4 bits em 1 dígito
- **Operações binárias** (AND, OR, XOR) são fundamentais em criptografia

### Codificação
- **ASCII** mapeia 128 caracteres (0-127) para números
- **UTF-8** é compatível com ASCII e suporta Unicode em 1-4 bytes
- **Base64** codifica dados binários em 64 caracteres imprimíveis

### Python
- Linguagem legível com tipagem dinâmica
- **Listas e dicionários** são estruturas de dados versáteis
- **Compreensão de listas** oferece sintaxe elegante
- **Bibliotecas**: cryptography, hashlib, requests, json, re, datetime
- **Try/except** para tratamento robusto de erros

### JavaScript
- Executa em navegadores e servidores (Node.js)
- **Var vs Let vs Const**: escopo diferente, const para imutabilidade
- **Arrow functions** são sintaxe moderna
- **DOM** permite manipular HTML dinamicamente
- **Closures** permitem estado privado

### SQL
- **CRUD**: CREATE, READ, UPDATE, DELETE são operações básicas
- **WHERE** filtra registros; **JOIN** combina tabelas
- **Prepared statements** protegem contra SQL Injection
- **Foreign Keys** mantêm integridade relacional
- **Agregação e GROUP BY** para análise de dados

### Segurança de Dados
- **SQL Injection** ocorre com concatenação direta de strings
- **Usar parâmetros/placeholders** em todas as queries
- **Validar e sanitizar** entrada de usuário
- **Base64 não é criptografia** - apenas codificação

---

## 🚀 Próximos Passos no Pre Security Path

### Sequência de Aprendizagem
1. **Dominar Python:** Praticar scripts de automação e análise — essencial para ferramentas de segurança
2. **Compreender SQL:** Exploração de injeção SQL é comum em pentesting web
3. **Conhecer JavaScript:** Compreender ataques XSS e DOM manipulation em aplicações web
4. **Estudar Ataques:** Attacks and Defenses — aplicar conhecimento a vulnerabilidades reais

### Prática Recomendada
- **Escrever scripts Python:** Criar ferramentas de automação, parsing de dados, análise
- **Testar SQL Injection:** Usar ferramentas como SQLMap em ambientes seguros
- **Manipular DOM com JavaScript:** Entender como XSS funciona e impacto na segurança
- **Análise de Código:** Revisar código para identificar vulnerabilidades
- **Exercícios TryHackMe:** Fazer as tarefas práticas de programação e SQL

### Tópicos de Interesse Posterior
- **Advanced Python:** Web scraping, automatização, análise criptográfica
- **ORM (Object-Relational Mapping):** SQLAlchemy, Django ORM para proteção contra SQL Injection
- **Frameworks Web:** Django, Flask, Node.js - construção segura de aplicações
- **Reverse Engineering:** Análise de código compilado e binários
- **Vulnerability Research:** Exploração de CVEs e 0-days

---

## 🔖 Tags

#cybersecurity #programming #presecurity #tryhackme #python #javascript #sql #database #coding #sqlinjection #security #webdev

---

_Notas criadas para o TryHackMe Pre Security Path — Software Basics_  
_Formatado para Obsidian_
