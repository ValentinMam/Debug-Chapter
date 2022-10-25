# Récupérez des données sur une API externe

Exemple : 

-	Pour récupérer les données météo, je passe par une API : [WeatherStack](https://weatherstack.com/). Créer un compte pour obtenir une clé API 
-	Regarder la documentation de l’API. 
-	Utiliser [Postman](https://www.postman.com/) requête GET : access key :  clé API  / Query : value (nom d’une ville) 

Deux manières de récupérer les données météo :
1.	soit via le fichier de données “mockées” que j’utilise. Il m’évite de faire trop de requêtes quand je fais mes tests.

- data/weahter-api-mocked-data.json :


```
{
    "request": {
        "type": "LatLon",
        "query": "Lat 48.88 and Lon 2.38",
        "language": "en",
        "unit": "m"
    },
    "location": {
        "name": "Villette",
        "country": "France",
        "region": "Ile-de-France",
        "lat": "48.883",
        "lon": "2.367",
        "timezone_id": "Europe/Paris",
        "localtime": "2021-05-02 18:33",
        "localtime_epoch": 1619980380,
        "utc_offset": "2.0"
    },
    "current": {
        "observation_time": "04:33 PM",
        "temperature": 10,
        "weather_code": 389,
        "weather_icons": [
            "https://assets.weatherstack.com/images/wsymbols01_png_64/wsymbol_0024_thunderstorms.png"
        ],
        "weather_descriptions": [
            "Rain With Thunderstorm"
        ],
        "wind_speed": 15,
        "wind_degree": 360,
        "wind_dir": "N",
        "pressure": 1022,
        "precip": 0.5,
        "humidity": 66,
        "cloudcover": 75,
        "feelslike": 9,
        "uv_index": 3,
        "visibility": 10,
        "is_day": "yes"
    }
}

```
2.	soit via une fonction dédiée qui va requêter l’API en fonction des données géographiques du capteur.

- utils/weatherStackAPI.js : 


```
const ACCESS_KEY = ''

const _retrieveWeatherForecastMockedData = () => fetch('/data/weather-api-mocked-data.json')
.then(res => res.json())
.catch(err => console.log("Oh no", err))


const _retrieveWeatherForecastApiData = coordinates => fetch(`https://api.weatherstack.com/current?access_key=${ACCESS_KEY}&query=${coordinates.lat},${coordinates.lng}`)
    .then(res => res.json())
    .catch(err => console.log("Oh no", err))


const retrieveWeatherForecastData = async (coordinates, isMocked) => {
    if (isMocked) {
        return await _retrieveWeatherForecastMockedData()
    }
    return await _retrieveWeatherForecastApiData(coordinates)
}
```

# Comprenez les messages d’erreur d’une API externe

Quand on développe une API et qu’on souhaite la rendre publique, autrement dit, la mettre à disposition d’autres développeurs externes à notre structure, il y a souvent des règles à respecter :
```
•	Il est important d’utiliser des noms au lieu des verbes pour chaque endpoint (cela correspond à l’URL appelé). Ce sont les méthodes HTTP (GET, POST, PUT, etc.) qui vont préciser l’action à réaliser.
•	les status code HTTP doivent vous permettre de traiter les erreurs de façon propre. Par exemple, un status code 400 correspond à des données côté client non valides, 403 à une erreur d’authentification, etc.
•	l’API doit contenir sa version dans son URL. Cela permet d’aider les développeurs utilisant cette API à réaliser des montées de versions.
```
Rappel 

```
HTTP signifie HyperText Transfer Protocol. C'est un protocole qui permet de communiquer avec un site Internet. Il va permettre de charger des pages HTML, des styles CSS, des polices de caractères, des images, etc. Mais ce n'est pas tout, le protocole HTTP  nous permet aussi d'envoyer des formulaires et de récupérer et d'envoyer toutes sortes de données depuis ou vers un serveur implémentant ce protocole grâce à son API !
________________________

La méthode. Il s’agit de l’action que l’on souhaite faire : récupérer une ressource, la supprimer, etc… Voici les méthodes HTTP les plus courantes :

- GET : permet de récupérer des ressources, comme par exemple le temps actuel sur un service de météo ;

- POST : permet de créer ou modifier une ressource, comme la création d'un nouvel utilisateur sur votre application ;

- PUT : permet de modifier une ressource, comme le nom de l'utilisateur que vous venez de créer avec POST ;

- DELETE : Permet de supprimer une ressource, comme un commentaire dans un fil de discussion. 
________________________

L’URL. C’est l’adresse sur le service web que vous souhaitez atteindre. Un peu comme un identifiant unique afin que le web service comprenne ce que vous voulez
______________________

Les données. Lorsqu’on fait une requête pour enregistrer des données (par exemple un formulaire) il faut pouvoir envoyer ces données au service web.

```
Une fois votre requête envoyée et traitée par le service web, celui-ci va vous répondre avec, entre autres, les informations suivantes :
```
Les données. Les données que vous avez demandées : une page HTML, etc…

______________________

Le code HTTP. Il s’agit d’un code numérique qui vous indique comment s’est déroulée la requête. Voici les plus courants :

- 200 : indique que tout s’est bien passé

- 400 : indique que votre requête n’est pas conforme à ce qui est attendu

- 401 : indique que vous devez être authentifié pour faire cette requête

- 403 : indique que vous êtes bien authentifié mais que vous n’êtes pas autorisé à faire cette requête

- 404 : indique que la ressource demandée n’existe pas

- 500 : indique une erreur avec le service web
```
[Liste des codes HTTP](https://fr.wikipedia.org/wiki/Liste_des_codes_HTTP)


-	Simplifiez vos problèmes en les isolant
```
Ce conseil ne s’applique d’ailleurs pas que pour le débogage de vos API. Il faut tester !  
```
-	Utilisez l’onglet réseau du navigateur


```
Cet onglet peut vous communiquer des informations très intéressantes sur les appels API comme la requête réalisée, la réponse reçue par l’API et les en-têtes HTTP. Cet outil vous permet de rapidement voir si une de vos requêtes échoue.
```


-	Attrapez vos erreurs


```
Pensez à traiter vos messages d’erreur. Quand vous travaillez avec la méthode fetch, vous travaillez avec des promesses. Les promesses ont plusieurs statuts : 
•	Pending (en cours), 
•	Resolve (résolue),
•	et Reject (rejetée).
```

La méthode fetch traite les erreurs de la manière suivante :

```
const _retrieveWeatherForecastMockedData = () => 
fetch('/data/weather-api-mocked-data.json')
        .then(res => res.json()) 
        // Ici, le cas de succès
        .catch(err => console.log("Oh no", err)) 
        // Ici, le cas d'erreur
```

# Récupérez des données sur une API interne
Une API n’est pas forcément liée à un webservice. Votre navigateur comporte de très nombreuses API internes :
-	Le LocalStorage utilise l’API du Web Storage pour stocker des informations sur votre navigateur ;
-	L’API Canvas fournit un moyen de dessiner via le JavaScript et le HTML.
-	 [Liste de toutes les API possibles](https://developer.mozilla.org/fr/docs/Web/API).

# Comprenez les messages d’erreur d’une API interne
La gestion des erreurs et les messages d’erreur des API internes ne sont pas les mêmes d’une API à l’autre.
Il faut donc toujours lire la partie « Gérer les erreurs » dans la documentation de l’API en question. 



