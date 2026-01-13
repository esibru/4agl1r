# Organisation 

_organisation des cours / labos_


## Organisation du laboratoire virtuel

:::info
Un laboratoire virtuel, accessible en dehors de l'école, est disponible depuis 2020. Il permet de mettre à disposition une machine linux à chaque étudiant ou étudiante. 
:::

Le laboratoire virtuel est composé d'une machine physique, un _hyperviseur_ et de machines virtuelles. Le schéma du laboratoire est ci-dessous. 

![](public/img/lab.png)

L'accès au laboratoire virtuel se fait en `ssh` _via_ la machine _pica_. Les identifiants sont donnés au laboratoire. 

:::warning
La machine se trouve au sein de l'école : 
- l'accès à partir de **l'extérieur** de l'école se fait _via_ son IP publique. Cette IP publique est correctement donnée par les serveurs DNS;
- l'accès de **l'intérieur** de l'école doit se faire avec l'adresse IP privée de la machine. Les serveurs DNS publics ne donnent pas cette IP.
:::

:::tip
Utiliser son fichier `/etc/hosts` est une bonne idée. 
:::

Une fois connecté en `ssh` à la machine _pica_, il est possible de faire un saut sur la machine qui vous a été attribuée. Inutile de connaitre son IP privée, le serveur DNS interne la connait et résoudra le nom. 

## Planning

Planning informatif (peut-être sujet à des changements).
| Séance | Thème de la Séance      | Objectifs d'Apprentissage (modèle Bloom)                | Activité Pratique (Lab)      |
|--------|------------------------|------------------------------------------|------------------------------|
| 1  | Présentation <br/>Rappels linux        | Se souvenir des commandes de base Linux. Comprendre l'environnement de travail. |—|
| 2  | Rappels réseaux      | Expliquer les concepts fondamentaux des réseaux. <br/>Identifier les composants du laboratoire virtuel. |Découverte du laboratoire virtuel|
| 3      | PAM                  | Comprendre le rôle de PAM dans la gestion des accès. <br/>Modifier et adapter la configuration PAM. | **PAM** <br/>Modifier la configuration de certaines commandes. <br/>Écrire un programme _pam enabled_.|
| 4  | SSH                  | Comprendre le protocole SSH. <br/>Appliquer des notions de chiffrement. <br/>Analyser la sécurité d'un serveur SSH. | **SSH** <br/>Vérification de la configuration SSH. <br/>Sécurisation du serveur. <br/>Tentative de cracker un mot de passe. |
| 5      | DNS                    | Définir le rôle du DNS. <br/>Installer et configurer un serveur DNS. | **DNS** <br/>Installer un serveur DNS à cache seul. <br/>Configurer une zone `in.example.org`. <br/>Configurer un DNS menteur (_RPZ policy_)  |
| 6      | DNS / DNSSEC                   | <br/>Mettre en œuvre la configuration avancée d'un serveur DNS. <br/>Évaluer les politiques de sécurité DNS. | **DNS** (suite) |
| 7      | DHCP                  | Expliquer le fonctionnement du protocole DHCP. <br/>Installer et configurer un serveur DHCP. <br/>Analyser les baux (_leases_) DHCP et leur gestion. |**DHCP** <br/>Installation d'un serveur DHCP. <br/>Configuration de pools d'adresses. <br/>Réservations d'adresses |
| 8      | HTTP(s)                  | Installer et configurer un serveur web. <br/>Différencier les types de virtual hosts.<br/>Comprendre ce qu'est un _proxy_ et le mettre en œuvre. | **Apache2** <br/>Installation d'un serveur avec _vhosts_. <br/>  |
| 9      | LDAP                   | Décrire l'utilité d'un annuaire LDAP. <br/>Installer et utiliser un annuaire LDAP. | **LDAP** <br/>Installation d'un annuaire LDAP (open LDAP). <br/>Utilisation d'un annuaire avec un schéma existant |
| 10     | LDAP                   | Administrer et sécuriser un annuaire LDAP. | **LDAP** (suite)|
| 11     | LDAP             | Évaluer les usages avancés de LDAP.  | **LDAP** (suite) |
| 12     | _Récupération_, <br/>réponse aux questions,  <br/>fin du travail                | Synthétiser les connaissances acquises.  |— |

## Pendant les manips

Pendant que vous faites vos _manips_ : 

1. complétez un document — c'est-à-dire un **rapport** — reprenant toutes vos manipulations.  Incluez :
    - les contenus de vos fichiers de configuration
    - vos démarches
    - les problèmes rencontrés
    - les solutions et moyens utilisés

2. consultez les pages de manuels (_si si, ça reste intéressant_)
    - commencez par un `man man` si vous ne savez pas ce qu'est une page de manuel
    
:::danger
Le **rapport** sera demandé lors de l'examen. Il **doit** être rédigé correctement en _markdown_. 
:::