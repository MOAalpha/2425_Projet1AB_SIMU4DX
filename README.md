# 2425_Projet1AB_SIMU4DX
A super nice projet

 L'objectif de ce projet est de reconstituer un simulateur de voiture permettant de ressentir les vraies sensations de conduite, avec un frein à retour de force et 4 pieds movibles.
 
 On s'inspire du projet : https://github.com/ChrGri/DIY-Sim-Racing-FFB-Pedal

 La base ayant déjà été faite, on souhaite modifier le châssis et les pédales de frein afin d'augmenter la sensation de conduire une véritable voiture.

 On a tout d'abord écrit un code qui récupère les données du jeu. Notre travail est simplifié par l'utilisation de SimHub, un logiciel qui récupère pour nous les données du jeu Assetto Corsa.

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





