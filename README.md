# 2425_Projet1AB_SIMU4DX
A super nice projet

 L'objectif de ce projet est de reconstituer un simulateur de voiture permettant de ressentir les vraies sensations de conduite, avec un frein à retour de force et 4 pieds movibles.
 
 On s'inspire du projet : https://github.com/ChrGri/DIY-Sim-Racing-FFB-Pedal

 La base ayant déjà été faite, on souhaite modifier le châssis et les pédales de frein afin d'augmenter la sensation de conduire une véritable voiture.

 On a tout d'abord écrit un code qui récupère les données du jeu. Notre travail est simplifié par l'utilisation de SimHub, un logiciel qui récupère pour nous les données du jeu Assetto Corsa.
 INSTALLER ET FAIRE FONCTIONNER SIMHUB
 1) Tout d'abord il te faut installer simhub sur ton ordinateur.
 2) clique sur add/remove/features
 3) clique sur addons motion pour activer le motion contrôle
 4) normalement motion apparait sur simhub (icone avec un siège)
 5) clique sur let's test it
 6) configure le port en serial pour la carte
 7) choisi comme configuration 3 DOFs, 2 fronts, 1 rear
 8) clique sur output setting
 9) Dans connexion assure toi que ta carte est connecté sur le bon COM.
 10) clique ensuite sur edit serial commands setting.
Tu vois dans cette onglet le type de donnée que simhub t'envoie, ce sont deux angles (le roll et le pitch) et une translation selon l'axe horizontal qui est appelé heave.
 11) C'est dans cette onglet que tu peut régler la forme des données que tu veux envoyé:
     Baudrate:115000
     Data bits: 8
     Stop bits: 1
     Parity: none

     Number of controlled axis: 3
     Axis output format: decimal
     Axis resolution: 8 bits (donc de 0 à 255)
     Motion update commands: <axis1> <axis2> <axis3> (à copier coller tu peux aussi cliquer sur les ... pour les ajouter)
     12) clique sur Edit axis assignment. On a que trois axes (rear center, front leaft corner, front right corner). tu peux tester l'envoie des données dans cette onglet.
     
     
     
     
     


     
     
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





