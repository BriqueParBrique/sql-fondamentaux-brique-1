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

Plusieurs films partagent le même genre. Si on demande juste la colonne `genre`,
on obtient donc la même valeur plusieurs fois :

```sql
SELECT genre FROM films;
```

On récupère 10 lignes, alors qu'il n'y a que 5 genres différents. `DISTINCT`
élimine les doublons :

```sql
SELECT DISTINCT genre FROM films;
```

| genre            |
| ---------------- |
| Animation        |
| Comédie          |
| Comédie musicale |
| Science-fiction  |
| Thriller         |

C'est la façon la plus simple de répondre à la question « quelles valeurs
existent dans cette colonne ? ».

*(L'ordre d'affichage peut varier d'un outil à l'autre : sans `ORDER BY`, SQL ne
promet aucun ordre. On verra ça à l'étape 5.)*

`DISTINCT` se place juste après `SELECT` et s'applique à **l'ensemble** des
colonnes demandées, pas seulement à la première :

```sql
-- Les combinaisons genre + année qui existent réellement
SELECT DISTINCT genre, annee FROM films;
```

Deux lignes ne sont supprimées que si **toutes** leurs colonnes sont identiques.

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

En utilisant la table `films` créée à l'étape précédente. Le nombre de lignes
attendu est indiqué entre parenthèses : c'est ta façon de vérifier ton résultat
**avant** d'ouvrir le corrigé.

1. Affiche uniquement les titres de tous les films *(10 lignes)*
2. Affiche le titre et la note de chaque film *(10 lignes)*
3. Affiche toutes les colonnes de la table *(10 lignes, 5 colonnes)*
4. Affiche le genre et le titre (dans cet ordre) de chaque film *(10 lignes)*
5. Affiche la liste des années de sortie, sans doublon *(9 lignes)*

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

-- 5. Années sans doublon
--    (2001 apparaît trois fois dans la table, une seule fois ici)
SELECT DISTINCT annee FROM films;
```

</details>
