---
marp: true
headingDivider: 1
paginate: true
header: 'SSH'
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


# SSH
<br/>

## Secure shell

![bg](images/coffre-fort.jpeg)

<!-- 
_class: highlight
_footer: ''
_paginate: false
-->


# SSH


SSH (_Secure Shell_) est un protocole de communication sécurisé qui permet aux utilisateurs et utilisatrices de se connecter à un serveur distant et d'exécuter des commandes à distance.

# Ateliers de recherche

`ssh -v bob@pica.esigoto.info`

<!--
_class: 'inverted'
-->

# SSH

```bash
ssh [<user>@]<ip | hostname>
```

```bash
ssh alice@harmony.example.org
ssh 10.0.0.5
```

<br/>

- Connexion à une machine distante pour obtenir un `shell`. 
- Son ancêtre: `rsh` _aka_ _remote shell_.

# 1
SSH permet de s'assurer que l'on se connecte au bon serveur…

<!--
_class: 'inverted-orange'
-->

# SSH

Première connexion à une machine : 

```
The authenticity of host 'localhost (::1)' can t be established.
ECDSA key fingerprint is SHA256:yHN0v46EffSqvY6yl[cut].
Are you sure you want to continue connecting 
(yes/no/[fingerprint])? 
```

- Le serveur présente sa clé publique que j'accepte.
- Pour les autres connexions `ssh` prévient si elle change : mise à jour du serveur ou usurpation.

<!-- class: tip -->
> La vérification de l'empreinte est possible avant de l'accepter  
`ssh-keygen -l -f /etc/ssh/ssh_host…` et diffusée sur un autre canal. 

# 2
SSH chiffre la communication…

<!--
_class: 'inverted-orange'
-->


# SSH

Principe : 

**1** le client reçoit la clé publique du serveur

- Algorithme de cryptographie **asymétrique** : `DSA` (obsolète), 
`RSA` (taille minimale 4096), `ed25519`, `ecdsa`… 

    ```bash 
    ssh -Q key
    ```

<br/>
<small>

<!-- class: tip -->
> - La vérification de l'empreinte permet de s'assurer de sa légitimité (voir **1**)
> - Le client peut aussi vérifier que le serveur possède la clé privée en envoyant un message. 

</small>

# SSH

**2** le client et le serveur doivent s'accorder — sur un canal non sûr — pour s'échanger une **clé de session** commune.
    
- Algorithme cryptographique d'échange de clés : _Diffie-Hellman_

    ```bash
    ssh -Q kex
    ```

# SSH

**3** le client peut alors s'authentifier.

**4** ils peuvent communiquer en chiffrant les messages (_confidentialité_) et en les signant (_intégrité_).

- Algorithme de cryptographie **symétrique** : _AES_, _blowfish_, _chacha20_…

    ```bash
    ssh -Q cipher
    ```


# Échange de clés

<!--
_class: 'inverted'
-->


# Cryptographie - Échange de clés - Diffie-Hellman

<div class='columns'>
<div>

Les algorithmes _Diffie-Hellman_ sont une méthode d'échange de clés sur un canal de communication non sûr. 


_Illustration avec des pots de peinture_

</div>
<div>
<center>

![w:340px](images/Diffie-Hellman_Key_Exchange_(fr)_paint.png)

</div></div>


# Cryptographie - Échange de clés - Diffie-Hellman

![center w:600](images/Diffie-Hellman-Schlusselaustausch.png)

- **Diffie-Hellman** se base sur l'exponentielle (et est sensible au problème du logarithme discret)

- **Elliptic Curve Diffie-Hellman** `ECDH` se base sur les courbes elliptiques

# Cryptographie - Échange de clés - Diffie-Hellman

**Exemple**

Données communes :
- Nombre premier `P = 419`
- Générateur `G = 7`

**Génération des clés privées :**

<div class='columns'>
<div>

**Alice** « choisit » `a = 178`  
Envoie à Bob :  
`A = 7^178 mod 419 = 208`

</div>
<div>

**Bob** « choisit » `b = 344`  
Envoie à Alice :  
`B = 7^344 mod 419 = 49`

</div>
</div>

---
**Exemple** (suite)

**Calcul de la clé partagée :**

