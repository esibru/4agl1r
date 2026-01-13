---
marp: true
headingDivider: 1
paginate: true
footer: 'Pierre Bettens _pbt_'  
header: 'DHCP'
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
    section.inverted-orange a,
    section.inverted-orange h1,
    section.inverted-orange h2 {
      color: white;
    }
    section.inverted-orange {
      background-color:rgb(217, 124, 30);
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

# DHCP

![bg](images/Green-Frog-umbrella-leaf-hiding-from-rain.jpg)

<!-- 
_class: highlight
_footer: ''
_paginate: false
-->


# Atelier de recherche

**Que fait cette commande `dhclient -v`** 
**Expliquer.**

<!--
_class: inverted-orange
-->

# DHCP - Exemple d'exécution

```bash
root@harmony:~# dhclient -v
Internet Systems Consortium DHCP Client 4.4.3-P1
Copyright 2004-2022 Internet Systems Consortium.
All rights reserved.
For info, please visit https://www.isc.org/software/dhcp/

Listening on LPF/enp1s0/52:54:00:68:79:20
Sending on   LPF/enp1s0/52:54:00:68:79:20
Sending on   Socket/fallback
DHCPDISCOVER on enp1s0 to 255.255.255.255 port 67 interval 4
DHCPOFFER of 10.1.0.23 from 10.0.0.1
DHCPREQUEST for 10.1.0.23 on enp1s0 to 255.255.255.255 port 67
DHCPACK of 10.1.0.23 from 10.0.0.1
bound to 10.1.0.23 -- renewal in 41659 seconds.
```

# DHCP - Définition

**DHCP** (_Dynamic Host Configuration Protocol_)

- Mécanisme d'allocation d'adresse IP
- Livraison de paramètres de configuration

**Protocole UDP**
- Port 67 (client → serveur)
- Port 68 (serveur → client)

<br/>

Références : [RFC 2131](https://www.rfc-editor.org/rfc/rfc2131), [RFC 3203](https://www.rfc-editor.org/rfc/rfc3203)

# DHCP - Mécanismes d'allocation

**3 mécanismes :**

- allocation **automatique**
  - IP dans le _pool_ permanente
  
- allocation **dynamique**
  - IP dans le *pool* pour une certaine durée
  
- allocation **manuelle**
  - IP fixe

<!-- class: tip -->
> Une IP est attribuée pour une certaine durée : un bail (*lease*)
> 

# DHCP - Avantages et Inconvénients

**Avantages**
- Configuration fiable
- Empêche / évite les conflits d'IP
- Configuration centralisée
  - Si la passerelle change, la configuration se *propagera*
- Facilité de gestion des périphériques itinérants

**Inconvénient**
- Se fait par *broadcast*

# Fonctionnement

<!-- 
_class: inverted
-->

# DHCP - Processus d'attribution

<style scoped>
.columns {
  display: grid;
  grid-template-columns: 30% 70%;
  gap: 1rem;
}
</style>
<div class="columns">
<div>

![w:270px](images/dhcp-rfc-1.png)

</div>
<div>

- `DHCP DISCOVER`
    - recherche d'un serveur (_broadcast_)
- `DHCP OFFER`
    - les serveurs répondent en proposant une IP (+ options éventuelles ; masque, passerelle…)
- `DHCP REQUEST`
    - après avoir choisi, le client envoie son paquet (à **tous** les serveurs)
- `DHCP ACK`
    - le serveur envoie un `ACK` (ou un `NACK`) pour valider la demande

</div></div>


# Quels sont les autres *DHCP messages* ?

(Voir RFC)

<!--
_class: inverted 
-->

# DHCP - Renouvellement de bail

<style scoped>
.columns {
  display: grid;
  grid-template-columns: 30% 70%;
  gap: 1rem;
}
</style>
<div class="columns">
<div>

![w:320](images/dhcp-rfc-2.png)

</div>
<div>

Pour la réattribution d'une adresse (en fin de *lease* par exemple), le client envoie directement un paquet `DHCPREQUEST`

<br/>

<!-- class: tip -->
> **Remarque :** Si l'IP est encore utilisée, la demande est envoyée en *unicast* (et pas *broadcast*)

</div></div>


# BOOTP Relay Agent

_Un serveur DHCP ne peut servir qu'un seul segment IP_

- Les requêtes DHCP utilisent le broadcast UDP
- Un agent intermédiaire peut relayer les requêtes DHCP (_broadcast_ vers _unicast_)
<br/>

<!-- class: note -->
> Le Relay Agent ajoute son adresse IP dans le champ `giaddr` (Gateway IP Address)


# BOOTP vs BOOTP Relay Agent

<!-- class: warning -->
> Ne pas confondre BOOTP et BOOTP relay agent
<br/>

<br/>
<div class="columns">
<div>

**BOOTP (Bootstrap Protocol)**
- Protocole original pour l'attribution d'adresses IP (ancêtre, _legacy_)
- Allocation statique uniquement (pas de pool dynamique)
- [RFC 951](www.rfc-editor.org/rfc/rfc951.html)

</div><div>

**BOOTP Relay Agent**
- Mécanisme de relais pour BOOTP et DHCP
- Permet de traverser les routeurs
- [RFC 1542](www.rfc-editor.org/rfc/rfc1542.html)


</div></div>

# Configuration

**Routeur Cisco**

```cisco
ip helper-address 10.0.0.10
```

<!-- class: tip -->
> `ip helper-address` redirige automatiquement les broadcasts DHCP, TFTP, DNS, etc.

<br/>
<br/>

**Linux**
Le paquet `isc-dhcp-relay` (`dhcrelay`) ou le paquet `dhcp-helper`. 


# Atelier de recherche

**Capturer les trames DHCP via Wireshark et déduire le format des trames.**

<br/>
<br/>
<br/>

Le filtre « qui va bien » :
```
udp.port == 67 || udp.port == 68
```
<!-- 
_class: inverted-orange
-->

---
![bg w:70%](images/screenshot-wireshark-dhcp-1.png)

<!--
_header: ''
_footer: ''
_paginate: false 
-->

---
![bg w:70%](images/screenshot-wireshark-dhcp-2.png)

<!--
_header: ''
_footer: ''
_paginate: false 
-->

---
![bg w:70%](images/screenshot-wireshark-dhcp-3.png)

<!--
_header: ''
_footer: ''
_paginate: false 
-->

---
![bg w:70%](images/screenshot-wireshark-dhcp-4.png)

<!--
_header: ''
_footer: ''
_paginate: false 
-->


# isc-dhcp-server
<br/>
<br/>
<br/>

Depuis 2022, l'ISC (_Internet Software Consortium_) recommande **Kea DHCP** (voir plus loin) au lieu de **ISC DHCP**.

<!--
_class: inverted
-->

---
## isc-dhcp-server

`isc-dhcp-server` est un serveur DHCP proposé par l'ISC.

- installation
    ```bash
    apt install isc-dhcp-server
    ```

- configuration

<small><small><small>

```bash
> tree /etc/dhcp
.
├── …
├── debug
├── dhclient.conf
├── dhclient-enter-hooks.d
│   └── …
├── dhclient-exit-hooks.d
│   └── …
├── dhcpd6.conf
└── dhcpd.conf
```

</small></small></small>

---
## isc-dhcp-server 

- préciser dans `/etc/default/isc-dhcp-server` les interfaces sur lesquelles le serveur écoute.

- quelques éléments de configuration (extrait de `dhcpd.conf`)

    ```bash
    option domain-name "example.org";
    option domain-name-servers ns.example.org;
    default-lease-time 86400;
    max-lease-time 604800;
    ```

---
## isc-dhcp-server 

**Attribution automatique d'une adresse dans un certain range**

```conf
subnet 10.0.0.0 netmask 255.0.0.0 {                                               
  range 10.1.0.0 10.1.0.255;  
  option domain-name-servers ns.example.org;
  option domain-name "example.org";
  option subnet-mask 255.0.0.0;                                                   
  option broadcast-address 10.255.255.255;                                        
  option routers 10.0.0.1;                                                        
}  
```

---
## isc-dhcp-server 

**Attribution d'une adresse en fonction de l'adresse MAC** (et envoi du nom de la machine)

```conf
subnet 192.168.192.0 netmask 255.255.192.0 {                                     
    option routers 192.168.192.1;
    option domain-name "example.org";
    option domain-name-servers 192.168.210.1; 
}

host harmony {   
    option host-name harmony;
    hardware ethernet 00:1b:21:[cut];
    fixed-address 192.168.210.2; 
}
```

# DHCP et DNS
**Mise à jour du DNS après attribution d'une IP**
<!--
_class: inverted
-->

---
## DHCP et DNS
<!-- class: info -->
> installation de DDNS (**_dynamic DNS_**) pour la mise à jour automatique de la zone DNS lors de l'octroi d'un *lease* par le server DHCP.

**Rapide procédure :**

1. Création d'une clé pour la communication entre DNS et DHCP et copie dans les répertoires `/etc/bind9` et `/etc/dhcp` pour *bind* et *dhcp*

    ```bash
    dnssec-keygen -a RSASHA512 -b 2048 DDNS_UPDATE
    ```


---
2. Copie de la clé dans un fichier `ddns.key` et copie du fichier aux *endroits qui vont bien*

    ```sh
    > vim ddns.key

    key DDNS_UPDATE {
        algorithm RSASHA512.SIG-ALG.REG.INT;
        secret "r9Fx--cut--tuw==";
    };

    > install -o root -g bind -m 0640 ddns.key /etc/bind/ddns.key
    > install -o root -g root -m 0640 ddns.key /etc/dhcp/ddns.key
    ```

---
3. Configuration de bind9, ajout de la zone

    ```sh
    > vim /etc/bind/named.conf.local

    include "/etc/bind/ddns.key";

    zone "example.org" {
        type master;
        notify no;
        file "/var/cache/bind/db.example.org";
        allow-update { key DDNS_UPDATE; };
    };

    zone "10.in-addr.arpa" {
        // idem
    };
    ```

---
4. Configuration de bind9, création du fichier de zone

    ```sh
    # vim /etc/bind/db.example.org

    ; Zone file 
    ;
    $TTL	86400
    @	IN	SOA	example.org. root.example.org. (
        1970010100 7d 2h 42d 3h);

    @	IN	NS	ns.example.org.
    pica	IN	A	10.0.0.1
    ns		IN	CNAME	pica 

    ; "below" update via dhcp
    ```

    *idem* pour la zone *reverse* *db.10*

---
5. mise à jour de `dhcpd.conf` pour que DHCP fasse les *updates* auprès du DNS

    ```sh
    > vim /etc/dhcpd.conf

    ddns-updates on;
    ddns-update-style interim;
    ignore client-updates;

    include "/etc/dhcp/ddns.key";

    zone example.org. {
        primary 127.0.0.1;
        key DDNS_UPDATE;
    }

    zone 10.in-addr.arpa. {
        // idem
    }
    ```

# Kea DHCP
<br/>
<br/>

successeur de `isc-dhcp-server`
<!--
_class: inverted
-->

---
## Kea DHCP

Quelles sont les différences avec _ISC DHCP_ ?

- modularité : Kea est séparé en 3 daemons ; **DHCPv4 server**, **DHCPv6 server** et **dynamic DNS (DDNS)** module (avec les paquets correspondants `kea-dhcp4-server`, `kea-dhcp6-server` et `kea-dhcp-ddns-server`) auxquels peuvent s'ajouter d'autres modules (par ex. pour la HA (_high availability_));

- configuration _via_ un fichier **JSON** et API REST pour la reconfiguration _à chaud_;

- Kea permet l'utilisation d'un **_backend_** (MySQL, PostgreSQL) pour stocker les données du réseau (_leases_, définition de réservations des hôtes…)
    - un _backend_ partagé par plusieurs instances de Kea

---

- **Stork**, _dashboard graphique_ (peut monitorer plusieurs serveurs)

    ![](images/stork-dashboard.png)

---
- implémentation moderne (_pub inside_)
    - multi-threads
    - performant à grande échelle (beaucoup de machines, _leases_ courts)

---
## Kea DHCP - Configuration 

JSON est utilisé pour la **configuration** et pour l'**API**.  

```json
{
    "Dhcp4": {
        "interfaces-config": {
            "interfaces": [ "eth0" ],
            "dhcp-socket-type": "raw"
        },
        "valid-lifetime": 4000,
        "renew-timer": 1000,
        "rebind-timer": 2000,
    }
}
```


---
Spécifier _lease database_ (ici un fichier plat)

```json
{
    "Dhcp4": {
        # [cut]

        "lease-database": {
            "type": "memfile",
            "persist": true,
            "name": "/var/lib/kea/dhcp4.leases"
        },

    }
}
```

---
Définir le _pool_

```json
{
    "Dhcp4": {
        # [cut]

        "subnet4": [{
            "subnet": "10.1.0.0/8",
            "pools": [ { "pool": "10.1.0.0-10.1.255.255"} ],
            "id": 1
        }]
    }
}
```

---
Faire de la réservations d'hôte

```json
{
    "Dhcp4": {
        # [cut]
        "subnet4": [{
            "subnet": "10.1.0.0/8",
            "pools": [ { "pool": "10.1.0.0-10.1.255.255"} ],
            "id": 1,
            "reservations": [{
                "hw-address": "1a:1b:1c:1d:1e:1f",
                "ip-address": "10.0.0.2",
                "hostname": "harmony"
            },{
                # other host
            }]
        }]
    }
}
```

---
Dans la configuration, possibilité de configurer les _loggers_

```json
{
    "Dhcp4": {
        # [cut]

        "loggers": [{
            "name": "*",
            "severity": "DEBUG"
        }]
    }
}
```

---
Le serveur DHCP peut envoyer des options comme des serveurs DNS

```json
{
    "Dhcp4": {
        # [cut]

        "option-data": [{
            "name": "domain-name-servers",
            "data": "10.0.0.1, 8.8.8.8"
        }]
    }
}
```

---
Les paramètres sont semblables pour le serveur DHCPv6 qui a une section propre

```json
{
    "Dhcp6": {
        # idem

        "subnet6": [
            # …
        ]
    }
}
```

ainsi que le serveur DDNS

```json
{
    "DhcpDdns": {
        # …
    }
}
```




---
Slides dans le cadre de mes cours.
<span class="square"></span>

### Qui suis-je ? 
Pierre Bettens (_pbt_)  
[blog.namok.be](https://blog.namok.be)
pbettens@he2b.be · bettensp@helha.be

### Crédits
GNU linux, _markdown_, Codium, Marpit

Licence WTFL

<style scoped>
    section {text-align: center;}
    .square {
        margin: 15px auto;
        display: block;
        width: 150px;
        height: 150px;
        cursor: pointer;
        background-color: peru;
    }
</style>