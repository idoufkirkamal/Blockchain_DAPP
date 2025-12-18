# 🔐 Sécurité du Projet

## ⚠️ IMPORTANT - Clé Privée

**NE JAMAIS** pusher votre clé privée sur GitHub ou tout autre dépôt !

### Configuration sécurisée

1. **Créez un fichier `.env`** à la racine du projet (déjà ignoré par Git) :
   ```bash
   cp .env.example .env
   ```

2. **Récupérez votre clé privée depuis Ganache** :
   - Ouvrez Ganache
   - Cliquez sur l'icône de clé 🔑 à droite d'un compte
   - Copiez la "PRIVATE KEY"

3. **Ajoutez la clé dans `.env`** :
   ```
   PRIVATE_KEY=0xvotre_cle_privee_complete_ici
   ```

4. **Modifiez `lib/contract_linking.dart`** :
   Remplacez `"Enter Private Key"` par votre vraie clé privée
   (Uniquement pour le développement local - la clé n'est pas pushée grâce au .gitignore)

### Bonnes pratiques

- ✅ Le fichier `.env` est dans `.gitignore` - il ne sera jamais pushé
- ✅ Ne partagez JAMAIS votre clé privée
- ✅ Utilisez des comptes Ganache différents pour dev/test
- ✅ Pour la production, utilisez un système de gestion de secrets (Azure Key Vault, AWS Secrets Manager, etc.)

### Si vous avez déjà pushé une clé privée

1. **Changez IMMÉDIATEMENT le compte Ganache**
2. **Supprimez l'historique Git contenant la clé** :
   ```bash
   git filter-branch --force --index-filter "git rm --cached --ignore-unmatch lib/contract_linking.dart" --prune-empty --tag-name-filter cat -- --all
   git push origin --force --all
   ```
3. **Ne réutilisez JAMAIS cette clé**

## Fichiers sensibles à ne jamais pusher

- `.env`
- Clés privées
- Fichiers `private_key*`
- Keystores Android (*.keystore, *.jks)
- Certificats iOS (*.mobileprovision, *.p12)
