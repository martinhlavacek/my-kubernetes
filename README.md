# My Kubernetes

@autor: Kubectl.cz (martin.hlavacek@kubectl.cz)

---

# 1. Info a upravy

Kdyz jsem neco resil z kubernetes a nefungovalo mi to tak jsem musel neco upravovat a tady je seznam mych uprav



## [1.1. Metrics-server](./metrics-server/readme.md)
Informace o vyuziti prostredku jako je CPU(cores), CPU%, Memory(bytes) a MEMORY%

## Kubectl extend
`kubectx` a `kubens` release je tady [release](https://github.com/ahmetb/kubectx/releases)

> stahnout kubectx a kubens release pro danou verzi pro ubuntu jsem pouzil `linux_x86_64`
nastavit jako spustitelny soubor

```bash
chmod +x kubectx
```

```bash
chmod +x kubenx
```
prekopirovat(presunout) do `/usr/local/bin`

```bash
sudo mv kubectx /usr/local/bin
```

```bash
sudo mv kubens /usr/local/bin
```

overit ze oba soubory jsou v path

```bash
which kubectx
```

```bash
which kubens
```

> Poznamka do `.profile` `.zshrc` atd vytvorit alias `kx = kubectx` a `kn = kubens`
> ```bash
> alias kx="kubectx"
> alias kn="kubens"
> ```


