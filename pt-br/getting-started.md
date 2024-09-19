# Download, instalação e execução

# Tutorial de Instalação do Kytos

Este tutorial irá guiá-lo através do processo de instalação do Kytos e suas dependências no Ubuntu, utilizando Python 3.11, Docker, Mininet, e MongoDB.

## Passo 1: Instalando Python 3.11.x

### 1. Atualize os repositórios de pacotes:


sudo apt update


### 2. Adicione o repositório PPA do Python 3.11:


sudo add-apt-repository ppa:deadsnakes/ppa


### 3. Atualize novamente os repositórios e instale o Python 3.11, junto com ferramentas essenciais para desenvolvimento:


sudo apt update
sudo apt install python3.11-dev python3.11-venv


# Passo 2: Instalando os Requisitos

### 1. Instale o Git, que será necessário para clonar os repositórios:

 sudo apt install git


# Passo 3: Criando e Ativando um Ambiente Virtual


### 1. Crie um ambiente virtual chamado `test` com Python 3.11:

python3.11 -m venv test


### 2. Ative o ambiente virtual:


source test/bin/activate


### Dentro do ambiente virtual, você verá o prefixo `(test)` no início do terminal.

# Passo 4: Instalando Dependências no Ambiente Virtual

### 1. Atualize o `pip`, `setuptools` e `wheel`:


pip install --upgrade pip setuptools wheel


## Passo 5: Baixando e Instalando o Kytos-ng

### 1. Clone os repositórios principais do Kytos-ng:


for repo in python-openflow kytos-utils kytos; do
  git clone https://github.com/kytos-ng/"${repo}"
done


### 2. Clone os repositórios de Napps (Network Applications) do Kytos-ng:


for repo in of_core flow_manager topology of_lldp of_l2ls; do
  git clone https://github.com/kytos-ng/"${repo}"
done


### 3. Instale os pacotes localmente no modo "editable" (para permitir alterações locais):


for repo in of_core flow_manager topology of_lldp of_l2ls; do
  cd "${repo}"
  python -m pip install --editable .
  cd ..
done


### Se houver algum erro, você pode proceder manualmente com os comandos abaixo:


python3 -m pip install -e git+https://github.com/kytos-ng/mef_eline@master#egg=kytos-mef_eline
python3 -m pip install -e git+https://github.com/kytos-ng/sdntrace_cp@master#egg=amlight-sdntrace_cp
python3 -m pip install -e git+https://github.com/kytos-ng/sdntrace@master#egg=amlight-sdntrace
python3 -m pip install -e git+https://github.com/kytos-ng/coloring@master#egg=amlight-coloring
python3 -m pip install -e git+https://github.com/kytos-ng/pathfinder@master#egg=kytos-pathfinder


## Passo 6: Instalando o MongoDB (Localmente)

### Atualize o sistema e adicione a chave GPG para o repositório oficial do MongoDB:

sudo apt-get update
sudo apt-get install gnupg
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -


### Adicione o repositório MongoDB ao APT:

echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list

### Atualize os repositórios e instale o MongoDB:

sudo apt-get update
sudo apt-get install -y mongodb-org

### Inicie o MongoDB e habilite-o para iniciar automaticamente no boot:

sudo systemctl start mongod
sudo systemctl enable mongod


### Verifique o status do MongoDB:

sudo systemctl status mongod

## Configurando MongoDB
### Caso precise alterar a configuração, edite o arquivo /etc/mongod.conf para ajustar parâmetros como bindIP e portas. Após editar o arquivo, reinicie o MongoDB:
sudo systemctl restart mongod


## Passo 7: Instalando o Mininet e Configurando VLANs

### 1. Instale o Mininet:

sudo apt install mininet


### 2. Para rodar o Mininet com uma topologia linear de 3 switches e um controlador remoto:

sudo mn --topo=linear,3 --controller=remote,ip=127.0.0.1


### 3. Para configurar VLANs nas máquinas:

h1 ip link add link h1-eth0 name vlan198 type vlan id 198
h1 ip link set up vlan198
h1 ip addr add 10.1.98.1/24 dev vlan198
   
h3 ip link add link h3-eth0 name vlan198 type vlan id 198
h3 ip link set up vlan198
h3 ip addr add 10.1.98.3/24 dev vlan198
   

### 4. Teste se o ping responde entre os hosts:

h1 ping 10.1.98.3
   

## Passo 8: Configurações Necessárias Sempre que Reiniciar o Ambiente

