# 🎮 EDHEC Trivial — Trivial Pursuit en ligne

Jeu de culture générale multijoueur en temps réel, inspiré du Trivial Pursuit, aux couleurs de l'EDHEC Business School.

## 🎯 Fonctionnalités

- **1 035 questions** en français (source : OpenQuizzDB — Licence Creative Commons)
- **6 catégories** : Géographie, Histoire, Sciences & Nature, Arts & Littérature, Sport & Loisirs, Divertissement
- **Multijoueur en ligne** en temps réel via Firebase Firestore
- **3 modes de victoire** : 3 wedges (rapide), 6 wedges (classique), 1 wedge par catégorie (hardcore)
- **Timer configurable** par question (20s / 30s / 45s / 60s / illimité)
- **Stats personnelles** sauvegardées localement
- PWA-ready (fonctionne sur mobile)

## 🚀 Déploiement rapide (GitHub Pages)

### 1. Créer un repo GitHub

```bash
git init
git add .
git commit -m "Initial commit — EDHEC Trivial"
```

Crée un repo GitHub nommé `trivial-edhec` puis :

```bash
git remote add origin https://github.com/TON_USERNAME/trivial-edhec.git
git push -u origin main
```

### 2. Activer GitHub Pages

Dans le repo → **Settings** → **Pages** → Source : `main` / `/ (root)` → **Save**

Ton appli sera live sur : `https://TON_USERNAME.github.io/trivial-edhec/`

### 3. Firebase — Règles Firestore

Dans la console Firebase (`objectif-montreal`), ajouter une collection `trivial_games` et configurer les règles :

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /trivial_games/{gameId} {
      allow read, write: if true;  // Simplifié pour dev
      // Pour production, ajouter authentification
    }
  }
}
```

## 📁 Structure du projet

```
trivial-edhec/
├── index.html          # Appli complète (SPA)
├── questions.js        # Banque de 1035 questions (OpenQuizzDB)
└── README.md
```

## 🎨 Charte graphique

- **Couleur principale** : Grenat EDHEC `#8B1A2E`
- **Accent** : Or `#C8A96E`
- **Fond** : Blanc cassé `#FAF7F2`
- **Typographies** : Playfair Display (titres) + DM Sans (texte) + DM Mono (codes)

## 🃏 Sources des questions

Questions issues de [OpenQuizzDB](https://openquizzdb.org) — Philippe Bresoux
Licence : Creative Commons BY-NC-SA

Catégories couvertes :
| Catégorie | Questions | Thèmes |
|-----------|-----------|--------|
| Géographie | 180 | Monuments, Capitales, Europe, Villes du monde... |
| Histoire | 195 | Guerres, Dates, Égypte ancienne, France, Culture G... |
| Sciences & Nature | 165 | Animaux, Chimie, Inventions, Environnement... |
| Arts & Littérature | 135 | Sculpture, Louvre, Auteurs, Musique... |
| Sport & Loisirs | 180 | Tennis, JO, Foot, NBA, Sports d'hiver... |
| Divertissement | 180 | Cinéma, Séries, Star Wars, Dessins animés... |

## 🔧 Comment jouer

1. **Hôte** : Clique "Créer une partie", configure la partie, partage le code
2. **Amis** : Cliquent "Rejoindre", entrent le code
3. L'hôte lance quand tout le monde est prêt
4. Chaque joueur répond à son tour — l'hôte passe au tour suivant
5. Premier à atteindre l'objectif de wedges gagne !

## 🔄 Ajouter des questions

Le fichier `questions.js` est généré depuis OpenQuizzDB. Pour en ajouter :

1. Récupérer des fichiers JSON depuis [github.com/Zeuh/OpenQuizzDB](https://github.com/Zeuh/OpenQuizzDB)
2. Ajouter les questions au format :
```json
{ "q": "Question ?", "a": ["Choix A", "Choix B", "Choix C", "Choix D"], "c": 0, "cat": "geo" }
```
3. L'ajouter dans le bon tableau de `questions.js`
