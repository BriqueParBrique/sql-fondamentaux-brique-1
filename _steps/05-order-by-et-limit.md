---
title: "ORDER BY et LIMIT"
---

## Trier et limiter les résultats

### Trier avec `ORDER BY`

Par défaut, SQL ne garantit aucun ordre particulier. `ORDER BY` permet de trier les résultats.

Trier par année (du plus ancien au plus récent) :

```sql
SELECT titre, annee FROM films
ORDER BY annee;
```

### Ordre croissant et décroissant

- `ASC` (ascending) : du plus petit au plus grand — **c'est le comportement par défaut**
- `DESC` (descending) : du plus grand au plus petit

```sql
-- Les films les mieux notés en premier
SELECT titre, note FROM films
ORDER BY note DESC;
```

### Trier sur plusieurs colonnes

On peut trier sur une colonne, puis sur une autre en cas d'égalité :

```sql
-- Trier par genre, puis par note décroissante
SELECT titre, genre, note FROM films
ORDER BY genre, note DESC;
```

### Limiter le nombre de résultats avec `LIMIT`

`LIMIT` permet de ne récupérer que les N premiers résultats :

```sql
-- Les 3 films les mieux notés
SELECT titre, note FROM films
ORDER BY note DESC
LIMIT 3;
```

| titre | note |
|-------|------|
| Inception | 8.8 |
| Matrix | 8.7 |
| Spirited Away | 8.6 |

### Paginer avec `OFFSET`

`OFFSET` permet de sauter un certain nombre de résultats avant de commencer à afficher. Combiné avec `LIMIT`, c'est le mécanisme de **pagination** utilisé par les sites web :

```sql
-- Page 1 : les 3 premiers films
SELECT titre, note FROM films
ORDER BY note DESC
LIMIT 3 OFFSET 0;

-- Page 2 : les 3 suivants
SELECT titre, note FROM films
ORDER BY note DESC
LIMIT 3 OFFSET 3;
```

`OFFSET 3` signifie "saute les 3 premiers résultats". C'est comme ça que fonctionnent les boutons "Page suivante" sur les sites de recherche.

### Combiner avec `WHERE`

On peut bien sûr combiner `WHERE`, `ORDER BY` et `LIMIT` :

```sql
-- Le film d'animation le mieux noté
SELECT titre, note FROM films
WHERE genre = 'Animation'
ORDER BY note DESC
LIMIT 1;
```

### L'ordre des clauses

L'ordre des mots-clés dans une requête SQL est toujours le même :

```sql
SELECT colonnes
FROM table
WHERE conditions
ORDER BY colonnes
LIMIT nombre
OFFSET décalage;
```

Cet ordre est **obligatoire**. On ne peut pas mettre `WHERE` après `ORDER BY`, par exemple.

### Exercice

1. Affiche tous les films triés par titre en ordre alphabétique
2. Affiche les 5 films les plus récents
3. Affiche le film le plus ancien
4. Affiche les films d'animation triés par note décroissante
5. Affiche les 3 films les mieux notés sortis après 2000
6. Affiche les films classés 4e à 6e par note décroissante (la "page 2" du top)

<details>
<summary>Voir les réponses</summary>

```sql
-- 1. Triés par titre
SELECT * FROM films
ORDER BY titre;

-- 2. Les 5 plus récents
SELECT * FROM films
ORDER BY annee DESC
LIMIT 5;

-- 3. Le plus ancien
SELECT * FROM films
ORDER BY annee
LIMIT 1;

-- 4. Animation par note décroissante
SELECT * FROM films
WHERE genre = 'Animation'
ORDER BY note DESC;

-- 5. Top 3 après 2000
SELECT * FROM films
WHERE annee > 2000
ORDER BY note DESC
LIMIT 3;

-- 6. Page 2 du classement (positions 4 à 6)
SELECT * FROM films
ORDER BY note DESC
LIMIT 3 OFFSET 3;
```

</details>
