# BGP (Border Gateway Protocol) - Cheat Sheet

## 1. **Qu'est-ce que BGP ?**
- **BGP (Border Gateway Protocol)** : Protocole de routage utilisé pour échanger des informations de routage entre systèmes autonomes (AS).
- Fonctionne au niveau 3 du modèle OSI.
- Utilisé pour le routage inter-domaine (externe) et parfois intra-domaine (interne).
- Basé sur une connexion TCP (port 179).

**AS** : Autonomous System (réseau géré autonome)
---

## 2. **Caractéristiques principales de BGP**
- **Types de BGP** :
  - **eBGP (External BGP)** : Entre systèmes autonomes différents.
  - **iBGP (Internal BGP)** : Au sein d’un même système autonome.
- **Convergence lente en théorie** :
  - BGP n’a pas de mécanisme rapide de convergence en cas de changement.
  - **En pratique**, des optimisations (par exemple, timers ajustés, politiques de routage) permettent une très bonne performance.
  - Recommandé pour sa **stabilité et scalabilité**.
- **Politique de routage flexible** : Basée sur des attributs.
- **Chemins explicites** : Utilise des routes exactes via l'attribut AS-Path.

---

## 3. **Attributs BGP et critères de décision**
### Attributs des routes BGP :
1. **Weight** (Cisco uniquement) : Priorité locale, non propagé hors du routeur.
2. **Local Preference** : Indique la préférence pour les routes à travers un AS (plus élevé = préféré).
3. **AS Path** : Nombre d’AS traversés, plus court = préféré.
4. **MED (Multi-Exit Discriminator)** : Préférence pour un point d'entrée spécifique dans un AS, plus petit = préféré.
5. **Type de routeur** : Préfère eBGP à iBGP.
6. **IGP Metric** : Coût interne pour atteindre le next-hop, plus faible = préféré.
7. **Multipath BGP** (si activé) : Permet plusieurs routes.
8. **Router ID** : Plus bas = préféré.
9. **Cluster list** : Préfère la route avec la liste la plus courte.
10. **Neighbor Address** : Plus basse = préférée.

---

## 4. **Commandes utiles**

### Configuration BGP de base (IPv4) sur un routeur Cisco :
```bash
router bgp <local_as>
 bgp router-id <router_id>
 neighbor <neighbor_ip> remote-as <neighbor_as>
 network <network_address> mask <subnet_mask>
```
- `router bgp <local_as>` : Configure le processus BGP pour un AS local.
- `bgp router-id <router_id>` : Définit l'identifiant du routeur BGP.
- `neighbor <neighbor_ip> remote-as <neighbor_as>` : Définit le voisin BGP et son AS.
- `network <network_address> mask <subnet_mask>` : Annonce un réseau.

#### Exemple concret (eBGP) :
```bash
router bgp 65001
 bgp router-id 1.1.1.1
 neighbor 192.0.2.1 remote-as 65002
 network 10.0.0.0 mask 255.255.255.0
```

### Configuration BGP pour IPv6 :
```bash
router bgp <local_as>
 bgp router-id <router_id>
 neighbor <neighbor_ip> remote-as <neighbor_as>
 address-family ipv6 unicast
   network <ipv6_prefix> mask <prefix_length>
   neighbor <neighbor_ip> activate
```
- `bgp router-id <router_id>` : Définit l'identifiant du routeur BGP.
- `address-family ipv6 unicast` : Active le routage unicast IPv6 dans BGP.
- `network <ipv6_prefix> mask <prefix_length>` : Annonce un réseau IPv6.

#### Exemple concret (eBGP avec IPv6) :
```bash
router bgp 65001
 bgp router-id 1.1.1.1
 neighbor 2001:db8::1 remote-as 65002
 address-family ipv6 unicast
  network 2001:db8:1::/64
  neighbor 2001:db8::1 activate
```

### Configuration iBGP avec OSPFv3 sur loopbacks :
1. **Configurer OSPFv3 pour propager les loopbacks**
```bash
router ospfv3 <process_id> ipv6
 passive-interface default
 no passive-interface <interface_name>
 interface Loopback0
  ipv6 address <ipv6_address>/<prefix>
  ospfv3 area 0
```
- `passive-interface default` : Définit toutes les interfaces en mode passif (aucun adjacence OSPF).
- `no passive-interface <interface_name>` : Active OSPF sur les interfaces non passives.
- `ospfv3 area 0` : Associe l'interface à une aire OSPF.

