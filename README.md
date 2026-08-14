# 🛡️ Anti-Ghosting — Suivi automatisé des candidats

> **54 % des candidats Gen-Z disparaissent après une offre (2026).**
> Anti-Ghosting envoie vos relances au bon moment — email à J+2, email à J+5, SMS à J+9 — pour garder vos candidats en vie jusqu'à l'embauche. Sans ATS, sans Excel, sans y penser.

Micro-SaaS destiné aux SMB français qui recrutent sans ATS et sans temps à consacrer au suivi des candidats. Abonnement **39 à 99 €/mois**.

---

## 📦 Livrables

| Fichier | Rôle |
|---|---|
| `index.html` | Page de vente 3D immersive (WebGL Three.js) : hero, comment ça marche, aperçu des relances, 3 offres, formulaire EmailJS, chatbot |
| `app.html` | **L'app web réelle** en JS pur : tableau de bord candidats, relances J+2 / J+5 / J+9, pipeline visuel (kanban) |
| `chatbot.js` | Widget chatbot autonome (capture de leads, réponses préprogrammées) |
| `chatbot-config.js` | Configuration du chatbot : marque, ton, FAQ, EmailJS |
| `templates/` | 6 templates de messages prêts à l'emploi (email J+2, J+5, SMS J+9, accueil, réponse positive, non-retenu) |
| `README.md` | Ce fichier |

---

## 🚀 Lancer

Aucune installation, aucun build. Deux options :

```bash
# Option 1 — ouvrir directement
open ~/Documents/livrables/anti-ghosting/index.html

# Option 2 — serveur local (recommandé)
cd ~/Documents/livrables/anti-ghosting
python3 -m http.server 8080
# puis http://localhost:8080
```

L'app (`app.html`) fonctionne en **100 % local** : les données sont stockées dans le `localStorage` du navigateur, aucune donnée ne quitte la machine.

---

## 🧪 Tester l'app en 30 secondes

1. Ouvrez `app.html` — 4 candidats de démonstration sont préchargés.
2. La bannière « 📨 Relances à envoyer » liste les relances dues (Léa Martin → SMS J+9, Thomas Bernard → Email J+5).
3. Cliquez sur un candidat → **« Voir le message »** : le message prêt à copier s'affiche, personnalisé (prénom, poste, entreprise).
4. **« Marquer comme envoyée »** → puis **« ✅ Réponse positive »** : le statut passe en *En discussion*, les étapes suivantes s'annulent automatiquement.
5. **Mode démo :** avancez la date simulée (en haut à droite) pour voir les relances se déclencher en direct. Ex. : ajoutez un candidat avec une offre datée d'il y a 2 jours → l'email J+2 apparaît immédiatement.

### Logique des relances

| Étape | Jour | Canal | Déclencheur |
|---|---|---|---|
| J+2 | offre + 2 jours | Email | Aucune réponse |
| J+5 | offre + 5 jours | Email | Toujours aucune réponse |
| J+9 | offre + 9 jours | SMS | Toujours aucune réponse |

- Une réponse reçue **annule les étapes suivantes** (inutile de relancer quelqu'un qui a répondu).
- Un statut final (*Embauché*, *Non retenu*) **arrête les relances**.
- Statuts possibles : En attente → En discussion → Offre acceptée → Embauché (ou Non retenu).

---

## 💰 Offres

| | Starter | Pro ★ | Cabinet |
|---|---|---|---|
| **Prix** | 39 €/mois | 69 €/mois | 99 €/mois |
| Candidatures suivies | 5 | Illimitées | Illimitées |
| Relances email J+2 / J+5 | ✅ | ✅ | ✅ |
| Relances SMS J+9 | — | ✅ | ✅ |
| Multi-clients | — | — | jusqu'à 5 |
| Reporting | — | statistiques de réponse | par client |
| Templates personnalisés | — | entreprise | logo + signature |

Sans engagement, première semaine offerte.

---

## ✉️ Formulaire EmailJS (réel)

Le formulaire de contact (`index.html`) et le chatbot envoient les demandes via **EmailJS** — aucun backend :

- `serviceId` : `service_cy1ytdb`
- `templateId` : `template_xpo58cv`
- `publicKey` : `8Pui4ZEqxW2jRVF7h`
- Payload : `{ site, name, email, question }`

Pour changer le compte de réception : modifiez la clé publique et les IDs dans `index.html` (fonction `envoyerContact`) et dans `chatbot-config.js` (bloc `emailjs`), puis mettez à jour le template côté [EmailJS](https://www.emailjs.com).

---

## 🎨 Design

- Sombre haut de gamme : fond `#070b14`, dégradés cyan → violet (`#5eead4 → #38bdf8 → #818cf8`).
- Page de vente : scène WebGL Three.js (particules, icosaèdre wireframe, anneaux orbitaux, onde de relance pulsante), parallaxe 3D souris + profondeur au scroll.
- Orthographe française soignée, ton direct et professionnel.

---

## 🔧 Personnalisation

- **Entreprise / signature** : réglable dans l'app (champ « Votre entreprise ») — utilisé dans tous les messages générés.
- **Messages de relance** : modifiez l'objet `MESSAGES` en tête de `<script>` dans `app.html` — ils doivent rester cohérents avec `templates/`.
- **Délais des relances** : ajustez `ETAPES` (variable `jour`) dans `app.html`.
- **Candidats de démo** : modifiez `seedDemo()` ou supprimez-les depuis l'interface ; le bouton « Réinitialiser la démo » (via la console ou en effaçant le localStorage `anti_ghosting_v1`) les restaure.

---

## 🗂️ Structure des templates

| Fichier | Usage |
|---|---|
| `templates/email-accueil-candidat.md` | Envoi de l'offre (J0) — cadre clair pour éviter le flou |
| `templates/email-relance-j2.md` | Relance courtoise J+2 |
| `templates/email-relance-j5.md` | Relance directe J+5 (« oui » ou « non » suffit) |
| `templates/sms-relance-j9.md` | SMS final J+9 — réponse en un mot |
| `templates/email-reponse-positif.md` | Confirmation d'embauche + prochaines étapes |
| `templates/email-non-retenu.md` | Clôture respectueuse d'un dossier refusé |

---

© 2026 Anti-Ghosting — le suivi candidat qui répond pour vous.
