# CLATA Pipeline – Instructions de déploiement

## Architecture
- **Frontend** : PWA hébergée sur GitHub Pages (CLATASOFT)
- **Données** : Google Sheets (ton Google Drive)
- **Auth** : Google OAuth 2.0
- **Compatible** : Chrome Windows + Android (installable comme app)

---

## Étape 1 – Google Cloud Console

1. Va sur https://console.cloud.google.com
2. Crée un projet : **CLATA Pipeline**
3. **APIs & Services → Library** → active :
   - Google Sheets API
   - Google Drive API
4. **APIs & Services → Credentials → Create Credentials → OAuth 2.0 Client ID**
   - Type : **Web application**
   - Authorized JavaScript origins :
     ```
     https://clatasoft.github.io
     ```
   - Authorized redirect URIs :
     ```
     https://clatasoft.github.io/clata-pipeline/
     ```
5. Copie le **Client ID** (format : `xxxxx.apps.googleusercontent.com`)

---

## Étape 2 – Google Sheet

1. Crée un nouveau Google Sheet sur ton Drive
2. Nomme-le : **CLATA Pipeline Data**
3. Copie l'ID dans l'URL :
   `https://docs.google.com/spreadsheets/d/**SPREADSHEET_ID**/edit`

---

## Étape 3 – Configurer index.html

Dans `index.html`, remplace les deux lignes :
```javascript
const CLIENT_ID = 'VOTRE_CLIENT_ID.apps.googleusercontent.com';
const SPREADSHEET_ID = 'VOTRE_SPREADSHEET_ID';
```

---

## Étape 4 – GitHub Pages

1. Crée un repo `clata-pipeline` sur le compte CLATASOFT
2. Push les fichiers :
   ```
   index.html
   manifest.json
   sw.js
   icon-192.png  (à créer)
   icon-512.png  (à créer)
   ```
3. Settings → Pages → Source : main branch / root
4. L'app sera disponible sur :
   **https://clatasoft.github.io/clata-pipeline/**

---

## Étape 5 – Premier import

1. Ouvre l'app → Se connecter avec Google
2. Clique **Import XLS** → sélectionne `pipeline_test.xlsx`
3. Les 152 projets sont chargés et sauvegardés sur ton Drive
4. À partir de là, l'app lit/écrit directement sur Google Sheets

---

## Utilisation Android

1. Ouvre Chrome sur Android
2. Va sur `https://clatasoft.github.io/clata-pipeline/`
3. Menu Chrome → **Ajouter à l'écran d'accueil**
4. L'app s'installe comme une vraie appli native

---

## Structure Google Sheet (auto-créée)

**Onglet Projects** : Country | Company | Agent | Solution | Phase | Description | mail ID | Amount | Target

**Onglet Tasks** : proj_id | task_id | text | status | owner | note