2. **Configurer iBGP pour utiliser les loopbacks comme voisins**
```bash
router bgp <local_as>
 bgp router-id <router_id>
 neighbor <loopback_ip> remote-as <local_as>
 update-source Loopback0
 address-family ipv6 unicast
   neighbor <loopback_ip> activate
```
- `bgp router-id <router_id>` : Définit l'identifiant du routeur BGP.
- `update-source Loopback0` : Utilise l'adresse de Loopback0 comme source pour BGP.
- `address-family ipv6 unicast` : Active l'échange de préfixes IPv6.

#### Exemple concret (iBGP avec OSPFv3) :
```bash
! OSPFv3 Configuration
router ospfv3 100 ipv6
 passive-interface default
 no passive-interface GigabitEthernet0/0
 interface Loopback0
  ipv6 address 2001:db8::1/128
  ospfv3 area 0
! iBGP Configuration
router bgp 65001
 bgp router-id 1.1.1.1
 neighbor 2001:db8::2 remote-as 65001
 update-source Loopback0
 address-family ipv6 unicast
   neighbor 2001:db8::2 activate
```

---

## 5. **Politique de préférence et filtrage**
### Préférer un voisin spécifique
Utiliser **Weight** ou **Local Preference** pour prioriser un chemin :
```bash
route-map PREFER_NEIGHBOR permit 10
 set weight 1000
!
router bgp <local_as>
 neighbor <neighbor_ip> route-map PREFER_NEIGHBOR in
```
- `set weight <value>` : Définit une priorité locale.
- `route-map` : Applique une politique de routage.

### AS Path Prepending
Ajouter des AS pour rendre un chemin moins attrayant :
```bash
route-map PREPEND_AS permit 10
 set as-path prepend <local_as> <local_as>
!
router bgp <local_as>
 neighbor <neighbor_ip> route-map PREPEND_AS out
```
- `set as-path prepend` : Ajoute des AS au chemin.

### Filtrer les préfixes
Accepter ou refuser des routes spécifiques avec `<filtre>` :
```bash
ip as-path access-list 1 permit <regexp>
ip as-path access-list 2 deny <regexp>
!
route-map FILTER_ROUTES permit 10
 match as-path <filtre>
!
router bgp <local_as>
 neighbor <neighbor_ip> route-map FILTER_ROUTES in
```
#### Options de filtre :
- **Regex** : Exemple : `^$` (routes locales uniquement).
- **AS Path** : Exemple : `_65002_` (routes passant par AS 65002).
- **Préfixes** : Définir des plages spécifiques.
- `match as-path` : Associe une politique à une règle de chemin AS.

### Configurer un peering BGP
Définir un peering avec des conditions spécifiques :
```bash
router bgp <local_as>
 neighbor <neighbor_ip> remote-as <neighbor_as>
 neighbor <neighbor_ip> password <password>
 neighbor <neighbor_ip> ttl-security hops <hops>
```
- `password` : Authentifie le peering avec un mot de passe.
- `ttl-security hops` : Définit une limite de distance pour éviter les attaques.

---

## 6. **ADJ-RIB-IN, LOC-RIB et ADJ-RIB-OUT**
### ADJ-RIB-IN
- Table contenant les routes reçues des voisins BGP avant application des filtres.
- Affiche toutes les routes apprises, y compris celles rejetées par des politiques de filtrage.

### LOC-RIB
- Table des routes sélectionnées après application des filtres et critères de décision BGP.
- Représente les routes utilisées dans la table de routage locale.

### ADJ-RIB-OUT
- Table contenant les routes prêtes à être envoyées aux voisins BGP après application des politiques de sortie.

---

## 7. **Vérification et débogage**
### Commandes de vérification :
```bash
show bgp ipv4                  # Affiche la table BGP IPv4
show bgp ipv4 summary          # Résumé des voisins BGP IPv4
show bgp ipv6 unicast          # Affiche la table BGP IPv6
show bgp ipv6 unicast summary  # Résumé des voisins BGP IPv6
show bgp ipv6 unicast route    # Affiche les routes par préfixe, avec les AS traversées
show ip route bgp              # Routes apprises via BGP
```

### Commandes de débogage :
#### IPv4
```bash
debug ip bgp updates      # Débogue les mises à jour BGP IPv4
debug ip bgp events       # Débogue les événements BGP IPv4
debug ip bgp keepalives   # Débogue les messages Keepalive IPv4
```
#### IPv6
```bash
debug ipv6 bgp unicast updates      # Débogue les mises à jour BGP IPv6 unicast
debug ipv6 bgp unicast events       # Débogue les événements BGP IPv6 unicast
debug ipv6 bgp unicast keepalives   # Débogue les messages Keepalive IPv6 unicast
```

---

## 7. **Ressources**
- [RFC 4271 - BGP-4](https://www.rfc-editor.org/rfc/rfc4271)
- [Cisco - Configuration de BGP](https://www.cisco.com/)
