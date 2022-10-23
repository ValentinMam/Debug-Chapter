
# DOM - bugs liés à la sélection de nœuds

-	Le type des objets et les méthodes querySelector et querySelectorAll

La mauvaise compréhension des méthodes querySelector et querySelectorAll.
```
•	querySelector  ne vous retourne toujours qu’UN seul élément même si la page en comporte plusieurs similaires. Par exemple, si vous sélectionnez une classe, l’élément retourné sera toujours la première occurrence à votre sélection.
•	querySelectorAll  vous retourne toujours une NodeList (autrement dit, une liste de noeuds) HTML MÊME si votre page n’en contient qu’un. Autrement dit, vous aurez d’abord besoin d’extraire le, ou les, nœud(s) de votre tableau avant de pouvoir utiliser une méthode spécifique.
```

# DOM - bugs liés à la création de nœuds

Lors du développement d’une application, vous allez parfois vouloir ajouter des éléments dynamiques sur votre site en passant, par exemple, par une API. Cette dernière va vous permettre de récupérer des données, créer une liste avec ces données et les afficher.
À ce moment-là, vous devrez souvent créer de nouveaux nœuds HTML directement depuis le JavaScript : vous pourrez alors être confrontés à des bugs de création.

-	Initiez-vous aux bugs de création les plus courants

```
Les bugs de création arrivent le plus souvent parce que vous avez mal créé ou mal ajouté un élément sur votre DOM. Il peut aussi parfois arriver que vous ayez un bug parce que vous avez mal sélectionné un élément (ce dernier n’existe pas) et vous ne pouvez donc pas l’ajouter.
```
```
Autre chose, évitez d’utiliser les méthodes innerHTML ou insertAdjacentHTML. Ces méthodes peuvent être, certes, bien pratiques, mais elles font le plus souvent trop de choses à la fois : vous créez un, voire plusieurs nouveaux nœuds HTML, vous ajoutez du texte, vous avez des classes. Le mieux à faire dans ce type de cas est de bien réaliser la création de votre noeud :

•	utilisez  createElement  pour créer votre noeud ;
•	puis, servez-vous de  textContent  pour lui ajouter un contenu textuel (si c’est possible)
•	puis, tirez parti de l’objet  classList  pour ajouter, lister ou enlever une classe.
•	et enfin, ajoutez le noeud nouvellement créé à son nœud “parent” via  appendChild.

Le plus souvent, c’est quand vous essayez de tout faire à la fois que vous risquez de vous prendre les pieds dans le tapis. 
 L’un des autres avantages de cette méthode est qu’elle est plus facilement testable via des tests automatisés.
```
-	La méthode appendChild et ses messages d’erreur


```
Dans le cadre de la méthode  appendChild  , vous serez susceptible d’avoir deux grands types de messages d’erreur :

•	la  TypeError  (ou erreur de type).Cette erreur sera le plus souvent présente quand vous aurez mal sélectionné un élément sur le DOM.
•	la  ReferenceError  (ou erreur de référence) qui correspondra à une variable non définie. Dans l’exemple ci-dessous, je supprime délibérément une lettre (la lettre l de title) sur ma variable  sensorInfoTitle.
```

# DOM - bugs liés à la modification de nœuds existants
Côté bug et modification des nœuds existants, le bug le plus courant est celui où vous essayez d’utiliser une propriété ou une méthode qui n’existe pas sur le nœud sélectionné. Une fois encore, il est important de connaître le type de variable que vous manipulez et de comprendre le message d’erreur associé.

-	Utilisez le CSS pour ajouter du style à vos éléments

Il est important que nous revenions sur un sujet particulier : le CSS et le DOM. Admettons que vous soyez en train de travailler sur un formulaire de contact et que vous souhaitiez gérer les cas où le champ de votre formulaire est correct et incorrect. Il existe deux solutions :

1.	Vous utilisez le JavaScript pour ajouter et supprimer des classes, par exemple ; chaque classe étant liée à un sélecteur CSS et se chargeant d’ajouter le style. On ajoute (ou supprime une classe) en fonction de la condition (si le mot de passe de l’utilisateur est valide).


```
const checkUserPasswordInput = () => {
   const isUserPasswordValid = $userPasswordInput.value === USER_PASSWORD
   if (isUserPasswordValid) {
       // J'ajoute une classe HTML "hidden" à mon noeud userPasswordErrorMsg, elle a pour règle css un display: none
       $userPasswordErrorMsg.classList.add('hidden')
   } else {
       // J'enlève une classe HTML "hidden" à mon noeud userPasswordErrorMsg, elle a pour règle css un display: none
       $userPasswordErrorMsg.classList.remove('hidden')
   }
   return isUserPasswordValid
}
```
2.	Vous ajoutez directement du style via le JavaScript sur le nœud HTML avec la propriété  .style . On injecte directement du style depuis le JavaScript dans le HTML :

