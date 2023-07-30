# Présentation de REST (avec Node.js et Express)

## Définition de REST

REST (Representational State Transfer), est un style d'architecture logicielle **standardisé** qu'on emploie pour créer des services Web **évolutifs et interopérables**, qui permettent à un client d'**accéder à des ressources** distantes (potentiellement soumises à des autorisations d'accès). La structure REST repose sur un ensemble de **contraintes et de principes** qui favorisent la simplicité et l'efficacité des échanges **client/serveur**. Les ressources sont considérées comme des objets accessibles via des *URI* (**U**niform **R**esource **I**dentifier), et les méthodes *HTTP* (qui sont la base du Web depuis 30 ans) sont utilisées pour effectuer des opérations *CRUD* (**C**reate, **R**ead, **U**pdate, **D**elete) sur ces ressources.

## Concepts clés de REST

### Ressources
Accessibles par des **URI uniques**, les ressources sont les entités de données exposées par l'API REST. Elles peuvent être représentées dans **différents formats** (JSON, XML, HTML, texte brut...) et l'accès à celles-ci dépend de la **requête HTTP** opérée par le client. En effet, on peut récupérer, mais aussi modifier ou supprimer une ressource choisie (*CRUD*).

### URI 
L'URI est utilisée pour identifier de manière **unique** une ressource afin d'y accéder. Par exemple, "/products" pourrait être l'URI pour accéder à une liste de produits.

### Méthodes HTTP
Les principales méthodes HTTP utilisées dans REST sont :

- **GET** pour récupérer une ressource.
- **POST** pour créer une nouvelle ressource.
- **PUT** pour mettre à jour une ressource existante.
- **DELETE** pour supprimer une ressource.

## Avantages de l'approche REST dans la conception d'API Web

L'adoption de l'approche REST présente plusieurs avantages significatifs :

### Scalabilité et performance
L'un des principaux avantages de REST est sa capacité à être hautement évolutive. Une API REST est **sans état**, ce qui signifie que chaque requête du client au serveur contient toutes les informations nécessaires pour être traitée **indépendamment**, aucune information n'est donc conservée côté serveur entre deux requêtes. Cela implique que pour gérer un traffic plus élevé, on peut simplement ajouter plus de serveurs pour l'API, **sans se soucier d'une gestion des sessions utilisateurs**. 

### Interopérabilité 
REST étant basé sur des standards du Web tels que *HTTP*, *JSON* et *HTML*, il facilite l'interaction entre différentes applications et plateformes.
Les clients et les serveurs peuvent être développés dans **différents langages** de programmation, et sur des **plateformes différentes** et seront toujours capables de communiquer efficacement.

### Flexibilité des formats de données 
Les représentations des ressources dans REST peuvent être variées (*JSON*, *XML*, etc.), permettant aux clients d'utiliser le format qui convient le mieux à leurs besoins.
Par exemple, un client peut préférer recevoir des données au format *JSON* plutôt qu'*XML*, et l'API REST peut fournir cette représentation sans nécessiter de modifications majeures du côté serveur.

### Lisibilité et sécurité 
Les opérations *CRUD* simplifient le fonctionnement d'une API, et on peut aisément sécuriser les données transitées grâce au protocole *HTTPS*.

## Principes REST avec Node.js et Express
Exemples de code :

1. Configuration d'Express et définition des routes principales
``(/app.js)``

```js
const express = require('express');
const app = express();

// Importation des routes spécifiques
const productRoutes = require('./routes/productRoutes');
const clientRoutes = require('./routes/clientRoutes');

// Définition des routes produits
app.use('/products', productRoutes);

// Définition des routes clients
app.use('/clients', clientRoutes);

// Écoute du port 3000 pour les requêtes client
app.listen(3000, () => {
    console.log('App listening on port 3000');
});
```

2. Définition des routes produits
``(routes/productRoutes.js)``

```js
const express = require('express');
const router = express.Router();
const productController = require('../controllers/productController');

// Route pour récupérer la liste des produits
router.get('/', productController.getProduct);

// Route pour créer un nouveau produit
router.post('/', productController.createProduct);

// Route pour mettre à jour les informations d'un produit
router.put('/:id', productController.updateProduct);

// Route pour supprimer un produit
router.delete('/:id', productController.removeProduct);

module.exports = router;
```

3. Définition du contrôleur pour la gestion des produits
``(controllers/productController.js)``

```js
// Récupérer la liste des produits
exports.getProducts = (req, res) => {
    // Récupération de la liste des produits depuis la base de données
    res.json({ products: [{ name: 'Lance-pierre', price: 15.99 }, { name: 'Marteau', price: 12.99 }] });
};

// Créer un nouveau produit
exports.createProduct = (req, res) => {
    // Création d'un nouveau produit dans la base de données
    res.status(201).json({ message: 'Product was succesfully created.' });
};

// Mettre à jour les infos d'un produit
exports.updateProduct = (req, res) => {
    const productId = req.params.id;
    const productData = req.body;
    // Mise à jour du produit avec l'ID spécifié dans la base de données 
    // (utilisation des données dans le body de la requête)
    res.json({ message: `Product n°${productId} was successfully updated.` });
};

// Supprimer un produit
exports.removeProduct = (req, res) => {
    const productId = req.params.id;
    // Suppression du produit avec l'ID spécifié de la base de données
    res.json({ message: `Product n°${productId} was successfully deleted.` });
};
```

Dans ces exemples on utilise les **méthodes HTTP appropriées** pour effectuer des **opérations CRUD** sur les produits de la base de données. *GET* pour récupérer la liste des produits, *POST* pour créer un nouveau produit, *PUT* pour mettre à jour les infos d'un produit existant et *DELETE* pour supprimer un produit.

Avec cette architecture routeur/contrôleur, le programme principal ``app.js`` gère la configuration du module ExpressJS et utilise les routes définies dans le programme ``productRoutes.js`` pour toutes les requêtes liées aux produits. Chaque route est associée à un contrôleur spécifique (``productController.js`` pour les routes produit), qui contient les fonctions pour **manipuler les requêtes et les réponses** pour chaque opération CRUD. 
Par exemple, pour la modification d'un produit, le contrôleur va changer les infos du produit en base de données à partir de son id, récupéré en **paramètre de la requête**, et des nouvelles données, renseignées dans le **body** de la requête *PUT*.

Cette approche permet de maintenir un code bien **organisé et modulaire**, ce qui facilite la gestion et l'évolutivité de l'API.

## Exemple d'API REST avec le backend de mon projet de fin d'année (en groupe)

Dans ce même repo, vous trouverez l'API (sous NodeJS avec Express) que nous avons réalisée pour notre projet de fin d'année à l'ESGI : la création d'une application web pour la gestion des appels en cours, des absences, etc.
Elle servait de backend à notre application (le frontend étant du React), et dispose de différents concepts d'une API RESTful comme du routage, des controllers des middlewares, mais aussi un système de login, une connexion base données (inaccessible sans VPN Sciences-U)...