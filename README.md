capture 1 — Vérification des interfaces réseau de la VM:

Cette capture montre l’exécution de la commande ip a dans le terminal Linux de la machine virtuelle Mobexler.
Cette commande permet d’afficher toutes les interfaces réseau disponibles ainsi que leurs adresses IP et leur état.

On peut observer :

lo (loopback) : interface locale utilisée par le système pour communiquer avec lui-même (127.0.0.1).
enp0s8 : interface réseau inactive (NO-CARRIER), probablement configurée mais non connectée.
enp0s17 : interface réseau active (UP) utilisée pour la connexion Internet.
L’adresse IP attribuée à la VM est 10.0.2.15/24, ce qui indique que la machine utilise un réseau privé de type NAT fourni par VirtualBox.

Cette étape permet de vérifier que la machine virtuelle possède bien une connectivité réseau avant de commencer les tests Android ou réseau.

Capture 2 — Vérification de la connectivité réseau

Cette capture montre plusieurs commandes réseau utilisées pour tester la connexion Internet de la machine virtuelle.

1. Commande ip route

Elle affiche la table de routage de la VM :

La passerelle par défaut est 10.0.2.2
Le trafic réseau sort par l’interface enp0s17
Le réseau utilisé est 10.0.2.0/24

Cela confirme que la VM utilise correctement le mode réseau NAT.
3-capture 3:
Contenu : Terminal Mobexler

Commande ip route : affiche la table de routage avec la passerelle par défaut 10.0.2.2 et l’interface enp0s17.

Commande ping -c 2 8.8.8.8 : réussite (2 paquets reçus, temps ~33–45 ms).

Commande ping -c 2 google.com : résolution en 142.251.142.142 et réponse (2 paquets reçus, temps ~26–27 ms).
→ Conclusion : La connectivité réseau (IP et DNS) fonctionne.
4-capture 4:
Suite des commandes ping (résultats similaires à la capture précédente).

Fenêtre VirtualBox intitulée Prendre un instantané de la machine virtuelle :

Nom : CLEAN_BASELINE_TP1

Description : "import OK, réseau OK, boot OK, pret ABD"
→ Conclusion : L’utilisateur crée un point de restauration propre avant de travailler sur ADB.
5-capture 5:
Contenu : Fenêtre Oracle VirtualBox (machine Mobexler)

Menu Périphériques > USB déroulé.

Plusieurs périphériques listés :

Intel Corp. [0010]

Acer, Inc. [5422] (avec détails : VID 5986, PID 2113, révision 5422, état “Occupé”)

Alcor Micro Corp. AU9540 Smartcard Reader [0120]

Logo MOBEXLER – FOR HACKERS | BY HACKERS.
→ Conclusion : Gestion des périphériques USB dans la VM (préparation pour passer un appareil Android à ADB).
6-capture:
Contenu : Terminal Mobexler
adb version → version 1.0.39 installée.

adb devices → aucune liste, mais message d’erreur :
Ba5a0df4 no permissions (user in plugdev group; are your udev rules wrong?)
→ Conclusion : ADB reconnaît un appareil (ID Ba5a0df4) mais l’utilisateur n’a pas les droits d’accès (problème de règles udev ou de groupe).
7-capture :
Contenu : Terminal Mobexler

adb version → version 1.0.39 installée.

adb devices → aucune liste, mais message d’erreur :
Ba5a0df4 no permissions (user in plugdev group; are your udev rules wrong?)
→ Conclusion : ADB reconnaît un appareil (ID Ba5a0df4) mais l’utilisateur n’a pas les droits d’accès (problème de règles udev ou de groupe).


