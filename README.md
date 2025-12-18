# TP8 - Blockchain et Application Décentralisée (DApp)

## Structure du projet créée ✅

Tous les fichiers nécessaires ont été créés :

- `contracts/HelloWorld.sol` - Contrat intelligent
- `migrations/2_deploy_contracts.js` - Script de migration
- `test/helloWorld.js` - Tests du contrat
- `lib/contract_linking.dart` - Liaison Flutter-Blockchain
- `lib/helloUI.dart` - Interface utilisateur
- `lib/main.dart` - Point d'entrée de l'application
- `pubspec.yaml` - Dépendances Flutter
- `truffle-config.js` - Configuration Truffle

## Étapes suivantes à réaliser

### 1. Installer et configurer Ganache

1. Téléchargez Ganache depuis : https://archive.trufflesuite.com/ganache/
2. Installez et lancez Ganache
3. Assurez-vous que Ganache fonctionne sur le port **7545** (par défaut)
4. Notez une clé privée depuis Ganache :
   - Cliquez sur l'icône de clé 🔑 à droite d'un compte
   - Copiez la clé privée
   - Remplacez `"Enter Private Key"` dans `lib/contract_linking.dart` par votre clé privée

**Alternative : Utiliser Ganache CLI**

```bash
npx ganache
```

### 2. Compiler le contrat intelligent

```bash
truffle compile
```

**Résultat attendu :** Création des fichiers JSON dans `src/artifacts/`

### 3. Migrer le contrat vers la blockchain

```bash
truffle migrate
```

**Note :**

- Si vous utilisez Ganache UI, le port est 7545
- Si vous utilisez `npx ganache`, le port est par défaut 8545
- Le fichier `truffle-config.js` est configuré pour le port 8545
- Pour Ganache UI (port 7545), modifiez `truffle-config.js` :
  ```javascript
  port: 7545,  // au lieu de 8545
  ```

### 4. Tester le contrat intelligent

```bash
truffle test
```

**Résultat attendu :** Tous les tests doivent passer ✓

### 5. Installer les dépendances Flutter

**IMPORTANT : Vous devez installer Flutter avant de continuer**

Si Flutter n'est pas installé :

1. Téléchargez Flutter : https://flutter.dev/docs/get-started/install
2. Suivez les instructions d'installation pour Windows
3. Ajoutez Flutter au PATH

Une fois Flutter installé :

```bash
flutter pub get
```

### 6. Vérifier la configuration

Après la migration, vérifiez que le fichier `src/artifacts/HelloWorld.json` contient :

- Une section `abi`
- Une section `networks` avec l'adresse du contrat déployé

### 7. Lancer l'application Flutter

**Pour Android Emulator :**

```bash
flutter run
```

**Pour Chrome (développement web) :**

```bash
flutter run -d chrome
```

**Note importante pour l'URL RPC :**

- Émulateur Android : `http://10.0.2.2:7545`
- Navigateur/iOS : `http://127.0.0.1:7545`
- Modifiez `lib/contract_linking.dart` selon votre plateforme

### 8. Problèmes courants

#### Port Ganache

- Ganache UI utilise le port 7545
- Ganache CLI (`npx ganache`) utilise le port 8545
- Assurez-vous que `truffle-config.js` et `contract_linking.dart` utilisent le même port

#### Clé privée

- La clé privée doit être récupérée depuis Ganache
- Ne partagez JAMAIS votre clé privée réelle !
- Utilisez uniquement les clés de développement de Ganache

#### Version Solidity

- Le contrat utilise Solidity 0.5.9
- Le compilateur est configuré pour 0.8.21
- Si vous avez des erreurs, essayez d'ajuster la version dans `truffle-config.js`

## Tester l'application

1. Lancez Ganache
2. Compilez et migrez le contrat (`truffle compile` puis `truffle migrate`)
3. Récupérez et configurez votre clé privée
4. Lancez l'application Flutter
5. Testez en entrant un nom et en cliquant sur "Set Name"
6. Le nom devrait s'afficher en temps réel depuis la blockchain !

## Vérifications finales

✅ Ganache fonctionne
✅ Contrat compilé
✅ Contrat migré
✅ Clé privée configurée
✅ Dépendances Flutter installées
✅ Application lancée

Bonne chance avec votre TP ! 🚀
