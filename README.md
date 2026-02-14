# 🏃 Appel AS - Application de Scan QR Code pour Association Sportive

Application web moderne pour gérer les présences des élèves de l'association sportive via le scan de QR codes. Les données sont automatiquement enregistrées dans Google Sheets.

## 📱 Fonctionnalités

- ✅ Scan de QR codes via la caméra du smartphone
- 📊 Enregistrement automatique dans Google Sheets
- 📈 Statistiques en temps réel
- 🕒 Historique des scans de la session
- 🎨 Interface moderne et responsive
- 🔔 Notifications visuelles et sonores
- 💾 Sauvegarde locale pour éviter les doublons

## 🚀 Installation

### Étape 1 : Configurer Google Sheets

1. Ouvrez votre Google Sheet : [Lien du classeur](https://docs.google.com/spreadsheets/d/1PMGS3tkb0ftG_Tbz3L1CDd2c_AFxLJCyC61g-Pg3mUY/edit?usp=sharing)

2. Allez dans **Extensions** > **Apps Script**

3. Supprimez tout le code par défaut et copiez-collez le contenu du fichier `google-apps-script.js`

4. (Optionnel) Exécutez la fonction `initializeSheet()` pour formater la feuille :
   - Sélectionnez `initializeSheet` dans le menu déroulant
   - Cliquez sur ▶️ Exécuter
   - Autorisez l'application si demandé

5. Cliquez sur **Déployer** > **Nouveau déploiement**

6. Cliquez sur l'icône ⚙️ à côté de "Sélectionner un type" et choisissez **Application Web**

7. Configurez le déploiement :
   - **Description** : Appel AS API
   - **Exécuter en tant que** : Moi
   - **Qui a accès** : Tout le monde
   
8. Cliquez sur **Déployer**

9. **IMPORTANT** : Copiez l'URL du déploiement qui apparaît (elle ressemble à : `https://script.google.com/macros/s/AKfycby.../exec`)

### Étape 2 : Configurer l'application HTML

1. Ouvrez le fichier `appel-as-lycee.html` dans un éditeur de texte

2. Recherchez la ligne (environ ligne 350) :
   ```javascript
   const GOOGLE_SCRIPT_URL = 'VOTRE_URL_GOOGLE_APPS_SCRIPT_ICI';
   ```

3. Remplacez `VOTRE_URL_GOOGLE_APPS_SCRIPT_ICI` par l'URL copiée à l'étape précédente :
   ```javascript
   const GOOGLE_SCRIPT_URL = 'https://script.google.com/macros/s/AKfycby.../exec';
   ```

4. Sauvegardez le fichier

### Étape 3 : Publier sur GitHub Pages

1. Créez un nouveau dépôt GitHub (public)

2. Uploadez les fichiers suivants **dans le même dossier** :
   - `appel-as-lycee.html` → **renommez-le en `index.html`**
   - `Logo_AS_RR.png` (ne pas renommer)
   - `generateur-qr-codes.html` (optionnel)
   - `exemple-codes-eleves.xlsx` (optionnel)

3. Allez dans **Settings** > **Pages**

4. Dans **Source**, sélectionnez la branche `main` et le dossier `/root`

5. Cliquez sur **Save**

6. Votre application sera disponible à l'adresse : `https://votre-username.github.io/nom-du-repo/`

## 📖 Utilisation

### Pour l'enseignant

1. Ouvrez l'application sur votre smartphone
2. Cliquez sur "Démarrer le scanner"
3. Autorisez l'accès à la caméra si demandé
4. Scannez les QR codes des élèves présents
5. Chaque scan enregistre automatiquement la présence dans Google Sheets

### Pour les élèves

⚠️ **Conformité RGPD** : Les QR codes ne contiennent que des codes numériques anonymes (ex: "25025070001"), jamais de noms ou prénoms.

**Générateur intégré (recommandé)**
Utilisez le fichier `generateur-qr-codes.html` fourni qui permet :

1. **Mode manuel** : Saisissez un code numérique à la fois
2. **Import fichier Excel** : Préparez un fichier .xlsx avec :
   - **Colonne A uniquement** : Code numérique de l'élève (ex: 25025070001)
   - Format suggéré : AAMMMLLLNNN
     - AA = année (25 pour 2025)
     - MMM = code établissement ou AS (025)
     - LLL = code lycée (070)
     - NNN = numéro séquentiel élève (001, 002, etc.)
   - Un fichier d'exemple `exemple-codes-eleves.xlsx` est fourni avec 30 codes
3. **Impression** directe sur A4 (3x3 QR codes par page)

La correspondance code ↔ élève est conservée dans un fichier séparé par l'enseignant (non publié sur GitHub).

**Option alternative : Services en ligne**
Vous pouvez aussi générer des QR codes sur :
- [QR Code Generator](https://www.qr-code-generator.com/)
- [QRCode Monkey](https://www.qrcode-monkey.com/)
- [GoQR](https://goqr.me/)

## 🎫 Générateur de QR Codes (Conforme RGPD)

Le fichier `generateur-qr-codes.html` permet de créer facilement les QR codes anonymes pour tous vos élèves.

### ⚠️ Conformité RGPD

- **Aucun nom** n'apparaît sur les QR codes
- Seuls des **codes numériques** sont utilisés (ex: 25025070001)
- La correspondance code ↔ élève reste **confidentielle** (fichier séparé, non partagé)
- Les QR codes peuvent être distribués sans risque de violation de données personnelles

### Format de code suggéré

`AAMMMLLLNNN`
- **AA** = Année (25 pour 2025)
- **MMM** = Mois ou code AS (025 pour février)
- **LLL** = Code lycée (070)
- **NNN** = Numéro séquentiel (001, 002, 003...)

Exemple : `25025070001` = AS 2025, février, lycée 070, élève n°1

### Utilisation avec fichier Excel

1. **Préparez votre fichier Excel** (.xlsx) avec :
   - **Colonne A uniquement** : Code numérique de l'élève
   - La première ligne sera ignorée (en-tête)
   - Utilisez `exemple-codes-eleves.xlsx` comme modèle (30 codes fournis)

2. **Ouvrez** `generateur-qr-codes.html` dans votre navigateur

3. **Sélectionnez** "Import fichier Excel (.xlsx)"

4. **Choisissez** votre fichier Excel

5. **Vérifiez** l'aperçu (nombre de codes détectés)

6. **Cliquez** sur "Générer tous les QR Codes"

7. **Imprimez** les QR codes directement (format 3x3 par page A4)

### Utilisation manuelle

1. Sélectionnez "Manuel (un par un)"
2. Entrez le code numérique (uniquement des chiffres)
3. Cliquez sur "Générer le QR Code"
4. Répétez pour chaque code

### Gestion de la correspondance

**Important** : Conservez un fichier séparé (non partagé) avec la correspondance :
- Code numérique → Nom de l'élève
- Ce fichier reste sur votre ordinateur personnel
- Ne le publiez JAMAIS sur GitHub ou autre plateforme publique

## 📊 Structure du Google Sheets

| N° | DATE | CODE ELEVES |
|----|------|-------------|
| 1  | 13/02/26 - 14:30:00 | 25025070001 |
| 2  | 13/02/26 - 14:30:15 | 25025070012 |
| 3  | 13/02/26 - 14:30:22 | 25025070003 |

- **N°** : Numéro d'ordre auto-incrémenté
- **DATE** : Date et heure du scan (format : jj/mm/aa - hh:mm:ss)
- **CODE ELEVES** : Code numérique anonyme de l'élève scanné

⚠️ **Confidentialité** : Le tableau de correspondance code ↔ nom de l'élève doit être conservé séparément et de manière sécurisée par l'enseignant.

## 🔒 Sécurité et RGPD

### Fichiers à NE JAMAIS publier sur GitHub

❌ `CONFIDENTIEL-correspondance-codes-eleves.xlsx` (fourni en exemple)
- Ce fichier contient la correspondance code ↔ identité des élèves
- À conserver **uniquement** sur votre ordinateur personnel sécurisé
- Ne JAMAIS l'uploader sur GitHub, Google Drive partagé, ou tout cloud public

### Fichiers pouvant être publiés sur GitHub Pages

✅ `index.html` (appel-as-lycee.html renommé) - Application de scan
✅ `Logo_AS_RR.png` - Logo de l'association sportive
✅ `generateur-qr-codes.html` - Générateur de QR codes
✅ `exemple-codes-eleves.xlsx` - Liste de codes anonymes (sans noms)
✅ `README.md` - Documentation

**Important** : Assurez-vous que le logo `Logo_AS_RR.png` est dans le même dossier que `index.html` sur GitHub Pages.

### Bonnes pratiques RGPD

1. **Codes anonymes** : Seuls les codes numériques circulent publiquement
2. **Correspondance privée** : Le lien code-élève reste chez l'enseignant
3. **Google Sheets** : Ne contient que les codes, jamais les noms
4. **QR codes imprimés** : Peuvent être distribués sans risque
5. **Destruction** : Les QR codes périmés peuvent être jetés sans précaution particulière

## 🎨 Personnalisation

### Modifier les couleurs

Dans le fichier HTML, modifiez les variables CSS (lignes 15-23) :

```css
:root {
    --primary: #FF6B35;      /* Couleur principale */
    --secondary: #004E89;    /* Couleur secondaire */
    --accent: #F7B801;       /* Couleur d'accentuation */
    --success: #06D6A0;      /* Couleur de succès */
    --dark: #1A1A2E;         /* Couleur sombre */
    --light: #F8F9FA;        /* Couleur claire */
}
```

### Modifier le titre

Ligne 353 dans le HTML :
```html
<h1>Appel AS</h1>
<p class="subtitle">Scanner les QR codes des élèves</p>
```

## 🔧 Dépannage

### La caméra ne se lance pas
- Vérifiez que vous utilisez HTTPS (nécessaire pour accéder à la caméra)
- Vérifiez les permissions de la caméra dans les paramètres du navigateur
- Essayez avec un autre navigateur (Chrome recommandé)

### Les données ne s'enregistrent pas
- Vérifiez que l'URL du script Google Apps est correcte
- Vérifiez que le déploiement est accessible à "Tout le monde"
- Regardez la console du navigateur (F12) pour voir les erreurs éventuelles

### Les QR codes ne sont pas détectés
- Assurez-vous que le QR code est net et bien éclairé
- Rapprochez ou éloignez le QR code de la caméra
- Vérifiez que le QR code contient bien du texte simple

## 📱 Compatibilité

- ✅ Chrome (Android/iOS)
- ✅ Safari (iOS)
- ✅ Firefox (Android)
- ✅ Edge (Android)

## 🔒 Sécurité et confidentialité

- Les données sont stockées uniquement dans votre Google Sheets
- Le stockage local est utilisé uniquement pour éviter les doublons
- Aucune donnée n'est envoyée à des serveurs tiers
- L'accès à la caméra est géré par le navigateur

## 📄 Licence

Cette application est libre d'utilisation pour les établissements scolaires.

## 👨‍💻 Support

Pour toute question ou problème :
1. Vérifiez la section Dépannage
2. Consultez la console du navigateur pour les erreurs
3. Vérifiez que toutes les étapes d'installation ont été suivies

---

**Développé pour faciliter la gestion des associations sportives en lycée** 🏃‍♂️🏃‍♀️
