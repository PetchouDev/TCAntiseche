# RIP (Routing Information Protocol) - Cheat Sheet

## 1. **Qu'est-ce que RIP ?**
- **RIP (Routing Information Protocol)** : Un protocole de routage de niveau 3 utilisé pour échanger des informations de routage entre routeurs.
- Basé sur l'algorithme de vecteur de distance.
- Fonctionne sur UDP (port 520).

---

## 2. **Caractéristiques principales de RIP**
- **Distance maximale (hop count)** : Limité à 15 sauts pour éviter les boucles infinies.
- **Mises à jour périodiques** : Les routeurs échangent leurs tables toutes les 30 secondes.
- **Simple et facile à configurer** : Adapté pour de petits réseaux.

---

## 3. **Versions de RIP**
- **RIP v1** :
  - Protocole sans classe (classful), ne supporte pas le CIDR.
  - Envoi les mises à jour en diffusion (*broadcast*).
- **RIP v2** :
  - Protocole avec classe (classless), supporte le CIDR et le VLSM.
  - Utilise des adresses multicast (224.0.0.9) pour réduire le trafic inutile.
- **RIPng** :
  - Extension pour IPv6.

---

## 4. **Messages RIP**
- **Request** : Demande d'informations de routage.
- **Response** : Envoi de la table de routage mise à jour.

### Format d'un message RIP :
| Champ           | Taille   | Description                        |
|-----------------|----------|------------------------------------|
| Commande        | 1 octet  | Request (1) ou Response (2).       |
| Version         | 1 octet  | Version RIP (1, 2 ou 6 pour RIPng).|
| Adresse famille | 2 octets | Indique le protocole réseau.       |
| Adresse IP      | 4 octets | Adresse du réseau cible.           |
| Metric          | 4 octets | Nombre de sauts vers le réseau.    |

---

## 5. **Problèmes communs et solutions**
### **Boucles de routage**
- RIP peut subir des boucles de routage dues à des mises à jour retardées.

#### **Techniques de prévention :**
1. **Split Horizon** : N’envoie pas d'informations de routage sur l'interface par laquelle elles sont reçues.
2. **Route Poisoning** : Définit la métrique à 16 (infinie) pour indiquer qu'une route est inaccessible.
3. **Hold-down Timer** : Empêche l'acceptation de mises à jour pour une route défaillante pendant un certain temps.
4. **Triggered Updates** : Envoie immédiatement des mises à jour lorsque des changements se produisent, plutôt que d’attendre l’intervalle périodique.
5. **Distance maximale (hop count)** : Limite les sauts à 15 pour éviter des boucles infinies.

### **Spécifications de convergence**
- **Temps de convergence lent** :
  - Les mises à jour RIP se produisent toutes les 30 secondes, ce qui ralentit la détection et la correction des changements.
  - L’utilisation de techniques comme les **triggered updates** améliore la convergence.
- **Propagation des routes** :
  - Les informations de routage sont propagées progressivement de routeur en routeur.

---

## 6. **Commandes utiles**
### Configuration RIP sur un routeur Cisco :
Note: Les interfaces doivent être configurées avec des adresses IPv4 avant d'utiliser RIP. RIP v1 utilisera le masque par défaut (classful), tandis que RIP v2 respectera les masques configurés sur les interfaces.
```bash
router rip
 version 2
 network 192.168.1.0
 no auto-summary
```
- `router rip` : Active le protocole RIP.
- `version 2` : Active RIP version 2 (classless).
- `network <network_address>` : Définit le réseau IPv4 à inclure dans RIP. Pour RIP v1, utilise les masques par défaut.
- `no auto-summary` : Désactive le résumé automatique des routes (recommandé pour éviter les erreurs avec des sous-réseaux).

### Redistribution des routes connectées dans RIP :
```bash
router rip
 redistribute connected
 network <network_address>
```
- `redistribute connected` : Redistribue les routes connectées directement dans RIP.

### Configuration RIPng (IPv6) sur un routeur Cisco :
Note: L'interface doit déjà avoir été configurée en IPv6.
```bash
ipv6 router rip <protocol_id>
 redistribute connected
interface <interface_name> <number>
 ipv6 rip <protocol_id> enable
```
- `ipv6 router rip <protocol_id>` : Configure RIPng avec un identifiant spécifique.
- `redistribute connected` : Redistribue les routes connectées directement dans RIPng.
- `interface` : Sélectionne l'interface où RIPng sera activé.
- `ipv6 rip <protocol_id> enable` : Active RIPng sur l'interface.

### Vérification de l'état RIP :
```bash
show ip protocols       # Affiche les protocoles actifs
show ip rip database    # Montre la base de données RIP
show ip route rip       # Affiche les routes apprises via RIP
show ipv6 rip           # Vérifie la configuration RIPng
```

---

## 7. **Ressources**
- [RFC 1058 - RIP v1](https://www.rfc-editor.org/rfc/rfc1058)
- [RFC 2453 - RIP v2](https://www.rfc-editor.org/rfc/rfc2453)
- [Cisco - Configuration de RIP](https://www.cisco.com/)
