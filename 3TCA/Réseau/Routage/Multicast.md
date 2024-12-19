
## Pourquoi utiliser le multicast ?

- **Avantages :**
    
    - Envoyer les mêmes données à plusieurs récepteurs en une seule transmission.
        
    - Moins coûteux que l’unicast pour des groupes nombreux.
        
    - Moins de gaspillage que le broadcast pour des petits groupes.
        
- **Applications principales :**
    
    - Streaming vidéo (IPTV).
        
    - Mise à jour d’images systèmes.
        
    - Vidéoconférences, jeux multijoueurs.
        
    - Diffusion de données boursières.
        
    - Mises à jour de firmware IoT (FUOTA).
        

---

## Adresses multicast

### En IPv4 :

- **Classe D** : Plage 224.0.0.0/4.
    
- **Cas particuliers :**
    
    - 224.0.0.x : Utilisation locale (TTL = 1, pas routé sur Internet).
        
    - 224.0.1.x : Contrôle inter-réseau, ex. NTP (224.0.1.1).
        

### En IPv6 :

- Adresses bien connues vs. transitoires.
    
- Exemple : Groupe NTP
    
    - FF02::101 : Serveurs NTP sur le même lien.
        
    - FF0E::101 : Serveurs NTP sur Internet.
        

---

## Protocoles multicast

### Gestion des groupes (Host-Router) :

- **IPv4 : IGMP** (Internet Group Management Protocol).
    
- **IPv6 : MLD** (Multicast Listener Discovery - encapsulé dans ICMPv6)
    

#### IGMP/MLD :

- Types de messages :
    
    - **Query** : Interroger les abonnements multicast.
        
    - **Report** : Rejoindre un groupe.
        
    - **Done** : Quitter un groupe.
        

---

## Routage multicast

### Objectif :

Créer un ou plusieurs arbres reliant les routeurs ayant des membres du groupe.

### Types d’arbres :

- **Arbre basé sur la source** :
    
    - Exemple : Un service de streaming vidéo où chaque serveur source diffuse un flux unique aux abonnés. Chaque source construit un arbre individuel reliant uniquement ses abonnés via le chemin le plus court.
        
    - Arbre unique par source -> Receveurs.
        
    - Basé sur le **Reverse Path Forwarding** (RPF - basé sur les routes unicast).
        
    - Coût élevé à maintenir.
        
- **Arbre partagé** :
    
    - Exemple : Une vidéoconférence où tous les participants partagent un même canal multicast. Un point central, appelé Rendezvous Point (RP), gère la diffusion des données pour tous les membres du groupe.
        
    - Arbre unique pour tous les membres du groupe.
        
    - Basé sur un **rendezvous point (RP)** central.
        

---

## Protocoles de routage multicast

- **DVMRP** (Distance Vector Multicast Routing Protocol).
    
- **MOSPF** (Multicast OSPF).
    
- **PIM** (Protocol-Independent Multicast) :
    
    - **Dense mode** :
        
        - Utilise le flood-and-prune.
	        - Flood => Inonde le réseau de paquets pour trouver toutes les routes
	        - Prune => Un routeur sans client supprime sa route, un routeur qui en reçoit plusieurs avec des métriques différentes ne garde que la plus courte (prune les autres)
	        - Assert => Un routeur qui reçoit plusieurs routes de même poids en choisit une arbitrairement
            
        - Adapté aux réseaux avec une forte densité de membres.
            
    - **Sparse mode** :
        
        - Basé sur des RPs.
            
        - Adapté aux réseaux avec peu de membres dispersés.
            

---

## Déploiements multicast

- IPTV dans les hôtels.
    
- Mise à jour des systèmes sur campus ou réseaux d'entreprise.
    
- Diffusion de radio (BBC, CBC).
    
- Distribution des données financières (Thomson Reuters, Bloomberg).
    
- FUOTA pour réseaux IoT.
    

---

## Définition : NTP

- **NTP (Network Time Protocol - serveur de temps)** : Protocole permettant de synchroniser l’heure entre différents dispositifs sur un réseau. Il utilise des adresses multicast pour synchroniser efficacement un grand nombre de clients.
    

---

## Résumé

Le multicast réduit le coût et l'utilisation de bande passante pour les communications multi-récepteurs. Cependant, il introduit une complexité protocolaire et des défis de sécurité et de scalabilité.