### 1. Ative o ambiente virtual e configure as variáveis do MongoDB:

   
source test/bin/activate
export MONGO_USERNAME=k1
export MONGO_PASSWORD=k1
export MONGO_DBNAME=k1
   
### 2. Inicie o Kytos com o banco de dados MongoDB:


kytosd -f --database mongodb
   

# Execução e detecção de ataques usando mnsec e Suricata
O uso do Mininet-sec detalhado neste texto foi baseado no uso da topologia básica contida no arquivo firewall.py.
## Força Bruta
Existem várias técnicas de autenticação que podem ser usadas em ataques de Força Bruta:
SSH: LOGIN (padrão), PLAIN, CRAM-MD5, DIGEST-MD5, NTLM
Além disso, a criptografia TLS via STARTTLS pode ser aplicada com a opção TLS. Exemplo: smtp://target/TLS:PLAIN; Referência.
IMAP: CLEAR ou APOP (padrão), LOGIN, PLAIN, CRAM-MD5, CRAM-SHA1, CRAM-SHA256, DIGEST-MD5, NTLM
Também suporta TLS como: imap://target/TLS:PLAIN; Referência
POP3: CLEAR (padrão), LOGIN, PLAIN, CRAM-MD5, CRAM-SHA1, CRAM-SHA256, DIGEST-MD5, NTLM.
Também suporta TLS como: pop3://target/TLS:PLAIN; Referência
No uso documentado do Mininet-sec, a principal técnica de autenticação utilizada foi LOGIN. O pacote Python Honeypots, que está sendo usado no projeto Mininet-sec, suporta apenas a técnica de autenticação PLAIN e retorna uma mensagem de execução bem-sucedida, o que pode ser um problema, já que um dos objetivos do uso de honeypots é enganar o atacante e mantê-lo executando comandos, a fim de analisar melhor o processo de ataque. Algumas soluções para esse problema, como modificar o pacote Honeypots, podem ser aplicadas em versões futuras do Mininet-sec.
# IMAP
Comando executado no diretório que continha a lista de senhas e logins:
sudo mnsecx o1 hydra  -L top-usernames-shortlist.txt -P top-usernames-shortlist.txt imap://192.168.1.103/LOGIN -V -I -F
Regras que geraram alertas:

1. alert tcp $EXTERNAL_NET any -> $HOME_NET 143 (msg:"ET SCAN Rapid IMAP Connections - Possible Brute Force Attack"; flow:to_server; flags: S,12; threshold: type both, track by_src, count 30, seconds 60; classtype:misc-activity; sid:2002994; rev:7; metadata:created_at 2010_07_30, updated_at 2019_07_26;)
2. alert tcp $EXTERNAL_NET any -> $HOME_NET 143 (msg: "Possible IMAP Brute Force attack"; flags:S; flow: to_server; threshold: type limit, track by_src, count 20, seconds 40; tcp.mss:1460; dsize:0; window:42340; classtype: credential-theft; sid: 100000137; rev:1;) (self-authored)

### SSH

Comando executado no diretório que continha a lista de senhas e logins:

```
sudo mnsecx o1 hydra  -L top-usernames-shortlist.txt -P top-usernames-shortlist.txt ssh://192.168.1.103/LOGIN -V -I -F
```

## Regra que gerou alertas:

1. alert tcp $EXTERNAL_NET any -> $HOME_NET 22 (msg:"ET SCAN Potential SSH Scan"; flow:to_server; flags:S,12; threshold: type both, track by_src, count 5, seconds 120; reference:url,en.wikipedia.org/wiki/Brute_force_attack; classtype:attempted-recon; sid:2001219; rev:20; metadata:created_at 2010_07_30, updated_at 2019_07_26;)

### POP3

Comando executado no diretório que continha a lista de senhas e logins:

```
sudo mnsecx o1 hydra  -L top-usernames-shortlist.txt -P top-usernames-shortlist.txt pop3://192.168.1.103/LOGIN -V -I -F
```

## Regra que gerou alertas:

1. alert tcp $EXTERNAL_NET any -> $HOME_NET 110 (msg: "Possible POP3 Brute Force attack"; flags:S; flow: to_server; threshold: type threshold, track by_src, count 5, seconds 20; classtype: credential-theft; sid: 100000138; rev:1;) (self-authored)

## TCP, UDP and ICMP Flood

### --rand-source

É um parâmetro de ataques Hping3 que promove o uso de diversos endereços IP para executar floods. Nesse sentido, todos os ataques de flood ICMP, UDP e TCP acionaram regras ET DROP. Essas regras são baseadas na detecção de atividades relacionadas a endereços IP conhecidos por sua relação com ataques de flood.


