# Laboratoire DHCP

| Objectifs |
|:-----------|
| Comprendre le fonctionnement du protocole DHCP et son rôle dans l'attribution automatique d'adresses IP |
| Appliquer les concepts de configuration DHCP en implémentant un serveur |
| Configurer un pool d'adresses avec les paramètres réseau appropriés |
| Analyser le processus d'attribution d'adresses via les logs et les outils de diagnostic |
| Étendre la configuration pour supporter DHCPv6 (exercice avancé) |

**Durée estimée :** 2 heures

## Serveur DHCP IPv4

Implémentez sur votre machine un serveur DHCP.  
Ce serveur doit :
- attribuer automatiquement des adresses IP aux clients
- fournir les paramètres réseau nécessaires (passerelle, DNS, masque)

**Choix du logiciel :**
- [ISC DHCP (_legacy_ depuis 2022 mais encore très rencontré)](https://www.isc.org/dhcp/)
- [Kea DHCP (le successeur)](https://www.isc.org/kea/)

|**Exigences**||
|:--|:--|
|Plage d'adresses | `10.i.0.1/8` à `10.i.0.255/8` (où `i` vous est attribué)
|Passerelle par défaut (_default gateway_) |`10.0.0.1`
|Serveurs DNS  | `10.0.0.1`
|Nom de domaine | `in.esigoto.info`


Redemandez une configuration IP pour voir si votre serveur DHCP répond. 

## Réservation d'adresse

Configurez une réservation d'adresse IP basée sur l'adresse MAC de votre machine. 

|**Exigences**|
|:--|
|Attribuez l'adresse `10.i.0.42` à votre machine


## Exercice avancé : DHCPv6

:::tip Pour aller plus loin
Si vous avez terminé les exercices précédents, configurez DHCPv6 sur votre serveur.  
_Exercice facultatif_
:::

- Configurer un serveur DHCPv6 (_stateful_ ou _stateless_)
- Attribuer des adresses IPv6 aux clients
- Tester avec un client DHCPv6

|**Exigences**||
|:--|:--|
| Préfixe IPv6    | `2001:db8:i::/64` (où `i` est votre numéro attribué)
| Plage d'adresses | `2001:db8:i::100` à `2001:db8:i::200`

**Test :**
- Utilisez `dhclient -6` sur le client
- Vérifiez l'attribution d'adresses IPv6 avec `ip -6 addr`

:::tip Réflexion 
Comparez les différences entre DHCPv4 et DHCPv6.  
Quelles sont les implications de SLAAC (Stateless Address Autoconfiguration) sur DHCPv6 ?
:::
