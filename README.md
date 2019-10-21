# Docuementation Laravel

## Installation

Installer Laravel en utilisant Composer.

```
composer create-project laravel/laravel blog
```

## Routes 

Les routes vous permettent d'assigner un bout de code aux différentes URLs.

Elles sont définit dans le fichier ``` app/routes/web.php```

## Middleware

Permet de filtrer les requêtes HTTP entrant dans votre application.
Les Middlewares de bases sont pour vérifier si l'utilisateur est identifié ou non.

* Créer un Middleware
```
php artisan make:middleware FiltreIpMiddleware
```

Création de la classe FiltreIpMiddleware avec la methode handle qui permet d'intercepter la requête.

Grace au fichier ``` app/Http/Kernel.php ``` vous pouvez ajouter le Middleware à votre Application.

## Controller

On ne peut pas tout mettre dans routes.php on va avoir besoin des Controllers pour organiser la logique de notre application.

Un Controller est un classe qui contient differentes methodes.

Appel du controller et de ca methode 
```
Route::get('demo', 'MonController@index'); 
```

> On peut aussi définir les middleware à utiliser pour un controller lors du constructeurs. 

## View

Les vues générées par Blade sont en PHP
Une vue peut en étenndre une autre on appelle ca un héritage

Vous pouvez déclarer une vue comme parent en utilisant extends :
```
@extends('front.NomDeLaVue')
```

et yield pour les vues enfant :
```
@yield('css')
```

## Migration

Vous pouvez gerer les migrations dans le dossier databases, vous aurez accés aux
informations de la bdd 
Les commandes seed vous permettent de créer des users ainsi que de faire des tests avec des commandes en boucle.


# Seeders

Pour generer un seeder vous devez utiliser la commander ```make:seeder```
Les seeders seront placés dans le dossier ```database/seeds```

```
php artisan make:seeder UsersTableSeeder
```

La classe ne contient qu'une methode ```run```
Dans cette méthode, vous pouvez insérer des données dans votre bdd comme vous le souhaitez. 


## Model Factories

Vous pouvez utiliser des model factories pour générer facilement de grandes quantités d’enregistrements de base de données.
Une fois que vous avez défini vos usines, vous pouvez utiliser la fonction factory d'assistance pour insérer des enregistrements dans votre base de données.

Exemple créer 50 utilisateurs
```
public function run()
{
    factory(App\User::class, 50)->create()->each(function ($user) {
        $user->posts()->save(factory(App\Post::class)->make());
    });
}
```


## Arborescence

```
bootstrap : scripts d'initialisation de Laravel pour le chargement automatique des classes, la fixation de l'environnement et des chemins, et pour le démarrage de l'application,

public : tout ce qui doit apparaître dans le dossier public du site : images, CSS, scripts...

vendor : tous les composants de Laravel et de ses dépendances,

config : toutes les configurations : application, authentification, cache, base de données, espaces de noms, emails, systèmes de fichier, session...

database : migrations et les populations,

resources : vues, fichiers de langage et assets (par exemple les fichiers LESS ou Sass),

storage : données temporaires de l'application : vues compilées, caches, clés de session...

tests : fichiers de tests unitaires.

Fichiers de la racine
Il y a un certain nombre de fichiers dans la racine dont voici les principaux :

artisan : outil en ligne de Laravel pour des tâches de gestion,

composer.json : fichier de référence de Composer,

phpunit.xml : fichier de configuration de phpunit (pour les tests unitaires),

.env : fichier pour spécifier l'environnement d'exécution.
```

