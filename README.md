# PROJET DEEPLEARNING : ROAD DAMAGE INSPECTOR


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

Les deux premières : step = 140 / epoch = 5 / batch_size = 1 / NON ABOUTIES : 

- La première à révélé le problème d'annotation, où la classe _D30_ apparaîssait alors qu'elle n'était pas référencée.

- Concernant la seconde, je me suis trompé de touche et ai relancé sans avoir sauvegardé...

Troisième phase : step = 150 / epoch = 4 / batch_size = 1 / 6h de calcul.
Les détections sont moyennes, on obtient des détections parfois complètement décalées et le taux de confiance est en général compris entre 0.4 et 0.6

Quatrième phase : step = 300 / epoch = 7 / batch_size = 1 / NON ABOUTIE.
Problème d'enregistrement du chkpnt à la fin de la première epoch. Je ne sais pas pourquoi.

Cinquième phase : step = 250 / epoch = 6 / batch_size = 1 / 14h de calcul.
Les détections sont moins bonnes que pour la phase 3. Cela est dû à un mauvais réglage du _detection minimum confidance_. Je l'avais ici réglé à 0.5 au lieu de 0.9. Le modèle a donc appris en partie sur des détections fausses ce qui expliquerait les résultats médiocres.

Sixième phase : step = 250 / epoch = 7 / batch_size = 1 / 16h de calcul.
Les résultats sont comparables à la phase 5. Il n'y a pas de réelle amélioration et je trouve cela plutôt bizarre. 

Septième phase : step = 150 / epoch = 5 / batch_size = 1 / EN COURS.
Le dataset est ici restreint à __Adachi__. Au vu du rapport temps de calcul/précision, je pense qu'il est préférable de restreindre les données à un seul type d'environnement.

-------------------------------------------------------------

## Installation

Il est préférable de faire tourner ce notebook dans un environnement virtuel dédié, car il nécessite des versions spécifiques de keras (2.2.4) et de tensorflow (1.14).

Pour installer les librairies : dans un terminal, dans l'environnement virtuel dédié muni de python3, installer les librairies :
- numpy
- matplotlib 

Ensuite, se rendre dans le dossier du projet contenant _req.txt_ et lancer la commande _pip3 install -r req.txt_ (ou remplacer _pip3_ par _pip_ en cas de bug)



Pour faire fonctionner le notebook, il est nécessaire de télécharger le dataset __RoadDamageDataset__ ainsi que le dossier Mask_RCNN qui nous était fournit en cours (mais peut être trouvé sur internet).

Il faut alors déplacer le dossier __/Mask RCNN/mrcnn__ dans le dossier courant du notebook, et extraire est placer le dataset dans le dossier courant également. 

RoadInspector/
		
		model.ipynb

		RoadDamageDataset/

		Mask_RCNN/

		mrcnn/

		(d'autres fichiers)

De plus, les poids des modèles que j'ai entraîné sont à placer dans __/trainedModels__. Ils ne sont pour le moment pas en ligne.


## Utilisation

L'intégralité du processus est contenu dans le notebook __model.ipynb__. 

-------------------------------------------------------------


## Auteur 

Florian CASTAIGNEDE
