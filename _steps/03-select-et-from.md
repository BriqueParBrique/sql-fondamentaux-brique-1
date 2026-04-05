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

### Supprimer les doublons avec `DISTINCT`

Si une colonne contient des valeurs répétées, `DISTINCT` permet de n'afficher chaque valeur qu'une seule fois :

```sql
SELECT DISTINCT genre FROM films;
```

| genre |
|-------|
| Science-fiction |
| Comédie |
| Animation |
| Thriller |
| Comédie musicale |
| Drame |

Sans `DISTINCT`, le genre "Comédie" apparaîtrait deux fois (une fois pour Amélie Poulain, une fois pour Intouchables).

### Renommer une colonne avec `AS`

`AS` permet de donner un nom temporaire (un **alias**) à une colonne dans le résultat :

```sql
SELECT titre, annee AS sortie FROM films;
```

| titre | sortie |
|-------|--------|
| Inception | 2010 |
| Amélie Poulain | 2001 |
| ... | ... |

La colonne s'appelle toujours `annee` dans la table, mais elle s'affiche comme `sortie` dans le résultat. C'est utile pour rendre les résultats plus lisibles.

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
5. Affiche la liste des genres disponibles (sans doublons)
6. Affiche le titre et la note, en renommant la colonne `note` en `evaluation`

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

-- 5. Genres sans doublons
SELECT DISTINCT genre FROM films;

-- 6. Alias sur la colonne note
SELECT titre, note AS evaluation FROM films;
```

</details>
