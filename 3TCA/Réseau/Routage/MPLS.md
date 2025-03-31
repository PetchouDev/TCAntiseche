## Introduction

Le protocole **MPLS** (**M**ulti**p**rotocol **L**abel **S**witching) est une technologie de commutation de paquets qui améliore l'efficacité et la flexibilité du routage dans les réseaux IP. Il est souvent utilisé par les fournisseurs de services pour assurer une meilleure qualité de service (QoS) et faciliter la mise en œuvre de VPN sécurisés.

## Architecture MPLS

MPLS repose sur le concept d'ajout d'un label aux paquets de données pour leur acheminement. Il est composé de plusieurs éléments :

- **Label Edge Router (LER)** : routeurs aux extrémités du réseau MPLS qui attribuent et suppriment les labels.
    
- **Label Switch Router (LSR)** : routeurs intermédiaires qui commutent les paquets en fonction des labels MPLS.
    
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

- **Data Plane** : Responsable de la transmission des paquets. Dans un réseau MPLS, les routeurs utilisent les labels MPLS pour transférer les paquets, évitant ainsi l’analyse des en-têtes IP.
    
- **Control Plane** : Gère l'établissement des chemins et l'allocation des labels. Il utilise des protocoles comme LDP ou BGP pour échanger des informations de routage et de labels entre les routeurs.
    

## Label Distribution Protocol (LDP)

LDP est le protocole principal utilisé pour distribuer les labels MPLS entre les routeurs.

- **Fonctionnement** :
    
    - Les routeurs établissent une session LDP entre eux.
        
    - Ils échangent des messages pour annoncer les correspondances entre les labels et les préfixes IP.
        
    - Ces labels sont utilisés par les LSR (Label Switch Routers) pour commuter les paquets en fonction du LSP (Label Switching Path).
        
- **Avantages** : Simple à déployer et compatible avec le routage IP classique.
    
- **Inconvénients** : Ne permet pas une gestion avancée de la QoS comme RSVP-TE.
    

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

