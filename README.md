# Ton niveau IA sur 10

Un test express, signé IALS. 10 questions, 2 minutes, une note sur 10, une reco à la fin.

Hébergé en HTML pur. Zéro dépendance. Embarquable n'importe où.

---

## Aperçu

Trois écrans : intro, questions, résultat.
Trois paliers de scoring :

```
0 à 3   →   Niveau débutant      →   CTA Formations IALS
4 à 7   →   Niveau intermédiaire →   CTA Formations IALS
8 à 10  →   Niveau expert        →   CTA LinkedIn
```

Charte rose poudré sur noir. Inter Black pour les titres, Inter Light pour le corps. Animations CSS uniquement.

---

## Personnalisation rapide

Ouvre `index.html`, cherche le bloc `LINKS` (autour de la ligne 270). Remplace par tes vrais liens :

```js
const LINKS = {
  formations: 'https://nathaliedupuy.com/formations',
  linkedin: 'https://www.linkedin.com/in/nathaliedupuy/'
};
```

Tu peux aussi modifier directement :

- Les 10 questions dans le tableau `QUESTIONS`
- Les messages de paliers dans `TIERS`
- Les couleurs dans `:root` (CSS variables, tout en haut du `<style>`)

---

## Déploiement GitHub Pages

Méthode la plus simple : un repo public, GitHub Pages activé sur la branche `main`.

```bash
# 1. Créer le repo en local
git init
git add .
git commit -m "init quiz IALS"

# 2. Le pousser sur GitHub (créer d'abord le repo vide sur github.com)
git branch -M main
git remote add origin https://github.com/TON-USER/quiz-niveau-ia.git
git push -u origin main
```

Ensuite sur GitHub : **Settings → Pages → Source : Deploy from a branch → Branch : main / root**. Sauvegarder.

Une à deux minutes plus tard, ton quiz est en ligne à l'adresse :

```
https://TON-USER.github.io/quiz-niveau-ia/
```

Pour brancher un sous-domaine type `quiz.nathaliedupuy.com` : ajouter un fichier `CNAME` à la racine contenant la valeur du sous-domaine, puis configurer un enregistrement CNAME chez ton registrar pointant vers `TON-USER.github.io`.

---

## Intégration dans Wix

Wix ne lit pas directement un repo. Deux options :

1. Tu héberges sur GitHub Pages, tu embeds via un widget HTML / iframe pointant sur l'URL Pages.
2. Tu copies-colles le contenu d'`index.html` directement dans un widget HTML Wix (Embed Code → Custom Embeds).

L'option 1 te laisse modifier le quiz sans toucher à Wix.

---

## Structure du repo

```
.
├── index.html      Le quiz, tout-en-un
└── README.md       Ce fichier
```

Un seul fichier, pas de build, pas de dépendance. Volontairement.

---

## Crédits

Conçu par Nathalie Dupuy.
IALS, Intelligence Artificielle La Suite.
