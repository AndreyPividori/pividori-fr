# Guide de mise en place — www.pividori.fr

Ce guide te permet de déployer la nouvelle architecture en réutilisant ton repo GitHub `AndreyPividori/resume` existant.

## Architecture cible

```
www.pividori.fr/                           ← landing (index.html)
www.pividori.fr/resume/                    ← portfolio actuel
www.pividori.fr/polytech/                  ← hub étudiants (3 cartes)
www.pividori.fr/polytech/teaching/         ← cours
www.pividori.fr/polytech/qlog_4A/          ← TP Qualité Logicielle 4A
www.pividori.fr/polytech/test_security_5A/ ← TP Test & Sécurité 5A
```

## Étape 1 — Renommer le repo (optionnel mais conseillé)

Le repo s'appelle aujourd'hui `resume`. Comme il va contenir bien plus, renomme-le pour quelque chose de plus représentatif :

1. Va sur https://github.com/AndreyPividori/resume/settings
2. Dans la section **Repository name**, renomme en `pividori-fr` (ou `andrey-pividori.github.io` si tu veux passer en user page, mais inutile ici)
3. GitHub conserve automatiquement la redirection de l'ancien nom, rien à craindre

Si tu préfères ne pas renommer, tout fonctionnera quand même avec le nom `resume`. Saute cette étape.

## Étape 2 — Restructurer les fichiers en local

Sur ta machine, clone (ou tire) le repo :

```bash
git clone https://github.com/AndreyPividori/resume.git pividori-fr
cd pividori-fr
```

Puis réorganise :

```bash
# 1. Déplace le portfolio actuel dans un sous-dossier resume/
mkdir resume
git mv index.html resume/index.html
git mv IMG_6767.JPEG resume/IMG_6767.JPEG

# 2. Copie les nouveaux fichiers (depuis le dossier outputs de Cowork)
#    - index.html              → racine
#    - polytech/index.html     → polytech/
#    - polytech/teaching/index.html
#    - polytech/qlog_4A/index.html
#    - polytech/test_security_5A/index.html
#    - CNAME                   → racine (contient "www.pividori.fr")
#    - .nojekyll               → racine (vide)
```

Le `CNAME` doit contenir **une seule ligne** : `www.pividori.fr`. Si tu préfères le domaine apex sans `www`, mets juste `pividori.fr`.

Structure finale :

```
pividori-fr/
├── index.html              ← landing
├── CNAME                   ← www.pividori.fr
├── .nojekyll
├── README.md
├── resume/
│   ├── index.html          ← portfolio actuel
│   └── IMG_6767.JPEG
└── polytech/
    ├── index.html          ← hub étudiants
    ├── teaching/
    │   └── index.html
    ├── qlog_4A/
    │   └── index.html
    └── test_security_5A/
        └── index.html
```

## Étape 3 — Pousser sur GitHub

```bash
git add -A
git commit -m "Restructure into landing + resume + polytech hub"
git push
```

## Étape 4 — Configurer GitHub Pages

1. Sur le repo, va dans **Settings → Pages**
2. **Source** : Deploy from a branch
3. **Branch** : `main` / `(root)`
4. **Custom domain** : `www.pividori.fr` (GitHub lira le CNAME automatiquement)
5. Coche **Enforce HTTPS** une fois le certificat émis (peut prendre 10 min)

## Étape 5 — Configurer le DNS chez OVH

Connecte-toi à l'espace client OVH → zone DNS de `pividori.fr` :

**Pour `www.pividori.fr` :**
- Type : `CNAME`
- Sous-domaine : `www`
- Cible : `andreypividori.github.io.` (avec le point final, c'est important)

**Pour rediriger l'apex `pividori.fr` vers `www` :**

Option A — A records (recommandé GitHub Pages) :
- Type `A`, sous-domaine vide, valeurs (les 4 IP GitHub Pages) :
  - `185.199.108.153`
  - `185.199.109.153`
  - `185.199.110.153`
  - `185.199.111.153`

Option B — redirection web OVH (plus simple) :
- Dans OVH → ton domaine → **Redirection** → ajouter une redirection 301 de `pividori.fr` vers `https://www.pividori.fr`

## Étape 6 — Vérifier

Une fois la propagation DNS faite (5–30 min), teste :
- https://www.pividori.fr → landing (les 2 cartes)
- https://www.pividori.fr/resume → portfolio
- https://www.pividori.fr/polytech → hub Polytech
- https://www.pividori.fr/polytech/teaching → stub cours
- https://www.pividori.fr/polytech/qlog_4A → stub TP 4A
- https://www.pividori.fr/polytech/test_security_5A → stub TP 5A

## Étape 7 — Migrer l'ancien TP

Le contenu actuel de `polytech-tours.qlog.senis.pividori.fr` (cahier des charges + starter kit Corpo Padel) sera placé dans `polytech/qlog_4A/` à la prochaine étape. On y reviendra ensemble : tu pourras m'envoyer le fichier HTML actuel comme tu l'as fait pour le portfolio, et je le retravaillerai pour qu'il colle au nouveau design (sombre/cream/gold) tout en gardant le contenu pédagogique intact.

## Étape 8 — Désactiver les anciens sous-domaines (optionnel)

Une fois tout migré et testé :
- `resume.pividori.fr` → soit le supprimer côté OVH, soit le rediriger 301 vers `www.pividori.fr/resume`
- `polytech-tours.qlog.senis.pividori.fr` → idem, rediriger vers `www.pividori.fr/polytech/qlog_4A` (ou supprimer)

---

## Récap des fichiers à copier depuis Cowork

| Fichier dans Cowork | Destination dans le repo |
|---------------------|--------------------------|
| `index.html` | `index.html` (racine) |
| `CNAME` | `CNAME` (racine) |
| `.nojekyll` | `.nojekyll` (racine) |
| `polytech/index.html` | `polytech/index.html` |
| `polytech/teaching/index.html` | `polytech/teaching/index.html` |
| `polytech/qlog_4A/index.html` | `polytech/qlog_4A/index.html` |
| `polytech/test_security_5A/index.html` | `polytech/test_security_5A/index.html` |

Le fichier `resume/index.html` (et `resume/IMG_6767.JPEG`) reste celui que tu as déjà — il suffit juste de le déplacer dans le sous-dossier `resume/`.
