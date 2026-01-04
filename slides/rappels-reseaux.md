---
marp: true
headingDivider: 1
paginate: true
header: 'AGR1i'
footer: 'Pierre Bettens _pbt_'  
style: |
    h1, h2 {
        color: #3e8ea3;
    }
    footer {
        background: #D2D2D2;
        color: peru;
        position: absolute;
        left: 0px;
        right: 0px;
        height: 25px;
        bottom: 0px;
        padding: 5px 20px;
    }
    section::after {
        /* Layout of pagination content */
        background-color: darkgrey;
        color:#3e8ea3;
        position: absolute;
        bottom: 0px;
        right: 0px;
        width: 150px;
        height: 25px;
        line-height: 20px;
        padding: 5px 2px 5px 35px;
        text-align: center;
        /* Add number of pages*/
        content: attr(data-marpit-pagination) ' / ' attr(data-marpit-pagination-total);
      }
    section.inverted {
        background-color: #3e8ea3;
        color: white;
    }
    section.inverted h1,
    section.inverted h2 {
        color: white;
    }
    section.highlight h1, 
    section.highlight h2, 
    section.highlight p {
        background-color: white;
        display: inline-block;
        padding:.32rem;
    }
    .columns {
        display: grid;
        grid-template-columns: repeat(2, minmax(0, 1fr));
        gap: 1rem;
    }
    /* Add center option for image */
    img[alt~="center"] {
      display: block;
      margin: 0 auto;
    }
    blockquote {
      padding: .3rem;
      border-left: 4px solid #ccc;
      border-radius: 6px;
      position: relative;
      background-color: #f9f9f9;
    }

    /* Base icon style */
    blockquote::before {
      content: "";
      position: absolute;
      left: 1em;
      top: 1.1em;
      width: 1em;
      height: 1em;
      background-repeat: no-repeat;
      background-size: contain;
    }

    /* Note: blue info icon */
    section.note blockquote {
      padding-left: 3rem;
      border-left: 4px solid #0078d4;
      background: #f3f9fd;
    }
    section.note blockquote::before {
      background-image: url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAxNiAxNiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ij48cGF0aCBkPSJNMCA4YTggOCAwIDEgMSAxNiAwQTggOCAwIDAgMSAwIDhabTgtNi41YTYuNSA2LjUgMCAxIDAgMCAxMyA2LjUgNi41IDAgMCAwIDAtMTNaTTYuNSA3Ljc1QS43NS43NSAwIDAgMSA3LjI1IDdoMWEuNzUuNzUgMCAwIDEgLjc1Ljc1djIuNzVoLjI1YS43NS43NSAwIDAgMSAwIDEuNWgtMmEuNzUuNzUgMCAwIDEgMC0xLjVoLjI1di0yaC0uMjVhLjc1Ljc1IDAgMCAxLS43NS0uNzVaTTggNmExIDEgMCAxIDEgMC0yIDEgMSAwIDAgMSAwIDJaIj48L3BhdGg+PC9zdmc+");
    }
    
    /* Tip: green lightbulb */
    section.tip blockquote {
      padding-left: 3rem;
      border-left: 4px solid #107c10;
      background: #f1faf1;
    }
    section.tip blockquote::before {
      background-image: url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAxNiAxNiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ij48cGF0aCBkPSJNOCAxLjVjLTIuMzYzIDAtNCAxLjY5LTQgMy43NSAwIC45ODQuNDI0IDEuNjI1Ljk4NCAyLjMwNGwuMjE0LjI1M2MuMjIzLjI2NC40Ny41NTYuNjczLjg0OC4yODQuNDExLjUzNy44OTYuNjIxIDEuNDlhLjc1Ljc1IDAgMCAxLTEuNDg0LjIxMWMtLjA0LS4yODItLjE2My0uNTQ3LS4zNy0uODQ3YTguNDU2IDguNDU2IDAgMCAwLS41NDItLjY4Yy0uMDg0LS4xLS4xNzMtLjIwNS0uMjY4LS4zMkMzLjIwMSA3Ljc1IDIuNSA2Ljc2NiAyLjUgNS4yNSAyLjUgMi4zMSA0Ljg2MyAwIDggMHM1LjUgMi4zMSA1LjUgNS4yNWMwIDEuNTE2LS43MDEgMi41LTEuMzI4IDMuMjU5LS4wOTUuMTE1LS4xODQuMjItLjI2OC4zMTktLjIwNy4yNDUtLjM4My40NTMtLjU0MS42ODEtLjIwOC4zLS4zMy41NjUtLjM3Ljg0N2EuNzUxLjc1MSAwIDAgMS0xLjQ4NS0uMjEyYy4wODQtLjU5My4zMzctMS4wNzguNjIxLTEuNDg5LjIwMy0uMjkyLjQ1LS41ODQuNjczLS44NDguMDc1LS4wODguMTQ3LS4xNzMuMjEzLS4yNTMuNTYxLS42NzkuOTg1LTEuMzIuOTg1LTIuMzA0IDAtMi4wNi0xLjYzNy0zLjc1LTQtMy43NVpNNS43NSAxMmg0LjVhLjc1Ljc1IDAgMCAxIDAgMS41aC00LjVhLjc1Ljc1IDAgMCAxIDAtMS41Wk02IDE1LjI1YS43NS43NSAwIDAgMSAuNzUtLjc1aDIuNWEuNzUuNzUgMCAwIDEgMCAxLjVoLTIuNWEuNzUuNzUgMCAwIDEtLjc1LS43NVoiPjwvcGF0aD48L3N2Zz4=");
    }
  
    /* Important: purple icon */
    section.important blockquote {
      padding-left: 3rem;
      border-left: 4px solid #8a2be2;
      background: #f6f0fb;
    }
    section.important blockquote::before {
      background-image: url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAxNiAxNiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ij48cGF0aCBkPSJNMCAxLjc1QzAgLjc4NC43ODQgMCAxLjc1IDBoMTIuNUMxNS4yMTYgMCAxNiAuNzg0IDE2IDEuNzV2OS41QTEuNzUgMS43NSAwIDAgMSAxNC4yNSAxM0g4LjA2bC0yLjU3MyAyLjU3M0ExLjQ1OCAxLjQ1OCAwIDAgMSAzIDE0LjU0M1YxM0gxLjc1QTEuNzUgMS43NSAwIDAgMSAwIDExLjI1Wm0xLjc1LS4yNWEuMjUuMjUgMCAwIDAtLjI1LjI1djkuNWMwIC4xMzguMTEyLjI1LjI1LjI1aDJhLjc1Ljc1IDAgMCAxIC43NS43NXYyLjE5bDIuNzItMi43MmEuNzQ5Ljc0OSAwIDAgMSAuNTMtLjIyaDYuNWEuMjUuMjUgMCAwIDAgLjI1LS4yNXYtOS41YS4yNS4yNSAwIDAgMC0uMjUtLjI1Wm03IDIuMjV2Mi41YS43NS43NSAwIDAgMS0xLjUgMHYtMi41YS43NS43NSAwIDAgMSAxLjUgMFpNOSA5YTEgMSAwIDEgMS0yIDAgMSAxIDAgMCAxIDIgMFoiPjwvcGF0aD48L3N2Zz4=");
    }
  
    /* Warning: orange triangle */
    section.warning blockquote {
      padding-left: 3rem;
      border-left-color: #b58900;
      background: #fffbe6;
    }
    section.warning blockquote::before {
      background-image: url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAxNiAxNiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ij48cGF0aCBkPSJNNi40NTcgMS4wNDdjLjY1OS0xLjIzNCAyLjQyNy0xLjIzNCAzLjA4NiAwbDYuMDgyIDExLjM3OEExLjc1IDEuNzUgMCAwIDEgMTQuMDgyIDE1SDEuOTE4YTEuNzUgMS43NSAwIDAgMS0xLjU0My0yLjU3NVptMS43NjMuNzA3YS4yNS4yNSAwIDAgMC0uNDQgMEwxLjY5OCAxMy4xMzJhLjI1LjI1IDAgMCAwIC4yMi4zNjhoMTIuMTY0YS4yNS4yNSAwIDAgMCAuMjItLjM2OFptLjUzIDMuOTk2djIuNWEuNzUuNzUgMCAwIDEtMS41IDB2LTIuNWEuNzUuNzUgMCAwIDEgMS41IDBaTTkgMTFhMSAxIDAgMSAxLTIgMCAxIDEgMCAwIDEgMiAwWiI+PC9wYXRoPjwvc3ZnPg==");
    }
  
    /* Caution: red icon */
    section.caution blockquote {
      padding-left: 3rem;
      border-left-color: #d13438;
      background: #fdf3f4;
    }
    section.caution blockquote::before {
      background-image: url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAxNiAxNiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ij48cGF0aCBkPSJNNC40Ny4yMkEuNzQ5Ljc0OSAwIDAgMSA1IDBoNmMuMTk5IDAgLjM4OS4wNzkuNTMuMjJsNC4yNSA0LjI1Yy4xNDEuMTQuMjIuMzMxLjIyLjUzdjZhLjc0OS43NDkgMCAwIDEtLjIyLjUzbC00LjI1IDQuMjVBLjc0OS43NDkgMCAwIDEgMTEgMTZINWEuNzQ5Ljc0OSAwIDAgMS0uNTMtLjIyTC4yMiAxMS41M0EuNzQ5Ljc0OSAwIDAgMSAwIDExVjVjMC0uMTk5LjA3OS0uMzg5LjIyLS41M1ptLjg0IDEuMjhMMS41IDUuMzF2NS4zOGwzLjgxIDMuODFoNS4zOGwzLjgxLTMuODFWNS4zMUwxMC42OSAxLjVaTTggNGEuNzUuNzUgMCAwIDEgLjc1Ljc1djMuNWEuNzUuNzUgMCAwIDEtMS41IDB2LTMuNUEuNzUuNzUgMCAwIDEgOCA0Wm0wIDhhMSAxIDAgMSAxIDAtMiAxIDEgMCAwIDEgMCAyWiI+PC9wYXRoPjwvc3ZnPg==");
    }
