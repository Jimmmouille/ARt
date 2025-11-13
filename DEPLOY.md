# 🚀 Guide de Déploiement - ARt

Trois méthodes simples pour déployer votre application ARt.

---

## ⚡ Méthode 1 : Déploiement Automatique (Recommandé)

**Prérequis** : [GitHub CLI](https://cli.github.com/) installé

```bash
# Rendre le script exécutable
chmod +x deploy.sh

# Lancer le déploiement
./deploy.sh
```

Le script va automatiquement :
- ✅ Créer un nouveau dépôt GitHub public
- ✅ Pousser tout le code
- ✅ Activer GitHub Pages
- ✅ Vous donner l'URL de votre application

**Temps estimé** : 2-3 minutes

---

## 🌐 Méthode 2 : GitHub Pages Manuel

### Étape 1 : Créer le dépôt GitHub

1. Allez sur https://github.com/new
2. Nom du dépôt : `ARt` (ou autre)
3. Type : **Public**
4. ✅ Cliquez sur **Create repository**

### Étape 2 : Pousser le code

```bash
# Initialiser Git
git init
git add .
git commit -m "Initial commit: ARt"

# Ajouter le remote (remplacez USERNAME)
git remote add origin https://github.com/USERNAME/ARt.git

# Pousser vers GitHub
git branch -M main
git push -u origin main
```

### Étape 3 : Activer GitHub Pages

1. Allez dans **Settings** de votre dépôt
2. Menu de gauche : **Pages**
3. **Source** : `main` branch, `/` (root)
4. Cliquez sur **Save**
5. ✅ Attendez 1-2 minutes

**Votre app sera disponible à** : `https://USERNAME.github.io/ARt/`

**Temps estimé** : 5 minutes

---

## 🚀 Méthode 3 : Netlify (Le plus rapide)

### Option A : Drag & Drop

1. Allez sur https://app.netlify.com/drop
2. **Glissez-déposez** le dossier `ARt` entier
3. ✅ C'est tout ! Votre app est en ligne

**Temps estimé** : 30 secondes

### Option B : CLI Netlify

```bash
# Installer Netlify CLI
npm install -g netlify-cli

# Déployer
netlify deploy --prod --dir=.
```

**Temps estimé** : 1 minute

---

## 🧪 Test en Local

Avant de déployer, testez localement :

```bash
# Option 1 : Python
python3 -m http.server 8000

# Option 2 : Node.js
npx http-server -p 8000

# Option 3 : PHP
php -S localhost:8000
```

Ouvrez : http://localhost:8000

---

## 📋 Checklist Post-Déploiement

- [ ] L'application se charge correctement
- [ ] Vous pouvez importer une image sur `index.html`
- [ ] Le sélecteur de taille (4096/8192/10240) fonctionne
- [ ] L'indicateur de charge GPU s'affiche
- [ ] Les statistiques d'image apparaissent après l'import
- [ ] Le bouton "Ouvrir en AR" mène vers `app.html`
- [ ] Sur Meta Quest : Le bouton "Enter AR" apparaît
- [ ] Sur Meta Quest : Le zoom au joystick fonctionne (jusqu'à 20x)

---

## 🐛 Dépannage

### "Permission denied" lors du déploiement
```bash
chmod +x deploy.sh
```

### GitHub Pages ne fonctionne pas
- Vérifiez que le dépôt est **public**
- Attendez 2-3 minutes après activation
- Videz le cache : Ctrl+Shift+R

### "gh: command not found"
Installez GitHub CLI :
- **macOS** : `brew install gh`
- **Linux** : https://github.com/cli/cli/blob/trunk/docs/install_linux.md
- **Windows** : https://cli.github.com/

### Netlify : "Build failed"
Pas de problème ! ARt n'a pas de build. Assurez-vous de déployer le dossier racine contenant `index.html`.

---

## 🎯 Prochaines Étapes

Une fois déployé :

1. **Testez sur Quest** : Ouvrez l'URL dans le navigateur Meta Quest
2. **Importez une image de test** : Commencez avec 4096px
3. **Entrez en AR** et testez le zoom au joystick
4. **Partagez** : L'URL fonctionne sur n'importe quel appareil compatible WebXR

---

## 📞 Besoin d'aide ?

- 📖 Documentation WebXR : https://immersiveweb.dev/
- 💬 Three.js Discord : https://discord.gg/threejs
- 🐛 Issues GitHub : Créez une issue sur votre dépôt

---

**Bon déploiement ! 🚀**
