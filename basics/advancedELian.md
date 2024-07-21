# Exercices Avancés MongoDB avec la Base de Données Titanic

## Exercice 1: Importation et Création de la Collection

Importer les données du fichier `titanic.csv` dans une collection `Passengers` de la base de données `TitanicDB`.

## Exercice 2: Analyse des Données

**Objectif :** Effectuer des opérations de lecture et d'analyse sur les données.

### Instructions

1. Comptez le nombre total de passagers.

```bash
db.Passengers.countDocuments()
```

2. Trouvez combien de passagers ont survécu.

```bash
db.Passengers.countDocuments({ Survived: 1 })
```

3. Trouvez le nombre de passagers femmes.

```bash
db.Passengers.countDocuments({ Sex: "female" })
```

4. Trouvez le nombre de passagers avec au moins 3 enfants.

```bash
db.Passengers.countDocuments({ SibSp: { $gte: 3 } })
```

## Exercice 3: Mise à Jour de Données

**Objectif :** Corriger ou ajouter des informations à certains documents.

### Instructions

1. Mettez à jour les documents pour lesquels le port d'embarquement est manquant, en supposant qu'ils sont montés à bord à Southampton.

```bash
db.Passengers.updateMany(
  { Embarked: { $exists: false } },
  { $set: { Embarked: "S" } }
```

2. Ajoutez un champ `rescued` avec la valeur `true` pour tous les passagers qui ont survécu.

```bash
db.Passengers.updateMany(
   { Survived: 1 },
   { $set: { rescued: true } }
)
```

## Exercice 4: Requêtes Complexes

**Objectif :** Effectuer des requêtes plus complexes pour analyser les données.

### Instructions

1. Sélectionnez les noms des 10 passagers les plus jeunes.

```bash
db.Passengers.find({}, { Name: 1, _id: 0 }).sort({ Age: 1 }).limit(10)
```

2. Identifiez les passagers qui n'ont pas survécu et qui étaient dans la 2e classe.

```bash
db.Passengers.find({ Survived: 0, Pclass: 2 })
```

## Exercice 5: Suppression de Données

**Objectif :** Supprimer des données spécifiques de la base de données.

### Instructions

Supprimez les enregistrements des passagers qui n'ont pas survécu et dont l'âge est inconnu.

```bash
db.Passengers.deleteMany({ Survived: 0, Age: null })
```

## Exercice 6: Mise à Jour en Masse

**Objectif :** Augmenter l'âge de tous les passagers de 1 an.

### Instructions

1. Utilisez une opération de mise à jour pour augmenter la valeur du champ `Age` de 1 pour tous les documents.

```bash
db.Passengers.updateMany({}, { $inc: { Age: 1 } })
```

## Exercice 7: Suppression Conditionnelle

**Objectif :** Supprimer les enregistrements des passagers qui n'ont pas de numéro de billet (`Ticket`).

### Instructions

1. Supprimez tous les documents où le champ `Ticket` est absent ou vide.

```bash
db.Passengers.deleteMany({ $or: [{ Ticket: { $exists: false } }, { Ticket: "" }] })
```

## Bonus: Utiliser les REGEX

**Objectif :** Utiliser une regex pour trouver tous les passagers selon une condition.

### Instructions

1. Utiliser une regex pour trouver tous les passagers qui porte le titre de `Dr.`

```bash
db.Passengers.find({ Name: { $regex: /Dr\./ } })
```

## Validation

Utilisez les commandes MongoDB appropriées pour valider les résultats de chaque exercice. Assurez-vous que les opérations de mise à jour, d'insertion, et de suppression ont été effectuées correctement.

Vérifier que les passagers sans numéro de billet ont été supprimés

```bash
db.Passengers.find({ $or: [{ Ticket: { $exists: false } }, { Ticket: "" }] }).count()
```

Vérifier que les passagers qui n'ont pas survécu et dont l'âge est inconnu ont été supprimés

```bash
db.Passengers.find({ Survived: 0, Age: null }).count()
```

Vérifier que l'âge de tous les passagers a été augmenté de 1 an

```bash
db.Passengers.find({}, { Age: 1, _id: 0 }).forEach(printjson)
```

Vérifier que les passagers portant le titre de `Dr.` sont correctement trouvés

```bash
db.Passengers.find({ Name: { $regex: /Dr\./ } }).forEach(printjson)
```