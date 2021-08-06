# lxd/lxc kontejner

## Instalace [zde](./install.md)
---
!!Po nainstalovani lxc/lxd je potreba spustit 
```bash
lxd init
```
## LCD init

## SEZNAM PRIKAZU

### REMOTE LIST
> seznam repository
```bash
lxc remote list
```

### LIST
> seznam bezicih lxc kontejneru
```bash
lxc list
```

### IMAGE LIST
> seznam stazenych obrazu
```bash
lxc image list
```

### IMAGE LIST IMAGE:CEB
> vyhledani centos v images repo
```bash
lxc image list images:cen
```
```bash
lxc image list images:cent | less
```

### LAUNCH
> spusteni kontejneru
> pokud obraz neni stazeny tak se stahne a spusti se kontejner

```bash
lxc launch [nazev obrazu]:[verze] [nazev kontaineru]
```
*priklad*
```bash
lxc launch ubuntu:20.04 ubuntu1
```

### LAUNCH - S PROFILE
> spusteni kontejneru s profilem

```bash
lxc launch [nazev obrazu]:[verze] [nazev kontaineru] --profile [nazev profilu]
```
*priklad*
```bash
lxc launch ubuntu:20.04 ubuntu1 --profile custom
```

### DELETE
> smazani beziciho kontaineru
```bash
lxc delete [nazev kontaineru]
```

*priklad*

```bash
lxc delete ubuntu1
```
> _bezici kontainer ktery chces smazat tak se musi pouzit parametr `--force`_

### STOP
> zastaveni kontejneru
```bash
lxc stop [nazev kontejneru]
```
*priklad*
```bash
lxc stop ubuntu1
```

### START
> start zastaveneho kontejneru
```bash
lxc start [nazev]
```

*priklad*
```bash
lxc start ubuntu1
```
### COPY
> kopirovani kontejneru
```bash
lxc copy [nazev zdrojoveho kontejneru] [nazev jak se bude jmenovat novy kontejner]
```

*priklad*
```bash
lxc copy ubuntu1 ubuntu2
```

### MOVE
> prejmenovani kontejneru
> prejmenovani se muze delat jen kdyz je kontejner zastaveny
```bash
lxc move [nazev] [novy nazev]
```
*priklad*
```bash
lxc move ubuntu1 ubuntu1New
```


### EXEC
> pristup do beziciho kontejneru
```bash
lxc exec [nazev] [prikaz]
```
*priklad*
```bash
lxc exec ubuntu1 bash
```
### EXEC su - ubuntu
> pristup do beziciho kontejneru jako jiny uzivate
```bash
lxc exec ubuntu1 su - ubuntu
```
#### 1.12 - info o kontejneru
```bash
lxc info ubuntu1
```

### CONFIG
> config kontejneru
```bash
lxc config show ubuntu1
```

### CONFIG SET LIMITS - MEMORY
> kontejner musi byt zastaveny
> config kontejneru na limit pameti
```bash
lxc config set [nazev kontejneru] limits.memory [velikost]
```
*priklad*

```bash
lxc config set ubuntu limits.memory 512MB
```

### CONFIG SET LIMITS - CPU
> kontejner musi byt zastaveny
> config kontejneru na limit cpu
```bash
lxc config set [nazev kontejneru] limits.cpu [pocet]
```
*priklad*

```bash
lxc config set ubuntu limits.cpu 1
```



### PROFILE LIST
> seznam profilu
> profily slouzi ke specifikovani napriklad nastaveni pro dany lxc kontejner...jako je napriklad velikost pameti, cpu atd
```bash
lxc profile list
```

### PROFILE - SHOW
> zobrazeni informaci o profilu
```bash
lxc profile show [nazev profilu]
```
*priklad*
```bash
lxc profile show default
```

### PROFILE - COPY
> vytvoreni noveho profilu z existujiciho

```bash
lxc profile copy [nazev existujiciho profilu] [nazev nove profilu]
```

```bash
lxc profile copy default custom
```

### PROFILE - EDIT
> editace profilu

```bash
lxc profile edit [nazev]
```

```bash
lxc profile edit custom
```
> spusti se editor `vi` a muze se nastavit napriklad limit na pamet
```yaml
config:
  limits.memory: 512MB
```

## FILE

### PUSH
> upload soubrou
```bash
lxc file push [jmeno souboru] [nazev kontejneru]/path/
```

*priklad*
```bash
lxc file push readme ubuntu1/root/
```

### PULL
> download soubrou
```bash
lxc file pull [nazev kontejneru]/path/ [cesta na lokale]
```

*priklad*
```bash
lxc file pull ubuntu1/root/readme .
```

### SNAPSHOT
> vytvoreni snapshotu kontejneru
```bash
lxc snapshot [nazev kontejneru] [nazev snapshoru]
```

*priklad*
```bash
lxc snapshot u1 su1
```

### RESTORE
> obnoveni kontejneru ze snapshotu
> pokud potrebujes znat nazev snapshotu ktery se ma obnovit tak `lxc info u1` a dole je videt seznam snapshots
```bash
lxc restore [nazev kontejneru] [nazev snapshoru]
```

*priklad*
```bash
lxc restore u1 su1
```

## Prace v kontejneru

> prikaz pro spusteni `bash` v kontaineru a pristup do nej `lxc exec ubuntu bash`

### ping mezi kontejnerama

```bash
ping ubuntu1.lxd
```

## Vnorovani lxc/lxd
> pokud chce vnorovat do kontaineru dalsi lxc/lxd, tak je potreba nastavit konfiguraci pro kontejner

### Rucni nastaveni kontejneru
> je potreba zastavit kontejner
```bash
lxc stop ubuntu1
```
> rucni nastaveni konfigurace pro nesting kontejneru
```bash
lxc config set ubuntu1 security.privileged true
lxc config set ubuntu1 security.nesting true
```

### Nastaveni profilu
> editace profilu
```bash
lxc profile edit custom
```
> nastaveni profilu - pridat security.privilaged true a security.nesting true do sekce config

```yaml
config:
  security.privilaged true
  security.nesting true
```