# Site de Brunel Guendehou — mise en ligne gratuite

Le site tient en quelques fichiers. Il se met en ligne gratuitement avec **GitHub** (qui garde les fichiers), **Cloudflare Pages** (qui publie le site) et **YouTube** (qui héberge les vidéos et propose le choix de qualité jusqu’à la 4K).

```
index.html      le site (design, lecteur vidéo, espace admin)
content.json    tout le contenu : profil, productions, parcours, matériel
media/          photos et CV (portrait.jpg est déjà dedans)
_headers        réglage Cloudflare : le contenu est toujours servi à jour
LISEZ-MOI.md    ce guide
```

Ne renommez pas ces fichiers et gardez-les à la racine du dépôt.

---

## Étape 1 — Mettre les fichiers sur GitHub (10 min)

1. Créez un compte gratuit sur **https://github.com** (si ce n’est pas déjà fait).
2. En haut à droite : **+** → **New repository**.
   - Nom : `site-brunel` (ou ce que vous voulez).
   - **Private** ou **Public** : les deux fonctionnent avec Cloudflare.
   - Cochez **Add a README file**, puis **Create repository**.
3. Dans le dépôt : **Add file** → **Upload files**.
4. Décompressez le dossier sur votre ordinateur, puis glissez **le contenu** du dossier (pas le dossier lui-même) : `index.html`, `content.json`, `_headers`, `LISEZ-MOI.md` et le dossier `media`.
5. En bas : **Commit changes**.

Vérification : à la racine du dépôt, vous devez voir `index.html` et `content.json` directement, et `media/portrait.jpg`.

## Étape 2 — Publier le site avec Cloudflare Pages (10 min)

1. Créez un compte gratuit sur **https://dash.cloudflare.com**.
2. Menu de gauche : **Workers & Pages** → **Create** → onglet **Pages** → **Connect to Git** (ou « Import an existing Git repository »).
3. Autorisez Cloudflare à accéder à GitHub et choisissez le dépôt `site-brunel`.
4. Réglages de build :
   - Framework preset : **None**
   - Build command : **laissez vide**
   - Build output directory : **laissez vide** (ou `/`)
5. **Save and Deploy**. Au bout d’une minute, le site est en ligne à une adresse du type **`site-brunel.pages.dev`**.

À partir de là, chaque modification enregistrée sur GitHub remet le site à jour automatiquement en une à deux minutes.

**Nom de domaine (facultatif, environ 10 € par an)** : achetez par exemple `brunelguendehou.com` (chez Cloudflare Registrar, OVH, Namecheap…), puis dans le projet Cloudflare : **Custom domains** → **Set up a custom domain** et suivez les indications.

## Étape 3 — Créer la clé de l’espace admin (5 min)

L’admin du site enregistre vos modifications directement dans le dépôt GitHub. Il lui faut une clé (un « jeton ») qui n’a accès qu’à ce dépôt.

1. Sur GitHub : votre photo en haut à droite → **Settings** → tout en bas **Developer settings** → **Personal access tokens** → **Fine-grained tokens** → **Generate new token**.
2. Remplissez :
   - Token name : `admin site`
   - Expiration : la plus longue possible (notez la date : il faudra en recréer un à l’expiration)
   - Repository access : **Only select repositories** → `site-brunel`
   - Permissions → Repository permissions → **Contents** : **Read and write**
3. **Generate token**, puis copiez le jeton (il commence par `github_pat_`). Il ne s’affiche qu’une fois.

Ne partagez jamais ce jeton : il permet de modifier le site.

## Étape 4 — Se connecter à l’admin

1. Ouvrez le site et ajoutez `#admin` à la fin de l’adresse, par exemple `https://site-brunel.pages.dev/#admin`. (Il y a aussi un lien discret « Admin » tout en bas de la page.)
2. Remplissez :
   - Compte GitHub : votre nom d’utilisateur GitHub
   - Dépôt : `site-brunel`
   - Branche : `main`
   - Jeton : celui de l’étape 3
3. **Se connecter**. Le bouton rouge **Admin** apparaît alors en bas à droite sur ce navigateur.

La connexion reste enregistrée dans ce navigateur seulement. Sur un autre ordinateur ou téléphone, refaites l’étape 4.

### Ce que vous pouvez faire dans l’admin

- **Productions** : ajouter, modifier, supprimer, réordonner, mettre à la une (★), masquer (◉). Pour chaque production : poste, production, diffuseur, date, description, liens, **vidéos**, image de couverture, galerie.
- **Profil** : textes, coordonnées, chaînes et partenaires, portrait, **CV en PDF**.
- **Parcours** et **Matériel**.
- Cliquez sur **Publier sur le site** quand vous avez fini. Le site en ligne se met à jour en une à deux minutes.

Les images et le CV sont envoyés sur GitHub au moment où vous les choisissez (10 Mo maximum par fichier conseillé).

## Étape 5 — Ajouter les vidéos avec YouTube (taille illimitée en pratique, 4K)

1. Sur **https://youtube.com** : **Créer** → **Importer une vidéo**.
2. Choisissez la visibilité :
   - **Publique** : visible partout, y compris dans les recherches YouTube ;
   - **Non répertoriée** : visible uniquement par ceux qui ont le lien, et donc sur votre site.
3. Copiez le lien de la vidéo (bouton **Partager**).
4. Dans l’admin du site : ouvrez la production → **Vidéos** → collez le lien, ajoutez un titre si vous voulez → **Enregistrer** → **Publier sur le site**.

Sur la fiche de la production, la vidéo se lit directement. Le visiteur choisit la qualité avec la roue dentée du lecteur : 4K (2160p), 1440p, Full HD (1080p), HD (720p), 480p, 360p…

**Bon à savoir sur YouTube**
- Pour envoyer des vidéos de plus de 15 minutes, il faut **valider votre compte** une fois avec votre numéro de téléphone : https://www.youtube.com/verify. Ensuite : jusqu’à 256 Go ou 12 heures par vidéo.
- Après l’envoi, YouTube prépare d’abord les petites qualités. La 4K apparaît plus tard (parfois plusieurs heures pour un gros fichier).
- Sans image de couverture, le site utilise automatiquement la miniature YouTube.
- Les liens **Vimeo** et **Google Drive** (fichier partagé « Tous les utilisateurs disposant du lien ») fonctionnent aussi.

---

## En cas de problème

| Message | Solution |
|---|---|
| « jeton invalide ou expiré » | Recréez un jeton (étape 3) et reconnectez-vous (étape 4). |
| « dépôt ou fichier introuvable » | Vérifiez l’orthographe du compte et du dépôt, et que le jeton a bien accès à ce dépôt. |
| « le jeton n’a pas le droit d’écrire » | Dans le jeton : Contents doit être sur **Read and write**. |
| « conflit » | Rechargez la page : vos modifications sont gardées en brouillon et vous seront proposées. |
| Le site ne change pas après publication | Attendez deux minutes, puis rechargez. Vérifiez dans Cloudflare → votre projet → **Deployments** que le dernier déploiement est réussi. |
| La vidéo ne s’affiche pas | Vérifiez que la vidéo n’est pas « Privée » sur YouTube (choisissez Publique ou Non répertoriée). |

Pour tester le site sur votre ordinateur avant de le mettre en ligne, il faut un petit serveur local (ouvrir `index.html` directement par double-clic ne charge pas `content.json`). Le plus simple est de le tester directement sur Cloudflare après l’étape 2.