---
  
  
# Administration et gestion des réseaux I
<br/>

## Rappels réseaux

![bg](images/vic20.jpg)

<!-- 
_class: highlight
_footer: ''
_paginate: false
-->

---

![bg w:90%](images/grille-cut.png)

<!--
_paginate: false
_footer: ''
_header: ''
-->

---
![bg](images/reseaux.png)

---

## Modèle TCP/IP

| Couche         | Fonction principale  | Protocoles exemples|
|:---------------|:---------------------|:-------------------|
| Application    | Services réseau      | HTTP, FTP, SMTP, DNS |
| Transport      | Communication de bout en bout  | **TCP**, UDP   |
| Internet | Routage des paquets         | **IP**, ICMP, ARP|
| Network access | Accès physique au média | Ethernet, Wi-Fi, PPP |
<br/>

<!-- class: note -->
> **Remarque :** 
>La couche 2 du modèle TCP/IP est parfois appelée « Internet » ou « Réseau » selon les sources. 


# Adresse IPv4

- Une adresse IPv4 est composée de 4 octets (32 bits), séparés par des points.
- Exemple : `192.168.210.1`
- Chaque octet varie de 0 à 255.
<br/><br/>
```
Exemple :  192 . 168 .  1  . 10
             |     |     |    |
           Octet Octet Octet Octet
```

