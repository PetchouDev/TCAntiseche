# IPV6

## 1. Format
### 1.1. Généralités
- 128 bits
- Divisée en 8 groupes de 16 bits
- Chaque groupe est représenté par 4 chiffres hexadécimaux
- Chaque groupe est séparé par un `:`
- Les groupes de 0 consécutifs peuvent être omis et remplacés par `::` (1 seule fois par adresse)

### 1.2. Exemple
- `2001:0db8:0000:0042:0000:8a2e:0370:7334`
- `2001:db8::42:0:8a2e:370:7334`
- `2001::1234`

### 1.3. Addressage d'une interface
- Chaque interface réseau peut avoir plusieurs adresses IPv6 parmis :
    - **Adresse de lien local (LLA)**: adresse de l'interface (`fe80::/10`) $\rightarrow$ paquets non routés
    - **Adresse locale unique (ULA)**: adresse de l'interface (`fc00::/7`) $\rightarrow$ paquets routés uniquement à travers les sous-réseaux locaux, pas sur internet
    - **Adresse globale**: adresse routable sur internet (permanente ou temporaire)
    - **Adresse anycast**: adresse partagée par plusieurs interfaces ou appareils (utilisée pour la redondance)
    - **Adresse multicast**: adresse identifiant un groupe de machines (`ff00::/8`, fonctionne comme un abonnement)

    En sachant qu'une interface peut avoir plusieurs adresses de chaque type.

## 2. Types d'adresses
### 2.1. Unicast
- Identifie une interface réseau
- Peut être routée
- 3 types:
  - **Global unicast**: routable sur internet
  - **Link-local**: utilisée pour la communication sur un réseau local
  - **Unique local**: utilisée pour la communication sur un réseau local, mais pas routable sur internet

### 2.2. Multicast
#### 2.2.1. Usage
- Identifie un groupe de machines
- Les paquets envoyés à une adresse multicast sont reçus par toutes les machines du groupe

#### 2.2.2. Plage d'adresses
**Structure d'une adresse multicast**: `FF<flags><scope>::<group>`
- flags: `0` pour les adresses permanentes, `1` pour les adresses dynamiques
- scope: portée de l'adresse (principaux ci-dessous)
    - `1`: noeud local (loopback)
    - `2`: lien local (LAN)      |
    - `5`: site local (LAN)      |  De plus en plus large
    - `8`: organisation (LAN)    V
    - `E`: global (internet)
- group: identifiant du groupe
    - `1`: tous les noeuds (compatibles IPv6 - équivalent du broadcast)
    - `2`: tous les routeurs
    - `FB`: multicast mDNSv6 

### 2.3. Anycast
- Identifie un groupe de machines
- Les paquets envoyés à une adresse anycast sont reçus par la machine la plus proche du groupe
- C'est une addresse IPv6 unicast, mais partagée par plusieurs machines
- Utilisé pour la redondance

## 3. Configuration
IPv6 peut être configuré de 3 manières:
- Manuelle : Adresse et paramètres configurés statiquement.
- Auto-configuration sans état : Adresse générée à partir du préfixe réseau et de l'adresse MAC, sans DHCPv6.
- Auto-configuration avec état : Adresse attribuée par un serveur DHCPv6, qui gère aussi d'autres paramètres.

## 4. ICMPv6
### 4.1. Généralités
- ICMPv6 est utilisé pour le diagnostic et la gestion des erreurs
- Les messages ICMPv6 sont encapsulés dans des paquets IPv6
- Les messages ICMPv6 sont identifiés par un type et un code

### 4.2. Types de messages
- **Type 1**: Destination Unreachable
- **Type 2**: Packet Too Big
- **Type 3**: Time Exceeded
- **Type 4**: Parameter Problem
- **Type 128**: Echo Request
- **Type 129**: Echo Reply
- **Type 133**: Router Solicitation
- **Type 134**: Router Advertisement
- **Type 135**: Neighbor Solicitation
- **Type 136**: Neighbor Advertisement


## 5. Fragmentation
- La fragmentation est effectuée par l'émetteur, pas par les routeurs intermédiaires (contrairement à IPv4)
- Les routeurs intermédiaires peuvent envoyer un message ICMPv6 "Packet Too Big" si le paquet est trop gros

## 6. Transition IPv4 -> IPv6
- **Dual stack**: Les machines supportent IPv4 et IPv6
- **Tunneling**: Encapsulation d'un paquet IPv6 dans un paquet IPv4 pour le transport si le paquet passe par un réseau IPv4-only
- **Translation**: Traduction d'un paquet IPv6 en IPv4 et vice-versa

## 7. Liens utiles
- [IPv6 multicast addresses](https://www.iana.org/assignments/ipv6-multicast-addresses/ipv6-multicast-addresses.xhtml)










