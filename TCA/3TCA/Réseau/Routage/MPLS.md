## Introduction

Le protocole **MPLS** (**M**ulti**p**rotocol **L**abel **S**witching) est une technologie de commutation de paquets qui améliore l'efficacité et la flexibilité du routage dans les réseaux IP. Il est souvent utilisé par les fournisseurs de services pour assurer une meilleure qualité de service (QoS) et faciliter la mise en œuvre de VPN sécurisés.

## Architecture MPLS

MPLS repose sur le concept d'ajout d'un label aux paquets de données pour leur acheminement. Il est composé de plusieurs éléments :

- **Label Edge Router (LER)** : routeurs aux extrémités du réseau MPLS qui attribuent et suppriment les labels (équivalent PE dans le TD).
    
- **Label Switch Router (LSR)** : routeurs intermédiaires qui commutent les paquets en fonction des labels MPLS (équivalent P dans le TD).
    
- **Label Switching Path (LSP)** : chemin prédéfini emprunté par les paquets dans le réseau MPLS, permettant une transmission efficace et prévisible.
    

### Schéma MPLS simplifié

```
CE1 ---- PE1 ---- P ---- PE2 ---- CE2
        MPLS Core        
```

- **CE (Customer Edge)** : Routeur du client, connecté au réseau MPLS.
    
- **PE (Provider Edge)** : Routeur de bordure du fournisseur, qui applique MPLS et interagit avec BGP/MPLS VPN.
    
- **P (Provider)** : Routeur du cœur de réseau MPLS, assurant la commutation des labels.
    

## Data Plane vs Control Plane

### Data Plane

Le Data Plane est responsable de la transmission des paquets. Dans un réseau MPLS, les routeurs utilisent les labels MPLS pour transférer les paquets, évitant ainsi l’analyse des en-têtes IP.

Éléments du Data Plane :

- Transmission des paquets MPLS
    
- Commutation des labels
    
- Tables de FIB (Forwarding Information Base) : Lookup dans la VRF, opérations sur les labels
    

### Control Plane

Le Control Plane gère l'établissement des chemins et l'allocation des labels. Il utilise des protocoles comme LDP ou BGP pour échanger des informations de routage et de labels entre les routeurs.

Éléments du Control Plane :

- Protocoles de routage (OSPF, iBGP)
	- OSPF: Routage de Loopback à Loopback entre les LER à travers le backbone (LER + LSR)
	- iBGP: Partage des routes des clients entre les LER
    
- Protocoles de distribution de labels (LDP, RSVP-TE)
    
- Tables de RIB (Routing Information Base)
    

## Label Distribution Protocol (LDP)

LDP est le protocole principal utilisé pour distribuer les labels MPLS entre les routeurs.
Il existe 2 types de labels :

### Labels de transit

#### Échange :

- Deux routeurs voisins établissent une session LDP pour échanger des labels pour leurs *Next-Hops*.
  
- Chaque message associe un préfixe IP à un label transit (ex: `10.0.0.0/8 par moi = label 1`)
    
#### Attribution et stockage :

- Le mapping (préfixe → label transit) est stocké dans la **LIB**.
        
- La **LFIB** est ensuite construite pour le forwarding réel des paquets.
	- Utilisation effective pour le forwarding MPLS
	- Un seul label par préfixe
	- Consultation en temps réel
        
#### Schéma labels de transit :

```
+---------------------------+
|   Message LDP reçu        |
| (préfixe IP  --> label)   |
+-------------+-------------+
              |
              v
+---------------------------+
|         LIB               |
| (Mapping préfixe -> label)|
+-------------+-------------+
              |
              v
+---------------------------+
|         LFIB              |
| (Info pour switching)     |
+---------------------------+
```

### Labels VPN

#### Échange :

- Les routeurs PE échangent les routes VPN via BGP VPNv4/6.
        
- Chaque route contient l’identifiant VRF et le label VPN associé.
        
#### Attribution et stockage :

- L’information VPN est d’abord stockée dans la **table VRF**.
        
- Le label VPN associé est intégré dans la **LIB**.
        
- La **LFIB** est ensuite construite pour le forwarding des paquets VPN.
        
#### Schéma labels VPN :

```
+-----------------------------------+
|  Message BGP VPNv4/6 reçu         |
| (route VPN, VRF, label VPN)       |
+---------------+-------------------+
                |
                v
+-----------------------------------+
|         Table VRF                 |
| (Association route -> VPN label)  |
+---------------+-------------------+
                |
                v
+-----------------------------------+
|            LIB                    |
| (Mapping VRF -> label VPN)        |
+---------------+-------------------+
                |
                v
+-----------------------------------+
|            LFIB                   |
| (Info pour switching VPN)         |
+-----------------------------------+

```

### Scénario de routage VPN MPLS/BGP :

