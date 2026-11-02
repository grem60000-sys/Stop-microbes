# Stop microbes · CAP AEPE

Six jeux à projeter pour les modules **bionettoyage** et **ergonomie-soins** (séances 1 et 2).

| Fichier | Contenu |
|---|---|
| `index.html` | Accueil + 4 jeux où les élèves manipulent (Casser la chaîne, Scanner UV, La recette du nettoyage, Le coin change) |
| `live.html` | 2 jeux en direct présentés par Audrey, les élèves répondent sur téléphone (Grand quiz, Tri express) |
| `config.js` | Les 2 informations Supabase à coller (seulement pour les jeux en direct) |
| `lib/qrcode.js` | Générateur de QR code (ne pas modifier) |

Les 4 jeux de `index.html` fonctionnent tout de suite, même sans Supabase.

---

## 1. Mettre en ligne sur GitHub Pages

1. Sur github.com, créer un dépôt (par exemple `stop-microbes`), en **Public**.
2. **Add file › Upload files** : déposer tout le contenu du dossier (`index.html`, `live.html`, `config.js`, le dossier `lib`). Valider avec **Commit changes**.
3. **Settings › Pages** : *Source* = **Deploy from a branch**, branche **main**, dossier **/ (root)**, puis **Save**.
4. Après une minute, le site est en ligne à l'adresse `https://<votre-compte>.github.io/stop-microbes/`.

## 2. Brancher Supabase (jeux en direct)

Aucune table à créer : les jeux utilisent seulement le temps réel (*Realtime › Broadcast*).

1. Ouvrir un projet Supabase (celui de l'agenda convient, ou un nouveau projet gratuit).
2. **Project Settings › API** : copier **Project URL** et la clé **anon public**.
3. Les coller dans `config.js`, entre les apostrophes :
   ```js
   window.SM_CONFIG = {
     supabaseUrl: 'https://xxxx.supabase.co',
     supabaseAnonKey: 'eyJhbGciOi...'
   };
   ```
4. Sur GitHub, éditer `config.js` (icône crayon), coller, puis **Commit changes**.
5. Si la connexion échoue : **Project Settings › Realtime**, vérifier que l'accès public aux canaux est autorisé (réglage par défaut).

La clé *anon public* est faite pour être visible dans une page web. Ne jamais coller la clé *service_role*.

## 3. En classe

**Jeux à manipuler (`index.html`)**
- Choisir le trinôme en haut à droite. Chaque trinôme joue à son tour, et le classement se met à jour automatiquement.
- TBI ou écran tactile recommandés. Tout fonctionne aussi à la souris (glisser-déposer, ou toucher l'objet puis l'emplacement).
- Le son se coupe avec 🔊, et ⛶ passe en plein écran.

**Jeux en direct (`live.html`)** : Audrey projette, les élèves jouent sur téléphone.
1. Ouvrir `live.html` sur l'ordinateur relié au vidéoprojecteur, puis choisir le jeu.
2. Les élèves scannent le QR code (ou tapent l'adresse avec le code), saisissent un pseudo et leur trinôme.
3. Cliquer sur **Lancer la partie**. Le temps s'arrête tout seul quand tout le monde a répondu.
4. Après chaque question : la révélation, l'explication à commenter, puis **Classement** ou **Suivant**.
5. À la fin, un podium s'affiche avec le classement des élèves et des trinômes (moyenne par joueur).

Les téléphones ont besoin d'Internet (wifi ou 4G). Sans Supabase, `live.html` passe en **mode test** : on peut l'essayer sur un seul ordinateur, avec une page joueur ouverte dans un autre onglet.
