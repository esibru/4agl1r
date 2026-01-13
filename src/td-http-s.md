# Laboratoire HTTP[S] – Serveur web Apache

Mise en œuvre des concepts de serveur web avec Apache.

## Lectures

- La documentation officielle d'Apache : http://httpd.apache.org/docs/2.4/
- *Apache: The Definitive Guide*, O'Reilly, 3rd edition. ISBN : 0-596-00203-3.  
  Laurie, B. and Laurie, P. (December 2002)

## Préalables

À ce stade de l'année, l'installation d'Apache ne devrait plus poser de problème. Faites une recherche sur les paquets contenant « apache » et choisissez ce que vous voulez installer.

```bash
apt search apache2
apt install apache2
```

Lisez bien le fichier de configuration `/etc/apache2/apache2.conf` afin de vous en imprégner.

:::tip Structure de configuration Apache sous Debian
Sous Debian/Ubuntu, la configuration Apache est modulaire :
- `/etc/apache2/apache2.conf` – configuration principale
- `/etc/apache2/sites-available/` – configurations des sites disponibles
- `/etc/apache2/sites-enabled/` – liens vers les sites actifs
- `/etc/apache2/mods-available/` – modules disponibles
- `/etc/apache2/mods-enabled/` – modules actifs

Utilisez `a2ensite`, `a2dissite`, `a2enmod`, `a2dismod` pour gérer les sites et modules.
:::

## Travaux à réaliser

### 1. Installation et page d'accueil

Installer le serveur web et placer à la racine de celui-ci une page HTML reprenant des liens vers les différents sites qui se trouveront sur le serveur (à ce stade, aucun).

La racine par défaut est `/var/www/html/`.

```bash
# Vérifier que le serveur fonctionne
systemctl status apache2
curl http://localhost
```

### 2. Support PHP pour les pages utilisateurs

Permettre aux utilisateurs d'utiliser un langage de script (PHP par exemple).

```bash
# Installer PHP
apt install libapache2-mod-php php
```

Vérifier que tout est fonctionnel en ajoutant une page `index.php` au site web par défaut. Cette page peut, par exemple, afficher `phpinfo()`.

### 3. VirtualHost

Créer deux sites différents; `red.esigoto.info` et `blue.esigoto.info` par exemple. Le premier rendant la page `index.hmtl` et le second la page `index.php` précédemment créées. 

:::info Qu'est-ce qu'un VirtualHost ?
Un VirtualHost permet d'héberger plusieurs sites web sur un même serveur Apache. Chaque site peut avoir :
- Son propre nom de domaine (`ServerName`)
- Sa propre racine de documents (`DocumentRoot`)
- Sa propre configuration
:::

:::warning Prérequis DNS
Il faudra modifier votre serveur DNS (ou bien votre fichier `/etc/hosts` si vous voulez tricher 😉).
:::

Un hôte virtuel _virtual host_ se crée dans un fichier `/etc/apache2/sites-available/red.esigoto.info.conf` [^f1] :

```apache
<VirtualHost *:80>
    ServerName red.esigoto.info
    DocumentRoot /var/www/html/info.esigoto.red
    
    ErrorLog ${APACHE_LOG_DIR}/users-error.log
    CustomLog ${APACHE_LOG_DIR}/users-access.log combined
</VirtualHost>
```

Activez le site :

```bash
a2ensite red.esigoto.info
systemctl reload apache2
```
[^f1]: En fait, le choix du nom du fichier est libre — mais pas l'extension — et je propose ici un moyen simple de s'y retrouver lorsque l'on a plusieurs — beaucoup — de _vhosts_.

### 4. Service web avec VirtualHost dédié

Installer un service web que nous déterminerons ensemble (par exemple : un CMS/blog ou un service « Framasoft »…).

Ce service aura son propre VirtualHost.

Exemple pour un service `wiki.esigoto.info` :

```apache
<VirtualHost *:80>
    ServerName wiki.esigoto.info
    DocumentRoot /var/www/info.esigoto.wiki
    
    ErrorLog ${APACHE_LOG_DIR}/wiki-error.log
    CustomLog ${APACHE_LOG_DIR}/wiki-access.log combined
</VirtualHost>
```

### 5. HTTPS avec Let's Encrypt (bonus)

Pour sécuriser vos sites avec HTTPS :

```bash
# Installer certbot
apt install certbot python3-certbot-apache

# Obtenir un certificat (remplacez par votre domaine)
certbot --apache -d wiki.esigoto.info
```

:::tip Certificats auto-signés pour les tests
Pour un environnement de test sans accès Internet :

```bash
# Activer le module SSL
a2enmod ssl

# Utiliser le site SSL par défaut (certificat auto-signé)
a2ensite default-ssl
systemctl reload apache2
```
:::

## Vérifications

```bash
# Tester la configuration Apache
apache2ctl configtest

# Voir les VirtualHosts actifs
apache2ctl -S

# Logs en temps réel
tail -f /var/log/apache2/error.log
```