---
## Notation CIDR

- La notation CIDR (Classless Inter-Domain Routing) permet d'indiquer le nombre de bits utilisés pour le masque de réseau.
- Elle s'écrit sous la forme : `adresse_ip/longueur_du_prefixe`
- Exemple : `192.168.210.1/24` signifie que les 24 premiers bits sont utilisés pour le réseau.

<!-- class: note -->
> **Remarque :**  
> Les anciennes classes d'adresses correspondent aux préfixes : classe A : `/8`, classe B : `/16` et classe C : `/24`

---
## Plages d'adresses IP privées

- **Classe A** : `10.0.0.0` à `10.255.255.255` (`10.0.0.0/8`)
- **Classe B** : `172.16.0.0` à `172.31.255.255` (`172.16.0.0/12`)
- **Classe C** : `192.168.0.0` à `192.168.255.255` (`192.168.0.0/16`)

<!-- class: tip -->
> Ces plages sont réservées pour un usage privé et ne sont pas routables sur Internet.

---

## Pourquoi la plage privée Classe B est en /12 ?

- Historiquement, la **classe B** correspond à des réseaux en `/16` (soit 65 536 adresses par réseau).
- Cependant, la plage privée `172.16.0.0/12` regroupe **plusieurs réseaux de classe B privés** de `172.16.0.0` à `172.31.255.255`.
- Le préfixe `/12` permet d’englober **16 réseaux de classe B** (de `172.16.0.0/16` à `172.31.0.0/16`) dans une seule plage privée.
- Cela offre une grande flexibilité pour créer de nombreux sous-réseaux privés.

<!-- class: note -->
> **En résumé :**  
> La notation `/12` pour la plage privée permet de couvrir tous les réseaux privés de classe B, et pas seulement un seul réseau en `/16`.

## Pourquoi la plage privée Classe C est en /16 ?

- Historiquement, la **classe C** correspond à des réseaux en `/24` (soit 256 adresses par réseau).
- Cependant, la plage privée `192.168.0.0/16` regroupe **tous les réseaux de classe C privés** de `192.168.0.0` à `192.168.255.255`.
- Cela permet d'utiliser **plusieurs réseaux privés** (256 réseaux en `/24`) dans la plage réservée, et non un seul réseau.

<!-- class: note -->
> **En résumé :**  
> La notation `/16` pour la plage privée signifie qu'elle englobe tous les réseaux de classe C privés, chacun pouvant être subdivisé en `/24` selon les besoins.

---
## Protocole ARP (Address Resolution Protocol)

- **ARP** permet de trouver l'adresse MAC associée à une adresse IP sur un réseau local.
- Fonctionnement :
    - Un hôte envoie une requête ARP pour connaître l'adresse MAC correspondant à une IP.
    - L'appareil possédant cette IP répond avec son adresse MAC.
