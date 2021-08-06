# Instalace Let's Encrypt certifikat

## Install cert-manager
Instalace vseho co je potreba k vyzadani certifikatu, automaticke obnove a jak otestovat ze vsecho funguje je [tady - instalace cert-manager](./install-cert-manager.md)

## Vytvoreni clusterIssuer

K Vytvoreni certifikatu je potreba dodat existujici adresu.

Email adresa je potreba, protoze ti na tento email prijde email ze dojde expiraci atd

instalace:

 ```
 kubectl apply -f cert-issuer-nginx.yaml
 ```

 ## Overeni cluster issuer

 ```
kubectl describe clusterissuer letsencrypt-cluster-issuer
 ```
 > melo by dojit k registraci u ACME serveru a mel bys videt toto
 
 > _Message: The ACME account was registered with the ACME server_
 
 > _Reason: ACMEAccountRegistered_

## POZOR

 ***!!! u produkcniho certifikatu je potreba pred tim nez se spusti certifikace je aby byl napred instalovan ingress !!!***
 
 ten duvod je ten ze autorika ktera vystavuje produkcni certifikat overuje domenu a hlavne jestli je ziva. tzn nestaci nastavit `/etc/hosts` ale opravdu musi existovat dns ***A*** zaznam. ACME server pri requestu certifikatu `cert-manager` overuje jestli server existuje a nevraci 404. Pokud bude vracet 404 (stranka neexistuje) tak nevyda certifikat. Proto pokud web server bezi v klusteru tak musi napred existovat `ingress` nez se pozada o certifikat. U typu `Stanging let's encrypt` tato podminka neni potreba.

 ## Instalace nginx ingress

Instalaci nginx-ingress najdes [tady](../nginx-ingress/nginx-ingress/README.md) a muzes si zkusit nasadit [demo](../nginx-ingress/demo/README.md) doporucuji to spojit s loadbalancerem (pokud mas cloud provider tak o load balancer se postara) tady je jak jsem to resil s [haproxy](../haproxy-loadbalancer/README.md)

## Instalace ingress resource

[Tady](./ingress.yaml) je priklad jak propojit let's encrypt s domenou a tls secure.

## Instace a vytvoreni certifikatu
Instalace certifikatu je posledni krok ale je potreba abys mel vsechno nastartovane a bez chyb. Dulozita vec ze generace noveho certifikatu trochu trva.

### Co je potreba zkontrolovat

`kubectl get all -n cert-manager` - vse k cert-manageru

`kubectl get ing` - ingress resource -  s domenou

`kubectl get svc - overit jestli service a jeji port na kterou se odkazuje v _ingress.yaml_ existuje.

## Instalace certifikatu

`kubect apply -f certificate.yaml`

## Overeni certifikatu

`kubectl describe certificate nginx` - vysledkem by mel byt ***The certificate has been successfully issued***, tady se da zjistit i expirace (vetsinou se jedna o 3 mesicni certifikat)

a ze existuje secret `nginx-tls`

`kubectl get secret`

zobrazeni info o `nginx-tls`

`kubectl describe secret nginx-tls` - tady by se mel videt ze existuje certifikate a privatni klic napr `tls.crt` a `tls.key`

