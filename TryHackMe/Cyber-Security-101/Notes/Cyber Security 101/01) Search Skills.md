 
# Modulo 1
 
 Para procurar  a fonte da informaçao  e tomar cuidado com [^1]Snake Oil 
 com isso o primeiro modulo fala sobre um paço inicial que é importante avaliar bem as ferramentas criptográficas exatamente pelos critérios mencionados no texto (fonte, evidências, objetividade...).
 
 outra coisa que ele fala é sobre o comando ==ss== no Linux  que é o comando moderno que substitui o `netstat` em sistemas Linux. Faz parte do pacote `iproute2` e serve para exibir informações sobre conexões de rede, sockets, portas abertas, etc. É mais rápido e completo que o `netstat`, que pertencia ao pacote `net-tools`, hoje considerado obsoleto na maioria das distribuições.
 O comando `ss` (**S**ocket **S**tatistics) serve para **monitorar conexões de rede** num sistema Linux. É basicamente uma ferramenta de diagnóstico de rede.

**O que ele mostra:**

- Conexões TCP/UDP ativas
- Portas abertas e em escuta (listening)
- Endereços IP locais e remotos conectados
- Estado das conexões (ESTABLISHED, LISTEN, TIME-WAIT, etc.)

**Exemplos de uso comuns:**

bash

```bash
ss -tuln      # mostra portas TCP/UDP abertas
ss -ta        # todas as conexões TCP
ss -s         # resumo estatístico das conexões
ss -p         # mostra qual processo está usando cada conexão
```

**Na prática, serve para:**

- Ver se um serviço está realmente a escutar numa porta
- Detetar conexões suspeitas (útil em segurança)
- Diagnosticar problemas de rede
- Ver quais programas estão a usar a rede

# Modulo 2

