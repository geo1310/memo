###MODELE OSI :

---

* ###Couche 7
  * Nom : **application**
  * Rôle : RAS.
  * Rôle secondaire : RAS.
  * Matériel associé : le proxy.
---
* ###Couche 6
  * Nom : **presentation**
---  
* ###Couche 5
  * Nom : **session**
---
* ###Couche 4
  * Nom : **transport**
  * Rôle : gérer les connexions applicatives.
  * Rôle secondaire : garantir la connexion.
  * Matériel associé : RAS.
---
* ###Couche 3
  * Nom : **réseau**
  * Rôle : interconnecter les réseaux entre eux.
  * Rôle secondaire : fragmenter les paquets.
  * Matériel associé : le routeur.
  
La couche 3 va donc me permettre de joindre n'importe quel réseau sur Internet, en passant à travers d'autres réseaux.   
Ma connexion à une machine sur un autre réseau se fera à travers des réseaux, de proche en proche.

traceroute ( permet d'indiquer par quelles machines nous passons pour aller d'un point à un autre sur Internet ) -> Linux  
tracert -> Windows

L'adresse IP est l'adresse du réseau ET de la machine  
Elle est codée sur 4 octets (soit 32 bits, soit 2^32 possibilites) en IPV4  
Masque de Sous-reseau :  
* 00000000 -> 0
* 10000000 -> 128
* 11000000 -> 192
* 11100000 -> 224
* 11110000 -> 240
* 11111000 -> 248
* 11111100 -> 252
* 11111110 -> 254
* 11111111 -> 255

Ecriture CIDR : 
* 192.168.0.1/255.255.255.0 -> 192.168.0.1/24
* 192.168.0.1/255.255.240.0 -> 192.168.0.1/20

La première adresse d'une plage est l'adresse du réseau lui-même.  
La dernière adresse d'une plage est une adresse spéciale, l'adresse de broadcast.

RFC 79 ( Request For Comment) -> protocole IP  
RFC 1918 -> Cette RFC précise des plages d'adresses, soit des réseaux, qui ont une utilité particulière  
* 10.0.0.0/255.0.0.0
* 172.16.0.0/255.240.0.0
* 192.168.0.0/255.255.0.0


---
* ###Couche 2
  * Nom : **liaison de données**
  * Rôle : connecter les machines entre elles sur un réseau local.
  * Rôle secondaire : détecter les erreurs de transmission.
  * Matériel associé : le switch, ou commutateur.
  
L'adresse MAC est l'adresse d'une carte réseau.
Elle est unique au monde pour chaque carte.
Elle est codée sur 6 octets (soit 48 bits, soit 2^48 possibilites).  
3 premiers octets : achetes par le constructeur  
3 derniers octets : géré par le constructeur

ff:ff:ff:ff:ff:ff -> **adresse de broadcast**

##### TRAME ETHERNET :
**Adresse MAC DST --- Adresse MAC SRC --- Protocole de Couche 3 --- *Donnees* --- CRC**  
Entete Ethernet : 18 Octets  
Taille minimale : 64 Octets  
Taille maximale : 1518 Octets

##### SWITCH :
Analyse le contenu de la couche 2  
Cree une table MAC (Medium-Access-Control) ou table CAM (Content-Addressable-Memory) afin d'aiguiller les trames   
TTL : time to live  
La table MAC est effacée à chaque reboot du switch

**Un VLAN est la capacité de séparer des ports d'un switch dans des réseaux différents.**

Boucle de Commutation ( on offre 2 chemins differents pour une trame ) --> Tempete de Broadcasts

---
* ###Couche 1
  *  Nom : **physique**
  * Rôle : offrir un support de transmission pour la communication.
  * Rôle secondaire : RAS.
  * Matériel associé : le hub, ou concentrateur en français.


**Chaque couche est indépendante , chaque couche ne peut communiquer qu'avec une couche adjacente.**  
**Les couches réseau ( 1 à 4 ) offrent le service de communication à la couche applicative ( 7 )**

