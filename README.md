# check-point-2-

## exercice 1 : Modification IP client serveur

### Pratique

### Q.1.1:
PC Serveur : Adresse IP : 172.16.10.10 /24
PC Client :Adresse IP : 172.16.100.50/24
Comme on peux voir les VM se trouvent dans des sous-reseaux differentes, du coup le ping ne fonctionne pas probablement a ce probleme.
Pour réglé ce propbleme on doit faire quelque manipulation dans chaque vm, pour le PC Serveur il faut just verifier que les info soient correctes ( les roles de DHCP et DNS configure correctement et une adresse IP statique de 172.16.10.10/24) c'est chez le PC Client qu'on va devoir manipuler quelque  info. 
Il faut lui atribué une adresse IP statique dans le même sous-reseau que le PC Serveur, du style 172.16.10.30/24, en plus de ça il faut determiner le bon masque de sous-réseau  255.255.255.0 ou /24

### Q.1.2: 
Pour permettre le ping entre les machines en utilisant les noms d'hôtes au lieu des adresses IP, Cela implique généralement l'utilisation du DNS pour associer des noms d'hôtes à des adresses IP. 

#### Configurer le serveur DNS sur le serveur Windows 2022 (CheckPoint2-SRVWIN2022) :

On verifie  que le rôle DNS est correctement configuré sur le serveur.
je crée les enregistrements DNS correspondants pour les deux machine    
j'ajoute une entrée DNS statique pour le client dans la zone DNS du serveur.
j'ouvre la console DNS sur le serveur.
J'ajoute une nouvelle entrée pour le client avec son nom (CheckPoint2-CLIWIN10) et son adresse IP (par exemple, 172.16.10.30).nes.

#### Configurer les paramètres DNS sur le client Windows 10 (CheckPoint2-CLIWIN10) :

on va dans les paramètres réseau du client.
je m'assuer que le serveur DNS est configuré pour pointer vers l'adresse IP du serveur DNS dans ce cas, 172.16.10.10 .
j'exécute la commande **ipconfig /flushdns** dans une invite de commande sur le client pour vider le cache DNS, puis la commande **ping CheckPoint2-SRVWIN2022** pour tester le nom.

#### Vérification de la résolution de noms sur le client :

Ouvrez une invite de commande sur le client.
Essayez de pinguer le serveur en utilisant son nom d'hôte : ping WINSERV.

### Q.1.3 :
Pour configurer le client en mode DHCP:
1. **Client Windows 10 (CheckPoint2-CLIWIN10) :**
   - J'ouvre les paramètres réseau du client.
   - Modifie la configuration IP pour obtenir l'adresse IP automatiquement (mode DHCP)
2. **Vérification du paramétrage DHCP sur le serveur :**
   - J'accéde au serveur Windows 2022 (CheckPoint2-SRVWIN2022).
   - j'ouvre le Gestionnaire de serveur.
   - je vérifie que le rôle DHCP est installé et configuré.
   - la plage DHCP configurée sur le serveur.
### Q.1.4 :
Il est possible pour le client peut avoir l'adresse IP 172.16.10.15 en DHCP 
Il faut just modifier la plage d'exclusion par exemple de 172.16.10.1 à 172.16.10.14 et en excluant en plus 172.16.10.20.
Come ca quand on lance la comande "ipconfig /release puis ipconfig /renew" sur le client on poura récupérer cette IP.

## Exercice 2 Débogage de script PowerShell

### Q.2.1 
Pour que le script AddLocalUsers.ps1 s'éxecut il faut changer le path 

Start-Process -FilePath "powershell.exe" -ArgumentList "C:\Scripts\addlocalusers.ps1" -Verb RunAs  -WindowStyle Hidden


### Q.2.2 