### Single IP attacks

Usage example (Executed in mnsec shell):

```
<mnsec-host> hping3 <protocol-or-tcp-flag> --flood -p <port-number> <ip-address> 
```

```
o1 hping3 --icmp/--udp --flood --rand-source -p 567 --data 10 192.168.1.103 (h3 host ip address)
```

```
o1 hping3 -S/-P/-U/-A/-F --flood --rand-source -p 567 --data 10 192.168.1.103 (h3 host ip address)
```

### TCP Flood

Usando portas que não tem relação específica com nenhuma função na internet:

1. alert tcp any 4444 -> any any (msg:"POSSBL SCAN M-SPLOIT R.SHELL TCP"; classtype:trojan-activity; sid:1000013; priority:1; rev:1;)

**SSH port:**

## Regra que gerou alertas:

1. alert tcp $EXTERNAL_NET any -> $HOME_NET 22 (msg:"ET SCAN Potential SSH Scan"; flow:to_server; flags:S,12; threshold: type both, track by_src, count 5, seconds 120; reference:url,en.wikipedia.org/wiki/Brute_force_attack; classtype:attempted-recon; sid:2001219; rev:20; metadata:created_at 2010_07_30, updated_at 2019_07_26;)

**POP3 ports:**

## Regra que gerou alertas:

1. alert tcp $EXTERNAL_NET any -> $HOME_NET 110 (msg: "Possible POP3 Brute Force attack"; flags:S; flow: to_server; threshold: type limit, track by_src, count 5, seconds 20; classtype: credential-theft; sid: 100000138; rev:1;) (self-authored)
2. alert tcp $EXTERNAL_NET any -> $HOME_NET 110 (msg:"ET SCAN Rapid POP3 Connections - Possible Brute Force Attack"; flow:to_server; flags: S,12; threshold: type both, track by_src, count 30, seconds 120; classtype:misc-activity; sid:2002992; rev:7; metadata:created_at 2010_07_30, updated_at 2019_07_26;)

**IMAP Flood**

## Regras que geraram alertas:

1. alert tcp $EXTERNAL_NET any -> $HOME_NET 143 (msg:"ET SCAN Rapid IMAP Connections - Possible Brute Force Attack"; flow:to_server; flags: S,12; threshold: type both, track by_src, count 30, seconds 60; classtype:misc-activity; sid:2002994; rev:7; metadata:created_at 2010_07_30, updated_at 2019_07_26;)

### UDP Flood 

Regra que gerou alertas:

1. alert udp any 4444 -> any any (msg:"POSSBL SCAN M-SPLOIT R.SHELL UDP"; classtype:trojan-activity; sid:1000014; priority:1; rev:1;)

# ICMP Flood
Não foi detectado por nenhuma regra, e as dificuldades relacionadas à detecção de ICMP Floods podem ser justificadas pelo desafio de diferenciar o tráfego legítimo envolvendo ICMP do tráfego malicioso.
# Fragmentação
A promoção da fragmentação de pacotes no tráfego pode acontecer, por exemplo, das seguintes maneiras:
Envio de um tráfego em que os pacotes têm um tamanho de dados maior que o MTU do computador alvo;
Envio de pacotes com um tamanho de dados menor ou igual ao MTU do computador alvo, no entanto, usando técnicas para promover a fragmentação;
Redução do MTU do computador.
Os ataques de inundação com fragmentação de pacotes não foram detectados pelo Suricata, e há dificuldades para criar regras nesse sentido devido à dificuldade em obter informações sobre o tráfego relacionado a esse tipo de ataque. Além disso, remontar pacotes para análise é uma tarefa que consome recursos e tempo, aumentando a complexidade da investigação dos ataques.
Conclusão
Em geral, o Suricata fez uma boa detecção dos ataques promovidos, e também foi possível criar novas regras para os casos em que a detecção não estava acontecendo, e as regras personalizadas também tiveram um bom desempenho. Como algumas regras são baseadas nas características dos pacotes relacionados ao tráfego para os quais queremos criar alertas, algumas regras foram acionadas tanto para ataques de Força Bruta quanto para ataques de Inundação relacionados aos protocolos SSH, IMAP e POP3. As regras do Suricata para Possible Scan M-Sploit R.Shell TCP/UDP foram acionadas apenas para ataques de Inundação. Essas regras detectam tentativas de exploração da rede para detectar vulnerabilidades, a fim de implementar um shell remoto, ou seja, é um ataque relacionado a tentativas de obter acesso ao shell remoto em um computador alvo.

