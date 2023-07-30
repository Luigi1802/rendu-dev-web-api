# Notes du cours
*Luigi AUBRY-POUGET*

> Learn to code roadmap : https://www.youtube.com/watch?v=66tfvFeALBQ

## JS
> NodeJS -> executer du JavaScript en tant que language serveur

Connaître sa version de Node installée :
```
node --version
``` 
Éxecuter un code JS avec Node :
```
node [chemin du fichier js]
``` 

### Définition de variables et de fonctions : 
- pour une constante
```
const [nom variable]
```
- sinon 
```
let [nom variable]
```
> Ne pas utiliser var, pour avoir plus de contrôle sur la portée de ses variables

Structure minimale d'une fonction : 
```
([paramètres (optionnels)]) => {[instruction(s)]}
```
``()`` et ``{}`` sont faculatifs s'il y a 1 seul paramètre ou 1 seule instruction

### Astuces JS :
Pour parcourir un tableau : au lieu de faire un for of, on peut utilisier la méthode
forEach (et remettre une fonction callback à l'intérieur)

``...`` = rest operator/spread operator -> permet d'étendre un itérable (chaîne de caractères, tableau, ...), exemple :
```
let tableau = [1,2,3]
tableau = [...tableau, 4, 5, 6]
// tableau égal à [1,2,3,4,5,6]
```
La fonction sort est très performante, et utilisable avec une fonction de comparaison personnalisée, exemple :
```
tableau = [8,9,7,5,4,6,1,3,2]
tableau.sort()
// tableau est égal à [1,2,3,4,5,6,7,8,9]
tableau.sort((a, b) => {
    if (a%2===0) {
        return -1
    }
    if (b%2===0) {
        return 1
    }
    return 0
})
// tableau est égal à [8, 6, 4, 2, 1, 3, 5, 7, 9] (nombres pairs d'abord)
```

## API

PC/Serveur contenant une application disponible en ligne à laquelle on peut faire des requetes formatées pour recuperer des ressources -> moyen de communication client/serveur

> Données renvoyées souvent en JSON ou XML

### API REST 
ensemble de regles, conventions, contraintes -> representational state transfer : Standard de construction des APIs
exemple : une API REST est stateless -> les communiquants (API et clients n'ont pas à stocker d'infos sur l'autre, chaque requete est INDÉPENDANTE (pas multiples requetes pour accéder à une ressource)
voir standards REST

Diverses ressources disponibles via diverses URI -> Uniform Resource Identifier, qui permettent un accès spécifique à une ressource

### Format d'une requête API : 
> Verb : GET, POST, PATCH, DELETE, PUT, ...
> URI : ``/resource``

### Headers : metadonnées associées à une requête HTTP (exemples : Accept, Authorization, Body...)
Accept : format de réponse demandé (json, ...)
Autorisation : preuve du droit d'effectuer la requette (access token)

### Réponse à la requête

Requete HTTP avec un status code
- 2XX -> réussite (la ressource a été envoyée)
- 3XX -> redirection
- 4XX -> erreur du client (requete incorrecte)
- 5XX -> erreur du serveur

### Divers 

Logiciels d'utilisation d'API 
- Postman
- Insomnia

Sinon CURL (requetes sur terminal)

- LAMP = **L**inux **A**pache **M**ySQL **P**hp
- MERN = **M**ondoDB **E**xpress **R**eact **N**odeJS