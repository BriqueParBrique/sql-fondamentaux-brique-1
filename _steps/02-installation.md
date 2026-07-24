---
title: "Installer son environnement"
---

## Zéro friction, on code tout de suite

Pour pratiquer SQL, on va utiliser **SQLite** : une base de données légère qui ne nécessite aucune installation serveur. Deux options s'offrent à toi :

### Option 1 : En ligne (le plus rapide)

Rendez-vous sur **[sqliteonline.com](https://sqliteonline.com/)** :

1. Ouvre le site dans ton navigateur
2. Choisis **SQLite** dans le menu de gauche
3. Tu peux écrire tes requêtes directement dans la zone de texte
4. Clique sur **Run** pour exécuter

C'est prêt, rien à installer !

### Option 2 : Sur ton ordinateur (recommandé pour la suite)

Installe **DB Browser for SQLite**, un outil gratuit avec une interface graphique :

1. Télécharge-le sur [sqlitebrowser.org](https://sqlitebrowser.org/dl/)
2. Installe-le en suivant les instructions de ton système (Windows, Mac ou Linux)
3. Lance l'application

### Créer notre base de données de films

Quelle que soit l'option choisie, copie et exécute ce code SQL pour créer notre jeu de données :

```sql
CREATE TABLE films (
    id INTEGER PRIMARY KEY,
    titre TEXT,
    annee INTEGER,
    genre TEXT,
    note REAL
);

INSERT INTO films (id, titre, annee, genre, note) VALUES
(1, 'Inception', 2010, 'Science-fiction', 8.8),
(2, 'Amélie Poulain', 2001, 'Comédie', 8.3),
(3, 'Intouchables', 2011, 'Comédie', 8.5),
(4, 'Le Roi Lion', 1994, 'Animation', 8.5),
(5, 'Parasite', 2019, 'Thriller', 8.5),
(6, 'Toy Story', 1995, 'Animation', 8.3),
(7, 'La La Land', 2016, 'Comédie musicale', 8.0),
(8, 'Matrix', 1999, 'Science-fiction', 8.7),
(9, 'Le Dîner de cons', 1998, 'Comédie', 7.7),
(10, 'Spirited Away', 2001, 'Animation', 8.6);
```

### Vérification

Pour vérifier que tout est en place, exécute :

```sql
SELECT * FROM films;
```

Tu devrais voir les 10 films s'afficher. Si c'est le cas, bravo, ton environnement est prêt !

### Exercice

1. Exécute la requête `SELECT * FROM films;` et vérifie que tu obtiens bien 10 lignes
2. Essaie de modifier la requête pour écrire `SELECT titre FROM films;` — que se passe-t-il ?

<details>
<summary>Voir les réponses</summary>

1. Tu devrais voir un tableau avec 10 lignes et 5 colonnes (id, titre, annee, genre, note)
2. `SELECT titre FROM films;` affiche uniquement la colonne `titre` — on verra ça en détail à l'étape suivante !

</details>