# TESTS CONTENTION BLOCK (AÇÃO DE BLOQUEIO)

## TEST 01:
To create a containment to block traffic from VLAN 100 at the switch
00:00:00:00:00:00:00:01 port 1, one would have to run the following command:
curl -H 'Content-type: application/json' -X POST
http://127.0.0.1:8181/api/hackinsdn/containment/v1 -d '{"switch":
"00:00:00:00:00:00:00:01", "interface": 1, "match": {"vlan": 100}}'
Result: "contention created successfully ID 6a3c2d9afdd94136"
Drop the block (Only rule ID):
curl -H 'Content-type: application/json' -X DELETE
http://127.0.0.1:8181/api/hackinsdn/containment/v1 -d '{"block_id":
"6a3c2d9afdd94136"}'
Result: "contention deleted successfully ID 6a3c2d9afdd94136"
## TEST 02:
To create a containment to block traffic from IPv4 10.1.0.254 on VLAN 100 at the
switch 00:00:00:00:00:00:00:01 port 1, one would have to run the following
command:
curl -H 'Content-type: application/json' -X POST
http://127.0.0.1:8181/api/hackinsdn/containment/v1 -d '{"switch":
"00:00:00:00:00:00:00:01", "interface": 1, "match": {"vlan": 100, "ipv4_dst":
"10.1.0.254"}}'
Result: "contention created successfully ID 85b47cd567bb4b44"
## TEST 03:
To create a containment to block traffic from IPv4 10.1.0.254 on VLAN 100 and UDP
protocol at the switch 00:00:00:00:00:00:00:01 port 1, one would have to run the
following command:
curl -H 'Content-type: application/json' -X POST
http://127.0.0.1:8181/api/hackinsdn/containment/v1 -d '{"switch":
"00:00:00:00:00:00:00:01", "interface": 1, "match": {"vlan": 100, "ipv4_dst":
"10.1.0.254", "ip_proto":17}}'
Result: "contention created successfully ID 8b47dda543cc4ad3"
## TEST 04:
To list existing containments, one would have to run the following command
(two options):

curl -s http://127.0.0.1:8181/api/hackinsdn/containment/v1/
or
curl -X GET -H 'Content-type: application/json'
http://127.0.0.1:8181/api/hackinsdn/containment/v1/
## TEST 05:
NAPP doesn’t allow duplicate rules to be created:
Add rule:
curl -H 'Content-type: application/json' -X POST
http://127.0.0.1:8181/api/hackinsdn/containment/v1 -d '{"switch":
"00:00:00:00:00:00:00:01", "interface": 1, "match": {"vlan": 100}}'
Resultado: "contention created successfully ID 6a3c2d9afdd94136"
Add rule again:
curl -H 'Content-type: application/json' -X POST
http://127.0.0.1:8181/api/hackinsdn/containment/v1-d '{"switch":
"00:00:00:00:00:00:00:01", "interface": 1, "match": {"vlan": 100}}'
Resultado: "RULE already exists in the list. Contentation doesn't created"

## TESTS with IPV6:
Além dos testes apresentados, é possível criar regras também com match para IPV6.
Para isso, considere a VLAN101. É possível também add no match o “ipv6_src” ou
“ipv6_dst”.

# Tutorial do módulo MISP

