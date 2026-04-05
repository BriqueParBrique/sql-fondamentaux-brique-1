---
title: "WHERE"
---

## Filtrer les résultats

`WHERE` permet de ne garder que les lignes qui correspondent à une condition. C'est comme appliquer un filtre dans un tableur.

### Filtrer avec `=`

Pour trouver les films d'un genre précis :

```sql
SELECT titre, genre FROM films
WHERE genre = 'Animation';
```

| titre | genre |
|-------|-------|
| Le Roi Lion | Animation |
| Toy Story | Animation |
| Spirited Away | Animation |

### Comparer des nombres avec `<`, `>`, `<=`, `>=`

Films sortis après 2010 :

```sql
SELECT titre, annee FROM films
WHERE annee > 2010;
```

Films avec une note supérieure ou égale à 8.5 :

```sql
SELECT titre, note FROM films
WHERE note >= 8.5;
```

### Différent de : `!=` ou `<>`

Tous les films sauf les comédies :

```sql
SELECT titre, genre FROM films
WHERE genre != 'Comédie';
```

### Intervalle avec `BETWEEN`

`BETWEEN` permet de vérifier qu'une valeur se trouve dans un intervalle (bornes incluses) :

```sql
-- Films sortis entre 2000 et 2010
SELECT titre, annee FROM films
WHERE annee BETWEEN 2000 AND 2010;
```

C'est équivalent à `annee >= 2000 AND annee <= 2010`, mais plus lisible.

### Valeurs manquantes avec `IS NULL` et `IS NOT NULL`

En SQL, une valeur manquante s'appelle `NULL`. Ce n'est pas zéro ni une chaîne vide — c'est l'absence de valeur.

Pour tester si une valeur est manquante, on utilise `IS NULL` :

```sql
-- Films sans note
SELECT titre FROM films
WHERE note IS NULL;
```

Et pour trouver les lignes qui ont une valeur :

```sql
-- Films qui ont une note
SELECT titre, note FROM films
WHERE note IS NOT NULL;
```

> **Piège courant** : on ne peut pas écrire `WHERE note = NULL`. En SQL, `NULL` n'est égal à rien, même pas à lui-même. Il faut toujours utiliser `IS NULL` ou `IS NOT NULL`.

### Recherche partielle avec `LIKE`

`LIKE` permet de chercher un motif dans du texte. Le symbole `%` remplace n'importe quel texte :

```sql
-- Titres qui commencent par "Le"
SELECT titre FROM films
WHERE titre LIKE 'Le%';

-- Titres qui contiennent "Amélie"
SELECT titre FROM films
WHERE titre LIKE '%Amélie%';
```

### Plusieurs valeurs avec `IN`

Plutôt que d'écrire plusieurs conditions, `IN` permet de vérifier si une valeur fait partie d'une liste :

```sql
SELECT titre, genre FROM films
WHERE genre IN ('Animation', 'Science-fiction');
```

### Combiner des conditions avec `AND` et `OR`

```sql
-- Films d'animation sortis après 2000
SELECT titre, annee FROM films
WHERE genre = 'Animation' AND annee > 2000;

-- Films d'animation OU de science-fiction
SELECT titre, genre FROM films
WHERE genre = 'Animation' OR genre = 'Science-fiction';
```

### Exercice

1. Affiche les films sortis avant 2000
2. Affiche les films dont la note est strictement supérieure à 8.5
3. Affiche les films dont le titre contient "Land"
4. Affiche les films de genre "Comédie" sortis après 2005
5. Affiche les films qui sont soit des "Thriller" soit des "Animation"
6. Affiche les films sortis entre 1995 et 2005 (inclus)

<details>
<summary>Voir les réponses</summary>

```sql
-- 1. Films avant 2000
SELECT * FROM films
WHERE annee < 2000;

-- 2. Note > 8.5
SELECT * FROM films
WHERE note > 8.5;

-- 3. Titre contient "Land"
SELECT * FROM films
WHERE titre LIKE '%Land%';

-- 4. Comédie après 2005
SELECT * FROM films
WHERE genre = 'Comédie' AND annee > 2005;

-- 5. Thriller ou Animation
SELECT * FROM films
WHERE genre IN ('Thriller', 'Animation');

-- 6. Films entre 1995 et 2005
SELECT * FROM films
WHERE annee BETWEEN 1995 AND 2005;
```

</details>
