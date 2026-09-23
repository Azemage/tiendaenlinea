# Site de lectures de tarot

Site statique (HTML/CSS/JS, aucun serveur nécessaire) regroupant :
- tes liens vers les réseaux sociaux,
- un bouton de don PayPal,
- ton catalogue de lectures (20 min, 40 min, 1h, live, ...),
- un bouton de paiement Stripe pour chaque formule.

## 1. Personnaliser le contenu

Ouvre `index.html` et modifie les sections marquées d'un commentaire `👉` :

1. **Header** : ton nom/marque, ta phrase d'accroche, tes liens de réseaux sociaux.
2. **Don PayPal** : remplace `https://paypal.me/tonpseudo` par ton vrai lien. Pour
   l'obtenir, crée un compte sur [paypal.me](https://paypal.me) (lien du type
   `paypal.me/tonpseudo`) ou génère un lien "Donate" sur
   [paypal.com/donate](https://www.paypal.com/donate/buttons).
3. **À propos** : ta présentation.
4. **Catalogue** : pour chaque formule, le titre, la durée, la description, le prix affiché,
   et surtout le lien du bouton "Réserver" (voir la section Stripe plus bas).
5. **Contact** : ton email.

Les couleurs et polices sont dans `style.css` (variables en haut du fichier, section `:root`)
si tu veux ajuster le thème (violet/or par défaut, ambiance tarot).

## 2. Créer tes liens de paiement Stripe

Comme tu as déjà un compte Stripe, pour chaque formule de lecture :

1. Va sur [dashboard.stripe.com/payment-links](https://dashboard.stripe.com/payment-links).
2. Clique sur **+ Créer un lien de paiement**.
3. Crée un produit (ex. "Lecture privée — 20 minutes") avec son prix, en choisissant
   **MXN (peso mexicain)** comme devise (assure-toi que MXN est activé dans les
   paramètres de ton compte Stripe : Paramètres → Devises).
4. Valide : Stripe te donne une URL du type `https://buy.stripe.com/xxxxxxxx`.
5. Colle cette URL dans le `href="#"` du bouton "Réserver" correspondant dans `index.html`.

Les 6 formules déjà présentes dans le site :

| Formule | Durée | Prix |
|---|---|---|
| Lecture privée (appel vidéo) | 20 min | 400 MXN |
| Lecture privée (appel vidéo) | 40 min | 700 MXN |
| Lecture privée (appel vidéo) | 60 min | 1000 MXN |
| Lecture live/vidéo | 5 min | 80 MXN |
| Lecture live/vidéo | 10 min | 150 MXN |
| Lecture live/vidéo | 20 min | 300 MXN |

Répète la création de lien pour chacune de ces 6 formules. Comme il n'y a pas de créneau
horaire géré automatiquement, pense à activer, dans les paramètres du lien Stripe,
la collecte de l'email et éventuellement un champ "message" pour que le client précise
ses disponibilités — tu le recontacteras ensuite pour fixer l'horaire.

Astuce : dans Stripe, tu peux aussi configurer un **message de confirmation** après
paiement (ex. "Merci ! Je te recontacte sous 24h pour fixer le créneau.").

## 3. Tester en local

Aucune installation nécessaire. Ouvre simplement `index.html` dans ton navigateur,
ou lance un petit serveur local si tu préfères :

```bash
python3 -m http.server 8000
# puis ouvre http://localhost:8000
```

## 4. Mettre le site en ligne (gratuit)

Le plus simple : [Vercel](https://vercel.com) ou [Netlify](https://netlify.com).

- Connecte ton compte GitHub sur l'une de ces plateformes.
- Importe ce dépôt (`tiendaenlinea`).
- Aucune configuration de build n'est nécessaire (site 100% statique) : laisse les
  réglages par défaut et déploie.
- Tu obtiens une URL gratuite (ex. `tonsite.vercel.app`), et tu peux ensuite
  brancher un nom de domaine personnalisé si tu en achètes un.

## Évolutions possibles

- **Réservation de créneaux** : si un jour tu veux que les clients choisissent
  directement un horaire disponible (plutôt qu'un contact manuel après paiement),
  on pourra intégrer un outil comme Calendly ou Cal.com en complément de Stripe.
- **Formulaire de contact fonctionnel** : actuellement le contact se fait par email
  (lien `mailto:`) ; on peut ajouter un vrai formulaire plus tard si besoin.
