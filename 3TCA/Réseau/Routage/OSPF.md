# OSPF (Open Shortest Path First) - Cheat Sheet

## 1. **Qu'est-ce qu'OSPF ?**
- **OSPF (Open Shortest Path First)** : Protocole de routage à état de lien pour les réseaux IP.
- Fonctionne au niveau 3 du modèle OSI.
- Utilise l'algorithme SPF (Shortest Path First ou Dijkstra).
- Supporte les grandes topologies grâce au concept de zones.
- Protocoles :
  - **OSPFv2** : pour IPv4.
  - **OSPFv3** : pour IPv6.

---

## 2. **Caractéristiques principales d'OSPF**
- **Routage hiérarchique** : Utilisation d'une zone backbone (Area 0).
- **Convergence rapide** : Basé sur des LSAs (Link State Advertisements).
- **Méthode de coût** : Basé sur la bande passante des liens (coût = 100 Mbps / bande passante).
- **Multicast** :
  - IPv4 : Adresses multicast 224.0.0.5 (All SPF Routers) et 224.0.0.6 (All DR Routers - voir section 3).
  - IPv6 : FF02::5 et FF02::6.
- **Pas de limite de saut (hop count)**.

---

## 3. **Concepts clés d'OSPF**
- **Zones** :
  - **Backbone (Area 0)** : Obligatoire, connecte toutes les autres zones.
  - **Stub Area** : Réduit les LSAs externes.
  - **Totally Stubby Area** : Pas de LSAs externes ni interzones.
  - **NSSA (Not-So-Stubby Area)** : Autorise des routes externes limitées.
- **LSA Types** :
  - Type 1 : Router LSA.
  - Type 2 : Network LSA.
  - Type 3 : Summary LSA.
  - Type 4 : ASBR Summary LSA.
  - Type 5 : External LSA (routes externes).
  - Type 7 : NSSA External LSA.

- **DR/BDR** (Designated Router / Backup Designated Router) :
  - Réduisent le trafic sur les segments multi-accès comme Ethernet.

---

## 4. **Commandes utiles**

### Configuration OSPFv2 (IPv4) sur un routeur Cisco :
```bash
router ospf <process_id>
 router-id <router_id>
 network <network_address> <wildcard_mask> area <area_id>
```
- `router ospf <process_id>` : Active OSPF avec un ID de processus spécifique.
- `router-id <router_id>` : Définit un identifiant unique pour le routeur (format IPv4).
- `network <network_address> <wildcard_mask> area <area_id>` : Associe des interfaces à OSPF dans une zone donnée.

#### Exemple concret :
```bash
router ospf 1
 router-id 1.1.1.1
 network 192.168.1.0 0.0.0.255 area 0
 network 10.0.0.0 0.0.0.255 area 1
```

### Configuration OSPFv3 (IPv6) sur un routeur Cisco :
```bash
ipv6 router ospf <process_id>
 router-id <router_id>
 passive-interface <interface_name> <number>
interface <interface_name> <number>
 ipv6 ospf <process_id> area <area_id>
```
- `ipv6 router ospf <process_id>` : Active OSPFv3 pour IPv6.
- `router-id <router_id>` : Définit un identifiant unique pour le routeur (format IPv4).
- `interface` : Active OSPFv3 sur une interface donnée.
- `ipv6 ospf <process_id> area <area_id>` : Associe l'interface à une zone spécifique.
- `passive-interface <interface_name> <number>`: Si OSPF est activé sur cette interface, il va juste ajouter les routes qui lui sont accessible par cette derbière, sans envoyer de paquet OSPF (très utile sur les routeurs de bordure d'AS en BGP).

#### Exemple concret :
```bash
ipv6 router ospf 1
 router-id 1.1.1.1
interface GigabitEthernet0/0
 ipv6 ospf 1 area 0
interface GigabitEthernet0/1
 ipv6 ospf 1 area 1
```

### Redistribution des routes connectées dans OSPF :
```bash
router ospf <process_id>
 redistribute connected subnets
```
- `redistribute connected subnets` : Redistribue les routes connectées dans OSPF.

---

## 5. **Vérification et débogage**
### Commandes de vérification :
```bash
show ip ospf              # Affiche l'état général d'OSPF
show ip ospf neighbor     # Liste les voisins OSPF
show ip ospf database     # Affiche la base de données OSPF
show ip route ospf        # Montre les routes apprises via OSPF
show ipv6 ospf            # Vérifie l'état OSPFv3
show ipv6 ospf neighbor   # Liste les voisins OSPFv3
```

### Commandes de débogage :
```bash
debug ip ospf events      # Surveille les événements OSPF
show ipv6 ospf neighbors
show ipv6 ospf database
show ipv6 ospf database router
```

---

## 6. **Ressources**
- [RFC 2328 - OSPFv2](https://www.rfc-editor.org/rfc/rfc2328)
- [RFC 5340 - OSPFv3](https://www.rfc-editor.org/rfc/rfc5340)
- [Cisco - Configuration d'OSPF](https://www.cisco.com/)
