# 🚀 Blockchain DApp - Hello World

[![Flutter](https://img.shields.io/badge/Flutter-3.x-blue.svg)](https://flutter.dev/)
[![Solidity](https://img.shields.io/badge/Solidity-0.5.9-orange.svg)](https://soliditylang.org/)
[![Truffle](https://img.shields.io/badge/Truffle-5.x-brown.svg)](https://trufflesuite.com/)

Application décentralisée (DApp) Flutter qui interagit avec un smart contract Ethereum déployé sur une blockchain Ganache locale.

## 📖 Description

Cette DApp permet de :

- 📝 Stocker un nom sur la blockchain Ethereum
- 🔍 Lire le nom stocké depuis le smart contract
- ✏️ Modifier le nom via des transactions blockchain
- 💰 Visualiser les transactions dans Ganache

## 🏗️ Architecture

```
┌─────────────────┐
│  Flutter App    │  ← Interface utilisateur (Dart)
│  (lib/*.dart)   │
└────────┬────────┘
         │ web3dart
         ▼
┌─────────────────┐
│  Smart Contract │  ← Logique métier (Solidity)
│  HelloWorld.sol │
└────────┬────────┘
         │ Truffle
         ▼
┌─────────────────┐
│   Ganache       │  ← Blockchain locale (Port 7545)
│   (Development) │
└─────────────────┘
```

## 📁 Structure du Projet

```
Blockchain_DAPP/
├── contracts/              # Smart contracts Solidity
│   └── HelloWorld.sol     # Contrat principal
├── migrations/            # Scripts de déploiement
│   └── 2_deploy_contracts.js
├── test/                  # Tests unitaires
│   └── helloWorld.js
├── lib/                   # Code Flutter
│   ├── main.dart         # Point d'entrée
│   ├── contract_linking.dart  # Connexion Web3
│   └── helloUI.dart      # Interface utilisateur
├── src/artifacts/         # ABI compilés (générés)
├── .env                   # Variables d'environnement (NON versionnée)
├── .env.example          # Template pour .env
├── truffle-config.js     # Configuration Truffle
├── pubspec.yaml          # Dépendances Flutter
└── start-ganache.bat     # Script de démarrage Ganache
```

## ⚙️ Prérequis

Avant de commencer, assurez-vous d'avoir installé :

- **Node.js** (v14+) - [Télécharger](https://nodejs.org/)
- **Flutter** (v3.0+) - [Installation](https://docs.flutter.dev/get-started/install)
- **Git** - [Télécharger](https://git-scm.com/)

## 🚀 Installation

### 1️⃣ Cloner le projet

```bash
git clone https://github.com/idoufkirkamal/Blockchain_DAPP.git
cd Blockchain_DAPP
```

### 2️⃣ Installer Truffle globalement

```bash
npm install -g truffle
```

### 3️⃣ Installer les dépendances Flutter

```bash
flutter pub get
```

### 4️⃣ Activer le support Windows Desktop (optionnel)

```bash
flutter config --enable-windows-desktop
```

## 🔧 Configuration

### 1️⃣ Configurer les variables d'environnement

Créez un fichier `.env` à partir du template :

```bash
# Windows
copy .env.example .env

# Linux/Mac
cp .env.example .env
```

Le fichier `.env` sera automatiquement créé avec les valeurs par défaut. **Important** : Ce fichier contient votre clé privée et ne doit jamais être committé.

### 2️⃣ Lancer Ganache CLI

**Option A : Via le script (Recommandé)**

```bash
# Windows
start-ganache.bat

# Linux/Mac - Créez un terminal séparé et lancez :
npx ganache --port 7545 --networkId 5777 --deterministic
```

**Option B : Ganache UI**

1. Téléchargez [Ganache UI](https://archive.trufflesuite.com/ganache/)
2. Lancez l'application
3. Créez un workspace sur le port **7545**

**⚠️ Important** : Laissez Ganache tourner pendant toute la durée du développement !

### 3️⃣ Compiler le Smart Contract

```bash
truffle compile
```

**Résultat attendu :**

```
✓ Compiled successfully using solc: 0.5.9
✓ Artifacts written to ./src/artifacts
```

### 4️⃣ Déployer sur la blockchain

```bash
truffle migrate --reset
```

**Résultat attendu :**

```
✓ Deploying 'HelloWorld'
✓ contract address: 0x...
✓ block number: 1
✓ Total cost: 0.000... ETH
```

### 5️⃣ Tester le contrat (Optionnel)

```bash
truffle test
```

**Résultat attendu :**

```
✓ Hello World Testing (123ms)
1 passing
```

## ▶️ Lancement de l'Application

### Pour Windows Desktop

```bash
flutter run -d windows
```

### Pour Chrome (Web)

```bash
flutter run -d chrome
```

### Pour Android (Émulateur)

```bash
flutter run
```

**Note** : Pour Android, l'URL RPC dans `lib/contract_linking.dart` utilise `http://10.0.2.2:7545` (émulateur Android).

## 🎯 Utilisation

1. **Lancez l'application** - Vous verrez "Hello Unknown"
2. **Entrez votre nom** dans le champ de texte
3. **Cliquez sur "Set Name"** - Une transaction est envoyée au smart contract
4. **Observez** - Le nom est mis à jour et provient maintenant de la blockchain !
5. **Vérifiez dans Ganache** - Vous verrez la nouvelle transaction

## 🔐 Sécurité

### ⚠️ IMPORTANT - Gestion de la clé privée

- ✅ Le fichier `.env` contient votre clé privée
- ✅ Ce fichier est dans `.gitignore` et ne sera **JAMAIS** poussé sur GitHub
- ❌ **NE JAMAIS** partager votre clé privée
- ✅ Utilisez uniquement des clés de développement Ganache
- ✅ Pour la production, utilisez des solutions de gestion de secrets (Azure Key Vault, AWS Secrets Manager)

Consultez [SECURITY.md](SECURITY.md) pour plus de détails.

## 🛠️ Dépannage

### Problème : "Couldn't connect to node"

**Solution** : Vérifiez que Ganache tourne sur le port 7545

```bash
# Vérifier le port
netstat -an | findstr "7545"
```

### Problème : "Error: Private key does not satisfy"

**Solution** : Assurez-vous que la clé privée dans `.env` commence par `0x`

### Problème : "No supported devices connected"

**Solution** : Activez une plateforme Flutter

```bash
flutter config --enable-windows-desktop
# ou
flutter config --enable-web
```

### Problème : "Version solving failed"

**Solution** : Les dépendances sont déjà à jour. Si le problème persiste :

```bash
flutter clean
flutter pub get
```

### Problème : "µWS is not compatible"

**Avertissement** : Ce message est normal avec Node.js v22. Truffle utilise une implémentation NodeJS de fallback. Cela n'affecte pas le fonctionnement.

## 📚 Technologies Utilisées

- **Flutter** - Framework UI multiplateforme
- **Solidity** - Langage de smart contracts
- **Truffle** - Framework de développement Ethereum
- **Ganache** - Blockchain Ethereum locale
- **Web3dart** - Bibliothèque Web3 pour Dart
- **Provider** - Gestion d'état Flutter

## 🤝 Contribuer

Les contributions sont les bienvenues !

1. Fork le projet
2. Créez votre branche (`git checkout -b feature/AmazingFeature`)
3. Committez vos changements (`git commit -m 'Add AmazingFeature'`)
4. Push vers la branche (`git push origin feature/AmazingFeature`)
5. Ouvrez une Pull Request

## 📄 Licence

Ce projet est un projet éducatif dans le cadre du TP8 - Blockchain et Applications Décentralisées.

## 👨‍💻 Auteur

**Idoufkir Kamal**

- GitHub: [@idoufkirkamal](https://github.com/idoufkirkamal)
- Projet: [Blockchain_DAPP](https://github.com/idoufkirkamal/Blockchain_DAPP)

## 📖 Ressources Complémentaires

- [Documentation Truffle](https://trufflesuite.com/docs/)
- [Documentation Flutter](https://docs.flutter.dev/)
- [Documentation Solidity](https://docs.soliditylang.org/)
- [Documentation web3dart](https://pub.dev/packages/web3dart)
- [Ganache Documentation](https://archive.trufflesuite.com/ganache/)

---

⭐ Si ce projet vous a été utile, n'hésitez pas à lui donner une étoile !