```
const checkUserEmailInput = () => {
   const isUserEmailValid = $userEmailInput.value.toLowerCase() === USER_EMAIL
   if (isUserEmailValid) {
       $userEmailErrorMsg.style.display = "none"
   } else {
       $userEmailErrorMsg.style.display = "block"
   }
   return isUserEmailValid
}
```
Personnellement, j’ai tendance à utiliser la première solution. 
- D’une part, parce qu’il y a une violation des responsabilités* : le HTML est là pour le contenu, le CSS est là pour la mise en page et le JavaScript pour gérer les interactions.
- D’autre part, parce que vous multipliez les sources “de vérité”, à savoir là où les règles s’appliquent. C’est une source de bug très  commune.

```
* Violation des responsabilités : Cela vient du principe de responsabilité unique qui dit que chaque fonction ou module ne devrait avoir qu’une responsabilité. Dans le cadre du trio HTML, CSS et JavaScript : le HTML a la responsabilité du contenu, le CSS de la mise en page et le JavaScript des interactions. 
```
Dans ce type, tirez parti de l’excellent objet classList et de ses méthodes  .toggle()  ,.add(),.remove(), etc.

# DOM - bugs liés à la suppression de nœuds

Dernier focus : la suppression de nœuds. 


```
Vous est-il parfois arrivé d’avoir envie de masquer un nœud en le supprimant plutôt qu’en le masquant côté CSS ? Le plus souvent, les bugs liés à la suppression de nœuds viendront du fait qu’on a supprimé le nœud du DOM au lieu de simplement le masquer ou alors d’une mauvaise utilisation de la méthode  removeChild() 

En effet, la méthoderemoveChild()permet de supprimer un nœud enfant contenu dans un nœud parent. Cela dit, si vous ne sélectionnez pas directement le noeud parent mais un autre noeud, vous pouvez avoir une erreur.
```

Maintenant que vous avez découvert tous les types de bugs côté DOM, il est temps d’aller plus loin avec la console et le débogueur. 


# Utilisez la console pour déboguer votre DOM

-	Initialisez et accédez à des variables dans votre console.



```
L’une des principales fonctionnalités est de pouvoir créer et récupérer des variables. Cela dit, vous pouvez le faire uniquement si cette variable est accessible globalement, autrement dit si elle est déclarée en dehors d’une fonction.

la console nous permet de  :
•	initialiser de nouvelles variables dans la console.
•	récupérer une variable déjà existante et qui a été déclarée dans le code.
_____________________
Vous pourrez voir que la console propose de l’auto-completion. Une fonctionnalité bien pratique quand on ne connaît pas forcément le nom des variables qu’on utilise.

L’un des principaux intérêts de cette fonctionnalité est de pouvoir :
•	tester rapidement un bout de code.
•	connaître l’état d’une variable durant l’exécution d’un programme.
```
-	Analysez des erreurs JavaScript

```
L’importance va être de bien comprendre les messages d’erreur et à quelle ligne ils surviennent. Plus vous allez être confronté à une erreur, plus vous serez capable de comprendre d’où elle provient.
```
-	Affichez et filtrez des informations dans votre console

```
En plus d’initialiser des variables, vous pouvez aussi vous servir de la console pour afficher des informations (via le célèbre console.log et ses déclinaisons) ainsi que pour filtrer les différents niveaux d’information.
_____________________

Il peut être intéressant de filtrer vos informations si vous souhaitez afficher uniquement des informations relatives aux erreurs sur votre page ou aux requêtes HTTP par exemple.
_____________________

Je me sers très souvent du console.log pour déboguer mon code : j’affiche chaque variable qui me semble poser un problème et je me pose la question du type de variable que je manipule. Il me permet aussi de voir si le code passe aux endroits requis pour exécuter le code. 
```

-	Écrivez puis exécutez des fonctions
```
La console peut aussi vous permettre d’écrire et d'exécuter des fonctions. Cela peut être utile si vous souhaitez tester un bout de code rapidement et voir si ce dernier fonctionne.
_____________________

En plus du console.log classique, vous pouvez aussi parfois passer le console.group et le console.groupEnd. Cela va vous permettre d’afficher des blocks de message ensemble. Voici ci-dessous un exemple d’utilisation :

console.group()
console.log("Une variable")
console.log("Une autre variable")
console.groupEnd() // J'ai besoin d'ajouter le groupEnd ici pour faciliter la lecture des éléments
```
# Tirez parti du débogueur
Deux méthodes pour le débogueur : 

```
-	Avec l’extension Google Chrome 
-	Avec l’extension VSCode 
```