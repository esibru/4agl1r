---
marp: true
headingDivider: 1
paginate: true
footer: 'Pierre Bettens _pbt_'  
header: 'HTTP[s]'
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

# HTTP[s] - Hyper Text Transfert Protocol 
## Apache2 ~ nginx ~ caddyserver

![bg](images/indienne.jpg)

<!--
_class: highlight
_footer: ''
_paginate: false
-->

# HTTP

C'est **le** protocole du WEB¹

- Sur TCP
- Port 80 (par défaut)
- 1990 v0.9, 1996 v1.0

<br/>

[RFC 9110](https://www.rfc-editor.org/rfc/rfc9110.html)

<br/><small>
¹ Du **WEB** (_World Wide Web_), pas de l'**Internet**
</small>

---
## HTTP

```http
$ nc -C localhost 80
GET / HTTP/1.1
host: localhost
```
<small>
Réponse…

```http
HTTP/1.1 200 OK
Date: Wed, 01 Mar 2023 11:02:18 GMT
Server: Apache/2.4.54 (Debian)
Last-Modified: Mon, 20 Jan 2020 09:21:02 GMT
ETag: "44-59c8ecf63ee1e"
Accept-Ranges: bytes
Content-Length: 68
Content-Type: text/html

<h1>Think about</h1>
<p>There are no failures, only lessons.</p>
```
</small>

---
## HTTP

```http
$ nc -C example.org 80
GET / HTTP/1.1
host: example.org
```
<small><small><small>

Extrait…
```http
HTTP/1.1 200 OK
Age: 541560
Cache-Control: max-age=604800
Content-Type: text/html; charset=UTF-8
Date: Wed, 01 Mar 2023 11:33:27 GMT
(cut)

<!doctype html>
(cut)
<div>
    <h1>Example Domain</h1>
    <p>This domain is for use [cut]<p>
    <p><a href="https://www.iana.org/domains/example">More information...</a></p>
</div>
</body>
</html>
```
</small>
</small>
</small>

---
## HTTP

`curl` permet aussi d'exécuter simplement une requête http. 

```http
$ curl -v example.org
```

Extrait… 

```http
*   Trying 93.184.216 34:80... 
* Connected to example.org (93.184.216.34) port 80 (#0)
> GET / HTTP/1.1  
> Host: example.org 
> User-Agent: curl/7.88.1 
> Accept: */*
>                                 
< HTTP/1.1 200 OK
< Age: 601738    
< Cache-Control: max-age=604800
[cut]
```

---
## HTTP

Structure de la requête `HTTP`


>GET / HTTP/1.1\\
>host: example.org

- `GET`, la méthode
- `/`, la page demandée
- `HTTp/1.1`, le protocole
- `host: example.org`, précise le nom du site (cfr. _vhost_)
<br/>

À partir de la deuxième ligne, `field-name: token`

---
## HTTP

Les **méthodes**:

![w:700](images/http-method.png)

<small>

Extrait de rfc-editor.org
</small>

---
## HTTP

Les **entêtes**. 

L'entête `host`

```bash
host: example.org
```

- précise quel est le nom de l'hôte 
- obligatoire 
- permet de distinguer les ressources lorsque le serveur gère plusieurs hôtes virtuels (_vhosts_)

---
## HTTP

Il existe beaucoup d'autres entêtes de requête (_request context fields_), par exemple

- `referer: <value>`, URI de la ressource d'origine
- `user-agent: <value>`, identifie le client
- `accept-charset: <value>`, jeu de caractères accepté
- …

… et des entêtes de réponse (_response context fields_)

- `server: <value>`, le type de serveur HTTP
- `content-type: <value>`, le type de document échangé
- …


---

> Les **entêtes HTTP** contribuent à l'identification unique des navigateurs (_browser fingerprinting_).
<!-- _class: warning -->

Entêtes utilisés pour le fingerprinting :
<small><small>

- `User-Agent`: identifie le navigateur et le système d'exploitation
- `Accept-Language`: langue(s) préférée(s)
- `Accept-Encoding`: méthodes de compression supportées
- `Accept`: types MIME acceptés
- `DNT` (_Do Not Track_): préférence de pistage
</small>

Combinés avec d'autres données (résolution d'écran, plugins, canvas fingerprinting…), ces entêtes permettent de créer une **empreinte digitale unique** qui persiste même après suppression des cookies.