agora ele ta me ensinado a pesquisar no google  com comandos para por exemplo se eu pesquisar "Hacker"  ira achar sites que tenham a palavra hacker agora se eu pesquisar site:tryhackme.com falha ele ira pesquisar tudo sobre a falha no tryhackme  agr filetype:ppt cyber security ele ira pesquisar powerpoit de cyber security e esse link [lista de operadores de pesquisa avançada.](https://github.com/cipher387/Advanced-search-operators-list) ele tem todos os comandos  para pesquisa 


[^1]: **Snake Oil** — é o termo usado na criptografia para descrever métodos, algoritmos ou produtos que se apresentam como seguros mas que na prática são fracos, mal implementados ou deliberadamente enganosos. A analogia vem dos charlatões do século XIX que vendiam "óleo de cobra" como remédio milagroso. 


# Modulo 3

agora ta me dando ferramentas de pesquisas mais fortes  e para coisas especificas como o  [Shodan.](https://www.shodan.io/) que é um mecanismo de busca para dispositivos conectados à Internet. Ele permite pesquisar tipos e versões específicos de servidores, equipamentos de rede, sistemas de controle industrial eIoTdispositivos. Talvez você queira verificar quantos servidores ainda estão em execução.Apache2.4.1 e a distribuição entre países. Para encontrar a resposta, podemos pesquisar por `apache 2.4.1`, que retornará a lista de servidores com a string “apache2.4.1” em seus cabeçalhos.

Considere visitar [os exemplos de consultas de pesquisa do Shodan.(abre em nova aba)](https://www.shodan.io/search/examples)Para mais exemplos, consulte as tendências do Shodan. Além disso, você pode verificar [as tendências do Shodan.(abre em nova aba)](https://trends.shodan.io/)Para obter informações históricas, caso tenha uma assinatura.


À primeira vista, [Censys(abre em nova aba)](https://search.censys.io/)Parece semelhante ao Shodan. No entanto, o Shodan concentra-se em dispositivos e sistemas conectados à Internet, como servidores, roteadores, webcams eIoTO Censys, por outro lado, concentra-se em hosts conectados à Internet, sites, certificados e outros ativos da Internet. Alguns de seus casos de uso incluem a enumeração de domínios em uso, a auditoria de portas e serviços abertos e a descoberta de ativos não autorizados em uma rede. Você pode consultar [os Casos de Uso Introdutórios do Censys .(abre em nova aba)](https://docs.censys.com/docs/ls-introductory-use-cases#/).

[VirusTotal(abre em nova aba)](https://www.virustotal.com/)É um site online que oferece um serviço de verificação de vírus para arquivos usando vários mecanismos antivírus. Ele permite que os usuários carreguem arquivos ou forneçam URLs para serem verificados por diversos mecanismos antivírus e verificadores de sites em uma única operação. Eles podem até inserir hashes de arquivos para verificar os resultados de arquivos carregados anteriormente.

A captura de tela abaixo mostra o resultado da verificação do arquivo enviado em 67 mecanismos antivírus. Além disso, você pode consultar os comentários da comunidade para obter mais informações. Ocasionalmente, um arquivo pode ser sinalizado como vírus ou Trojan; no entanto, isso pode não ser preciso por vários motivos, e é aí que os membros da comunidade podem fornecer uma explicação mais detalhada.

[Fui enganado(abre em nova aba)](https://haveibeenpwned.com/)O HIBP (Hierarchical Information Protection) faz uma coisa: informa se um endereço de e-mail apareceu em um vazamento de dados. Encontrar o e-mail de alguém em dados vazados indica que informações privadas foram expostas e, mais importante, que senhas também foram. Muitos usuários usam a mesma senha em várias plataformas; se uma plataforma for invadida, a senha em outras plataformas também ficará exposta. De fato, as senhas geralmente são armazenadas em formato criptografado; no entanto, muitas senhas não são tão complexas e podem ser recuperadas usando diversos tipos de ataques.

# Modulo 4

agora ele me ensinou achar [^2]cve  para ver vunerabilidades que ja foram encontradas 
## CVE

Podemos pensar nas Vulnerabilidades e Exposições Comuns (CVE) programa como um dicionário de vulnerabilidades. Ele fornece um identificador padronizado para vulnerabilidades e problemas de segurança em produtos de software e hardware. Cada vulnerabilidade recebe um número.CVEID com um formato padronizado como `CVE-2024-29988`. Este identificador único (CVEO ID garante que todos, desde pesquisadores de segurança a fornecedores e profissionais de TI, estejam se referindo à mesma vulnerabilidade.[CVE-2024-29988(abre em nova aba)](https://nvd.nist.gov/vuln/detail/CVE-2024-29988)nesse caso.

OMITRAA empresa mantém oCVEsistema. Para obter mais informações e pesquisar CVEs existentes, visite o[CVEPrograma(abre em nova aba)](https://www.cve.org/)Como alternativa, visite o site [do Banco de Dados Nacional de Vulnerabilidades .(abre em nova aba)](https://nvd.nist.gov/)Site da NVD (National Vigilância Não Destrutiva). A captura de tela abaixo mostraCVE-2014-0160, também conhecido como Heartbleed.


## Banco de dados de exploração

É um recurso disponível é o [Banco de Dados de Exploração (Exploit Database).(abre em nova aba)](https://www.exploit-db.com/)O banco de dados de exploits lista códigos de exploração de diversos autores; alguns desses códigos foram testados e marcados como verificados.


# Modulo 5
## LinuxPáginas do manual

Muito antes da internet estar em todos os lugares, como você obteria ajuda usando um comando em umLinuxou um sistema do tipo Unix? A resposta seria consultar a página do manual, ou man page, para abreviar.LinuxEm todo sistema do tipo Unix, espera-se que cada comando tenha uma página de manual (man page). Aliás, também existem páginas de manual para chamadas de sistema, funções de biblioteca e até mesmo arquivos de configuração.

Digamos que queremos consultar a página do manual do comando `ip`. Executamos o comando `man ip`. A captura de tela abaixo mostra a página que recebemos. Você pode tentar fazer isso em uma máquina Linux que tenha disponível.

![A página do manual do comando ip](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1718112797192)

Se preferir ler a página do manual `ip`no seu navegador, basta digitar `man ip`no seu mecanismo de busca favorito. Esta [página(abre em nova aba)](https://linux.die.net/man/8/ip)pode estar no topo dos resultados.

## Microsoft Windows

A Microsoft fornece [documentação técnica oficial.(abre em nova aba)](https://learn.microsoft.com/)página para seus produtos. A captura de tela abaixo mostra os resultados da pesquisa para o comando `ipconfig`.

![Os resultados da pesquisa por ipconfig no site de documentação técnica da Microsoft.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1718112815041)

## Documentação do produto
É sempre vantajoso consultar a documentação oficial, pois ela é a mais atualizada e oferece as informações mais completas sobre o produto.


# Modulo 6

![Hacker com um laptop](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1720443820951.svg)

Existem bilhões de usuários cadastrados em plataformas de mídia social como [o Facebook.(abre em nova aba)](https://www.facebook.com/people/Tryhackme/100069557747714/)Twitter[​(abre em nova aba)](https://twitter.com/RealTryHackMe)e [LinkedIn(abre em nova aba)](https://www.linkedin.com/company/tryhackme/)Esperamos que você esteja familiarizado com as plataformas mais populares. No entanto, se você conhece alguma plataforma que não conhece, recomendamos que a explore e aprenda sobre ela. O ideal seria explorar uma plataforma sem criar uma conta; porém, isso limita bastante a sua experiência. Uma recomendação é usar um endereço de e-mail temporário para descobrir essas plataformas sem vinculá-las aos seus endereços de e-mail reais; depois disso, você pode encerrar as contas e os endereços de e-mail associados. Um dos motivos para não usar sua conta principal é evitar que seus contatos comecem a se conectar com você por lá enquanto você estiver apenas explorando a plataforma temporariamente.

O poder das redes sociais reside na possibilidade de conectar-se com empresas e pessoas de seu interesse. Além disso, as redes sociais oferecem uma vasta gama de informações para profissionais de segurança cibernética, seja para buscar pessoas ou informações técnicas. Por que buscar pessoas é importante, você pergunta?

Ao proteger uma empresa, você deve garantir que as pessoas que você protege não compartilhem informações pessoais em excesso nas redes sociais. Por exemplo, as redes sociais delas podem revelar a resposta para perguntas confidenciais, como "Em qual escola você estudou quando criança?". Essas informações podem permitir que invasores redefinam suas senhas e assumam o controle de suas contas com facilidade.

Além disso, como profissional de segurança cibernética, você deseja se manter atualizado sobre as novas tendências, tecnologias e produtos de segurança cibernética. Seguir os canais e grupos adequados pode proporcionar um ambiente propício para o desenvolvimento de sua expertise técnica.

Além de se manter atualizado por meio de redes sociais e grupos, devemos mencionar os veículos de notícias. Centenas de sites de notícias oferecem informações valiosas sobre segurança cibernética. Experimente diferentes opções e fique com aqueles que você mais gostar.

Responda às perguntas abaixo.

Você foi contratado para avaliar a segurança de uma determinada empresa. Qual rede social popular você usaria para obter informações sobre o conhecimento técnico de um dos funcionários dessa empresa?

LinkedIn

Continuando com o cenário anterior, você está tentando encontrar a resposta para a pergunta secreta: "Em qual escola você estudou quando criança?". Qual rede social você consideraria consultar para encontrar a resposta para perguntas secretas como essa?

Facebook



[^2]: Vulnerabilidades e Exposições Comuns (CVE, na sigla em inglês) é um termo usado para se referir a uma vulnerabilidade divulgada publicamente. 