## ➢ Instalação do MISP Threat Sharing (MISP)
Este tutorial é baseado nas instruções do site oficial do MISP (https://misp-project.org/).
O projeto HackInSDN utiliza a solução de containers Docker, com imagens mantidas por
Stefano Ortolani da VMware, que são atualizadas regularmente no repositório GitHub do
MISP.
○ Acesse a documentação do MISP para ter acesso às opções de instalação
disponibilizadas pela plataforma. Link: https://misp-project.org/download/
○ As instruções para a instalação usando as imagens mantidas por Stefano Ortolani
da VMware podem ser acessadas em: https://github.com/misp/misp-docker
○ Requisitos mínimos para implementar uma instância MISP:
■ Uma máquina virtual Linux (preferencialmente com as distribuições
Debian 12 ou Ubuntu 24.04 LTS) com:
● 1 processador;
● 4 GB de RAM;
● 80GB de disco;
● Versão mais recente do Docker Desktop e/ou Docker Engine.

○ Passos para a instalação:
■ Passo 1: Clonar o repositório do misp-docker. Para isso, execute o
seguinte comando no seu terminal:
$ git clone https://github.com/MISP/misp-docker/ && cd docker-misp
■ Passo 2: Copiar o arquivo de ambiente e remover seu prefixo temporário:
$ cp template.env .env
■ Passo 3: Dentro do diretório criado, verifique se o arquivo
docker-compose.yml foi baixado corretamente. Se positivo, você precisará

extrair as imagens pré-construídas ou construir novas imagens, sendo a
segunda opção mais recomendada.
Para extrair as imagens pré-construídas:
$ docker compose pull
Para construir novas imagens:
$ docker compose build
AVISO: O processo de geração das imagens pode demorar um pouco.
Aguarde até o término para seguir para o próximo passo. Em caso de
erros, consulte a seção Troubleshooting disponível no repositório indicado
nas referências deste tutorial.
■ Passo 4: Agora será necessário carregar os containers, responsáveis por
habilitar os componentes necessários (misp, misp-modules, redis, database
e mail) para a execução do MISP:
$ docker compose up
■ Passo 5: Acesse a interface web do MISP em https://localhost usando as
credenciais:
● E-mail: admin@admin.test
● Senha: admin

## ➢ Configuração da instância do MISP Threat Sharing (MISP)
Após a instalação do MISP, será necessário realizar algumas configurações, como troca
de senha, criação de organização e novos usuários.

○ Para alterar a senha do usuário padrão, clique em Administration >> List Users
>> Set password. Após inserir a nova senha, confirme a senha atual (admin) e
envie as alterações.

○ Para criar uma nova organização, clique em Administration >> Add Organisations
e preencha os campos com nome, UUID, descrição, nacionalidade, setor e outras
informações relevantes sobre sua organização.
○ Para criar um novo usuário, clique em Administration >> Add User e preencha os
campos com nome, e-mail, senha, função e organização, além de outras
informações pertinentes ao novo usuário da sua organização.
○ Para ter acesso aos eventos compartilhados por outras organizações, será
necessário habilitar os feeds. No exemplo abaixo, apresentamos o passo a passo
de como habilitar os feeds públicos disponibilizados no MISP:
■ Passo 1: Verificar se os Workers estão ativados;
■ Passo 2:Habilitar os feeds das organizações CIRCL e Botvrij.eu;
■ Passo 3: Fazer o download dos eventos.

## ➢ Instalação do PyMISP
PyMISP é uma biblioteca desenvolvida em Python que facilita a interação com a
plataforma MISP por meio de sua API REST. Com o PyMISP, é possível realizar
operações como buscar eventos, inserir ou modificar eventos e atributos, adicionar ou
atualizar amostras, além de realizar pesquisas de atributos. Para instalar a biblioteca, siga
os passos abaixo:

○ Passo 1: Instale as dependências obrigatórias:
$ pip3 install pymisp
○ Passo 2: Acesse o diretório
https://github.com/MISP/PyMISP/tree/main/examples e altere o
keys.py.sample para inserir sua URL MISP e chave de API:
cd examples
cp keys.py.sample keys.py
vim keys.py

## ➢ Scripts de exportação e importação de dados
○ Para exportar IPs comprometidos da sua instância MISP no formato de regra para
o Suricata, execute o script export_suricata:

$ sh export_suricata
○ Para exportar indicadores de comprometimento de um determinado evento no
formato CSV, execute o script export_csv com o seguinte comando:
$ python3 export_csv -e <ID_do_Evento> -f <Nome_do_Arquivo>

○ O script importCauma.py realiza uma importação básica de dados em uma
instância MISP. No exemplo abaixo, inserimos URLs maliciosas coletadas do
Catálogo de URLs Maliciosas (https://cauma.pop-ba.rnp.br/). Para executar o
script, utilize o comando:
$ python3 importCauma.py

## ➢ Referências
○ PyMisp: https://github.com/MISP/PyMISP
○ Documentação do MISP: https://www.misp-project.org/documentation/
○ Repositório MISP-Docker: https://github.com/misp/misp-docker

# Ativação Mininet-sec

[Instalação do Mininet-sec](https://github.com/mininet-sec/mininet-sec?tab=readme-ov-file#mininet-sec)

Se você receber a mensagem de erro *"No module called Mininet"* durante o processo de instalação, mesmo com o Mininet já instalado em seu sistema, você pode executar os seguintes comandos para resolver o problema:

```
sudo -i
cd ~
git clone https://github.com/mininet/mininet.git
export PYTHONPATH=$PYTHONPATH:$HOME/mininet
```

O [Kytos-ng](https://github.com/kytos-ng/kytos?tab=readme-ov-file#kytos-ngkytos) é o controlador SDN que será usado junto com o mnsec para criar e gerenciar as conexões entre os componentes da rede, além de executar outras funções. Ele pode ser ativado de diferentes maneiras. Cada um dos processos descritos a seguir deve ser executado em janelas diferentes.

⚠️ Os passos 1 e 3 não são necessários se o usuário vai usar a topologia definida no arquivo *firewall.py*. Eles são necessários para ativar o Kytos-ng, a fim de permitir seu uso como controlador remoto e estabelecer as conexões entre os componentes da rede (ativação do NOS), no caso de uso de uma topologia personalizada.

### 1. Ativar o Kytos;

```
source test_env/bin/activate
cd teste
cd kytos
sudo ./docker/scripts/add-etc-hosts.sh 
export MONGO_USERNAME=mymongouser
export MONGO_PASSWORD=mymongopass
docker compose up -d
docker ps 
kytosd -f --database mongodb
```

### 2. Iniciar o mnsec;

**É importante usar o modo root ao executar esses comandos.** O mnsec pode ser usado com topologias predefinidas, por exemplo:

```
cd mininet-sec
cd examples
python3 firewall.py
```

Nesta topologia, temos 3 hosts internos (h1, h2, h3), 1 servidor externo (o1), 2 servidores (srv1, srv2), 3 switches (s1, s2, nettap1) e a presença de um firewall (fw0).

Esta é a rede estabelecida:

1. fw0 fw0-eth0:s1-eth4 fw0-eth1:s2-eth3 fw0-eth2:nettap1-eth1
2. h1 h1-eth0:s1-eth1
3. h2 h2-eth0:s1-eth2
4. h3 h3-eth0:s1-eth3
5. o1 o1-eth0:nettap1-eth2
6. srv1 srv1-eth0:s2-eth1
7. srv2 srv2-eth0:s2-eth
8. nettap1 lo: nettap1-eth1:fw0-eth2 nettap1-eth2:o1-eth0 nettap1-ethmona: nettap1-ethmonb:
9. s1 lo: s1-eth1:h1-eth0 s1-eth2:h2-eth0 s1-eth3:h3-eth0 s1-eth4:fw0-eth0
10. s2 lo: s2-eth1:srv1-eth0 s2-eth2:srv2-eth0 s2-eth3:fw0-eth1

O nettap1 é um switch que promove a conexão entre os componentes internos da rede e a internet, através da interface do firewall fw0-eth2. Ele também usa a interface nettap-eth2 para se conectar com o host o1. Além disso, existem interfaces que promovem a conexão do firewall com a internet:

1. nettap1-ethmona: Conexão com a internet, promove o envio de tráfego do firewall para a internet.
2. nettap1-ethmonb: Conexão com a internet, promove o envio de tráfego da internet para o firewall.

Ou o usuário pode criar uma topologia personalizada, por exemplo:

```
mnsec --topo linear,3 --apps h3:ssh:port=22,h3:http:port=80,h3:ldap,h3:smtp,h3:imap,h3:pop3 --controller=remote,ip=127.0.0.1
```

Neste caso, estamos criando uma topologia linear com 3 hosts (h1, h2, h3), e o h3 tem algumas portas importantes definidas como abertas, a fim de testar ataques.

### 3. Ativação do NOS;

```
for sw in $(curl -s http://127.0.0.1:8181/api/kytos/topology/v3/switches | jq -r '.switches[].id'); do curl -H 'Content-type: application/json' -X POST http://127.0.0.1:8181/api/kytos/topology/v3/switches/$sw/enable; curl -H 'Content-type: application/json' -X POST http://127.0.0.1:8181/api/kytos/topology/v3/interfaces/switch/$sw/enable; done

for l in $(curl -s http://127.0.0.1:8181/api/kytos/topology/v3/links | jq -r '.links[].id'); do curl -H 'Content-type: application/json' -X POST http://127.0.0.1:8181/api/kytos/topology/v3/links/$l/enable; done
```
```
curl -H 'Content-type: application/json' -X POST http://127.0.0.1:8181/api/kytos/mef_eline/v2/evc/ -d '{"name": "my evc1", "dynamic_backup_path": true, "enabled": true, "uni_a": {"interface_id": "00:00:00:00:00:00:00:01:1"}, "uni_z": {"interface_id": "00:00:00:00:00:00:00:01:2"}}'
```