1. Le routeur LES ingress reçoit un paquet du routeur de bordure du client
	1. Il fait regarde dans la **VRF** associée à l'interface sur laquelle il reçoit le paquet pour trouver le **next-hop** (LES egress) associé à la destination IP.
	2. Il regarde dans sa **LIB** le **label VPN** associé a cette destination IP et ajoute l'en-tête au paquet (**push**).
	3. Il regarde dans sa **FIB globale (IGP)** pour trouver le **next-hop IP** vers le routeur egress (LES2).
	4. Il consulte ensuite sa **LFIB** (label forwarding) et récupère le **label de transit associé au LES egress par le next-hop** et l'ajoute (**push**) au paquet.
	5. Il **envoie le paquet** vers le **next-hop LSR**.
	   
2. Les routeurs LSR dans le backbone routent le paquet avec les labels
	1. Il regarde le label de transit pour déterminer le next-hop
	2. Il effectue un lookup dans sa **LFIB** pour déterminer l'action (**swap** ou **pop**) et le **next-hop** (swap si il y a encore un saut avant le LES egress, pop si le prochain saut est le LES egress). Ex: `LABEL 1 SWAP LABEL 2` ou `LABEL 1 POP`.
	3. Si nécessaire, il **swap** du label de transit avec le label prévu pour le prochain saut.
	4. Il transmet le paquet vers le prochain LSR ou le LES egress.
	   
