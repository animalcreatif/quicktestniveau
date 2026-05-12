# Ton niveau IA sur 10

Un test express, signé IALS. 10 questions, 2 minutes, une note sur 10, une reco à la fin.

Hébergé en HTML pur. Zéro dépendance. Embarquable n'importe où.

---

## Aperçu

Quatre écrans : intro, capture email + profil, questions, résultat.

Trois paliers de scoring :

```
0 à 4   →   Niveau débutant      →   CTA Site IALS
5 à 9   →   Niveau intermédiaire →   CTA Site IALS
10      →   Niveau expert        →   CTA LinkedIn
```

Charte rose poudré sur noir. Inter Black pour les titres, Inter Light pour le corps. Animations CSS uniquement.

---

## Personnalisation rapide

Ouvre `index.html`, cherche le bloc de configuration autour de la ligne 545. Trois choses à ajuster selon ton setup :

```js
const LINKS = {
  formations: 'https://www.nathaliedupuy.com',
  linkedin: 'https://www.linkedin.com/in/nathalie-dupuy-ia/'
};

// Endpoint de réception des leads (Make webhook, Formspree, etc.)
const FORM_ENDPOINT = 'https://hook.eu1.make.com/TON_WEBHOOK_ID';
```

Tu peux aussi modifier directement :

- Les 10 questions dans le tableau `QUESTIONS`
- Les messages et seuils de paliers dans `TIERS`
- Les couleurs dans `:root` (CSS variables, tout en haut du `<style>`)

---

## Récupération des leads (email + profil)

Le quiz capture l'email et le profil (créatif·ve / pas créatif·ve) avant les questions, envoie le tout avec le score à la fin du test vers ton endpoint.

### Setup actuel : Make webhook vers Notion

1. Webhook Make écoute en permanence l'URL configurée dans `FORM_ENDPOINT`.
2. Module Notion `Create a Data Source Item` crée une ligne dans la base `Leads Quiz IA`.
3. Scénario activé en mode `Immediately as data arrives`, traitement en temps réel.

### Payload envoyé par le quiz

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

### Structure de la base Notion `Leads Quiz IA`

| Propriété     | Type        | Mapping webhook         |
|---------------|-------------|-------------------------|
| Email         | Titre       | `email`                 |
| Profil        | Sélection   | `profil` (Map ON)       |
| Score         | Texte       | `score`                 |
| Niveau        | Sélection   | `niveau` (Map ON)       |
| Date capture  | Date        | `date` → Start          |
| Source        | Sélection   | `Quiz IALS niveau IA`   |
| Statut        | Sélection   | `Nouveau` (fixe)        |
| Notes         | Texte       | vide (suivi manuel)     |

---

## Déploiement GitHub Pages

Méthode la plus simple : un repo public, GitHub Pages activé sur la branche `main`.

```bash
git init
git add .
git commit -m "init quiz IALS"
git branch -M main
git remote add origin https://github.com/TON-USER/NOM-DU-REPO.git
git push -u origin main
```

Ensuite sur GitHub : **Settings → Pages → Source : Deploy from a branch → Branch : main / root**. Sauvegarder.

Une à deux minutes plus tard, ton quiz est en ligne à :

```
https://TON-USER.github.io/NOM-DU-REPO/
```

Pour brancher un sous-domaine type `quiz.nathaliedupuy.com` : ajouter un fichier `CNAME` à la racine contenant le sous-domaine, puis configurer un enregistrement CNAME chez ton registrar pointant vers `TON-USER.github.io`.

---

## Mise à jour des fichiers

Tu peux éditer directement sur GitHub (crayon ✏️ sur le fichier, modifie, Commit changes). GitHub Pages redéploie dans la minute.

Pour des modifs plus lourdes, en local :

```bash
git pull
# ... édite tes fichiers ...
git add .
git commit -m "ce que tu as changé"
git push
```

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
