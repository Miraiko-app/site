# Mise en ligne du site vitrine Miraiko

Le site tient en quelques fichiers statiques, hébergés gratuitement par GitHub Pages sur miraiko.app, en attendant l’application sur le serveur Hetzner.

## Contenu

- `index.html` : la page d’accueil, tirée de la maquette.
- `demo.html` : la séance de démonstration jouable.
- `mentions-legales.html` et `confidentialite.html` : obligatoires avant la mise en ligne.
- `fonts/` et `fonts.css` : les polices, hébergées avec le site (aucun appel à Google).
- `favicon.png` et `partage.png` : l’icône de l’onglet et l’image affichée quand on partage le lien.
- `CNAME` : indique à GitHub le domaine miraiko.app. Ne pas le supprimer.

## 1. Compléter les pages légales

Dans `mentions-legales.html` et `confidentialite.html`, remplacer chaque mention entre crochets, surlignée en rose :

- le prénom et le nom de Chema ;
- une adresse postale (après immatriculation, l’adresse de la micro-entreprise ou d’une domiciliation peut remplacer l’adresse personnelle) ;
- le SIRET, dès qu’il existe ;
- la date de mise en ligne.

## 2. Créer le formulaire de liste d’attente dans Brevo

1. Créer un compte Brevo avec admin@miraiko.app.
2. Dans Contacts, créer un attribut texte `NIVEAU`.
3. Créer un formulaire d’inscription avec les champs E-mail et NIVEAU, une case de consentement, et la double confirmation (double opt-in) activée.
4. Dans les options de partage du formulaire, choisir le code HTML et repérer l’adresse d’envoi du formulaire (elle se termine par une longue suite de caractères).
5. Dans `index.html`, remplacer `BREVO_ACTION_URL` par cette adresse. Vérifier que les noms des champs correspondent à ceux de Brevo : `EMAIL`, `NIVEAU`, `OPT_IN`. S’ils diffèrent, adapter l’attribut `name` dans `index.html`.

## 3. Publier sur GitHub Pages

1. Dans l’organisation GitHub « Miraiko-app », créer un dépôt public nommé `site`.
2. « Add file », puis « Upload files » : déposer tout le contenu du dossier, y compris le dossier `fonts`.
3. Dans « Settings », puis « Pages » : source « Deploy from a branch », branche `main`, dossier racine.
4. Vérifier que le domaine personnalisé indique `miraiko.app`.

## 4. Faire pointer miraiko.app vers GitHub, chez IONOS

Dans la gestion DNS du domaine miraiko.app :

1. Remplacer les enregistrements A du domaine racine (@) par ces quatre adresses :
   - 185.199.108.153
   - 185.199.109.153
   - 185.199.110.153
   - 185.199.111.153
2. Supprimer les enregistrements AAAA créés par IONOS pour le domaine racine, ou les remplacer par : 2606:50c0:8000::153, 2606:50c0:8001::153, 2606:50c0:8002::153, 2606:50c0:8003::153.
3. Créer un enregistrement CNAME pour `www` qui pointe vers `miraiko-app.github.io`.
4. Ne toucher à aucun enregistrement MX ni TXT : ils font fonctionner la messagerie.

## 5. Activer le HTTPS et protéger le domaine

1. Attendre la propagation des DNS (de quelques minutes à quelques heures).
2. Dans « Settings », puis « Pages », cocher « Enforce HTTPS ». Avec un .app, le site ne s’affiche pas sans HTTPS.
3. Dans les paramètres de l’organisation GitHub, rubrique Pages, faire vérifier le domaine miraiko.app (GitHub fournit un enregistrement TXT à ajouter chez IONOS). Cela empêche quiconque d’utiliser le domaine sur un autre compte GitHub.

## 6. Tester

- Ouvrir https://miraiko.app sur un téléphone et un ordinateur.
- S’inscrire à la liste d’attente avec une adresse de test, confirmer l’e-mail de Brevo, puis vérifier le contact dans Brevo.
- Ouvrir la démo et jouer un défi.

Quand l’application sera en ligne sur le serveur Hetzner, ces pages y seront reprises et les enregistrements DNS pointeront vers le serveur.
