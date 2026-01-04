# Laboratoire SSH

| Objectifs |
|:-------------|
| Identifier les paramètres de configuration SSH standards |
| Expliquer les principes de sécurité d'un serveur SSH |
| Configurer un serveur SSH selon les bonnes pratiques de sécurité |
| Évaluer la robustesse des mots de passe par attaque par force brute |

_Un serveur ssh est normalement déjà installé sur la machine._

:::info Exercice 1
Vérifiez si sa configuration est « sécurisée » au sens décrit dans les slides.
:::

:::info Exercice 2
Créez deux comptes `user1` et `user2`; le premier avec un mot de
passe dérivé du nom du compte et le second avec un mot de passe de 4 caractères minuscules aléatoires.  Demander l’IP de son voisin et essayer de cracker le mot de passe d’un de ses comptes.
:::

:::warning
Pour l'exercice suivant, une bonne connaissance de PAM est nécessaire. 
:::

:::info Exercice 3
Mettez en place une authentification à deux facteurs (2FA) pour SSH en utilisant Google Authenticator.
:::

**Objectifs :**
- Installer et configurer le module PAM Google Authenticator
- Configurer SSH pour exiger à la fois une clé SSH et un code OTP
- Tester l'authentification renforcée

**Indications :**
- Le paquet nécessaire est `libpam-google-authenticator`
- La configuration SSH nécessite des modifications dans `/etc/ssh/sshd_config` (notamment `ChallengeResponseAuthentication` et `AuthenticationMethods`)
- Le fichier `/etc/pam.d/sshd` doit être modifié pour intégrer le module PAM
- Chaque utilisateur doit initialiser son authenticateur avec `google-authenticator`
- Pensez à scanner le QR code avec une application compatible (Bitwarden Authenticator, Google Authenticator, etc.)
- Les codes de secours générés doivent être conservés précieusement

:::warning Questions
- Quelle méthode d'authentification utiliser : clé publique + OTP ou mot de passe + OTP ?
- Comment éviter de se bloquer l'accès en cas de mauvaise configuration ?
- Que se passe-t-il si on perd son téléphone avec l'application d'authentification ?
:::


