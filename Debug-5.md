# Découvrez un bug complexe
Quand vous rencontrez une erreur que vous devez déboguer, il y a deux types de situation :
```
•	soit le bug est “tout seul”. Autrement dit, il y a un bug, d’affichage par exemple, qui n’influe que sur l’affichage du projet sur une page spécifique. Dans ce type de cas, vous pouvez appliquer les méthodes de débogage que nous avons vues ensemble dans les parties précédentes.
____________________________________

•	soit le bug engendre un autre bug qui engendre un autre bug (qui engendre…).Et dans la plupart des cas, c’est ce qui se produit. En effet, dans le cas d’applications complexes réalisant beaucoup de traitements, comme des appels API, de l’affichage dynamique sur le DOM, l’erreur qui apparaît, dans votre console par exemple, ne peut être que la face visible de l’iceberg.
```
```
Il est aussi important de préciser que le bug peut venir de chez vous mais pas seulement ! Il peut aussi venir du serveur, l’API peut être boguée, les données que vous demandez à la base de données peuvent être incorrectes, etc. Le plus souvent, c’est l’analyse du code qui va vous permettre de voir d’où il peut venir.
```
```
il est important, face à un bug complexe, d'isoler le problème : il ne faut surtout pas essayer de tout déboguer à la fois, c’est le meilleur moyen de perdre du temps et de ne pas comprendre d’où le problème vient. En y réfléchissant bien, le problème de mon ami aura pu venir de plein d’endroits : de la configuration du WordPress, de son serveur, du serveur Smtp, des identifiants de connexion, de la librairie, etc.
```


# Résolvez un bug complexe

-	Utilisez les outils à votre disposition


```
•	L’inspecteur est souvent utilisé pour le débogage du HTML et du CSS. Vous pouvez voir les propriétés CSS qui sont utilisées, celles qui sont surchargées. Vous pouvez aussi voir le modèle de boite qui s’applique.
____________________________________

•	La console va vous permettre de déboguer du code JavaScript. Elle peut vous permettre d’exécuter des fonctions, de récupérer des variables. Vous pouvez aussi depuis votre code utiliser des console.log pour suivre l’état de votre application.

____________________________________

•	Le débogueur est un outil dédié au débogage du JavaScript. Grâce à des breakpoints, vous allez pouvoir suivre l’état de votre code, les variables et valeurs contenues dans les fonctions exécutées, etc. Vous pouvez aussi bien l’utiliser dans le navigateur qu’avec l’extension VsCode que nous avons vue durant le cours.

____________________________________

•	L’onglet Network vous permet d’en savoir un peu plus sur les requêtes et réponses HTTP reçues quand vous consultez une page. Vous pouvez voir le poids des fichiers reçus, les requêtes réalisées, etc.
```

-	Réfléchissez à l’implémentation de la solution

Une fois que vous avez isolé votre bug et que vous avez codé votre solution, il est important de vous poser ces questions :
```
•	Est-ce que cette solution va couvrir d’autres cas d’erreur ? Est-ce qu’elle va engendrer d’autres bugs ?
•	Comment faire pour éviter que cette erreur ne se reproduise ?
```

En effet, ce n’est pas parce que vous avez réglé votre bug à un endroit que le code ne va pas casser à un autre endroit. Il est donc toujours important de “faire le tour du propriétaire” avant de passer à autre chose.
C’est pour ça que dans des projets d’envergure, vous passerez par des tests automatisés ainsi que des outils de “monitoring” pour traquer votre application. 