- ARP est utilisé principalement dans les réseaux Ethernet (IPv4).

<!-- class: important -->
> ARP est essentiel pour la communication sur les réseaux locaux, car les paquets doivent être adressés à une adresse MAC pour être transmis physiquement.




# Adresse IPv6

- Une adresse IPv6 est composée de **128 bits** (16 octets).
- Elle s'écrit en **8 groupes** de 4 chiffres hexadécimaux, séparés par des deux-points `:`.
- Exemple :  
    `2001:0db8:85a3:0000:0000:8a2e:0370:7334`
<br/><br/>

```
Exemple :  2001 : 0db8 : 85a3 : 0000 : 0000 : 8a2e : 0370 : 7334
                         |      |      |      |      |      |      |      |
                     Groupe Groupe Groupe Groupe Groupe Groupe Groupe Groupe
```

---

## Règles de simplification IPv6

- Les zéros initiaux d’un groupe peuvent être omis :  
    `2001:db8:85a3:0:0:8a2e:370:7334`
- Une suite de groupes de zéros peut être remplacée par `::` (une seule fois par adresse) :  
    `2001:db8:85a3::8a2e:370:7334`
<br/><br/>

<!-- class: tip -->
> La notation `::` permet de raccourcir les adresses IPv6 comportant plusieurs groupes de zéros consécutifs.

---

## Types d'adresses IPv6

- **Unicast** : Identifie une seule interface.
- **Multicast** : Identifie un groupe d'interfaces.
- **Anycast** : Identifie un groupe d'interfaces, le paquet est délivré à la plus proche.
<br/><br/>

<!-- class: note -->
> Les adresses IPv6 privées commencent par `fd00::/8` (Unique Local Address).

# Quelques commandes 

<!-- _class: inverted-->

---

## Commande `ping`

Teste la connectivité réseau avec une adresse IP ou un nom de domaine.
<br/><br/>

```bash
$ ping 9.9.9.9
PING 9.9.9.9 (9.9.9.9) 56(84) bytes of data.
64 bytes from 9.9.9.9: icmp_seq=1 ttl=56 time=20.3 ms
```

---
## Commande `ip`

La commande `ip` est devenue la commande « à tout faire » et remplace `ifconfig`, `route`…

---
## Commande `ip address`

Affiche les interfaces réseau et leurs adresses IP.

```sh
ip address
ip a
```

Exemple de sortie :
```
3: wlp4s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 14:ab:c5:dd:83:08 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.59/24 brd 192.168.1.255 scope global dynamic noprefixroute wlp4s0
       valid_lft 2463sec preferred_lft 2463sec
    inet6 2a02:a03f:c57c:c600:6b17:9df5:3e67:91e4/64 scope global dynamic noprefixroute 
       valid_lft 73192sec preferred_lft 58792sec
    inet6 fd08:7685:d11:0:1232:f098:50aa:455a/64 scope global noprefixroute 
       valid_lft forever preferred_lft forever
```

---
## Commande `ip address`

Donne une adresse à une interface.

```sh
ip address add 192.168.1.10/24 dev eth0
```

---
## Commande `ip route`

Affiche la table de routage IP.

```sh
ip route
```

Exemple de sortie :
```
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.10
```

---
## Commande `ip route`

Ajoute une route vers un sous-réseau.

```sh
ip route add 192.168.2.0/24 via 192.168.1.1 dev eth0
```

- Cette commande indique que pour atteindre le réseau `192.168.2.0/24`, il faut passer par la passerelle `192.168.1.1` via l'interface `eth0`.

---
## Commande `ip neigh`

Affiche la table ARP (voisins connus sur le réseau local).

```sh
ip neigh
```

Exemple de sortie :
```
192.168.1.1 dev eth0 lladdr 00:11:22:33:44:55 REACHABLE
```

---

## Commande `netstat`

Affiche les connexions réseau, les tables de routage, etc.

```sh
netstat -tuln
```
- `-t` : affiche les connexions TCP
- `-u` : affiche les connexions UDP
- `-l` : affiche uniquement les sockets en écoute (listening)
- `-n` : affiche sous forme numérique (pas de résolution DNS)

> **Remarque :**  
> Il existe d'autres combinaisons d'options (et des moyens mnémotechniques pour les retenir)


---
## Commande `dig`

Interroge le DNS pour obtenir des informations sur un nom de domaine.

```sh
dig esi-bru.be
```
<br>

Exemple de sortie (extrait) :
```
;; ANSWER SECTION:
esi-bru.be.             10800   IN      A       178.32.5.10
```
<br/>

<!-- class: note-->
> Cette commande sera vue en détail dans la section consacrée au DNS.









---
pom

---
pom
