# MakerStock — Structure du projet pour déploiement Vercel

## Arborescence complète

```
makerstock-site/
│
├── index.html                  ← Détection langue → redirect automatique
├── vercel.json                 ← Config Vercel (headers sécurité, redirects)
│
├── fr/
│   ├── index.html              ← Landing page FR  ✅
│   ├── docs/
│   │   ├── vue-ensemble.html   ← Doc Partie 1 FR  ✅
│   │   ├── quickstart.html     ← Doc Partie 2 FR  ✅
│   │   ├── desktop-mobile.html ← Doc Partie 3 FR  ✅
│   │   ├── critiques.html      ← Doc Partie 4 FR  ✅
│   │   └── reference.html      ← Doc Partie 5 FR  ✅
│   └── legal/
│       ├── privacy.html        ← RGPD FR          ✅ (TODO à compléter)
│       └── tos.html            ← CGU FR            ✅ (TODO à compléter)
│
├── en/
│   ├── index.html              ← Landing page EN  ✅
│   ├── docs/
│   │   ├── overview.html       ← Doc Partie 1 EN  (à traduire)
│   │   ├── quickstart.html     ← Doc Partie 2 EN  (à traduire)
│   │   ├── desktop-mobile.html ← Doc Partie 3 EN  (à traduire)
│   │   ├── critical.html       ← Doc Partie 4 EN  (à traduire)
│   │   └── reference.html      ← Doc Partie 5 EN  (à traduire)
│   └── legal/
│       ├── privacy.html        ← Privacy policy EN (à traduire)
│       └── tos.html            ← Terms of service EN (à traduire)
│
└── es/
    ├── index.html              ← Landing page ES  ✅
    ├── docs/
    │   └── (idem EN, à traduire)
    └── legal/
        └── (idem EN, à traduire)
```

---

## Déploiement sur Vercel — étapes

### 1. Créer le dépôt GitHub
```bash
git init makerstock-site
cd makerstock-site
# Copier tous les fichiers dans la structure ci-dessus
git add .
git commit -m "chore: initial site structure"
git remote add origin https://github.com/VOTRE-USER/makerstock-site.git
git push -u origin main
```

### 2. Connecter Vercel
1. Aller sur https://vercel.com → New Project
2. Importer le dépôt GitHub makerstock-site
3. Framework Preset : **Other** (site statique)
4. Root Directory : `.` (racine)
5. Build Command : laisser vide
6. Output Directory : laisser vide
7. Cliquer Deploy

### 3. Ajouter votre domaine custom
Dans Vercel → Settings → Domains :
- Ajouter `TODO-votre-domaine.com`
- Ajouter `www.TODO-votre-domaine.com`
- Vercel génère automatiquement les certificats TLS (Let's Encrypt)

---

## Balises hreflang SEO

Ajouter dans le `<head>` de chaque page HTML :

```html
<!-- Pour la page FR -->
<link rel="alternate" hreflang="fr" href="https://TODO-domaine.com/fr/" />
<link rel="alternate" hreflang="en" href="https://TODO-domaine.com/en/" />
<link rel="alternate" hreflang="es" href="https://TODO-domaine.com/es/" />
<link rel="alternate" hreflang="x-default" href="https://TODO-domaine.com/en/" />
```

---

## Workflow de mise à jour

### Modifier un texte sur la landing FR
1. Éditer `fr/index.html`
2. Répliquer la modification dans `en/index.html` et `es/index.html`
3. `git add . && git commit -m "content: update hero text" && git push`
4. Vercel déploie automatiquement en ~30 secondes

### Traduire un nouveau document (docs ou legal)
Pour chaque nouveau fichier HTML :
1. Copier la version FR dans `en/` et `es/`
2. Utiliser Claude pour générer la traduction (coller le HTML, demander la traduction)
3. Relire attentivement — particulièrement les sections juridiques
4. Push → déploiement automatique

---

## Variables à compléter avant mise en ligne

| Fichier                | Champ TODO                          |
|------------------------|-------------------------------------|
| Tous les fichiers HTML | `TODO-votre-domaine.com`            |
| fr/legal/privacy.html  | Raison sociale, SIRET, adresse, email legal |
| fr/legal/tos.html      | Idem + médiateur consommateurs, tribunal |
| vercel.json            | Aucun (prêt)                        |
| index.html             | Aucun (prêt)                        |

---

## Coût estimé

| Service       | Coût                          |
|---------------|-------------------------------|
| Vercel        | **Gratuit** (Hobby plan)      |
| GitHub        | **Gratuit** (dépôt public ou privé) |
| Certificat TLS | **Gratuit** (Let's Encrypt via Vercel) |
| CDN mondial   | **Inclus** dans Vercel        |
| Nom de domaine | ~10-15 €/an (OVH, Namecheap…) |

**Coût total : ~12 €/an** (juste le nom de domaine)

