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

Écris les requêtes SQL pour répondre à chaque question. Le nombre de lignes
attendu est indiqué : vérifie-le avant d'ouvrir le corrigé.

**Défi 1 — Découverte** : Affiche le titre et le réalisateur de tous les films. *(15 lignes)*

**Défi 2 — Filtrage simple** : Quels films sont sortis après 2010 ? *(6 lignes)*

**Défi 3 — Filtrage par pays** : Affiche les films français (pays = 'France'). *(4 lignes)*

**Défi 4 — Les meilleurs** : Quels sont les 3 films les mieux notés ? Affiche leur titre et leur note. *(3 lignes)*

**Défi 5 — Recherche** : Trouve tous les films dont le titre **commence par** "Le" ou "Les". *(3 lignes)*

**Défi 6 — Combiné** : Affiche les films d'animation japonais, triés par note décroissante. *(2 lignes)*

**Défi 7 — Inventaire** : Quels pays sont représentés dans la table ? Chaque pays ne doit apparaître qu'une fois. *(4 lignes)*

**Défi 8 — Intervalle** : Quels films durent entre 100 et 130 minutes inclus ? Affiche le titre et la durée, du plus court au plus long. *(6 lignes)*

**Défi 9 — Ex æquo** : Affiche les 5 films les mieux notés avec leur note. *Interstellar* et *Spirited Away* sont tous deux à 8.6 et se disputent la 4ᵉ et la 5ᵉ place — assure-toi que ta requête donne toujours le même résultat. *(5 lignes)*

### Solutions

<details markdown="1">
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

-- Défi 5 : Titres commençant par "Le" ou "Les"
--    Un seul motif suffit : 'Le%' couvre déjà "Les…", puisque `%` remplace
--    n'importe quel texte — y compris le "s" de "Les".
SELECT titre FROM films
WHERE titre LIKE 'Le%';

-- Défi 6 : Animation japonaise
SELECT titre, note FROM films
WHERE genre = 'Animation' AND pays = 'Japon'
ORDER BY note DESC;

-- Défi 7 : Pays représentés, sans doublon
SELECT DISTINCT pays FROM films;

-- Défi 8 : Durée entre 100 et 130 minutes inclus
SELECT titre, duree_min FROM films
WHERE duree_min BETWEEN 100 AND 130
ORDER BY duree_min;

-- Défi 9 : Top 5 avec départage.
--    Interstellar et Spirited Away sont tous deux à 8.6 : sans `, titre`,
--    l'ordre des 4ᵉ et 5ᵉ places serait imprévisible.
SELECT titre, note FROM films
ORDER BY note DESC, titre
LIMIT 5;
```

</details>

### Bravo !

Tu maîtrises maintenant les bases de la lecture de données en SQL :

- **SELECT / FROM** pour choisir quoi afficher
- **DISTINCT** pour supprimer les doublons
- **WHERE** pour filtrer les résultats, avec `=`, `<`, `>`, `!=`, `BETWEEN`, `IN`, `LIKE`, `AND` et `OR`
- **ORDER BY** pour trier, et un **critère de départage** pour que le tri soit stable
- **LIMIT** pour limiter le nombre de résultats

Tu as aussi croisé deux réflexes qui te serviront longtemps : vérifier le nombre
de lignes obtenu avant de conclure, et te méfier des ex æquo dès qu'un `LIMIT`
entre en jeu.

Au **Niveau 2**, tu apprendras à **transformer et combiner** les données : compter, calculer des moyennes, et croiser plusieurs tables entre elles.
