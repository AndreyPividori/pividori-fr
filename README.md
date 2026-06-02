# 🎾 Corpo Padel — Application de gestion de tournois

> Application web de gestion de tournois de padel inter-entreprises, support du **TP Qualité, Tests & CI/CD** de Polytech Tours (cycle ingénieur 4A / 5A).

**Votre mission n'est pas de développer cette application, mais de l'éprouver** : revue de spécifications, tests fonctionnels manuels, tests End-to-End (Cypress), tests back-end (pytest), et construction d'une pipeline CI/CD. L'application fonctionne… en apparence.

📄 **Sujet du TP** : https://www.pividori.fr/polytech/qlog_4A
📋 **Cahier des charges** : https://www.pividori.fr/polytech/test_security_5A

- **Backend** : Python 3.11+ · FastAPI · SQLAlchemy · SQLite · JWT · bcrypt
- **Frontend** : Vue 3 · Vite · Vue Router · Pinia · axios · Tailwind CSS
- **Tests** : pytest + httpx (back) · Cypress (E2E)

---

## ⚠️ Avant tout — créez VOTRE dépôt de groupe

La pipeline CI/CD ne pourra s'exécuter que sur un dépôt **que vous possédez**. Ne vous contentez pas d'un `git clone` : commencez par **forker** ce dépôt vers le compte GitHub d'un membre du groupe (bouton **Fork** en haut de la page GitHub), puis travaillez sur votre fork. Un clone local seul ne déclenchera jamais GitHub Actions.

```bash
# Une fois le fork créé, clonez VOTRE fork :
git clone https://github.com/VOTRE-GROUPE/Polytech_Tours_TP_QLOG.git
cd Polytech_Tours_TP_QLOG
```

---

## 📋 Prérequis

| Outil | Version min. | Vérifier avec |
|-------|--------------|----------------|
| Python | 3.11+ | `python --version` |
| Node.js | 18+ | `node --version` |
| npm | 9+ | `npm --version` |
| Git | — | `git --version` |

> 💡 **Windows** : à l'installation de Python, cochez « Add Python to PATH ». Selon votre système, la commande peut être `python` ou `python3`, et `pip` ou `pip3`.

---

## 🚀 Installation

Deux terminaux : un pour le backend, un pour le frontend.

### 1. Backend (API FastAPI)

**🪟 Windows (PowerShell)**
```powershell
cd backend
python -m venv venv
venv\Scripts\Activate.ps1
pip install -r requirements.txt
copy .env.example .env
```
> Si l'activation est bloquée : `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` (une seule fois), puis relancez `venv\Scripts\Activate.ps1`.

**🍎 macOS / 🐧 Linux (bash/zsh)**
```bash
cd backend
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
```

### 2. Frontend (application Vue)

Dans un second terminal, depuis la racine du projet :
```bash
cd frontend
npm install
```
Créez le fichier d'environnement frontend :
- **Windows** : `copy .env.example .env`
- **macOS / Linux** : `cp .env.example .env`

---

## 🌱 Jeu de données de test (seed)

Un script crée un jeu de données réaliste et cohérent (entreprises, joueurs, équipes, poules, matchs **passés et à venir**) pour pouvoir tester immédiatement.

Depuis `backend/`, environnement virtuel activé :
```bash
python seed.py
```
> ⚠️ Le script **réinitialise** la base (`padel_corpo.db`) : toutes les données existantes sont supprimées puis recréées. Relancez-le pour repartir d'un état propre.

---

## ▶️ Lancement

**Backend** — depuis `backend/` (venv activé)
```bash
uvicorn app.main:app --reload --port 8000
```
➡️ API : http://localhost:8000 — Documentation Swagger : http://localhost:8000/docs

**Frontend** — depuis `frontend/`
```bash
npm run dev
```
➡️ Application : http://localhost:5173

---

## 🔑 Comptes de test

Créés par le seed :

| Rôle | Email | Mot de passe |
|------|-------|--------------|
| Administrateur | `admin@padel.com` | `Admin@2025!` |
| Joueur | `joueur@padel.com` | `Joueur@2025!` |

