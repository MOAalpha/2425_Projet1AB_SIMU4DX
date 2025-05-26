Séance 1 : Choix du projet, des groupes et respos, et création du git \
Séance 2 : Diagramme d'architecture, cahier des charges et répartition des tâches (3 types de PCB à faire : Moteur, communication et frein + recherche sur le logiciel de simu)
(Entre temps PCB Moteur terminé)

Séance 3 : Suite du design des PCB / en parallèle avancée sur le logiciel de simulation 


Séance 4 : Fin Shéma PCB Frein, Fin routage et envoi PCB COM \
Séance 5 : Première tentative de routage ... \
Séance 6 : PCB Frein en cours de soudure, Début soudure PCB COM \
Séance 7 : Fin soudure PCB COM (ajout switch et USB2.0 ...), test de la carte PCB COM => on a bien les 5V en entrée du régulateur et les 3.3V en sortie, test sur la réception des données \
Séance 8 : Test PCB COM \
            Etude de la transmission de données
            Voici un schéma simplifié de la transmission de données du jeu au mouvement de la voiture.
           ![WhatsApp Image 2025-05-12 à 13 50 35_ca1e2650](https://github.com/user-attachments/assets/4e729ca3-66ad-4e35-be5f-7ef5a2bbeb28)
           Le PC renvoie la position des vérins selon les données du jeu. Il y a une première STM qui va donc lire ces données et les envoyer à d'autres STM gérant les driver des moteurs et faire bouger les vérins. /
           Les données renvoyées par le logiciel sont 3 blocs de 8 bits correspondant à la valeur selon 3 axes.
           On prend comme niveau de base 127 (valeur du milieu). 
           Dans les grandes lignes, cela ressemble à ça : 
           ![WhatsApp Image 2025-05-12 à 14 01 50_deecc097](https://github.com/user-attachments/assets/6c9019bb-b929-43b1-aeed-a47685a364b4)

           
           

Séance 9 : Toujours test de la PCB com, on détecte un problème d'horloge. En utilisant une boucle vide, l'allumage de la LED fonctionne => c'est donc un problème d'horloge interne.
Le mode debugger montre que la variable uwTick ne s'incrémente pas. Après plusieurs recherches sur différents forums et requêtes à différentes IA, je n'ai toujours pas trouvé la solution. Ceci m'embête car son rôle est de transmettre à intervalle régulier les infos aux PCB moteurs. Je n'ai donc pas pu m'occuper de la PCB frein.\
Séance 10 : Présentation du projet ?  \
