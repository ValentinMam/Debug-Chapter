# L'origine des bugs Front End 

Certains bugs vont être détectables via des erreurs, dans la console par exemple, alors que d’autres vont être un petit peu plus sournois, comme un problème d’affichage sur un navigateur.
Il arrive très souvent que les bugs viennent en cascade

- HTML
```
on peut avoir oublié de fermer une balise ou alors avoir utilisé la mauvaise classe (et donc que le style appliqué ne soit pas le bon).
```  
- CSS 
```
il peut s’agir d’éléments qui s’affichent mal (ou pas du tout) sur un certain type d’appareil ; les smartphones par exemple.
```


- DOM 
```
les bugs peuvent être liés à la mauvaise sélection, modification ou suppression d’un nœud. Par exemple, on souhaite supprimer un nœud qui n’existe pas (parce qu’on l’a mal sélectionné).
```


- API interne / externe
```
1. dans le cas d’une API interne (l’API de géolocalisation ou de stockage par exemple), il se peut que vous l’utilisiez mal, autrement dit que vous n’ayez pas bien compris la documentation.
2. Dans le cas d’une API externe (API de météo par exemple), il se peut que vous ne lui envoyiez pas les bonnes informations dans la requête HTTP.
```

# Projet fil rouge 

Façadia, un site de façades d'immeubles connectées.