> Tous les comptes joueurs générés par le seed utilisent le mot de passe `Joueur@2025!`.

---

## 🧪 Tests

Un squelette est fourni avec un test d'exemple ; **à vous de l'étoffer**.

**Back-end (pytest)** — depuis `backend/`, venv activé
```bash
pytest                                   # lancer les tests
pytest --cov=app --cov-report=term       # avec couverture (console)
pytest --cov=app --cov-report=html       # rapport HTML (htmlcov/index.html)
pytest --cov=app --cov-fail-under=70     # quality gate (échoue sous 70 %)
```

**End-to-End (Cypress)** — depuis `frontend/` (backend + frontend lancés)
```bash
npx cypress open      # mode interactif
npx cypress run       # mode headless (CI)
```

---

## 📂 Structure du projet

```
corpo-padel/
├── backend/                # API FastAPI
│   ├── app/
│   │   ├── routers/        # endpoints (auth, players, teams, pools, events, matches, results, profile, admin)
│   │   ├── services/       # logique métier (classement, sérialisation)
│   │   ├── models.py       # modèles SQLAlchemy
│   │   ├── schemas.py      # schémas Pydantic (validation)
│   │   ├── security.py     # JWT, hachage, dépendances d'auth
│   │   ├── auth.py         # login + anti-brute force
│   │   ├── validators.py   # validations métier
│   │   └── main.py         # point d'entrée FastAPI
│   ├── tests/              # 👈 vos tests pytest
│   ├── seed.py             # jeu de données de test
│   └── requirements.txt
├── frontend/               # application Vue 3
│   ├── src/
│   │   ├── views/          # pages (accueil, planning, matchs, résultats, profil, admin…)
│   │   ├── components/     # composants réutilisables
│   │   ├── stores/         # état Pinia (auth)
│   │   ├── router/         # routes + gardes par rôle
│   │   └── api/            # client axios
│   └── cypress/            # 👈 vos tests E2E
├── .github/workflows/
│   └── ci.yml.example      # 👈 amorce de pipeline CI/CD (à compléter)
└── docs/                   # 👈 revue de specs, plan de test, fiches d'anomalies (à produire)
```

---

## 📦 Ce que vous devez produire

Conformément au [sujet du TP](https://www.pividori.fr/polytech/qlog_4A), votre fork doit contenir à la fin :

- `docs/revue-specs.md` — rapport de revue + matrice de traçabilité
- `docs/plan-de-test.md` — plan de test + cahier de recette
- `docs/anomalies/` — vos fiches d'anomalies
- `backend/tests/` — vos tests pytest (couverture ≥ 70 %)
- `frontend/cypress/` — vos tests E2E
- `.github/workflows/ci.yml` — votre pipeline (avec badge de build dans ce README)
- `rapport.pdf` — le rapport final

---

## 🆘 Dépannage

| Problème | Solution |
|----------|----------|
| `uvicorn: command not found` | L'environnement virtuel n'est pas activé. Réactivez-le. |
| Port 8000 ou 5173 déjà utilisé | Fermez l'autre processus, ou changez le port (`--port`, `npm run dev -- --port 5174`). |
| Le frontend n'atteint pas l'API | Vérifiez que le backend tourne et que `frontend/.env` contient `VITE_API_BASE_URL=http://localhost:8000/api/v1`. |
| Erreurs CORS | Vérifiez `ALLOWED_ORIGINS` dans `backend/.env` (par défaut `http://localhost:5173`). |
| Repartir d'une base propre | Relancez `python seed.py` depuis `backend/`. |

---

## 📚 Ressources

- FastAPI — https://fastapi.tiangolo.com/
- Vue 3 — https://vuejs.org/
- pytest — https://docs.pytest.org/
- Cypress — https://docs.cypress.io/
- GitHub Actions — https://docs.github.com/actions
- OWASP Top 10 — https://owasp.org/www-project-top-ten/

---

*Projet pédagogique — Polytech Tours — Qualité, Test & Sécurité.*