**Outil de test** : <https://coveryourtracks.eff.org/>
</small>


---
## HTTP

La **réponse** `HTTP` est constituée de _context fields_ et commence par un **code de retour** (_status code_). 


Extrait d'une réponse
```http
HTTP/1.1 200 OK
Date: Wed, 01 Mar 2023 11:02:18 GMT
Server: Apache/2.4.54 (Debian)
```
<br/>

>**Statut 200**
>OK Standard response for succesful HTTP requests


---
## HTTP

Les _status code_ sont catégorisés, le premier chiffre décrit le type de réponse; succès, erreur…

Il y a 5 catégories :

- `1xx` (Informational): The request was received, continuing process
- `2xx` (Successful): The request was successfully received, understood, and accepted 
- `3xx` (Redirection): Further action needs to be taken in order to complete the request 
- `4xx` (Client Error): The request contains bad syntax or cannot be fulfilled 
- `5xx` (Server Error): The server failed to fulfill an apparently valid request

---
## HTTP

Quelques codes de retour (_status code_) fréquents :

- `200` OK
- `301` _Move permanently_
- `307` _Temporary redirect_
- `403` _Forbidden_
- `404` _Not found_
- `500` _Internal server error_
- `502` _Bad gateway_
<br/>

Know your HTTP [[pdf](https://github.com/bigcompany/know-your-http)]

---
## HTTP - Cache

HTTP fournit un mécanisme de **cache**; des messages de réponses HTTP peuvent être sauvegardés par le navigateur (_private_) ou un proxy (_public_) sous certaines conditions. 

`Cache-Control` est un en-tête HTTP qui dicte le comportement de mise en cache du navigateur.
<br/>

Exemple

```http
Cache-Control: public, max-age=604800
```

---
Quelques entêtes :

- `max-age=[secondes]` — indique la quantité de temps maximale où la représentation sera considérée fraîche
- `s-maxage=[secondes]` — similaire à `max-age`, sauf qu'elle ne s'applique qu'aux caches partagés (_proxy_)
- `public` — marque les réponses authentifiées comme cachables
- `no-cache` — force à chaque fois les caches à soumettre la requête au serveur original
- `no-store` — instruit les caches de ne pas garder de copie de la représentation dans toutes les conditions
- …

---
Références

- <https://fr.wikipedia.org/wiki/Cache-Control>
- <https://developer.mozilla.org/fr/docs/Web/HTTP/Caching>
- [Whats the best way to set the cache control header](https://medium.com/@oahehc/whats-the-best-way-to-set-the-cache-control-header-4fdae94da054)


---
### Exercice
Une page html, un serveur… illustrer la gestion du cache \textit{via} son navigateur. 

<!--
_class: inverted-orange
-->

---
## HTTP - Cookie

Un cookie HTTP est une donnée de petite taille envoyée par le serveur au navigateur web de l'utilisatrice ou de l'utilisateur. 

Le navigateur peut alors enregistrer le cookie et le renvoyer au serveur lors des requêtes ultérieures.

Les cookies ont trois usages principaux :

- La gestion de session
- La personnalisation
- Le pistage

---

> Remarque
> Les cookies sont actuellement « remplacés » par _localstorage_, _sessionstorage_ et _IndexedDB_. 
<!-- class: tip -->
<br/>
<br/>

Cfr. <https://developer.mozilla.org/fr/docs/Web/HTTP/Cookies>

---
## HTTP - Envoi d'un formulaire

Envoi d'un formulaire

![w:600](images/http-form.png)

---
![bg contain](images/http-wireshark-form.png)
<!--
_paginate: false
_footer: ''
_header: ''
-->


# HTTP…s
![bg](images/lock_by_eva_isabella_d35x8po.jpg)
<!--
_class: highlight
_footer: ''
_paginate: false
-->

---
## HTTPS

**Qu'est-ce que HTTPS ?**

![w:300](images/http-s.jpg)

`HTTPS`, c'est `HTTP` encapsulé dans `TLS`.  

- Sur TCP encapsulé dans TLS
- Port 443 (par défaut)

---
## HTTPS

— La connection est sécurisée. 
— OK, mais quelle **confiance** ? 
<br/>

- confiance dans le protocole (TLS)
- confiance dans le navigateur (Firefox, Chrome, Edge, Netscape…)
- confiance dans l'autorité de certification (CA)

--- 
## HTTPS

> HTTPS ne fournit pas **que** le chiffrement
> HTTPS fournit 
> - **confidentialité**: le trafic est chiffré (TLS)
> - **intégrité**: les données recçues n'ont pas été altérations
> - **authentification**: preuve cryptographique que l’on parle bien au détenteur du certificat pour ce nom de domaine (chaîne de confiance CA).

---
## HTTPS

Fonctionnement

1. Le client envoie une demande de connexion HTTPS au serveur.
	- Il présente les méthodes de chiffrement qu'il connait.
2. Le serveur répond en envoyant son **certificat** SSL/TLS au client après avoir choisi une des méthodes de chiffrement.
3. Le client vérifie la validité du certificat SSL/TLS en vérifiant l'**autorité de certification** (CA) qui l'a émis.
4. Si le certificat est valide, le client et le serveur établissent une connexion sécurisée.
<small><small>

[Navigateurs et validation de certificats](https://www.ssl.com/fr/article/navigateurs-et-validation-de-certificat/)  
[Qu'est-ce qu'une autorité de certification (CA) ?](https://www.ssl.com/fr/article/qu%27est-ce-qu%27une-autorit%C3%A9-de-certification-ca/)
</small></small>

---  
## HTTPS

**L'autorité de certification** 

Les autorités de certification

- connues des navigateurs (_root CA_)
- certifie suivant 
	- http
	- dns 
	- mail 
- il existe EV SSL  
	(_extended validation_)

<small>

[Source thesslstore.com](https://www.thesslstore.com/blog/what-is-a-certificate-authority-ca-and-what-do-they-do/)
</small>

![w:600](images/certificate-authority.png)
<style scoped>
    img {
        position: absolute;
        top: 40px;
        right: 20px;
    }    
</style>

---
## HTTPS

```bash
$ openssl s_client -connect example.org:443

(cut)
GET / HTTP/1.1
Host: example.org
```
<br/>
<br/>

Voir _outssl_ 

---
## HTTPS

```bash
$ curl -v https://example.org
```
<br/>

```http
*   Trying 93.184.216.34:443...
* Connected to example.org (93.184.216.34) port 443 (#0)
[cut]
* Server certificate:  
*  subject: [cut] CN=www.example.org
*  start date: Jan 30 00:00:00 2024 GMT  
*  expire date: Mar  1 23:59:59 2025 GMT   
*  subjectAltName: host "example.org" matched cert's "example.org"  
*  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1 
```


---
## HTTPS - Obtention du certificat

- payer une autorité de certification 
	- créer une CSR (_certificate signing request_) contenant l'identité et une PK (_primary key_)

		```bash
		openssl req -nodes -newkey rsa:2048 -sha256 
			-keyout myserver.key -out server.csr
		```

	- le CA signe avec sa clé privée

- utiliser Let's Encrypt
	- `certbot`
	- `dehydrated`




# Serveur Web
<!--
_class: inverted
_footer: ''
_paginate: false
-->

---
## Serveur web

« Mise à disposition de l'information sur le réseau »

- Apache2, nginx, caddyserver… 
- HTML (CSS/JS)
- PHP, Ruby on rails, ASP… 
- Répartition de la charge (_load balancing_). Multi-thread / processus
<br/>


> `nodejs` avec le _framework_ Express est différent : c'est un environnement d'exécution serveur gérant des requêtes http.
<!-- class: warning -->

[Quels sont les serveurs web les plus utilisés ?](https://news.netcraft.com/archives/category/web-server-survey/)




# Apache 2
<!--
_class: inverted
_footer: ''
_paginate: false 
-->

---
## Apache2

Installation

- Paquets à installer : `apache2`, `libapache2-mod-php<i>`…

Configuration

- Fichiers 
    - `apache2.conf`, `conf-[available|enabled]`
	- `sites-[available|enabled]`, gestion des hôtes virtuels (voir plus loin)
	- `mods-[available|enabled]`, gestion des modules 
- Commandes
	`a2en[conf|site|mod]`, `apache2ctl`

---
![bg](images/vhost-octopus.png)
<!--
_header: ''
_footer: ''
_paginate: false
-->

---
## Apache2 - Virtual host

![w:600](images/vhost-fleche.png)
<style scoped>
    img {
        position: absolute;
        top: 50px;
        right: 20px;
    }
</style>

Un fichier de configuration par site (_vhost_). 
Extrait :

```apache
ServerName    example.org
DocumentRoot  /var/www/html/org.example
ServerAdmin   webmaster@example.org
```
<br/>

Que fait `a2ensite example.org` ?

---
## Exercice

Installer un serveur web apache et deux _vhosts_ : l'un répondant à `one.example.org` et l'autre `two.example.org`.  
<!-- _class: inverted-orange -->


---
## Apache2 - MPM

**Un exemple de module** : MPM - Modules multi-processus

- Apache fonctionne avec un essaim de _processus_
- Un module MPM, gère le nombre de _processus_ et de _threads_ lancés par Apache2
- Il existe plusieurs modules MPM: _prefork_, _event_, _worker_…
	- _prefork_ utilise plusieurs processus;
	- _worker_ et _event_ utilisent plusieurs processus… et plusieurs _threads_ / processus
- Sur un système d'exploitation moderne, ce sera _event_
<small><small>

[Apache MPM](https://httpd.apache.org/docs/2.4/mod/mpm.html)  
</small></small>

---
**MPM - Modules multi-processus**

Exemple
```apache
<IfModule mpm_event_module>
  StartServers             2
  MinSpareThreads          25
  MaxSpareThreads          75
  ThreadLimit              64
  ThreadsPerChild          25
  MaxRequestWorkers        150
  MaxConnectionsPerChild   0
</IfModule>
```

---
## Apache2 - ACL

**Gestion du contrôle d'accès (_access control list_)**

- spécifie les autorisations (_allow_) et les interdictions (_deny_) d'accès à une arborescence d'un serveur
- peut se faire dans la configuration de _vhost_ ou dans un fichier `.htaccess`
<br/>

Un fichier `.htaccess` est un extrait de configuration du serveur se trouvant dans un répertoire servi par le le serveur web. 

```apache
AccessFileName .htaccess
```

---
**Gestion du contrôle d'accès (_access control list_)** (suite)

L ’authentification dans HTTP peut se faire grâce aux ACL de différentes manières

- BASIC (RFC 2617)
- DIGEST (RFC 2617)
- SSL/TLS
<br/>

Une authentification _basic_ à travers une connexion TLS est sûre. Une alternative est l'utilisation de certificat pour une authentification _via_ ces certificats (voir exemples).
<small><small><br/>

[Index par classes des directives autorisées dans .htaccess](https://httpd.apache.org/docs/2.4/mod/overrides.html)
</small></small>

---
**Gestion du contrôle d'accès (_access control list_)** (suite)

**Exemple 1**

```apache
Order deny, allow
Deny from all
Allow from 127.0.0.1/8
```

_new way_

```apache
Require all denied
Require ip 127.0.0.1/8
```
<small><small><br/>

[Module Apache mod_authz_core](https://httpd.apache.org/docs/2.4/mod/mod_authz_core.html)
</small></small>

---
**Gestion du contrôle d'accès (_access control list_)** (suite)

**Exemple 2**  
(Fichier `.htaccess` à placer dans un répertoire)
<small>

```apache
AuthUserFile access/.htaccess_passwd
AuthGroupFile /dev/null
AuthName "Accès membres"
AuthType Basic

<FilesMatch verysecretfile.html>
<LIMIT GET POST>
require valid-user
</LIMIT>
</FilesMatch>

<FilesMatch .htaccess>
<LIMIT GET POST>
require all denied
</LIMIT>
</FilesMatch>
```
</small>

---
**Gestion du contrôle d'accès (_access control list_)** (suite)

**Exemple 3**
<small><small>

```apache
SSLCACertificateFile "conf/ssl.crt/company-ca.crt"

<Directory "/usr/local/apache2/htdocs">
#   En dehors de subarea, seul l'accès depuis l'intranet est
#   autorisé
    Require              ip 192.168.1.0/24
</Directory>

<Directory "/usr/local/apache2/htdocs/subarea">
#   Dans subarea, tout accès depuis l'intranet est autorisé
#   mais depuis l'Internet, seul l'accès par HTTPS + chiffrement fort + Mot de passe
#   ou HTTPS + chiffrement fort + certificat client n'est autorisé.

#   Si HTTPS est utilisé, on s'assure que le niveau de chiffrement est fort.
#   Autorise en plus les certificats clients comme une alternative à
#   l'authentification basique.
    SSLVerifyClient      optional
    SSLVerifyDepth       1
    SSLOptions           +FakeBasicAuth +StrictRequire
    SSLRequire           %{SSL_CIPHER_USEKEYSIZE} >= 128
```
</small></small>

---
**Exemple 3** (suite)
<small><small>

```apache
    
    #   On oblige les clients venant d'Internet à utiliser HTTPS
    RewriteEngine        on
    RewriteCond          "%{REMOTE_ADDR}" "!^192\.168\.1\.[0-9]+$"
    RewriteCond          "%{HTTPS}" "!=on"
    RewriteRule          "." "-" [F]
    
    #   On permet l'accès soit sur les critères réseaux, soit par authentification Basique
    Satisfy              any
    
    #   Contrôle d'accès réseau
    Require              ip 192.168.1.0/24
    
    #   Configuration de l'authentification HTTP Basique
    AuthType             basic
    AuthName             "Protected Intranet Area"
    AuthBasicProvider    file
    AuthUserFile         "conf/protected.passwd"
    Require              valid-user
</Directory>
```

Source <https://httpd.apache.org/docs/2.4/ssl/ssl_howto.html>

</small></small>

---
## Apache2 - Authentification

**Authentification**  
Actuellement, l'authentification est plutôt **applicative**

- interface de _login_ intégrée à l'application et pouvant être paramétrée
- authentification à travers TLS puis (bien) gérée par le _framework_
- peut-être déléguée (_SSO_)
- « facile » pour l'application de gérer ensuite la session
- …

---
## Apache2 - HTTPS

**Configurer Apache pour servir un site en HTTPS**

- Se procurer les certificats
- Rendre le module `mod_ssl` disponible
- Configurer le _vhost_ pour écouter sur le port 443.  

---
## Apache2 - HTTPS

Extrait d'une configuration Apache

```apache
<IfModule mod_ssl.c>
	<VirtualHost _default_:443>
		ServerName example.org
		ServerAdmin webmaster@localhost
		DocumentRoot /var/www/html

		ErrorLog ${APACHE_LOG_DIR}/error.log
		CustomLog ${APACHE_LOG_DIR}/access.log combined

		SSLEngine on
		SSLCertificateFile	/elsewhere/cert.pem
		SSLCertificateKeyFile /elsewhere/key.key
	</VirtualHost>
</IfModule>
```
---
## Apache2 - HTTPS

**Génération des certificats** par une autorité tierce (payante) 

- générer sa CSR (_certificate signing request_) et l'envoyer
- recevoir le _challenge_ et le mettre en place 
- attendre (un peu)
- télécharger ses certificats et les mettre « à l'endroit qui va bien » 


> **Durée de validité**
> Le certificat est valide 398 jours (pour 10 ans en 2012). 
> À partir du 15 mars 2029, ce sera 47 jours. 
<!-- _class: tip -->

---
## Apache2 - HTTPS

**Génération des certificats** _via_ Let's encrypt

- automatisation de la tâche _via_ `certbot`, `dehydrated`…

**dehydrated** _quick start_
<small>

- installation (`apt install dehydrated dehydrated-apache2`)
- éditer `/etc/dehydrated/domain.txt`
- consulter `/etc/dehydrated/config` pour voir où sont les fichiers
- lancer `dehydrated -c`
- ajouter la configuration _https_ avec le lien vers les certificats
</small>

> Le certificat est valide 3 mois.
<!-- _class: tip -->

---
## Apache2 - Proxy 

Un **proxy** est un intermédiaire entre un client et un serveur

Par exemple :

- le client est le navigateur web qui interroge apache,
- le serveur est une application _tournant sur un autre port_ (ou une autre machine).


**proxy vs reverse proxy**  

- **proxy classique** : un client demande une ressource sur Internet à travers le proxy  
- **reverse proxy** : le proxy se place devant un serveur pour filtrer et gérer les requêtes des clients  

---
## Apache2 - Reverse Proxy  

Pour utiliser Apache en proxy, il faut activer les modules nécessaires :  

```bash
a2enmod proxy proxy_http
```

et ajouter à la configuration de _vhost_ :

```apache
<VirtualHost *:80>
    ServerName app.example.org
    # (…)
    ProxyPreserveHost On
    ProxyPass        / http://127.0.0.1:8080/
    ProxyPassReverse / http://app.example.org 
</VirtualHost>
```

> Pour HTTPS, c'est tout à fait semblable.
<!-- _class: tip -->

---
## Apache2 - *Load balancer*

Apache peut être utilisé comme un **équilibreur de charge** (_load balancer_) grâce au module `mod_proxy_balancer`.

- répartition de la charge;
- haute disponibilité;
- scalabilité 

---
**Apache2 - *Load balancer***

Activer les modules

```bash
a2enmod proxy proxy_balancer proxy_http lbmethod_byrequests
```

- `mod_proxy` permet à Apache d'agir en tant que proxy.  
- `mod_proxy_http` supporte les proxys HTTP.  
- `mod_proxy_balancer` active le gestionnaire de load balancing.  
- `mod_lbmethod_byrequests` définit la méthode de répartition par requêtes.  

---
**Apache2 - *Load balancer***

Exemple de configuration 
<small><small>

```apache
<VirtualHost *:80>
    ServerName loadbalancer.example.org

    ProxyPreserveHost On

    <Proxy "balancer://mycluster">
        BalancerMember http://192.168.1.11:8080 loadfactor=1
        BalancerMember http://192.168.1.12:8080 loadfactor=2
        BalancerMember http://192.168.1.13:8080 loadfactor=1
        ProxySet lbmethod=byrequests
    </Proxy>

    ProxyPass "/" "balancer://mycluster/"
    ProxyPassReverse "/" "balancer://mycluster/"

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
</small></small>




# Nginx
<!-- 
_class: inverted
_paginate: false
_footer: ''
-->

---
## Nginx

Installation 

- Paquets à installer : nginx, libnginx-mod-_foo_…

Configuration 
	
- `nginx.conf`
- `sites-[available|enabled]`, gestion des hôtes virtuels (_servers blocks_)
- `modules-[available|enabled]`, gestion des modules

> **freenginx**
> Le 14 fév. 2024, un _fork_ est créé : *freenginx*.   
> Le but du projet est de conserver le développement de _nginx_ libre. 

---
## Nginx - _Servers blocks_

Le premier _server block_ est celui par défaut 

```nginx
http {
	server {
   		root /data/www;
	}
}
```

- `server` détermine la configuration du _server block_
- `root` l'endroit où se trouvent les fichiers (`/var/www` est très bien aussi)

---
**Nginx - _Servers blocks_**

```nginx
http {
	server {
		location / {
    		root /data/www;
		}
		location /images {
    		root /data/images;
		}
	}
}
```

- plusieurs _locations_ peuvent être choisies pour un même _server block_

---
**Nginx - _Servers blocks_**

L'ajout d'une directive `server_name` permet de répondre pour un hôte virtuel 

```nginx
server {
    listen       80;
    server_name  example.org;
    root /data/www/org.example;
    ;...
}
```

---
**Nginx - _Servers blocks_**


```nginx
server {
    listen       80;
    server_name  _;
	root /data/www/default;
    ;...
}

server {
    listen       80;
    server_name  example.org;
	root /data/www/org.example;
    ;...
}
```

- `server_name _` est un *catch_all*

---
## Nginx - proxy

Un simple _proxy_ est un changement de _location_

```nginx
server {
    location / {
        proxy_pass http://localhost:8080;
    }
}
```

---
### Exercice

Installer un serveur web nginx et deux _vhosts_ : l'un répondant à `one.example.org` et l'autre `two.example.org`.  
<!--
_class: inverted-orange 
-->








# caddy server
<!-- 
_class: inverted 
_paginate: false
_footer: ''
-->


---
### Atelier de recherche
caddy web server
<!-- 
_class: inverted-orange 

-->

---
## Caddy server

- Dæmon `caddy` géré _comme d'habitude_ 
- Fichier de configuration JSON ou CaddyFile (`/etc/caddy/CaddyFile`)
- La configuration est visible _via_ `curl localhost:2019/config/`
	- _Tips_ `|jq`{.bash} or `|python3 json.tools`
- _Multiples sites_ définis dans _CaddyFile_ (cfr. infra)
<br/>
<small>	

[Caddy doc, getting started](https://caddyserver.com/docs/getting-started)  
[Caddy doc, API tutorial](https://caddyserver.com/docs/api-tutorial)
</small>

--- 
![w:900 center](images/caddyfile-visual.png)

<small><small>

[Caddy doc, caddyfile](https://caddyserver.com/docs/caddyfile/concepts)
[Source](https://caddyserver.com)
</small></small>

---
## Caddy server 

CaddyFile exemple 

```config
example1.com {
	root * /www/example.com
	file_server
}

example2.com {
	reverse_proxy localhost:9000
}
```

> **Vocabulaire**
> Le vocabulaire est un peu différent: block, directives, _snippets_, adresses, _matchers_, _placeholders_ 

---
![bg contain](images/caddyfile-addresses.png)
<!--
_paginate: false
_footer: ''
_header: ''
-->

---
### Défi

Écrire dans le langage de son choix, un _client http_ minimaliste. 
Un programme qui affiche la page html demandée : par ex. `example.org/index.html`
<!--
_class: inverted-orange
-->


---
### Défi

Écrire dans le langage de son choix, un _serveur http_ (très) minimaliste. 
Un programme qui écoute sur le port 80 et envoie la page html demandée.
<!--
_class: inverted-orange
-->







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





# TODO
TODO demander d'écrire une requete post avec nc comme suit : 

```bash
POST /login.php HTTP/1.1
Host: example.org
Content-Type: application/x-www-form-urlencoded
Content-Length: 29

username=testuser&password=1234

```