3. Le routeur **LES egress** reçoit le paquet MPLS
	1. Il: reçoit un paquet avec **un ou deux labels** :
	    - Un seul label si **PHP** (Penultimate Hop Popping) a été fait (label VPN uniquement).
	    - Deux labels sinon (label de transit au-dessus du label VPN.
	2. Il consulte sa **LFIB** avec le **label du dessus** :
	    - Si c’est un **label de transit**, il le **dépile** (pop).
	    - Il continue avec le **label VPN** restant.
	3. Il consulte de nouveau sa **LFIB** avec le **label VPN** :
	    - Ce label est mappé à une **VRF**.
	    - Il dépile le label VPN → récupère le **paquet IP**.
	4. Il fait un **lookup IP dans la VRF** correspondante pour déterminer le next-hop client et l'interface de sortie
	5. l **envoie le paquet IP** au client final

## Resource Reservation Protocol - Traffic Engineering (RSVP-TE)

RSVP-TE est une extension du protocole RSVP permettant la réservation de ressources et l’ingénierie du trafic dans un réseau MPLS.

- **Cas d’usage** :
    
    - Réservation de bande passante pour les applications sensibles à la latence (ex. VoIP, streaming vidéo).
        
    - Création de chemins explicitement définis pour éviter la congestion réseau.
        
    - Redondance et protection des chemins en cas de panne.
        
- **Avantages** :
    
    - Permet une gestion avancée de la QoS
        
    - Prend en charge des chemins explicitement définis
        
- **Inconvénients** :
    
    - Complexité accrue
        
    - Nécessite plus de ressources de signalisation
        

## Segment Routing (SR-MPLS)

Segment Routing (SR) est une alternative à MPLS utilisant des segments plutôt que des labels traditionnels.

- **Cas d’usage** :
    
    - Réduction de la dépendance aux protocoles de signalisation (LDP, RSVP-TE).
        
    - Optimisation du trafic pour les applications SDN (Software-Defined Networking).
        
    - Scalabilité améliorée pour les grands réseaux.
        
- **Fonctionnement** :
    
    - Utilise des **Segment Identifiers (SID)** pour définir les chemins
        
    - Élimine la nécessité des protocoles de distribution de labels (ex: LDP)
        
    - Compatible avec MPLS et IPv6 (SRv6)
        
- **Avantages** :
    
    - Simplification du réseau
        
    - Meilleure scalabilité
        
- **Inconvénients** :
    
    - Nécessite une mise à jour des équipements
        

## Route Distinguishers (RD) vs Route Targets (RT) vs VRF

### **Route Distinguisher (RD)**

Un RD est un identifiant unique utilisé pour différencier les routes des différents clients dans un réseau MPLS VPN.

- **Cas d’usage** :
    
    - Différenciation des routes provenant de plusieurs clients sur un même réseau MPLS.
        
    - Exemple : Deux clients ayant le même sous-réseau `192.168.1.0/24` peuvent être différenciés par des RD distincts (`65000:1` pour Client A, `65000:2` pour Client B).
        
- **Format** : `ASN:Numéro` ou `IP:Numéro`
    
- **Ne joue pas un rôle dans la sélection des routes**
    

### **Route Target (RT)**

Les RT sont des attributs BGP permettant d’exporter et d’importer des routes entre différents VRF.

- **Cas d’usage** :
    
    - Partage de routes entre plusieurs VRF sur différents sites.
        
    - Exemple : Un site A exporte ses routes avec `RT:65000:100`, et un site B importe ce même `RT:65000:100`, permettant ainsi l'interconnexion entre ces deux VRF.
        
- **Export RT** : Attribué aux routes d’un VRF pour les rendre accessibles aux autres VRF
    
- **Import RT** : Permet à un VRF d’accepter des routes provenant d’autres VRF
    

### **VRF (Virtual Routing and Forwarding)**

Une VRF permet d'isoler plusieurs tables de routage sur un même routeur.

- **Cas d’usage** :
    
    - Séparation des flux de trafic pour différents clients sur un même backbone MPLS.
        
    - Mise en place de services réseau privés sans conflit d’adressage.
        
    - Exemple : Un FAI peut avoir une VRF pour ses services internes et une autre pour ses clients, assurant ainsi une isolation complète des routes.
        
- Chaque VRF a sa propre FIB et RIB
    
- Utilisé pour l’implémentation de VPN MPLS
    

### Configuration Cisco - Activation MPLS et LDP

```
Router(config)# mpls ip  
Router(config)# mpls ldp router-id <loopback_interface> force  
Router(config-if)# mpls ip  
```

- **mpls ip** : Active MPLS sur le routeur
    
- **mpls ldp router-id <loopback_interface> force** : Définit l'ID LDP basé sur l'interface spécifiée. Par défaut, l'ID LDP est l'adresse IP la plus haute d'une interface activée pour LDP. Cette commande force l'utilisation d'une interface spécifique, souvent une loopback, pour assurer une stabilité de l'ID même si des interfaces physiques changent.
    
- **mpls ip (interface)** : Active MPLS sur une interface spécifique
    

## VPN BGP/MPLS

BGP/MPLS VPN (RFC 4364) permet d'établir des VPN sur une infrastructure MPLS en utilisant BGP pour l'échange de routes entre les sites clients.

### Configuration Cisco - Création d'un VRF

```
Router(config)# ip vrf <vrf_name>
Router(config-vrf)# rd <route_distinguisher>
Router(config-vrf)# route-target export <export_rt>
Router(config-vrf)# route-target import <import_rt>
```

- **vrf_name** : Nom du VRF
    
- **route_distinguisher** : Identifiant unique du VPN
    
- **export_rt** : Route Target pour l'export des routes
    
- **import_rt** : Route Target pour l'import des routes
    

## Route Reflector et iBGP Full-Mesh

- Dans un réseau MPLS/BGP, **iBGP** doit être configuré en full-mesh entre tous les routeurs PE pour assurer une bonne distribution des routes VPN. Cependant, cette configuration devient complexe à grande échelle.
    
- **Route Reflector (RR)** : Permet de simplifier la topologie en désignant un ou plusieurs routeurs comme points centraux pour redistribuer les routes iBGP aux autres PE.
    

### Configuration Cisco d’un Route Reflector

```
Router(config)# router bgp <asn>
Router(config-router)# neighbor <neighbor_IP> remote-as <remote-as-number>
Router(config-router)# neighbor <neighbor_IP> route-reflector-client
```

### Configuration d'un peer BGP en tant que serveur Route Reflector

```
Router(config)# router bgp <asn>
Router(config-router)# neighbor <neighbor_IP> remote-as <remote-as-number>
```

On note que configuer du route reflector sur le client est similaire à celle d'un peer BGP  classique. La différence réside dans l'option `route-reflector-client` qui est ajoutée sur le Route Reflector pour indiquer que le voisin est un client.


- **asn** : Numéro d'AS du routeur
    
- **neighbor_IP** : Adresse IP du voisin BGP
    
- **remote-as-number** : Numéro d'AS du voisin
    
- **route-reflector-client** : Définit le voisin comme client du route reflector
    

## VPN BGP MPLS en pratique

### Étapes de configuration

1. **Établir le réseau iBGP mesh ou avec un Route Reflector**
    
    A. Configurer des interfaces de loopback
        
	B. Diffuser des routes vers les interfaces de loopback via OSPF
        
    C. Configurer iBGP entre les routeurs PE et P sur les interfaces de loopback au choix :
        - En réseau MESH : chaque routeur monte une session iBGP avec chaque autre routeur, soit $\frac{N(N-1)}{2} \approx O(N^2)$ sessions
        - En utilisant un Route Reflector (RR) pour réduire le nombre de sessions iBGP nécessaires à $N-1 \approx O(N)$ sessions.
        
2. **Activer MPLS et LDP**
    
    A. Activer MPLS et LDP sur les interfaces des routeurs
        
	B. Configurer le router-id LDP basé sur une loopback
        
3. **Configurer une VRF pour les CE**
    
    A. Créer et associer une VRF aux interfaces CE
        
    B. Configurer BGP VPN entre les PE

## Conclusion

MPLS et ses extensions, comme le VPN BGP/MPLS et le Segment Routing, jouent un rôle clé dans la gestion des réseaux modernes en offrant une QoS améliorée, une meilleure évolutivité et une plus grande flexibilité.

 