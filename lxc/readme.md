# lxd/lxc kontejner

## Instalace [zde](./install.md)
---
## 1. prikazy

### 1.1 - list repository

```bash
lxc remote list
```

### 1.2 - seznam bezicih lxc kontejneru

```bash
lxc list
```

### 1.3 - seznam stazenych obrazu

```bash
lxc image list
```

### 1.4 - vyhledani a zobrazeni obrazu

> vyhledani centos v images repo

```bash
lxc image list images:cen
```
```bash
lxc image list images:cent | less
```

### 1.5 - spusteni kontejneru

> pokud obraz neni stazeny tak se stahne a spusti se kontejner

```bash
lxc launch [nazev repository]:[verze] [nazev kontaineru]
```
*priklad*
```bash
lxc launch ubuntu:20.04 ubuntu1
```

### 1.6 - smazani beziciho kontaineru

```bash
lxc delete [nazev kontaineru]
```

*priklad*

```bash
lxc delete ubuntu1
```
> _bezici kontainer ktery chces smazat tak se musi pouzit parametr `--force`_

### 1.7 - zastaveni kontejneru
```bash
lxc stop [nazev kontejneru]
```
*priklad*
```bash
lxc stop ubuntu1
```

### 1.8 - start zastaveneho kontejneru
```bash
lxc start [nazev]
```

*priklad*
```bash
lxc start ubuntu1
```
### 1.9 - kopirovani kontejneru
```bash
lxc copy [nazev zdrojoveho kontejneru] [nazev jak se bude jmenovat novy kontejner]
```

*priklad*
```bash
lxc copy ubuntu1 ubuntu2
```

### 1.10 - prejmenovani kontejneru
> prejmenovani se muze delat jen kdyz je kontejner zastaveny
```bash
lxc move [nazev] [novy nazev]
```
*priklad*
```bash
lxc move ubuntu1 ubuntu1New
```


### 1.11 - pristup do beziciho kontejneru
```bash
lxc exec [nazev] [prikaz]
```
*priklad*
```bash
lxc exec ubuntu1 bash
```
#### 1.11.1 - pristup do beziciho kontejneru jako jiny uzivate
```bash
lxc exec ubuntu1 su - ubuntu
```


## Prace v kontejneru

> prikaz pro spusteni `bash` v kontaineru a pristup do nej `lxc exec ubuntu bash`

### 1. ping mezi kontejnerama

```bash
ping ubuntu1.lxd
```