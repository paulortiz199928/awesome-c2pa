# Guide de démarrage rapide C2PA

Démarrez avec C2PA en 5 minutes ! Ce guide vous aidera à comprendre, vérifier et créer du contenu signé C2PA.

## 📋 Table des matières

1. [Comprendre C2PA](#comprendre-c2pa)
2. [Vérifier le contenu C2PA](#vérifier-le-contenu-c2pa)
3. [Créer du contenu C2PA](#créer-du-contenu-c2pa)
4. [Prochaines étapes](#prochaines-étapes)

---

## Comprendre C2PA

### Ce que vous devez savoir

**C2PA** ajoute un « manifest » (manifeste) signé cryptographiquement à vos fichiers multimédias contenant :
- **Qui** : Identité du créateur/éditeur
- **Quoi** : Actions effectuées (créé, modifié, généré par IA)
- **Quand** : Horodatages
- **Comment** : Outils et paramètres utilisés
- **De** : Matériaux sources (ingrédients)

### Concepts clés en 30 secondes

```
Photo originale → [Ajout manifest C2PA] → Photo signée
                        ↓
                  Contient métadonnées :
                  • Créateur : John Doe
                  • Appareil : Nikon Z9
                  • Date : 2025-11-21
                  • GPS : 48.8566°N, 2.3522°E
                  • Signature : ✓ Valide
```

Lors de la modification :
```
Photo signée → [Modification dans Photoshop] → Nouvelle photo signée
                                                     ↓
                                            Le nouveau manifest référence
                                            l'original comme « ingrédient »
```

**Résultat** : Chaîne de provenance complète de l'original à la version actuelle.

---

## Vérifier le contenu C2PA

### Méthode 1 : Outil en ligne (Le plus simple)

**Aucune installation requise !**

1. Visitez https://contentcredentials.org/verify
2. Glissez-déposez n'importe quelle image/vidéo/document
3. Visualisez les informations de provenance :
   - Identité du créateur
   - Historique de modification
   - Statut de la signature
   - Contenu original (si disponible)

**Essayez maintenant** avec des exemples d'images : https://contentauthenticity.org/examples

### Méthode 2 : Extension de navigateur

**Pour la vérification automatique lors de la navigation :**

1. Installez [Content Credentials Extension](https://chrome.google.com/webstore)
   - Disponible pour Chrome, Edge, Brave
2. Naviguez normalement
3. L'extension détecte automatiquement le contenu C2PA
4. Cliquez sur l'icône pour voir les détails de provenance

### Méthode 3 : Ligne de commande

**Pour les développeurs et utilisateurs avancés :**

#### Installer c2patool

```bash
# macOS/Linux (avec Cargo)
cargo install c2patool

# macOS (avec Homebrew)
brew install c2patool

# Windows
# Télécharger depuis : https://github.com/contentauth/c2patool/releases
```

#### Vérifier un fichier

```bash
# Vérification de base
c2patool photo.jpg

# Sortie JSON détaillée
c2patool photo.jpg --detailed

# Enregistrer le manifest dans un fichier JSON
c2patool photo.jpg --output manifest.json

# Vérifier plusieurs fichiers
c2patool *.jpg
```

#### Exemple de sortie

```
File: photo.jpg
Status: ✓ Valid C2PA signature

Creator: John Doe (john@example.com)
Created: 2025-11-21T10:30:00Z
Camera: Nikon Z9
Signature: Valid
Certificate: DigiCert
Actions: Captured
```

### Méthode 4 : Par programmation

**Intégrez la vérification dans votre application :**

#### JavaScript/Node.js

```javascript
const c2pa = require('c2pa-node');

async function verify(imagePath) {
  const manifest = await c2pa.read(imagePath);

  if (manifest) {
    console.log('Creator:', manifest.claim.creator);
    console.log('Created:', manifest.claim.created);
    console.log('Valid:', manifest.validation_status);
  } else {
    console.log('No C2PA data found');
  }
}

verify('photo.jpg');
```

#### Python

```python
from c2pa import Reader

reader = Reader('photo.jpg')
manifest = reader.manifest()

if manifest:
    print(f"Creator: {manifest.creator}")
    print(f"Created: {manifest.created}")
    print(f"Valid: {manifest.is_valid}")
else:
    print("No C2PA data found")
```

---

## Créer du contenu C2PA

### Méthode 1 : Utiliser un logiciel compatible

**Aucun codage requis :**

#### Adobe Photoshop/Lightroom

1. Ouvrez l'image dans Photoshop/Lightroom
2. Allez dans **Édition → Content Credentials**
3. Remplissez les informations du créateur
4. Enregistrez le fichier → Le manifest C2PA est automatiquement ajouté

#### Appareils photo avec C2PA intégré

- **Nikon Z9/Z8** : Activez dans les paramètres de l'appareil → les photos sont signées à la capture
- **Leica M11-P/SL3** : Signature automatique activée
- **Série Sony Alpha** : Activez via une mise à jour du firmware

### Méthode 2 : Ligne de commande (c2patool)

#### Prérequis

Vous avez besoin d'un certificat de signature :

**Pour les tests (Auto-signé) :**
```bash
# Générer un certificat de test (non reconnu par les validateurs)
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes
```

**Pour la production :**
- Achetez un certificat auprès d'une autorité de certification de confiance (DigiCert, GlobalSign, etc.)
- Spécifiez les exigences d'utilisation de clé C2PA

#### Créer un manifest

Créez `manifest.json` :

```json
{
  "claim_generator": "mon-app/1.0",
  "assertions": [
    {
      "label": "stds.schema-org.CreativeWork",
      "data": {
        "@context": "https://schema.org",
        "@type": "CreativeWork",
        "author": [
          {
            "@type": "Person",
            "name": "John Doe"
          }
        ]
      }
    },
    {
      "label": "c2pa.actions",
      "data": {
        "actions": [
          {
            "action": "c2pa.created"
          }
        ]
      }
    }
  ]
}
```

#### Signer le fichier

```bash
# Signer avec votre certificat
c2patool photo.jpg \
  --manifest manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output signed_photo.jpg

# Vérifier que ça a fonctionné
c2patool signed_photo.jpg
```

### Méthode 3 : Par programmation

#### Rust

```rust
use c2pa::{Builder, SigningAlg};

fn main() -> Result<(), Box<dyn std::error::Error>> {
    let mut builder = Builder::from_file("input.jpg")?;

    // Ajouter une assertion de créateur
    builder.add_assertion("stds.schema-org.CreativeWork",
        r#"{"author": [{"name": "John Doe"}]}"#)?;

    // Signer et enregistrer
    let signer = get_signer(); // Votre certificat/clé
    builder.sign("output.jpg", signer)?;

    Ok(())
}
```

#### JavaScript/Node.js

```javascript
const c2pa = require('c2pa-node');

async function sign(inputPath, outputPath) {
  const manifest = {
    claim_generator: 'mon-app/1.0',
    assertions: [
      {
        label: 'stds.schema-org.CreativeWork',
        data: {
          author: [{ name: 'John Doe' }]
        }
      }
    ]
  };

  const signer = {
    cert: 'chemin/vers/cert.pem',
    key: 'chemin/vers/key.pem'
  };

  await c2pa.sign(inputPath, outputPath, manifest, signer);
  console.log('Signé avec succès !');
}

sign('input.jpg', 'output.jpg');
```

#### Python

```python
from c2pa import Builder, Signer

# Créer le builder
builder = Builder.from_file('input.jpg')

# Ajouter des assertions
builder.add_assertion('stds.schema-org.CreativeWork', {
    'author': [{'name': 'John Doe'}]
})

# Signer
signer = Signer('cert.pem', 'key.pem')
builder.sign('output.jpg', signer)

print('Signé avec succès !')
```

### Méthode 4 : Modifier du contenu signé (Préserver la provenance)

Lors de la modification de contenu signé C2PA, référencez l'original comme « ingrédient » :

```bash
# Modifier et préserver la chaîne
c2patool edited_photo.jpg \
  --parent original_photo.jpg \
  --manifest edit_manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output final_photo.jpg
```

Le nouveau manifest référencera `original_photo.jpg` comme ingrédient, préservant l'historique complet.

---

## Prochaines étapes

### En savoir plus

**Comprendre la spécification :**
- [English](../../docs/specifications/C2PA_Specification.pdf)
- [中文](../../docs/specifications/C2PA_Specification_zh-Hans.pdf)
- [日本語](../../docs/specifications/C2PA_Specification_ja.pdf)
- [Deutsch](../../docs/specifications/C2PA_Specification_de.pdf)

**Explorer les outils :**
- [Outils et bibliothèques](README.md#outils-et-bibliothèques) - SDK pour tous les principaux langages
- [Documentation officielle](https://opensource.contentauthenticity.org/docs)

**Questions courantes :**
- [FAQ](faq.md) - Plus de 25 questions fréquemment posées
- [GitHub Discussions](https://github.com/c2pa-org/../../docs/specifications/discussions)

### Tutoriels et exemples

**Tutoriels officiels :**
- [Tutoriel développeur C2PA](https://opensource.contentauthenticity.org/docs/tutorial)
- [Création de manifests](https://opensource.contentauthenticity.org/docs/manifest/guide)
- [Référence des assertions](https://opensource.contentauthenticity.org/docs/manifest/assertions)

**Exemples de code :**
- [Exemples c2pa-rs](https://github.com/contentauth/c2pa-rs/tree/main/sdk/examples)
- [Exemples c2pa-node](https://github.com/contentauth/c2pa-node/tree/main/examples)
- [Exemples c2pa-python](https://github.com/contentauth/c2pa-python/tree/main/examples)

### Déploiement en production

**Avant la mise en ligne :**

1. **Obtenir un certificat de production**
   - Achetez auprès d'une autorité de certification de confiance (DigiCert, GlobalSign, etc.)
   - Assurez-vous de l'utilisation de clé compatible C2PA
   - Coût : environ 50-500 $/an

2. **Stockage sécurisé des clés**
   - Utilisez un module de sécurité matériel (HSM) pour les clés privées
   - Ou HSM cloud (AWS CloudHSM, Azure Key Vault)
   - Ne jamais valider les clés dans le contrôle de source

3. **Tester minutieusement**
   - Vérifier les signatures avec plusieurs validateurs
   - Tester sur différents formats de fichiers
   - Vérifier la compatibilité multiplateforme

4. **Surveiller et maintenir**
   - Implémenter la rotation des certificats
   - Surveiller les révocations
   - Maintenir les SDK à jour

### Intégration avec votre application

**Points d'intégration clés :**

```
Workflow de votre application :

1. Création/Téléversement de contenu
   ↓
2. [Ajout manifest C2PA] ← Votre point d'intégration
   ↓
3. Signer avec le certificat
   ↓
4. Enregistrer/Publier le contenu signé
   ↓
5. [Optionnel] Vérifier à l'affichage ← Autre point d'intégration
```

**Temps d'intégration typique :**
- Vérification simple : 1-2 jours
- Signature de base : 3-5 jours
- Déploiement complet en production : 2-4 semaines

### Obtenir des certificats

**Tests (Gratuit) :**
- Certificats auto-signés
- Bon pour le développement uniquement
- Non reconnus par les validateurs

**Production :**
- **DigiCert** : https://www.digicert.com/
- **GlobalSign** : https://www.globalsign.com/
- **Entrust** : https://www.entrust.com/
- Demandez des certificats avec extensions d'utilisation de clé C2PA

### Rejoindre la communauté

**Obtenir de l'aide :**
- [GitHub Issues](https://github.com/c2pa-org/../../docs/specifications/issues) - Rapports de bogues
- [GitHub Discussions](https://github.com/c2pa-org/../../docs/specifications/discussions) - Questions
- [Site web C2PA](https://c2pa.org) - Ressources officielles

**Contribuer :**
- [awesome-c2pa](README.md) - Ajouter des ressources, traduire la documentation
- [Implémentations C2PA](https://github.com/contentauth) - Contribuer au code
- [Content Authenticity Initiative](https://contentauthenticity.org) - Rejoindre le mouvement

---

## Carte de référence rapide

### Vérifier le contenu
```bash
c2patool image.jpg
```

### Signer le contenu
```bash
c2patool input.jpg \
  --manifest manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output signed.jpg
```

### Vérifier depuis le web
```
https://contentcredentials.org/verify
```

### Modèle de manifest courant
```json
{
  "claim_generator": "nom-app/version",
  "assertions": [
    {
      "label": "stds.schema-org.CreativeWork",
      "data": {
        "author": [{"name": "Nom du créateur"}]
      }
    }
  ]
}
```

---

## Dépannage

### "No C2PA data found"
- Le fichier peut ne pas avoir de manifest C2PA
- Les métadonnées peuvent avoir été supprimées
- Essayez un format de fichier différent

### "Invalid signature"
- Fichier modifié après signature
- Certificat révoqué ou expiré
- Chaîne de confiance brisée

### "Certificate not trusted"
- Utilisation d'un certificat auto-signé (attendu pour les tests)
- Autorité de certification pas dans la liste de confiance
- Ajoutez des ancres de confiance personnalisées si nécessaire

### Problèmes de performance
- C2PA ajoute environ 10-50 Ko par manifest (minimal)
- La signature prend < 1 seconde pour les fichiers typiques
- La vérification est quasi instantanée

---

**Prêt à commencer ?** Choisissez votre méthode ci-dessus et lancez-vous !

**Questions ?** Consultez la [FAQ](faq.md) ou [ouvrez une issue](https://github.com/paulortiz199928/awesome-c2pa/issues).

---

*Dernière mise à jour : Novembre 2025*
