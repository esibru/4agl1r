---
marp: true
headingDivider: 1
paginate: true
footer: 'Pierre Bettens _pbt_'  
header: 'LDAP'
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
    .columns30 {
        display: grid;
        grid-template-columns: 30% 70%;
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

# LDAP  
<br/>

![bg](images/common_grass_yellow_070712_by_inckurei-d56ffl1.jpg)

## Lightweight Directory Access Protocol

<!-- 
_class: highlight
_footer: ''
_paginate: false
-->

---
## LDAP 

_Protocole d'accès à un annuaire_
<br/>

Base de données spécialisée avec une structure forte… 

… tout ce qui peut être nommé


# Un annuaire n'est pas un SGBD
<!-- 
_class: inverted 
_footer: ''
_paginate: false
-->

---
## LDAP fournit

- Protocole d'accès
- Modèle d'informations
- Conventions de nommage
- Modèle fonctionnel, de sécurité et de duplication
- API
- LDIF

---
![bg](images/yellow_world_by_Dieffi_1200.jpg)

<!-- 
_class: highlight 
_header: ''
_footer: ''
_paginate: ''
-->

---
## Modèle de données 

Structure en arbre

![w:300](images/nounproject-tree.png)

- Un nœud = une entrée
- Un nœud = un objet
<br/>
<br/>

<!-- class: tip -->
> La racine contient la description de l'arbre (_rootDSE_)

<style scoped>
    img {
        position: absolute;
        top: 200px;
        right: 50px;
    }

</style>
---
## Modèle de données 

`objectClass` (classe d'objet)

- **nom**
- **objectID**
- **attributs** : obligatoires (_MUST_) / optionnels (_MAY_)
- **type** : structurel | abstrait | auxiliaire

Un attribut a : un nom, un OID, une syntaxe et un format de valeur

---
## Modèle de données 

`objectID`

Normalisé (RFC2256), hiérarchie – héritage

- `2.5` (X.500)
- `1.3.6.1.4.1.4203` (OpenLDAP)
- `1.3.6.1.4.1.23162` (ESI)

---
## Modèle de données 

Exemple `objectClass : inetOrgPerson`


```
objectclass ( 2.16.840.1.113730.3.2.2
  NAME 'inetOrgPerson'
  DESC 'RFC2798: Internet Organizational Person'
  SUP organizationalPerson
  STRUCTURAL
  MAY (
    audio $ businessCategory $ carLicense $
    departmentNumber $ displayName $ employeeNumber
    $ employeeType $ givenName $ homePhone $
    homePostalAddress $ initials $ jpegPhoto $ … )
)
```
Extrait de `/etc/ldap/schema/inetorgperson.schema`

---
## Modèle de données 

Exemple `objectclass` et `attributetype`


```
objectclass ( 2.5.6.6 NAME 'person'
  DESC 'RFC2256: a person'
  SUP top STRUCTURAL
  MUST ( sn $ cn )
  MAY ( userPassword $ telephoneNumber 
    $ seeAlso $ description ) )
```

```
attributetype ( 2.5.4.4 NAME ( 'sn' 'surname' )
  DESC 'RFC2256: last (family) name(s) for which
        the entity is known by'
  SUP name )
```
Extraits de `/etc/ldap/schema/core.schema`

---
## Modèle de données 

_Schema checking_

Lorsque l'on insère une entrée, le serveur vérifie si la syntaxe est conforme
→ **schema checking**

![bg right:35%](images/Femme_Loupe.jpg)
<!--
_paginate: false
-->

---
## Modèle de données 

_Distinguished Name_ `DN`

Chaque nœud a un **identifiant unique** composé des attributs obligatoires
<br/>

**DN** = _distinguished name_

```
uid=fpignon, ou=construction, dc=example, dc=org
```

# LDIF 
### LDAP Data Interchange Format

<!-- 
_class: inverted 
_paginate: false
_footer: ''
-->

---

## LDIF

**LDAP Data Interchange Format**

Format de représentation des données

- Import / Export
- Modifications

---

## LDIF 

Représentation des données

```ldif
dn: cn=Marlene Sassœur,ou=student,dc=example,dc=be
objectclass: inetOrgPerson
cn: Marlene SASSOEUR
sn: Marlene
mail: marlene.sassoeur@dev.null
description: Elle me dit c'est Marlène sa soeur.
 Avouez que c'est confusant.
```

---
## LDIF

Ajout, suppression de données

```ldif
dn: cn=Marlene Sassœur,ou=student,dc=example,dc=be
changetype: modify
add: telephonenumber
telephonenumber: 123 45 67 89
```

```ldif
dn: cn=Marlene Sassœur,ou=student,dc=example,dc=be
changetype: delete
```

# Modèle fonctionnel

<!-- 
_class: inverted 
_paginate: false
_footer: ''
-->

---

## Portée de la recherche (search scope)

- **base** – l'entrée elle-même
- **onelevel** – les enfants directs
- **subtree** – toute la sous-arborescence

# LDAP et TLS

<!-- _class: inverted -->

---

## LDAP-TLS 

**Pourquoi sécuriser LDAP ?**

Par défaut, LDAP transmet **en clair** :

- Les requêtes de recherche
- Les données retournées
- **Les mots de passe** lors du `bind`

→ Faille de sécurité majeure !

---

## LDAP-TLS 
<br/>

| Méthode | Port | Description |
|---------|------|-------------|
| **LDAPS** | 636 | TLS dès la connexion <br/>Initiation d'une connexion TLS sur un autre port (comme HTTPS) |
| **StartTLS** | 389 | Upgrade en TLS<br/>Prénégotiation d'une connexion TLS (StartTLS) sur le port standard |

---

## LDAP-TLS

**Configuration TLS (serveur)**

Après la création de certificats (CA, certificat serveur et clé publique), exemple de configuration

```ldif
dn: cn=config
changetype: modify
add: olcTLSCACertificateFile
olcTLSCACertificateFile: /etc/ldap/tls/ca.crt
-
add: olcTLSCertificateFile
olcTLSCertificateFile: /etc/ldap/tls/server.crt
-
add: olcTLSCertificateKeyFile
olcTLSCertificateKeyFile: /etc/ldap/tls/server.key
```

---

## LDAP-TLS

**Configuration LDAPS (port 636)**

Pour activer LDAPS, modifier `/etc/default/slapd` :

```bash
SLAPD_SERVICES="ldap:/// ldaps:/// ldapi:///"
```

Puis redémarrer le service :

```bash
systemctl restart slapd
```
<br/>

<!-- class: note -->
> **Remargue**
> LDAPS nécessite la configuration TLS préalable (certificats)


---

**Tests connexion sécurisée**

**StartTLS** (port 389)

```bash
ldapsearch -ZZ -H ldap://server -x \
    -b "dc=example,dc=org" "(objectclass=*)"
```
- `-ZZ` pour initier StartTLS

**LDAPS** (port 636)

```bash
ldapsearch -H ldaps://server -x \
    -b "dc=example,dc=org" "(objectclass=*)"
```
- `ldaps` pour se connecter sur le port dédié `636`


# OpenLDAP
![bg](images/books.png)
<!-- 
_class: highlight 
_footer: ''
_paginate: false
-->

---

## OpenLDAP

Implémentation libre de LDAP

http://openldap.org

- **package** : `slapd`, `ldap-utils`
- **dæmons** : `slapd`, `slurpd`

---
## OpenLDAP

Configuration OpenLDAP

- Choix des schémas
- `/etc/ldap/slapd.d`
- Utilitaires `ldapfoo`

---
## Serveurs

- OpenLDAP
- Microsoft Active Directory
- Netscape Directory Server

---

## Clients

- Browsers
- MS Windows
- PAM LDAP
- API (Perl, Java, …)
- Samba

---
## Références

- [IANA enterprise numbers](https://www.iana.org/assignments/enterprise-numbers/enterprise-numbers)
- [OpenLDAP QuickStart](https://www.openldap.org/doc/admin24/quickstart.html)
- [LinuxMag (vieil) article mongueurs](http://articles.mongueurs.net/magazines/linuxmag65.html)


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