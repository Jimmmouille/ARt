# ARt

Application WebXR de réalité augmentée pour afficher des images en tant que "stencils" virtuels. Optimisée pour Meta Quest (Quest 2, Quest 3, Quest Pro).

![ARt](https://img.shields.io/badge/WebXR-Ready-brightgreen) ![Three.js](https://img.shields.io/badge/Three.js-0.147.0-blue) ![License](https://img.shields.io/badge/license-MIT-green)

## ✨ Fonctionnalités

### 🖼️ Gestion d'images avancée
- **Import d'images haute résolution** jusqu'à **10240×10240px** (10K)
- **Optimisation automatique** avec compression JPEG intelligente (qualité 92%)
- **Trois modes de qualité** :
  - 4096px : Performances optimales sur Quest ⚡
  - 8192px : Équilibre qualité/performances ⚖️
  - 10240px : Qualité maximale 🎨
- **Stockage IndexedDB** : pas de limite localStorage, support d'images volumineuses
- **Ré-optimisation rapide** : changez de résolution sans recharger l'image

### 📊 Statistiques en temps réel
- Résolution originale vs optimisée
- Taille du fichier en Mo
- Ratio d'aspect
- Facteur de réduction
- **Indicateur de charge GPU** (faible/moyen/élevé)

### 🥽 Expérience AR immersive
- **Zoom jusqu'à 20x** (contrôle au joystick des manettes Quest)
- **Ajustement de l'opacité** en temps réel (0-100%)
- **Repositionnement libre** de l'image dans l'espace 3D
- **Interface minimaliste** qui n'obstrue pas la vue
- **Bouton de réinitialisation** pour revenir aux paramètres par défaut

## 🚀 Démarrage rapide

### Option 1 : Déploiement en ligne (recommandé)

L'application fonctionne directement depuis n'importe quel hébergeur statique. Pas de build, pas de dépendances.

#### GitHub Pages
```bash
# Cloner le dépôt
git clone https://github.com/VOTRE-USERNAME/ARt.git
cd ARt

# Pousser vers votre dépôt GitHub
git remote set-url origin https://github.com/VOTRE-USERNAME/ARt.git
git push -u origin main

# Activer GitHub Pages
# Aller dans Settings > Pages > Source: main branch > Save
```

Votre app sera disponible à : `https://VOTRE-USERNAME.github.io/ARt/`

#### Netlify (déploiement en 1 clic)
[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start)

1. Cliquez sur le bouton ci-dessus
2. Connectez votre compte GitHub
3. Déployé en 30 secondes !

#### Vercel
```bash
# Installer Vercel CLI
npm i -g vercel

# Déployer
cd ARt
vercel --prod
```

### Option 2 : Développement local

```bash
# Serveur HTTP simple avec Python
python3 -m http.server 8000

# Ou avec Node.js
npx http-server -p 8000

# Ouvrir dans le navigateur
# http://localhost:8000
```

⚠️ **Important** : WebXR nécessite HTTPS en production. En local, `localhost` fonctionne sans HTTPS.

## 📱 Utilisation sur Meta Quest

### Première utilisation

1. **Accédez à l'URL** depuis le navigateur Meta Quest
2. **Importez une image** :
   - Tapez sur "Choisir un fichier"
   - Sélectionnez une image depuis votre Quest ou un service cloud
   - Choisissez la qualité selon vos besoins (4096px recommandé)
3. **Observez les statistiques** : charge GPU, résolution, taille
4. **Lancez l'AR** : tapez "Ouvrir en AR"
5. **Accordez les permissions** WebXR si demandé

### Contrôles AR

| Action | Contrôle |
|--------|----------|
| **Zoomer/Dézoomer** | Joystick droit (haut/bas) |
| **Ajuster l'opacité** | Slider "Opacité" dans l'UI |
| **Repositionner** | Déplacez votre tête et les contrôleurs |
| **Réinitialiser** | Bouton "Réinitialiser" |
| **Changer d'image** | Bouton "Changer d'image" |

### Astuces performances Quest

- **Quest 2** : Utilisez 4096px maximum pour éviter les ralentissements
- **Quest 3/Pro** : 8192px fonctionne bien, 10240px possible selon la complexité
- **Images complexes** : Privilégiez les résolutions plus basses
- **Arrière-plans unis** : Utilisez la qualité maximale sans problème

## 🛠️ Architecture technique

### Stack
- **Three.js 0.147.0** : Moteur 3D WebGL
- **WebXR Device API** : Interface AR native
- **IndexedDB** : Stockage persistant côté client
- **Canvas API** : Redimensionnement et optimisation d'images
- **Vanilla JS** : Zéro dépendances, zéro build

### Structure des fichiers
```
ARt/
├── index.html          # Page d'import et optimisation d'images
├── app.html            # Viewer WebXR AR
└── README.md           # Documentation
```

### Flux de données

1. **Import** : `index.html` → Fichier image sélectionné
2. **Optimisation** : Canvas API redimensionne selon la limite choisie
3. **Compression** : Conversion en JPEG qualité 92%
4. **Stockage** : Blob enregistré dans IndexedDB
5. **Chargement AR** : `app.html` récupère le Blob via `URL.createObjectURL()`
6. **Rendu** : Three.js charge la texture et l'affiche en AR

### Limites techniques

| Paramètre | Valeur |
|-----------|--------|
| Résolution max | 10240×10240px |
| Zoom max | 20x |
| Zoom min | 0.1x |
| Format de sortie | JPEG 92% |
| Stockage | IndexedDB (limites navigateur, généralement 50Mo-1Go+) |

## 🔧 Personnalisation

### Modifier les limites de résolution

**`index.html` ligne 33-37** :
```html
<select id="maxSize">
  <option value="4096">4096px (performances optimales)</option>
  <option value="8192">8192px (équilibré)</option>
  <option value="10240" selected>10240px (qualité maximale)</option>
  <option value="16384">16384px (expérimental)</option> <!-- Ajouter une option -->
</select>
```

### Modifier le zoom maximum

**`app.html` ligne 92** :
```javascript
currentScale = Math.min(Math.max(currentScale, 0.1), 20.0); // Changez 20.0
```

### Changer la qualité JPEG

**`index.html` ligne 150** :
```javascript
canvas.toBlob(async (blob)=>{
  // ...
}, 'image/jpeg', 0.92); // Changez 0.92 (entre 0.0 et 1.0)
```

## 🐛 Dépannage

### L'image ne s'affiche pas en AR
- Vérifiez que vous avez bien importé une image sur `index.html`
- Effacez l'image et réimportez-la
- Essayez une résolution plus basse (4096px)

### "Échec de l'enregistrement (IndexedDB)"
- Videz le cache du navigateur Quest
- Réduisez la résolution de l'image
- Vérifiez l'espace disque disponible sur le Quest

### Performances faibles / lag
- Réduisez la résolution (passez à 4096px)
- Utilisez le bouton "Re-optimiser" après avoir changé la taille
- Fermez les autres onglets du navigateur Quest
- Redémarrez le casque si nécessaire

### Le bouton "Entrer en AR" ne fonctionne pas
- Assurez-vous d'être sur **HTTPS** (obligatoire pour WebXR)
- Vérifiez que vous utilisez un navigateur compatible WebXR (navigateur Meta Quest)
- Accordez les permissions WebXR si demandé

## 📄 Licence

MIT © 2024

## 🤝 Contributions

Les contributions sont les bienvenues ! N'hésitez pas à ouvrir une issue ou une pull request.

### Idées d'amélioration
- [ ] Support du format PNG avec transparence
- [ ] Galerie multi-images
- [ ] Annotations et dessin en AR
- [ ] Export de sessions AR en vidéo
- [ ] Partage d'images via URL/QR code
- [ ] Mode multi-utilisateur

## 📞 Support

Pour toute question ou problème :
- Ouvrez une [issue GitHub](https://github.com/VOTRE-USERNAME/ARt/issues)
- Consultez la [documentation WebXR](https://immersiveweb.dev/)
- Rejoignez la communauté [Three.js](https://discourse.threejs.org/)

---

Fait avec ❤️ pour la communauté WebXR
