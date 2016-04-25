# Mise en page

Pour commencer nous allons faire la mise en page qui va être utilisée dans toutes les versions du site.

## Le fichier HTML

Créez un fichier HTML ```index.html```

```
<!doctype html>
<html>
 <head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1"/>
  <title>Mise en page</title>
 </head>
 <body>
  <!-- le corp du document -->
 </body>
</html> 
```

## Le fichier CSS

Nous allons utiliser [bootstrap](http://getbootstrap.com) de Twitter comme base pour les styles et un fichier ```style.css``` avec nos propres styles.

Créez le fichier ```style.css``` et ajoutez des liens aux feuilles de style à l'intérieur de la balise ```<head>``` du fichier ```index.html```.

```
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css" integrity="sha384-1q8mTJOASx8j1Au+a5WDVnPi2lkFfwwEAa8hDDdjZlpLegxhjVME1fgjWPGmkzs7" crossorigin="anonymous">
<link rel="stylesheet" href="style.css">
```

## Les différentes parties de la page

### Structure de base

Dans le corp du document, nous allons avoir une ```<div>``` qui englobe toute la page avec un ```id="contenu"```. Et à l'intérieur de celle-ci:
* le titre
* la liste de ce qu'il y a à faire
* un formulaire pour ajouter des choses à faire et supprimer ce qui a été fait

```
<div id="contenu">
 <h1>À faire</h1>
 <div id="liste"></div>
 <div id="formulaire"></div>
</div>
```

**CSS**

Dans ```style.css```:

```
/* le contenu fait 90% de la largeur du corp de la page */
#contenu {
 width: 90%;
 margin: auto;
}

/* si la page fait plus de 550 pixels de large, le contenu en fait 500 */
@media (min-width: 550px) {
 #contenu { width: 500px }
}
```

### Les éléments de la liste

La liste sera composée d'éléments qui sont soit "fait" ou "à faire". 

Si l'élément est "fait":

```
<div class="liste-element fait"></div>
```

S'il est "à faire":

```
<div class="liste-element a-faire"></div>
```

**CSS**

```
/* element de la liste */
.liste-element {
 padding: 20px;
 border-radius: 5px;
 margin-top: 5px;
}

/* fond rouge si fait, vert si à faire */
.fait {
 background-color: #fb9a99
}
.a-faire {
 background-color: #b2df8a
}
```

### Structure d'un élément de la liste

Chaque élément de la liste sera potentiellement composé de deux parties:

* Les infos: ce qu'il y a à faire, un bouton pour mettre à jour et un bouton pour le marquer comme "fait" ou "à faire"
* Si l'élément est en cours de modification, une partie avec une balise ```<input>``` pour faire la modification et un bouton pour l'envoyer

```
<div class="liste-element-info">
 <div class="liste-element-texte">
  <p>Ce qu'il y a à faire</p>
 </div>
 <div class="liste-element-modif">
  <span class="glyphicon glyphicon-pencil"></span>
 </div>
 <div class="liste-element-statut">
  <!-- si fait -->
  <span class="glyphicon glyphicon-ok"></span>
  <!-- si à faire -->
  <span class="glyphicon glyphicon-remove"></span>
 </div>
</div>

<!-- si en cours de modification: -->
<div class="liste-element-maj">
 <div class="liste-element-maj-input">
  <input class="form-control" id="liste-element-maj-input" type="text">
 </div>
 <div class="liste-element-maj-bouton">
  <button class="btn btn-primary" id="liste-element-maj-bouton">OK</button>
 </div>
</div> 
```

**CSS**

Le style des classes ```form-control```, ```btn btn-primary```, ```glyphicon```, ```glyphicon-ok```, ```glyphicon-remove``` et ```glyphicon-pencil``` sont définies par Bootstrap. Dans ```style.css```, nous définissons les autres:

```
/* table pour les infos */
.liste-element-info {
 display: table;
 width: 100%;
}

/* cellules de la table info */
.liste-element-texte, .liste-element-modif, .liste-element-statut {
 display: table-cell;
 vertical-align: middle;
}

/* première cellule de la table info */
.liste-element-texte {
 width: 80%;
 padding: 2px;
 overflow: scroll;
}

/* les deux autres cellules de la table info */
.list-item-update .list-item-completed {
 width: 10%;
}

/* table pour element en cours de mise à jour */
.liste-element-maj {
 margin-top: 20px;
 display: table;
}

/* cellules de la table de mise à jour */
.liste-element-maj-input, .liste-element-maj-input-bouton {
 display: table-cell;
 vertical-align: middle;
}

/* première cellule de la table de mise à jour */
.liste-element-maj-input {
 width: 80%;
}

/* deuxième cellule de la table de mise à jour */
.liste-element-maj-input-bouton {
 width: 20%;
}
```

### Le formulaire pour ajouter quelque chose à faire et supprimer ce qui a été fait
 
À l'intérieur de la balise ```<div id="formulaire"></div>```, nous ajoutons:

* Une partie pour ajouter quelque chose à faire avec une balise ```<input>``` et un bouton ```OK```
* Une autre avec un bouton ```Supprimer ce qui a été fait```

```
<div class="ajouter">
 <div class="ajouter-input">
  <input id="add-todo-input" class="form-control" placeholder="À faire" type="text">
 </div>
 <div class="ajouter-bouton">
  <button id="ajouter-bouton" class="btn btn-primary">OK</button>
 </div>
</div>
<div id="supprimer-fait">
 <button id="supprimer-fait-bouton" class="btn btn-danger">Supprimer ce qui a été fait</button>
</div>
```

**CSS**

Le style des classes ```form-control```, ```btn```, ```btn-primary``` et ```btn-danger``` est géré par Bootstrap, pour le reste:

```
/* table ajouter à faire */
.ajouter {
 display: table;
 width: 100%;
}

/* cellules de la table ajouter */
.ajouter-input, .ajouter-bouton {
 display: table-cell;
 vertical-align: middle;
}

/* première cellule de la table ajouter */
.ajouter-input {
 width: 80%;
}

/* deuxième cellule de la table ajouter */
.ajouter-bouton {
 width: 20%;
 text-align: center
}

/* aérer ajouter et supprimer-fait */
.ajouter, #supprimer-fait {
 margin-top: 30px;
}
```

## La page de test de mise en page

Pour vérifier que tout fonctionne créons une page avec trois éléments de liste:

* Un élément "à faire"
* Un élément "fait"
* Un élément "à faire" en cours de modification

```
<!doctype html>
<html>
 <head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1"/>
  <title>Mise en page</title>
<!-- feuille de style "bootstrap" de http://getbootstrap.com -->
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css" integrity="sha384-1q8mTJOASx8j1Au+a5WDVnPi2lkFfwwEAa8hDDdjZlpLegxhjVME1fgjWPGmkzs7" crossorigin="anonymous">
<!-- notre feuille de style -->
  <link rel="stylesheet" href="style.css">
 </head>
 <body>
<!-- une DIV pour tout le contenu -->
  <div id="contenu">
<!-- le titre -->
   <h1>À faire</h1>
<!-- la liste de ce qu'il y a à faire -->
   <div id="liste">
<!-- un element de la liste "fait" -->
    <div class="liste-element fait">
     <div class="liste-element-info">
      <div class="liste-element-texte">
       <p>Fait</p>
      </div>
      <div class="liste-element-modif">
       <span class="glyphicon glyphicon-pencil"></span>
      </div>
      <div class="liste-element-statut">
       <span class="glyphicon glyphicon-remove"></span>
      </div>
     </div>
    </div>
<!-- un element de la liste "à faire" -->
    <div class="liste-element a-faire">
     <div class="liste-element-info">
      <div class="liste-element-texte">
       <p>À faire</p>
      </div>
      <div class="liste-element-modif">
       <span class="glyphicon glyphicon-pencil"></span>
      </div>
      <div class="liste-element-statut">
       <span class="glyphicon glyphicon-ok"></span>
      </div>
     </div>
    </div>
<!-- un element de la liste en cours de modification -->
    <div class="liste-element a-faire">
     <div class="liste-element-info">
      <div class="liste-element-texte">
       <p>En cours de modification</p>
      </div>
      <div class="liste-element-modif">
       <span class="glyphicon glyphicon-pencil"></span>
      </div>
      <div class="liste-element-statut">
       <span class="glyphicon glyphicon-ok"></span>
      </div>
     </div>
     <div class="liste-element-maj">
      <div class="liste-element-maj-input">
       <input class="form-control" id="liste-element-maj-input" type="text">
      </div>
      <div class="liste-element-maj-bouton">
       <button class="btn btn-primary" id="liste-element-maj-bouton">OK</button>
      </div>
     </div>
    </div>
   </div>
   <div id="formulaire">
    <div class="ajouter">
     <div class="ajouter-input">
      <input id="ajouter-input" class="form-control" placeholder="À faire" type="text">
     </div>
     <div class="ajouter-bouton">
      <button id="ajouter-bouton" class="btn btn-primary">Ajouter</button>
     </div>
    </div>
    <div id="supprimer-fait">
     <button id="supprimer-fait-bouton" class="btn btn-danger">Supprimer ce qui a été fait</button>
    </div>
   </div>
  </div>
 </body>
</html>
```

Maintenant que nous avons la mise en page souhaitée, nous pouvons passer à l'interaction.

