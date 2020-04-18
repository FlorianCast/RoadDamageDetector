# RoadDamageDetector
Projet de deepLearning EISTI ING3

Ce projet a été réalisé sous la forme d'un notebook (avec Jupyter lab).

L'objectif de ce project est de construire un modèle de détection de l'état des routes (détection des dommages : fissures, nids de poules, ...).

Les classes à détecter sont :


- D00 : Fissure, longitudinale.

- D01 : Fissure, longitudinale, joint de construction.

- D10 : Fissure, latérale.

- D11 : Fissure, latérale, joint de construction.

- D20 : Faïençage (lézardes).

- D40 : Ornière, bosse, nid-de-poule, séparation.

- D43 : Passage piéton effacée.

- D44 : Ligne continue effacée.


J'ai décidé d'essayer de réaliser ce réseau en utilisant la technique de transfert learning. Je suis partit du réseau Mask_RCNN pré-entraîné sur le dataset __COCO__, et ai entraîné les quatres dernières couches avec le dataset __RoadDamageDataset__ purgé des images contenant des classes non-incluses dans la liste donnée (càd la classe D30). 

-------------------------------------------------------------

## Phases de test
Cinq phases de test ont été faîtes: 

Les deux premières step = 140 / epoch = 5 / batch_size = 1 / NON ABOUTIES : 

- La première à révélé le problème d'annotation, où la classe _D30_ apparaîssait alors qu'elle n'était pas référencée.

- Concernant la seconde, je me suis trompé de touche et ai relancé sans avoir sauvegardé...

Troisième phase : step = 150 / epoch = 4 / batch_size = 1 / 6h de calcul.
Les détections sont moyennes, on obtient des détections parfois complètement décalées et le taux de confiance est en général compris entre 0.4 et 0.6

Quatrième phase : step = 300 / epoch = 7 / batch_size = 1 / NON ABOUTIE.
Problème d'enregistrement du chkpnt à la fin de la première epoch. Je ne sais pas pourquoi.

Cinquième phase : step = 250 / epoch = 6 / batch_size = 1 / 14h de calcul.
Les détections sont moins bonnes que pour la phase 3. Cela est dû à un mauvais réglage du _detection minimum confidance_. Je l'avais ici réglé à 0.5 au lieu de 0.9. Le modèle a donc appris en partie sur des détections fausses ce qui expliquerait les résultats médiocres.

Sixième phase : step = 300 / epoch = 7 / batch_size = 1 / EN COURS

-------------------------------------------------------------

La suite de ce README sera rédigée demain Dimanche 19 mai.

-------------------------------------------------------------


## Auteur 

Florian CASTAIGNEDE
