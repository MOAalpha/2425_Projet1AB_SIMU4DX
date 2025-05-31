# 2425_Projet1AB_SIMU4DX
A super nice projet

 L'objectif de ce projet est de reconstituer un simulateur de voiture permettant de ressentir les vraies sensations de conduite, avec un frein à retour de force et 4 pieds movibles.
 
 On s'inspire du projet : https://github.com/ChrGri/DIY-Sim-Racing-FFB-Pedal

 La base ayant déjà été faite, on souhaite modifier le châssis et les pédales de frein afin d'augmenter la sensation de conduire une véritable voiture.


INSTALLER ET FAIRE FONCTIONNER SIMHUB

Tout d'abord, il vous faut installer SimHub sur votre ordinateur.

Cliquez sur "Add/Remove/Features" dans le menu de gauche.




![image](https://github.com/user-attachments/assets/c2bd8791-c2e5-4f3c-8426-ebb97fda86bb)



Cliquez sur "addons motion" pour activer le contrôle de mouvement.


![image](https://github.com/user-attachments/assets/2177430b-5e06-4e92-ad03-dfbeabd060a6)


Normalement, "Motion" apparaît sur SimHub (icône avec un siège).

![image](https://github.com/user-attachments/assets/9252f6bd-9b52-4ece-b539-9ad6005d7054)


Cliquez sur "Let's test it".

![image](https://github.com/user-attachments/assets/53154ed7-7f8b-4d71-a4f2-b71ffb7f00d0)



Choisissez comme configuration "3 DOFs, 2 fronts, 1 rear".

![image](https://github.com/user-attachments/assets/6c5ce84f-c5c0-4ff1-a6cc-c8b4d78fd7ce)


Cliquez sur "Add new controller".

![image](https://github.com/user-attachments/assets/fbc449f2-f812-4ac5-b156-56fbe5863f7e)

Choisissez "generic serial output"

![image](https://github.com/user-attachments/assets/e425af49-87b0-4b88-b149-83f58768f226)



Dans "Connexion", assurez-vous que votre carte est connectée sur le bon COM.

![image](https://github.com/user-attachments/assets/43b799e0-e77e-445a-9a5c-8c68d7682cab)


Vous pouvez régler la dimension de la plateforme ce qui vous permet d'obtenir la limitation des axes.

![image](https://github.com/user-attachments/assets/baffeaf2-2704-48fb-8d42-14defb698d94)


Cliquez ensuite sur "Edit serial commands setting".

![image](https://github.com/user-attachments/assets/869ad28e-5f9e-4e56-8b77-8a4bd7540512)


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


![image](https://github.com/user-attachments/assets/e0bbc29b-9cac-4638-b6fc-d3567d9ba844)

![image](https://github.com/user-attachments/assets/ac694552-e4a9-4869-9566-736214831ce8)

![image](https://github.com/user-attachments/assets/a32522a1-1f9c-4bab-8769-d039826b95f9)



Cliquez sur "Edit axis assignment". Vous n'avez que trois axes (rear center, front left corner, front right corner). Vous pouvez tester l'envoi des données dans cet onglet.

![image](https://github.com/user-attachments/assets/dce867b8-0fe0-401d-9f64-588b6ad7e091)


LIRE LES DONNÉES DE SIMHUB

Méthode avec deux STM32 :

Nous avons utilisé cette méthode au début de notre projet, car nous n'avions pas encore terminé l'impression des cartes.

Si vous disposez de deux microcontrôleurs STM32 ayant l'UART 1 et 2, il vous suffit de relier les ports RX, TX et GND de vos deux cartes STM32.

Par la suite, il vous faut installer STM32CubeIDE et PuTTY. Activez l'UART 1 et 2. Puis, ajoutez cette ligne de code qui vous permettra de lire les données.

![image](https://github.com/user-attachments/assets/caff48cc-a6ea-41e2-9633-f21c088fef22)


Une fois que le code est chargé dans les deux cartes, il faut par la suite ouvrir PuTTY et SimHub.

Dans SimHub : Il faut revenir dans l'onglet "Edit axis assignment" et cliquer sur le bouton de test pour que SimHub envoie les données.

Dans PuTTY : Cliquez sur "Connexion type" "Serial", puis choisissez le COM correspondant à votre carte et sélectionnez 115200 bauds.

![image](https://github.com/user-attachments/assets/7247ba2e-00cc-48d1-927d-c063c3a5bd46)


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





