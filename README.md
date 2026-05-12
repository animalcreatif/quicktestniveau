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

Ouvre `index.html`, cherche le bloc de configuration (autour de la ligne 540). Trois choses à remplacer :

```js
const LINKS = {
  formations: 'https://nathaliedupuy.com/formations',
  linkedin: 'https://www.linkedin.com/in/nathalie-dupuy-ia/'
};

// Endpoint de réception des leads
const FORM_ENDPOINT = 'https://formspree.io/f/TON_ID_FORMSPREE';
```

Tu peux aussi modifier directement :

- Les 10 questions dans le tableau `QUESTIONS`
- Les messages de paliers dans `TIERS`
- Les couleurs dans `:root` (CSS variables, tout en haut du `<style>`)

---

## Récupération des leads (email + profil)

Le quiz capture l'email et le profil (créatif·ve / pas créatif·ve) au début, envoie le tout avec le score à la fin du test.

### Option 1 : Formspree (recommandé pour démarrer)

1. Crée un compte sur [formspree.io](https://formspree.io) (gratuit, 50 soumissions / mois).
2. Crée un nouveau formulaire, récupère ton endpoint au format `https://formspree.io/f/XXXXX`.
3. Colle-le dans `FORM_ENDPOINT` (ligne 552).
4. Les leads arrivent dans ton dashboard Formspree + en notification email.

### Option 2 : Make / Zapier webhook (lien direct Notion CRM)

1. Crée un scénario Make ou un Zap déclenché par un webhook.
2. Connecte la sortie à ta base Notion `CRM Commercial IALS`.
3. Colle l'URL du webhook dans `FORM_ENDPOINT`.
4. Chaque lead arrive automatiquement dans ton CRM, avec email, profil, score, niveau, date.

### Payload envoyé

```json
{
  "email": "toi@exemple.com",
  "profil": "creatif",
  "score": "7/10",
  "niveau": "Niveau intermédiaire",
  "date": "2026-05-12T14:30:00.000Z",
  "source": "Quiz IALS niveau IA"
}
```

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
