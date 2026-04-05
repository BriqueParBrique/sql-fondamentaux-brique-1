---
title: "Mini-projet"
---

## Mini-projet : Explorons une base de films !

Félicitations, tu as appris les bases de SQL ! Il est temps de tout mettre en pratique avec un mini-projet.

### Le jeu de données

On va enrichir notre base de films. Exécute ce code pour remplacer les données par un jeu plus complet :

```sql
DROP TABLE IF EXISTS films;

CREATE TABLE films (
    id INTEGER PRIMARY KEY,
    titre TEXT,
    realisateur TEXT,
    annee INTEGER,
    genre TEXT,
    pays TEXT,
    note REAL,
    duree_min INTEGER
);

INSERT INTO films (id, titre, realisateur, annee, genre, pays, note, duree_min) VALUES
(1, 'Inception', 'Christopher Nolan', 2010, 'Science-fiction', 'USA', 8.8, 148),
(2, 'Amélie Poulain', 'Jean-Pierre Jeunet', 2001, 'Comédie', 'France', 8.3, 122),
(3, 'Intouchables', 'Olivier Nakache', 2011, 'Comédie', 'France', 8.5, 112),
(4, 'Le Roi Lion', 'Roger Allers', 1994, 'Animation', 'USA', 8.5, 88),
(5, 'Parasite', 'Bong Joon-ho', 2019, 'Thriller', 'Corée du Sud', 8.5, 132),
(6, 'Toy Story', 'John Lasseter', 1995, 'Animation', 'USA', 8.3, 81),
(7, 'La La Land', 'Damien Chazelle', 2016, 'Comédie musicale', 'USA', 8.0, 128),
(8, 'Matrix', 'Lana Wachowski', 1999, 'Science-fiction', 'USA', 8.7, 136),
(9, 'Le Grand Bleu', 'Luc Besson', 1988, 'Drame', 'France', 7.6, 168),
(10, 'Spirited Away', 'Hayao Miyazaki', 2001, 'Animation', 'Japon', 8.6, 125),
(11, 'The Dark Knight', 'Christopher Nolan', 2008, 'Action', 'USA', 9.0, 152),
(12, 'Coco', 'Lee Unkrich', 2017, 'Animation', 'USA', 8.4, 105),
(13, 'Les Choristes', 'Christophe Barratier', 2004, 'Drame', 'France', 7.8, 97),
(14, 'Your Name', 'Makoto Shinkai', 2016, 'Animation', 'Japon', 8.4, 106),
(15, 'Interstellar', 'Christopher Nolan', 2014, 'Science-fiction', 'USA', 8.6, 169);
```

### Les défis

Écris les requêtes SQL pour répondre à chaque question :

**Défi 1 — Découverte** : Affiche le titre et le réalisateur de tous les films.

**Défi 2 — Filtrage simple** : Quels films sont sortis après 2010 ?

**Défi 3 — Filtrage par pays** : Affiche les films français (pays = 'France').

**Défi 4 — Les meilleurs** : Quels sont les 3 films les mieux notés ? Affiche leur titre et leur note.

**Défi 5 — Recherche** : Trouve tous les films dont le titre contient "Le" ou "Les".

**Défi 6 — Combiné** : Affiche les films d'animation japonais, triés par note décroissante.

<details>
<summary>Indices</summary>

- **Défi 1** : `SELECT` avec deux colonnes, pas besoin de `WHERE`
- **Défi 2** : Utilise `WHERE` avec l'opérateur `>`
- **Défi 3** : Utilise `WHERE` avec `=` sur la colonne `pays`
- **Défi 4** : Combine `ORDER BY ... DESC` et `LIMIT`
- **Défi 5** : Utilise `LIKE` avec `%` et combine avec `OR`
- **Défi 6** : Combine deux conditions avec `AND` et ajoute `ORDER BY`

</details>

<details>
<summary>Voir les solutions</summary>

```sql
-- Défi 1 : Titre et réalisateur
SELECT titre, realisateur FROM films;

-- Défi 2 : Films après 2010
SELECT titre, annee FROM films
WHERE annee > 2010;

-- Défi 3 : Films français
SELECT titre, realisateur, annee FROM films
WHERE pays = 'France';

-- Défi 4 : Top 3
SELECT titre, note FROM films
ORDER BY note DESC
LIMIT 3;

-- Défi 5 : Titres avec "Le" ou "Les"
SELECT titre FROM films
WHERE titre LIKE 'Le%' OR titre LIKE 'Les%';

-- Défi 6 : Animation japonaise
SELECT titre, note FROM films
WHERE genre = 'Animation' AND pays = 'Japon'
ORDER BY note DESC;
```

</details>

### Défis bonus

Pour ceux qui veulent aller plus loin :

**Défi 7 — Réalisateur prolifique** : Quel réalisateur a le plus de films dans la base ? Affiche chaque réalisateur et ses films, triés par réalisateur.

**Défi 8 — Pays et genres** : Affiche la liste des pays représentés dans la base (sans doublons).

**Défi 9 — Longs métrages** : Quels films durent plus de 2h30 (150 minutes) ? Affiche leur titre et leur durée, renommée en `duree_heures_min`.

**Défi 10 — Classement paginé** : Affiche les films classés de la 4e à la 6e position par note décroissante (comme une "page 2").

<details>
<summary>Indices bonus</summary>

- **Défi 7** : Utilise `ORDER BY realisateur` — au Niveau 2, tu apprendras `GROUP BY` et `COUNT` pour compter automatiquement
- **Défi 8** : Pense à `DISTINCT`
- **Défi 9** : Utilise `AS` pour renommer et `WHERE` pour filtrer sur `duree_min`
- **Défi 10** : Combine `ORDER BY`, `LIMIT` et `OFFSET`

</details>

<details>
<summary>Voir les solutions bonus</summary>

```sql
-- Défi 7 : Films par réalisateur
SELECT realisateur, titre FROM films
ORDER BY realisateur, titre;

-- Défi 8 : Pays sans doublons
SELECT DISTINCT pays FROM films;

-- Défi 9 : Films de plus de 2h30
SELECT titre, duree_min AS duree_heures_min FROM films
WHERE duree_min > 150
ORDER BY duree_min DESC;

-- Défi 10 : Page 2 du classement
SELECT titre, note FROM films
ORDER BY note DESC
LIMIT 3 OFFSET 3;
```

</details>

### Bravo !

Tu maîtrises maintenant les bases de la lecture de données en SQL :

- **SELECT / FROM** pour choisir quoi afficher
- **DISTINCT** pour éliminer les doublons
- **AS** pour renommer les colonnes
- **WHERE** pour filtrer (`=`, `<`, `>`, `LIKE`, `IN`, `BETWEEN`, `IS NULL`)
- **ORDER BY** pour trier (`ASC`, `DESC`)
- **LIMIT / OFFSET** pour limiter et paginer les résultats

Au **Niveau 2**, tu apprendras à **transformer et combiner** les données : compter, calculer des moyennes, et croiser plusieurs tables entre elles.