[Code source du projet ici](https://github.com/tdimnet/debuggez-l-interface-de-votre-site/tree/main)

[Figma du projet](https://www.figma.com/file/jhus1mOSv5hnpVRxu2q3mf/Connected-Facades) 


- Il y a un dossier  pages  qui comprend toutes les pages HTML du  projet, en dehors de la page index.html qui est située à la racine du projet.
- Le projet n’utilise aucune librairie externe. C’est du JavaScript pur ; on appelle ça aussi du Vanilla JavaScript.
- Chaque page comprend plusieurs balises script ; elles vous permettent de récupérer les fichiers JavaScript à utiliser pour chaque page.

# Outils : Console  

Première étape de notre tour du monde des outils : la console ! C’est certainement l’un des outils les plus intéressants que vous ayez dans le monde du développement front-end. 
```
Première chose à savoir : la console est un environnement de programmation interactif . Grâce à cet environnement, vous allez pouvoir :
•	initialiser et stocker des variables ;
•	analyser les erreurs JavaScript ;
•	afficher (on dit aussi logger) des informations (fonctions, variables, objets, etc.)
•	et même écrire des fonctions pour les exécuter directement.

Cette dernière va nous être particulièrement utile lors de vos débogages : elle se prend très facilement en main, est très puissante et vous permet de directement coder du JavaScript dans votre navigateur. Une bonne compréhension de la console est essentielle pour bien déboguer vos applications front-end .
```


# Outils : Inspecteur

Deuxième étape dans notre tour du monde des outils du débogage : l’inspecteur ! Vous allez principalement vous servir de cet outil pour déboguer votre CSS et votre HTML ainsi que pour tester rapidement une solution (en ajoutant quelques règles CSS directement depuis l’outil).

```
L’un des principaux avantages de l’inspecteur est de pouvoir observer comment se comporte l’interface avec différentes résolutions et/ou différents types d'écran.
La page d'accueil de Façadia sur deux terminaux de taille différente
De plus, l’inspecteur vous donne parfois la ligne correspondant à la propriété CSS. Vous pourrez aussi voir si les propriétés sont surchargées à certains endroits.
Enfin, l’inspecteur vous permet de visualiser les règles d’espacement qui sont appliquées au modèle de boite (ou box model en anglais). Cet outil de visualisation bien pratique va vous permettre de traquer pourquoi un contenu dépasse de sa “boite” et entraîne un bug visuel.
```

# Outils : Débogueur 

Troisième étape de notre tour du monde des outils de débogage : le célèbre débogueur ! Cet outil bien pratique vous permet de suivre l’état de votre code étape par étape.
```
En ajoutant des points de rupture (ou breakpoint), vous allez savoir quelles fonctions vont être appelées, quel sera l’état des variables, etc. À la différence du console.log, le débogueur vous permet de comprendre plus finement et plus précisément comment se comporte une application.
•	Extension de débogage par défaut dans VSCode (fichier launch.json)
•	Installer Google Chrome 
```

# Outils : Onglet réseau du navigateur 

Dernière étape de notre tour du monde des outils de débogage : l’onglet Network / réseau ! C’est l’un des outils dont on parle le moins souvent et qui demeure pourtant essentiel pour déboguer.

```
Cet outil va vous permettre de traquer toutes les requêtes et réponses reçues par votre navigateur. Dans ce cours, vous utiliserez principalement cet outil pour déboguer nos requêtes HTTP. 
En plus de la partie débogage des API, l’onglet Réseaux vous permet de connaître le poids des fichiers reçus. Cela peut être particulièrement intéressant si vous souhaitez optimiser le chargement de votre site (ou au contraire, comprendre pourquoi ce dernier met du temps à charger ).
```

# Méthodologie de débogage 

```
1.	Observer le(s) bug(s)
2.	Ecrire un test repétable 
3.	Elaborer et tester sa théorie 
4.	Résoudre le bug 

Répéter cette méthodologie jusqu’à résolution complète du ou des bugs
```

1. Observer le(s) bug(s) 

```
Quand on enquête sur un bug, il est important de ne pas plonger directement dans le code. Vous devez essayer de prendre du recul, d’observer la situation, et donc le bug, et de vous poser des questions ! Essayez, par exemple, de vous demander :
•	Où se trouve le bug ? S’agit-il d’un bug d’affichage et donc potentiellement d’un bug côté CSS ou d’un bug côté JavaScript ?
•	Y a-t-il une erreur dans la console ? La comprenez-vous ? À quelle ligne de votre code cette erreur se produit-elle ?
•	Si le bug se trouve côté JavaScript, quel type de bug est-ce à première vue ? S’agit-il d’un bug plutôt lié à une API ou plutôt lié au DOM ? Ou peut-être les deux ?
•	Si le bug se trouve côté CSS, apparaît-il sur un appareil en particulier, par exemple sur un iPhone et pas sur un Android ?
•	Quel parcours précis je fais pour générer le bug ? Quel support j'utilise ?

 Il est important que vous gardiez en tête que le bug peut être l’arbre qui cache la forêt. Par exemple, un bug d’affichage, une div absente de l'écran, peuvent être liés à un problème côté API.

À cette étape, il est important d’aller du macroscopique vers le microscopique : regardez et observez le bug dans son ensemble puis essayez de zoomer sur certaines parties de votre code pour voir si ces dernières sont en relation avec ce dernier.
```

2. Ecrire un test repétable 
```
Écrire un test répétable est souvent la partie la plus complexe car reproduire un bug n’est pas toujours chose aisée. En effet, le bug peut se produire dans des circonstances particulières, sur l’ordinateur d’un certain type d’utilisateur mais pas sur le vôtre.
Votre première mission pour cette étape va donc être de reproduire le bug sur votre ordinateur et dans votre environnement de développement. Être en mesure de le répéter va vous permettre de comprendre son contexte d'exécution.
Si le bug se produit sur votre ordinateur, essayez de noter le parcours d’exécution de ce dernier : quelles sont les étapes qui amènent à ce bug et quel est le parcours utilisateur ?
Si le bug se produit sur l’ordinateur d’un collègue, ou pire, d’un utilisateur, il est important que vous ayez les informations suivantes :
•	Quel type d’appareil votre utilisateur a-t-il ? Utilise-t-il un ordinateur portable, une tablette, un téléphone ?
•	Quel système d’exploitation (Windows, Mac, Linux, iOS, Android) votre utilisateur a-t-il au moment où survient le bug ? De quelle version dispose-t-il ?
•	Quel navigateur est utilisé ? Quelle est sa version ?

Pour finir, vous devrez parfois écrire du code pour répliquer les conditions du bug. Cela vous permettra de tester automatiquement la fonctionnalité buggée et de travailler dessus.
Une fois que vous avez regroupé toutes ces informations, vous pouvez vous lancer dans la réalisation du test et essayer de le répéter. 
```

3. Elaborer et tester sa théorie 
```
Si vous résumez les étapes précédentes, vous pouvez voir qu’on commence à avoir une idée assez précise du bug. Vous savez notamment :
•	d’où il peut venir ; du CSS ou du JavaScript par exemple ;
•	comment le reproduire ;
•	à quel moment ce dernier survient.

Toutes ces informations vont vous permettre d’élaborer une théorie et de la tester. Cela dit, attention, tester une théorie, et plus particulièrement, si cette dernière fonctionne ne veut pas dire que le bug est résolu : cela veut surtout dire que vous avez compris d’où il venait.
La Règle du Boy Scout vise à ce que les développeurs laissent le code le plus propre possible une fois qu’ils sont intervenus dessus. Cela équivaut aussi pour les bugs : si vous trouvez un bug dans votre code en en corrigeant un autre, il est de votre devoir de le corriger aussi !

Si, par contre, votre théorie échoue, pas de panique, ce n’est pas grave : ces choses-là arrivent constamment ! Cela veut peut-être dire que vous êtes passé à côté de quelque chose d’important. Essayez alors de regarder les indices un à un et de comprendre ce qui n’a pas marché. N’hésitez surtout pas à demander à un collègue, il pourra aussi vous apporter son éclairage.
```

Une fois que la théorie a été testée et qu’elle a fonctionné, vous pouvez maintenant faire une proposition de solution.