<div class='columns'>
<div>

Alice calcule :  
`K = 49^178 mod 419 = 107`

</div>
<div>

Bob calcule :  
`K = 208^344 mod 419 = 107`

</div>
</div>


# Cryptographie asymétrique

<!--
_class: 'inverted'
-->


# Cryptographie asymétrique

![center w:700](images/Asymmetric-Encryption.png)

- Un clé **publique** disponible pour chiffrer, 
- une clé **privée** gardée secrète pour déchiffrer. 


# Cryptographie asymétrique


_Manip_

Avec la clé publique disponible, chiffrer un message et l'envoyer…
<br/>

<!-- class: warning -->
> Ceci est une simple illustration du concept. Pour chiffrer effectivement des messages, on utilise `GPG`


# Cryptographie asymétrique

_Solution_

- Générer une clé RSA

    ```bash
    $ openssl genrsa -out key.pem 2048
    ```

- Extraire la clé publique

    ```bash
    $ openssl rsa -in key.pem -pubout -out key_pub.pem
    ```

# Cryptographie asymétrique

_Solution (suite)_

- Chiffrer un message 

    ```bash
    $ echo "Alice learn crypto." 
    | openssl pkeyutl -encrypt -inkey key_pub.pem -pubin 
        -out message.enc
    ```


- Déchiffrer le message

    ```
    $ openssl pkeyutl -decrypt -inkey key.pem  -in message.enc 
    ```



# Cryptographie symétrique

<!--
_class: inverted
-->

# Cryptographie symétrique
![center w:700](images/Symmetric-Encryption.png)

- Une seule clé, pour le chiffrement et le déchiffrement. 


# Cryptographie symétrique

_Manip_

Chiffrer un message et l'envoyer…

# Cryptographie symétrique

_Solution_

Chiffrement

```bash
echo "Bob chiffre son message" 
    | openssl enc -e -aes-256-cbc -out message-bob.enc
```

Déchiffrement

```bash
openssl enc -d -aes-256-cbc -in message-bob.enc
```

<small>

- voir `man openssl enc`
- `openssl enc -list` ou `openssl list -cipher-commands` liste les algorithmes de chiffrement

</small>


# SSH
## _(suite)_

<!--
_class: inverted
-->

# SSH 

Connexion `SSH` par dépôt d'une clé privée plutôt que par mot de passe. 

- Générer une paire de clés chez le client (une paire par client)

    ```bash 
    ssh-keygen -t rsa -b 4096 -C "user@example.org"
    ```

    - utilité d'une _passphrase_ ? 
    - `ssh-agent` 

# SSH

- Déposer sa clé publique sur le serveur 

    ```bash
    ssh-copy-id -i ~/.ssh/id_rsa.pub user@host
    ```

    - Pour vérifier une clé
        
        ```bash
        ssh-keygen -lf .ssh/id…
        ssh-keygen -lf .ssh/id… -E md5
        ```


# SSH

Exercice

```bash
ssh -v <ip>
```

- interprèter  

<br/>

<!-- class: tip -->
> Au sujet des algorithmes
https://stribika.github.io/2015/01/04/secure-secure-shell.html




# Un peu de sécurité

Comment sécuriser son serveur `SSH` ? 

- `ClientAliveInterval 300` fixe un _idle timeout_ 
- `PermitEmptyPasswords no` empêche de se connecter avec un mot de pass vide
- `PermitRootLogin no` n'autorise pas _root_ à se loguer
- `AllowUsers <yours users>` liste des comptes autorisés
- _Paramétrer la connexion par échange de clés et interdire celle par mot de passe_
    - `PubkeyAthentication yes`
    - `PasswordAuthentication no`

# Un peu de sécurité

Changer de port ?   

- **OUI - NON**
- _knocking_

# Exercice

Installer un serveur ssh
- Créer 3 comptes `user1`, `user2`, `user3`; le premier avec un mot de
passe dérivé du nom du compte, le second avec un mot de passe
du dictionnaire et le troisième avec un mot de passe de 4
caractères minuscules aléatoires.
- Demander l’IP de son voisin et essayer de cracker le mot de passe
d’un de ses comptes.
- Mettre en place le knocking



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

