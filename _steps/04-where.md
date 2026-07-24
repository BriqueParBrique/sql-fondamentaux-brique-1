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

### Un intervalle avec `BETWEEN`

Pour cibler une plage de valeurs, on peut combiner deux conditions :

```sql
SELECT titre, annee FROM films
WHERE annee >= 2000 AND annee <= 2010;
```

`BETWEEN` écrit exactement la même chose, en plus lisible :

```sql
SELECT titre, annee FROM films
WHERE annee BETWEEN 2000 AND 2010;
```

| titre          | annee |
| -------------- | ----- |
| Inception      | 2010  |
| Amélie Poulain | 2001  |
| Spirited Away  | 2001  |

Deux points à retenir :

- Les **deux bornes sont incluses** : `BETWEEN 2000 AND 2010` garde 2000 et 2010.
- L'ordre compte : il faut écrire la petite valeur d'abord. `BETWEEN 2010 AND 2000` ne renvoie jamais rien.

### Différent de : `!=` ou `<>`

Tous les films sauf les comédies :

```sql
SELECT titre, genre FROM films
WHERE genre != 'Comédie';
```

> **À noter pour plus tard** : dans une vraie base, une colonne peut être *vide*
> (on parle de valeur `NULL`, par exemple un film dont on ne connaît pas le
> genre). Ces lignes ne sont renvoyées **ni** par `genre = 'Comédie'`, **ni** par
> `genre != 'Comédie'` — elles sont écartées des deux côtés. Notre table n'a
> aucune valeur vide, donc le problème ne se pose pas ici, mais garde-le en
> tête : on l'attaquera pour de bon au niveau 2.

### Recherche partielle avec `LIKE`

`LIKE` permet de chercher un motif dans du texte, alors que `=` exige une égalité
parfaite. Le symbole `%` remplace **n'importe quel texte, y compris rien du tout** :

```sql
-- Titres qui commencent par "Le"
SELECT titre FROM films
WHERE titre LIKE 'Le%';
```

| titre            |
| ---------------- |
| Le Roi Lion      |
| Le Dîner de cons |

L'intérêt devient net quand une valeur en contient une autre. Notre table a un
genre `Comédie` **et** un genre `Comédie musicale` :

```sql
-- Tous les genres qui contiennent "Comédie"
SELECT titre, genre FROM films
WHERE genre LIKE '%Comédie%';
```

| titre            | genre            |
| ---------------- | ---------------- |
| Amélie Poulain   | Comédie          |
| Intouchables     | Comédie          |
| La La Land       | Comédie musicale |
| Le Dîner de cons | Comédie          |

Avec `genre = 'Comédie'`, *La La Land* n'apparaîtrait pas.

### Le joker `_` : un seul caractère

Là où `%` remplace un texte de n'importe quelle longueur, le tiret bas `_`
remplace **exactement un caractère** :

```sql
-- M, puis un caractère quelconque, puis "trix"
SELECT titre FROM films
WHERE titre LIKE 'M_trix';
```

Cela trouve `Matrix`. En revanche `LIKE 'M_trix'` ne trouverait pas `Maatrix`
(deux caractères entre le M et le « trix »), là où `LIKE 'M%trix'` le trouverait.

### Deux pièges de `LIKE` avec le français

1. **La casse est ignorée… pour les lettres non accentuées seulement.** En
   SQLite, `LIKE 'le%'` trouve bien `Le Roi Lion` : `l` et `L` sont considérés
   comme équivalents.
2. **Mais les accents ne sont pas ignorés.** `LIKE '%comedie%'` ne trouve
   **rien**, parce que `e` et `é` sont deux caractères différents. Pour trouver
   « Comédie », il faut écrire l'accent : `LIKE '%comédie%'`.

Autrement dit, si une recherche accentuée ne renvoie rien alors que tu es sûr·e
que la donnée existe, vérifie d'abord tes accents.

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

Le nombre de lignes attendu est indiqué entre parenthèses.

1. Affiche les films sortis avant 2000 *(4 lignes)*
2. Affiche les films dont la note est strictement supérieure à 8.5 *(3 lignes)*
3. Affiche les films dont le titre contient "Land" *(1 ligne)*
4. Affiche les films de genre "Comédie" sortis après 2005 *(1 ligne)*
5. Affiche les films qui sont soit des "Thriller" soit des "Animation" *(4 lignes)*
6. Affiche les films sortis entre 1995 et 2001 inclus, en utilisant `BETWEEN` *(5 lignes)*
7. Affiche les films dont le titre fait exactement 6 caractères *(1 ligne — indice : combien de `_` faut-il ?)*

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

-- 6. Sortis entre 1995 et 2001 inclus
SELECT * FROM films
WHERE annee BETWEEN 1995 AND 2001;

-- 7. Titres de 6 caractères exactement : six jokers `_`, ni plus ni moins.
--    Seul « Matrix » convient.
SELECT titre FROM films
WHERE titre LIKE '______';
```

</details>
