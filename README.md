# pividori.fr — Site personnel

Site personnel d'**Andrey Pividori** — Directeur de Projets, intervenant à Polytech Tours.
Il héberge le CV interactif (portfolio) et les ressources pédagogiques (cours et TP).

🌐 **En ligne** : https://www.pividori.fr

> ℹ️ Le **starter kit du TP** (application Corpo Padel à tester) est dans un dépôt **séparé** :
> https://github.com/AndreyPividori/Polytech_Tours_TP_QLOG — ne pas confondre avec ce dépôt-ci, qui ne contient que le site.

---

## 🧱 Stack

Site **statique** : HTML / CSS / JavaScript natif, sans framework ni étape de build.
Polices via Google Fonts (Playfair Display + DM Sans). Hébergement **GitHub Pages**, domaine géré chez **OVH**.

Aucune dépendance à installer : les pages s'ouvrent directement dans un navigateur.

---

### Le hub `/polytech/`

C'est **la** page d'entrée des ressources Polytech. Elle présente quatre blocs :

| Bloc | Destination |
|------|-------------|
| Cours **CI/CD** | `/polytech/teaching/CI_CD/index.html` |
| Cours **Comprendre & utiliser l'IA** | `/polytech/teaching/IA_basics/index.html` |
| **Sujet du TP** | `/polytech/tutorial/index.html` |
| **Cahier des charges** | `/polytech/test_security_5A/index.html` |

> ⚠️ Le dossier `/polytech/teaching/` **n'a pas de page d'accueil** (choix volontaire : le hub unique est `/polytech/`). Y accéder directement renvoie donc une 404. Si tu veux éviter ça, tu peux y déposer une petite page de redirection vers `/polytech/` — optionnel.

> 💡 Les noms de dossiers `tutorial` et `test_security_5A` sont **historiques**. Renommer un dossier impose de mettre à jour : les liens du hub `/polytech/index.html`, les liens internes des pages concernées, et le `sitemap.xml`.

### Cours en ligne

Chaque cours (`CI_CD/`, `IA_basics/`) propose deux actions :
- **« Export du cours en ligne »** — impression / PDF de la page web (bouton `window.print()`).
- **« Télécharger le cours magistral »** — lien vers le **PDF des slides**, placé dans le **même dossier** que la page. Pour mettre à jour un support, remplacer simplement le fichier PDF correspondant.

### Conventions de liens

- Liens **internes** : **chemins absolus depuis la racine**, slash final — `/`, `/resume/`, `/polytech/`, `/polytech/tutorial/`, `/polytech/test_security_5A/`, `/polytech/teaching/CI_CD/`, `/polytech/teaching/IA_basics/`.
- Depuis le hub, les **deux cours** sont liés via leur `.../index.html` explicite.
- Le lien « site web » du CV utilise l'URL absolue complète `https://www.pividori.fr/` (le CV pouvant être consulté hors contexte).

---

## 🚀 Déploiement (GitHub Pages + OVH)

Le site se déploie automatiquement à chaque `push` sur la branche `main`.

### GitHub Pages
- **Settings → Pages** : source = branche `main`, dossier `/ (root)`.
- **Custom domain** : `www.pividori.fr` (doit correspondre au fichier `CNAME` de ce dépôt).
- **Enforce HTTPS** : activé (une fois le DNS propagé).

---

## 🎨 Système de design

Cohérent sur toutes les pages :

| Élément | Valeur |
|---------|--------|
| Crème / fonds | `#F5F2EC` · `#EAE5D8` · `#FFFCF4` |
| Encre / textes | `#1A1A18` · `#3A3A37` · `#6E6E6A` |
| Or / accent | `#B8892E` · `#E8D5A3` |
| Titres | Playfair Display (700 / 900) |
| Texte | DM Sans (300–600) |
| Mono | JetBrains Mono |
| Favicon | monogramme « AP » (SVG inline en data-URI) |

Les pages partagent ce vocabulaire visuel (hero sombre à cercles concentriques, cartes, modules dépliables, toggle FR/EN). Pour éditer une page, reprendre les variables CSS `:root` existantes.

---

*Andrey Pividori · Polytech Tours · andrey@pividori.fr*
