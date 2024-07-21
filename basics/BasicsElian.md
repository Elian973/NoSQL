# Exercices MongoDB avec la Base de Données Pokémon GO

## Exercice 1: Création d'une Base de Données et d'une Collection
Créer une base de données `PokemonDB` et une collection `Pokemons`.

## Exercice 2: Insertion de Données
Insérer les données des Pokémon à partir du fichier `pokemonGO.csv` dans la collection `Pokemons`.

## Exercice 3: Lecture de Données
**Objectif :** Lire les données de certains Pokémon spécifiques.

### Instructions
1. Trouvez tous les Pokémon de type "Feu".

```bash
db.Pokemons.find({
  "$or": [
    { "Type 1": "Fire" },
    { "Type 2": "Fire" }
  ]
})
```

2. Récupérez les informations du Pokémon nommé "Pikachu".

```bash
db.Pokemons.find({ "Name": "Pikachu" })
```

## Exercice 4: Mise à Jour de Données
**Objectif :** Mettre à jour les informations d'un Pokémon.

### Instructions
Mettez à jour les points de combat (CP) de "Pikachu" pour qu'ils soient de 900.

```bash
db.Pokemons.updateOne({
    'Name': 'Pikachu'},
    {'$set': {'Max CP': 900}
})
```

## Exercice 5: Suppression d'Éléments
**Objectif :** Supprimer un Pokémon de la base de données.

### Instructions
Supprimez le Pokémon "Bulbasaur" de la collection `Pokemons`.

```bash
db.Pokemons.deleteOne({ name: "Bulbasaur" })
```

## Validation
Après avoir complété chaque exercice, utilisez les commandes appropriées pour vérifier que vos opérations ont été réalisées correctement.

```bash
db.Pokemons.find({
  "$or": [
    { "Type 1": "Fire" },
    { "Type 2": "Fire" }
  ]
})
db.Pokemons.find({ Name: "Pikachu" })
db.Pokemons.updateOne({
    'Name': 'Pikachu'},
    {'$set': {'Max CP': 900}
})
db.Pokemons.find({ Name: "Bulbasaur" }).count()
```