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

### Attention aux ex æquo

`LIMIT` coupe la liste après N lignes. Mais que se passe-t-il si la 3ᵉ et la 4ᵉ
ligne ont **la même note** ?

Trois films de notre table ont exactement 8.5 : *Intouchables*, *Le Roi Lion* et
*Parasite*. Demandons les deux meilleurs parmi eux :

```sql
SELECT titre, note FROM films
WHERE note = 8.5
ORDER BY note DESC
LIMIT 2;
```

SQL doit en écarter un — mais **lequel n'est pas défini**. Le tri ne porte que
sur `note`, et pour lui ces trois lignes sont interchangeables. Deux exécutions,
deux outils, ou deux versions de SQLite peuvent renvoyer des résultats
différents, tous également corrects.

C'est une source classique de confusion : « mon collègue a la même requête et
pas le même résultat ». La solution est d'ajouter un **critère de départage**,
c'est-à-dire une deuxième colonne de tri qui, elle, n'a pas de doublon :

```sql
-- Départage par titre : le résultat est maintenant toujours le même
SELECT titre, note FROM films
WHERE note = 8.5
ORDER BY note DESC, titre
LIMIT 2;
```

**La règle** : dès que tu utilises `LIMIT`, demande-toi si la colonne de tri peut
contenir des doublons. Si oui, ajoute une colonne de départage (souvent `id`, qui
est unique par construction).

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
LIMIT nombre;
```

Cet ordre est **obligatoire**. On ne peut pas mettre `WHERE` après `ORDER BY`, par exemple.

### Exercice

Le nombre de lignes attendu est indiqué entre parenthèses.

1. Affiche tous les films triés par titre en ordre alphabétique *(10 lignes)*
2. Affiche le film le plus ancien *(1 ligne)*
3. Affiche les films d'animation triés par note décroissante *(3 lignes)*
4. Affiche les 5 films les plus récents. **Attention** : trois films sont sortis
   en 2001, il te faut donc un critère de départage pour que le résultat soit
   stable *(5 lignes)*
5. Affiche les 3 films les mieux notés sortis après 2000. Là encore, deux films
   sont à égalité à 8.5 : départage-les *(3 lignes)*

<details>
<summary>Voir les réponses</summary>

```sql
-- 1. Triés par titre
SELECT * FROM films
ORDER BY titre;

-- 2. Le plus ancien (1994, aucune égalité possible)
SELECT * FROM films
ORDER BY annee
LIMIT 1;

-- 3. Animation par note décroissante
SELECT * FROM films
WHERE genre = 'Animation'
ORDER BY note DESC;

-- 4. Les 5 plus récents.
--    Sans le départage par titre, on ne saurait pas lequel des trois films de
--    2001 est retenu à la 5ᵉ place.
SELECT * FROM films
ORDER BY annee DESC, titre
LIMIT 5;

-- 5. Top 3 après 2000.
--    Intouchables et Parasite sont tous deux à 8.5 : le tri par titre décide.
SELECT * FROM films
WHERE annee > 2000
ORDER BY note DESC, titre
LIMIT 3;
```

</details>
