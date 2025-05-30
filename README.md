# 2425_Projet1AB_SIMU4DX
A super nice projet

 L'objectif de ce projet est de reconstituer un simulateur de voiture permettant de ressentir les vraies sensations de conduite, avec un frein à retour de force et 4 pieds movibles.
 
 On s'inspire du projet : https://github.com/ChrGri/DIY-Sim-Racing-FFB-Pedal

 La base ayant déjà été faite, on souhaite modifier le châssis et les pédales de frein afin d'augmenter la sensation de conduire une véritable voiture.


INSTALLER ET FAIRE FONCTIONNER SIMHUB

Tout d'abord, il vous faut installer SimHub sur votre ordinateur.

Cliquez sur "Add/Remove/Features".

Cliquez sur "addons motion" pour activer le contrôle de mouvement.

Normalement, "Motion" apparaît sur SimHub (icône avec un siège).

Cliquez sur "Let's test it".

Configurez le port en "Serial" pour la carte.

Choisissez comme configuration "3 DOFs, 2 fronts, 1 rear".

Cliquez sur "Output Setting".

Dans "Connexion", assurez-vous que votre carte est connectée sur le bon COM.

Cliquez ensuite sur "Edit serial commands setting".
Dans cet onglet, vous voyez le type de données que SimHub vous envoie : ce sont deux angles (le roll et le pitch) et une translation selon l'axe horizontal qui est appelé "heave".

C'est dans cet onglet que vous pouvez régler la forme des données que vous souhaitez envoyer :

Baudrate: 115000

Data bits: 8

Stop bits: 1

Parity: none

Number of controlled axis: 3

Axis output format: decimal

Axis resolution: 8 bits (donc de 0 à 255)

Motion update commands: <axis1> <axis2> <axis3> (à copier-coller ; vous pouvez aussi cliquer sur les "..." pour les ajouter)

Cliquez sur "Edit axis assignment". Vous n'avez que trois axes (rear center, front left corner, front right corner). Vous pouvez tester l'envoi des données dans cet onglet.

LIRE LES DONNÉES DE SIMHUB

Méthode avec deux STM32 :

Nous avons utilisé cette méthode au début de notre projet, car nous n'avions pas encore terminé l'impression des cartes.

Si vous disposez de deux microcontrôleurs STM32 ayant l'UART 1 et 2, il vous suffit de relier les ports RX, TX et GND de vos deux cartes STM32.

Par la suite, il vous faut installer STM32CubeIDE et PuTTY. Activez l'UART 1 et 2. Puis, ajoutez cette ligne de code qui vous permettra de lire les données.

Une fois que le code est chargé dans les deux cartes, il faut par la suite ouvrir PuTTY et SimHub.

Dans SimHub : Il faut revenir dans l'onglet "Edit axis assignment" et cliquer sur le bouton de test pour que SimHub envoie les données.

Dans PuTTY : Cliquez sur "Connexion type" "Serial", puis choisissez le COM correspondant à votre carte et sélectionnez 115200 bauds.

Méthode avec le hub USB :

Cette méthode permet de tester le fonctionnement du hub USB.

La carte qui reçoit les données est le hub USB dans notre schéma d'architecture ; elle reçoit les données via le port USB. Il faut relier l'un des ports USB du hub USB dédié aux autres cartes vers le PC. Ensuite, vous pourrez lire les données envoyées avec PuTTY. Malheureusement, nous n'avons pas pu le faire, car nous avons rencontré un problème avec le timer de notre microcontrôleur.
    
     
 On a effectué une PCB de communication : 
 ![image](https://github.com/user-attachments/assets/e1604141-4f96-4855-8969-7bf1ef45cf7b)
 Elle a pour rôle la transmission des infos du jeu prélevés à l'aide de simhub aux 4 moteurs qui font bouger le châssis.

 NB : Le circuit semble correct (On a bien 5V en entrée du régulateur et 3.3V en sortie) MAIS son horloge interne ne fonctionne pas.

 On a effectué une PCB Moteur pour chacun des 4 moteurs : 
![image](https://github.com/user-attachments/assets/2d4a8cba-be1c-470e-84e4-8034b3ad4bc2)
Celle-ci se charge d'indiquer au driver à quel point il faut bouger le vérin.

A suivre : 

Tester la PCB du STEPPER pour commander la pédale de frein avec retour de force. \
![image](https://github.com/user-attachments/assets/7b19e395-d032-4816-b796-bd4b78a2df2d) \
Assembler le tout. \
Profiter des sensations. 





