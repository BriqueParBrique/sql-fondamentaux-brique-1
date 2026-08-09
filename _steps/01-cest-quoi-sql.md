---
title: "C'est quoi SQL ?"
---

## Une langue pour parler aux bases de données

**SQL** (Structured Query Language) est un langage qui permet de poser des questions à une base de données et d'obtenir des réponses.

Imagine un **tableur géant** (comme Excel ou Google Sheets) avec des milliers de lignes. Au lieu de chercher manuellement dans les colonnes, tu écris une phrase en SQL et la base te donne exactement ce que tu cherches.

### Où retrouve-t-on SQL ?

SQL est partout :

- **Applications web** : quand tu te connectes à un site, SQL vérifie ton mot de passe
- **E-commerce** : quand tu filtres des produits par prix, c'est du SQL en coulisses
- **Réseaux sociaux** : ton fil d'actualité est construit avec des requêtes SQL
- **Banques, hôpitaux, administrations** : toute organisation qui stocke des données utilise SQL

### L'analogie du tableur

| Concept tableur     | Équivalent SQL                   |
| ------------------- | -------------------------------- |
| Un fichier Excel    | Une **base de données**          |
| Un onglet / feuille | Une **table**                    |
| Une colonne         | Un **champ** (ou colonne)        |
| Une ligne           | Un **enregistrement** (ou ligne) |

### Un premier exemple

Imagine une table `films` dans une base de données :

| id  | titre          | annee | genre           |
| --- | -------------- | ----- | --------------- |
| 1   | Inception      | 2010  | Science-fiction |
| 2   | Amélie Poulain | 2001  | Comédie         |
| 3   | Intouchables   | 2011  | Comédie         |

Pour demander "quels sont tous les films ?", on écrit :

```sql
SELECT * FROM films;
```

C'est aussi simple que ça. `SELECT` = "montre-moi", `FROM` = "depuis la table".

### Exercice

Réponds à ces questions sans écrire de code (on fera ça très bientôt !) :

1. Dans l'exemple ci-dessus, combien de **colonnes** a la table `films` ?
2. Combien de **lignes** (enregistrements) contient-elle ?
3. Si tu voulais ajouter le film "Le Roi Lion" sorti en 1994, quelles informations faudrait-il donner ?

<details markdown="1">
<summary>Voir les réponses</summary>

1. 4 colonnes : `id`, `titre`, `annee`, `genre`
2. 3 lignes (Inception, Amélie Poulain, Intouchables)
3. Il faudrait donner : un id (4), le titre ("Le Roi Lion"), l'année (1994) et le genre ("Animation")

</details>
