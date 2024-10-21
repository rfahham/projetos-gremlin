# Instalando o Gemlin no Linux

https://www.gremlin.com/docs/getting-started-install-virtual-machine#/deb-packages


## Pacotes DEB

Para distribuições Linux baseadas em DEB, como Ubuntu, Debian e assim por diante.

```bash
# Add packages needed to install and verify gremlin (already on many systems)
sudo apt update && sudo apt install -y apt-transport-https dirmngr

# Add the Gremlin repo
echo "deb https://deb.gremlin.com/ release non-free" | sudo tee /etc/apt/sources.list.d/gremlin.list

# Import the GPG key
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 9CDB294B29A5B1E2E00C24C022E8EF3461A50EF6

# Install Gremlin
sudo apt update && sudo apt install -y gremlin gremlind

```

## Pacotes RPM

Distribuições baseadas em SUSE

Para distribuições baseadas no SUSE Linux, como SUSE Linux Enterprise Server (SLES), openSUSE, etc.:

```bash
# Install dependencies
sudo zypper install -y iproute-tc libcap-progs

# Add the Gremlin repo
curl https://rpm.gremlin.com/gremlin.repo -o /tmp/gremlin.repo && sudo zypper addrepo /tmp/gremlin.repo

# Install Gremlin and dependencies
sudo zypper refresh && sudo zypper install gremlin gremlind
```

## Distribuições não baseadas em SUSE

Para distribuições RPM não baseadas em SUSE, como Amazon Linux, RHEL, CentOS, etc.:

```bash
# Install dependencies
sudo yum install -y iproute-tc

# Add the Gremlin repo
sudo curl https://rpm.gremlin.com/gremlin.repo -o /etc/yum.repos.d/gremlin.repo

# Install Gremlin
sudo yum install -y gremlin gremlind
```

## Configurar Gremlin

A configuração mínima necessária para autenticar o Agente Gremlin é:

    ID da equipe
    Segredo ou certificado

Se você baixou um arquivo de configuração do cliente, você já tem tudo o que precisa para registrar o Agent. 

Basta seguir estas instruções:

Copie o arquivo de configuração (chamado config.yaml ) para o diretório /etc/gremlin/ . O caminho final deve ser /etc/gremlin/config.yaml :

```bash
sudo cp config.yaml /etc/gremlin/config.yaml
```
Reinicie o serviço gremlind

```bash
sudo systemctl restart gremlind
```

## Validar a instalação

Verifique o aplicativo da web Gremlin

https://app.gremlin.com/clients/hosts

Verifique o agente Gremlin

Primeiro, verifique se o Gremlin Agent está em execução no sistema de destino:

```bash
sudo systemctl status gremlind
```

Isso deve retornar o seguinte:

```bash
● gremlind.service - Gremlin Daemon
     Loaded: loaded (/etc/systemd/system/gremlind.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2023-01-04 10:44:12 EST; 5 days ago
```

Se o serviço estiver sendo reportado como inativo ou com falha, tente reiniciá-lo usando:

```bash
sudo systemctl restart gremlind
```

Depois de verificar se o Gremlin Agent está em execução, use gremlin check auth para verificar o status de autenticação do Gremlin Agent:


```bash
gremlin check auth
```

Se o Agente Gremlin for autenticado com sucesso, a saída será semelhante à seguinte:

auth
====================================================
Auth Input Type                      : Certificate
API Response                         : OK

Caso contrário, a saída explicará por que o Agente Gremlin não conseguiu autenticar:

auth
====================================================
Auth Input Type                      : No valid auth found
========= Identification ============:
Team ID Source                       : Team ID not found
Gremlin Identifier                   : [Host identifier]
Gremlin Identifier Source            : Not supplied explicitly, using the default
========= Secret/Token Info =========:
Team Secret Source                   : Team Secret not found
.credentials valid                   : /var/lib/gremlin/.credentials file not found
========= Certificate Info ==========:
Team Certificate Source              : Team Certificate not found
========= Private Key Info ==========:
Team Private Key Source              : Team Private Key not found


## Desinstalando pacotes DEB

Para distribuições Linux baseadas em DEB, como Ubuntu e Debian:

```bash
sudo apt remove gremlin gremlind
```