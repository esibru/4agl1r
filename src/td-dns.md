# Laboratoire DNS

| Objectifs |
|:-----------|
| Comprendre le fonctionnement des serveurs DNS et leur rôle dans la résolution de noms |
| Appliquer les concepts de configuration DNS en implémentant un serveur à cache seul |
| Créer une zone DNS maître avec différents types d'enregistrements |
| Synthétiser une solution DNS complète incluant la résolution directe et inverse |
| Critiquer les implications éthiques et politiques du filtrage DNS |

**Durée estimée :** 4 heures (exposé oral compris)

### Serveur DNS à cache seul (Résolveur)

Implémentez sur votre machine un serveur DNS à cache seul.  
Ce serveur doit :
- Résoudre les noms (ex. `example.org` → adresse IP)
- Faire la résolution inverse

**Test :**  
Utilisez la commande `dig` (probablement à installer via le paquet `dnsutils`).

**Choix du logiciel :**
- `bind9`
- `unbound`

:::tip Conseil
Lire ou relire le fonctionnement du gestionnaire de paquet `apt`.
:::

### Serveur DNS maître

Implémentez un serveur maître pour :
- La zone `<my>.esigoto.info` (où `<my>` est un _placeholder_ pour votre matricule)
- La zone inverse

Ajoutez :
- Champs `A`, `AAAA`, `CNAME`
- Champ `TXT` (réfléchir à son contenu)
- Champs `MX` (déterminer de « bonnes » valeurs)
- `DNSSEC` à votre zone

:::warning
Si vous avez utilisé `unbound` précédemment, passez à `bind9`.
:::

### Serveur DNS menteur

Un serveur DNS peut :
- Mentir
- Bloquer des résolutions de noms

**Mise en place :**
- Utilisez RPZ (Response Policy Zone)
- Bloquez `http://facebook.com`
- Redirigez `http://google.com` vers `http://ddg.gg`

:::tip Réflexion 
Considérez les implications politiques d’un DNS menteur ou bloquant.
:::

**Lectures complémentaires :**
- [Quand ton serveur DNS te bloque ou te ment](https://blog.namok.be/2016-10-18-quand-ton-serveur-dns-te-bloque-ou-te-ment.html)
- [Mise en place d’un DNS menteur](https://blog.namok.be/2017-03-05-mise-en-place-dns-menteur.html)

