---
title: "SELECT et FROM"
---

## Lire les données d'une table

`SELECT` et `FROM` sont les deux mots-clés les plus importants en SQL. Ensemble, ils forment la requête de base pour lire des données.

### Tout sélectionner avec `*`

L'étoile `*` signifie "toutes les colonnes" :

```sql
SELECT * FROM films;
```

Résultat : toutes les colonnes (`id`, `titre`, `annee`, `genre`, `note`) pour chaque film.

### Choisir des colonnes spécifiques

Plutôt que de tout afficher, on peut choisir uniquement les colonnes qui nous intéressent :

```sql
SELECT titre, annee FROM films;
```

| titre | annee |
|-------|-------|
| Inception | 2010 |
| Amélie Poulain | 2001 |
| Intouchables | 2011 |
| ... | ... |

### Choisir plusieurs colonnes

On sépare les noms de colonnes par des virgules :

```sql
SELECT titre, genre, note FROM films;
```

### L'ordre des colonnes

L'ordre dans le `SELECT` détermine l'ordre d'affichage :

```sql
SELECT annee, titre FROM films;
```

Ici, `annee` apparaîtra avant `titre` dans le résultat.

### La syntaxe SQL

Quelques règles à retenir :

- Les mots-clés SQL (`SELECT`, `FROM`) s'écrivent généralement en **MAJUSCULES** (convention, pas obligation)
- Les noms de tables et colonnes s'écrivent en **minuscules**
- Chaque requête se termine par un **point-virgule** `;`
- Les espaces et retours à la ligne n'ont pas d'importance pour SQL

Ces deux requêtes sont identiques :

```sql
SELECT titre, annee FROM films;
```

```sql
SELECT
    titre,
    annee
FROM
    films;
```

### Exercice

En utilisant la table `films` créée à l'étape précédente :

1. Affiche uniquement les titres de tous les films
2. Affiche le titre et la note de chaque film
3. Affiche toutes les colonnes de la table
4. Affiche le genre et le titre (dans cet ordre) de chaque film

<details>
<summary>Voir les réponses</summary>

```sql
-- 1. Titres uniquement
SELECT titre FROM films;

-- 2. Titre et note
SELECT titre, note FROM films;

-- 3. Toutes les colonnes
SELECT * FROM films;

-- 4. Genre puis titre
SELECT genre, titre FROM films;
```

</details>
