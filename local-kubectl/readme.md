# Instalace `kubectl` Ubuntu 20.04

## Ubuntu 20.04

### Pres oficialne apt repository apt.kubernetes.io

```bash
{
    apt install -y apt-transport-https curl
    curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
    apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
    apt update
    apt install -y kubectl
}
```

### Pres snap

```bash
snap install kubectl --classic
```
> `snap` snap je Software centre k installaci snap aplikaci
