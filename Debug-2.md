
# Identifiez les bugs d’intégration

Les bugs d’intégration correspondent aux bugs que nous pouvons rencontrer côté HTML et CSS. Ces derniers s'avèrent souvent assez compliqués à résoudre. 
En effet, à la différence du JavaScript, les erreurs d’intégration ne soulèvent pas d’erreurs dans la console ou ne font pas “planter” l’intégralité de votre application.

1. Les erreurs liées au HTML


```
La cause la plus fréquente d’erreur est souvent l’oubli de fermeture d’une balise. 
Une balise non fermée peut entraîner un comportement un peu bizarre côté navigateur. 
```
```
Autre erreur classique : l’utilisation d’une balise dépréciée ou expérimentale. 
Les balises dépréciées sont des balises qui ont été remplacées par d’autres et qui sont amenées à disparaître. 
À contrario, une balise expérimentale est une balise qui n’est pas encore supportée par l’ensemble des navigateurs. 

```
Astuce supplémentaire : regarder la console de l'extension Prettier. (ctrl + s)

2. Les erreurs liées au comportement du CSS

Petits rappels : 

```
Les types de sélecteurs de la liste suivante sont présentés dans l'ordre de spécificité croissante :

•	Sélecteurs de type (ex. h1) et pseudo-éléments (ex. ::before).
•	Sélecteurs de classe (ex. .exemple), sélecteurs d'attributs (ex. [type="radio"]) et pseudo-classes (ex. :hover).
•	Sélecteurs d'identifiant (ex. #exemple).
•	Sélecteur universel (*), combinateurs (+, >, ~, " ", ||) et pseudo-classe de négation (:not()) n'ont aucun effet sur la spécificité (cependant, les sélecteurs déclarés à l’intérieur de :not() ont un effet).
__________________________________

Il existe un ordre pour les feuilles de style selon leur priorité :

•	Styles En ligne
•	Feuille de Style Internes (Enfoncée)
•	Feuille de Style Externes (Reliée ou Importée)
•	Défauts de Navigateur
```



```
Face à un bug côté CSS, il convient donc que vous preniez bien le temps de regarder si une propriété CSS n’est pas surchargée par une autre !
```

```
L’autre cas de bug très classique, et très sournois aussi, est la mauvaise sélection d’un élément HTML auquel vous faites appel dans votre CSS, par exemple une faute de typographie dans le nom de la classe sélectionnée.
```


3. Les erreurs liées aux navigateurs

```
Il arrive régulièrement que des bugs puissent être liés à des incompatibilités navigateurs. Par exemple, pendant très longtemps, Firefox ne supportait pas l’input date : Chrome affichait un DatePicker alors que Firefox n’affichait rien ; on devait alors passer par une librairie JavaScript pour harmoniser ce comportement.
Heureusement, l’époque de la forte incompatibilité entre les navigateurs est derrière nous. Cela dit, il existe encore des moments où vous allez devoir gérer ce cas de figure. Par exemple, si vous souhaitez réaliser des animations CSS. Dans ce type de cas, vous allez devoir passer par les “Vendor Prefix”. (-webkit-  ,  -moz-  ou même  -ms-…).
```

# Analyser votre bug 

1. Utiliser l’inspecteur

Ce formidable outil va nous permettre d’analyser votre code HTML et CSS et plus particulièrement : 
- de changer la résolution ;
- de changer le type de devices ;
- d’inspecter les modèles de boite, ou Box Model, et de voir précisément les margin et padding utilisés ;
- de voir si certaines règles CSS sont surchargées ou ne sont pas appliquées.

Vous entendrez parfois parler de “reset” et de “normalization” CSS. 
Ces fichiers vous permettent de gommer les différences entre les navigateurs. 
Par exemple, les “margin” appliquées sur les titres pour Chrome ne sont pas les mêmes que sous Firefox. J’ai tendance à utiliser [Normalize](https://necolas.github.io/normalize.css/) pour tous mes projets.

2. Utiliser un validateur HTML et CSS

Recourir à un validateur peut parfois être une solution miracle. En effet, il arrive d’être totalement coincé devant un bug.
Dans ce type de cas, je vous invite à copier/coller votre code dans un [validateur HTML](https://validator.w3.org/) et/ou dans un [validateur CSS]( https://jigsaw.w3.org/css-validator) et voir si des erreurs et warnings remontent. 
En plus des validateurs, il existe une autre solution : les linters. Ces outils directement intégrés à votre éditeur de texte vont vous permettre de voir des erreurs de style ainsi que des oublis.
Le plus connu dans le monde du développement front-end est [EsLint]( https://eslint.org/). 

3. Utiliser CanIUse

Parfois les validateurs ne vont pas vous remonter des erreurs, mais des warnings ! Et ces warnings peuvent être super intéressants pour analyser votre code et comprendre ce qui ne va pas.
Par exemple, peut-être que votre propriété CSS a besoin de “Vendor Prefix” et que vous avez oublié de le mettre dans votre projet. Ou alors, vous vous servez peut-être d’une propriété qui, soit n’est plus utilisée, soit est peu supportée par les navigateurs.
Dans ce cas-là, [le site CanIUse]( https://caniuse.com/) est votre ami. Il va vous permettre d’analyser la propriété en détail : son pourcentage d’utilisation, les versions de navigateur supportées, etc.


# Inspectez votre HTML
```
Grâce à l’inspecteur, vous avez la possibilité d’éditer directement votre code HTML depuis l’outil. Vous allez pouvoir enlever ou ajouter une classe, modifier le contenu d’un  div  , etc.
Cette méthode va vous permettre de tester rapidement une hypothèse pour un débogage. Par exemple, si vous ajoutez une classe à un élément, comment ce dernier se comporte-t-il ?
Cela va, par exemple, vous permettre de résoudre des bugs de sélection CSS.
Cela dit, en pratique, on n’utilise cet outil que pour modifier quelques lignes ou quelques éléments dans votre page. Si vous devez, par exemple, ajouter une vingtaine de lignes pour tester votre hypothèse, il peut être plus malin de le faire sur votre code source plutôt que directement sur votre page web.

!!! Si vous rafraîchissez la page, les modifications que vous avez réalisées n'apparaîtront plus. En effet, il n’y a pas de système de sauvegarde quand vous modifiez votre HTML. !!!
```



# Inspectez votre CSS
```
Vous voyez comment inspecter les règles CSS qui sont appliquées et aussi comment les modifier en direct. En plus de ce panel d'outils, l’inspecteur peut vous donner la ligne précise où est définie une règle CSS. Cela va vous être particulièrement utile pour déboguer ce dernier.
```