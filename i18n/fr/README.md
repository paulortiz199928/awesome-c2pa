# Awesome C2PA [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Une liste organisée de ressources C2PA (Coalition for Content Provenance and Authenticity), incluant des spécifications multilingues, des outils, des bibliothèques et des supports pédagogiques.

**[English](../../README.md) | [简体中文](../zh-Hans/README.md) | [繁體中文](../zh-Hant/README.md) | [日本語](../ja/README.md) | [한국어](../ko/README.md) | [Deutsch](../de/README.md) | Français | [Русский](../ru/README.md)**

C2PA est une norme technique ouverte qui permet aux éditeurs, créateurs et consommateurs de retracer l'origine de différents types de médias. À l'ère du contenu généré par l'IA, C2PA aide à vérifier l'authenticité et la provenance du contenu.

## 🌟 Points forts

**🌍 Spécifications officielles multilingues** - Ce projet propose les premières traductions communautaires de la spécification officielle C2PA dans plusieurs langues, rendant C2PA accessible aux développeurs du monde entier.

**🤝 Aidez à améliorer les traductions** - Nos traductions sont assistées par IA (DeepL) et en version bêta. Locuteurs natifs : [signalez les erreurs](https://github.com/paulortiz199928/awesome-c2pa/issues/new?template=translation.md) pour améliorer la qualité !

## Sommaire

- [Spécifications officielles (Multilingues)](#-spécifications-officielles-multilingues)
- [Qu'est-ce que C2PA ?](#-quest-ce-que-c2pa)
- [Foire aux questions](#-foire-aux-questions)
- [Ressources officielles](#-ressources-officielles)
- [Outils et bibliothèques](#-outils-et-bibliothèques)
  - [Rust](#rust)
  - [JavaScript/TypeScript](#javascripttypescript)
  - [Python](#python)
  - [Go](#go)
  - [Java](#java)
  - [Autres langages](#autres-langages)
- [Outils en ligne de commande](#-outils-en-ligne-de-commande)
- [Extensions de navigateur et applications](#-applications)
- [Ressources pédagogiques](#-ressources-pédagogiques)
  - [Tutoriels](#tutoriels)
  - [Vidéos](#vidéos)
  - [Articles et blogs](#articles-et-blogs)
- [Cas d'usage et démos](#-cas-dusage-et-démos)
- [Organisations et écosystème](#-organisations-et-écosystème)
- [Actualités et mises à jour](#-actualités-et-mises-à-jour)
- [Communauté](#-communauté)
- [Contribution](#-contribution)

---

## 🌍 Spécifications officielles (Multilingues)

La spécification C2PA version 2.2 est disponible en plusieurs langues. Ces traductions aident les développeurs du monde entier à comprendre et à implémenter C2PA dans leurs applications.

| Langue | Document | Statut | Méthode | Dernière mise à jour |
|----------|----------|--------|--------|--------------|
| 🇬🇧 English | [C2PA Specification 2.2](../../docs/specifications/C2PA_Specification.pdf) | ✅ Officiel | C2PA Org | Mai 2025 |
| 🇨🇳 简体中文 | [C2PA 规范 2.2](../../docs/specifications/C2PA_Specification_zh-Hans.pdf) | 🔄 Bêta | IA + Révision | 2025 |
| 🇯🇵 日本語 | [C2PA 仕様 2.2](../../docs/specifications/C2PA_Specification_ja.pdf) | 🔄 Bêta | IA + Révision | 2025 |
| 🇩🇪 Deutsch | [C2PA Spezifikation 2.2](../../docs/specifications/C2PA_Specification_de.pdf) | 🔄 Bêta | IA + Révision | 2025 |
| 🇫🇷 Français | [Spécification C2PA 2.2](../../docs/specifications/C2PA_Specification_fr.pdf) | 🔄 Bêta | IA + Révision | 2025 |
| 🇰🇷 한국어 | Prochainement | 🚧 Planifié | - | - |
| 🇪🇸 Español | Prochainement | 🚧 Planifié | - | - |
| 🇵🇹 Português | Prochainement | 🚧 Planifié | - | - |

> **Avis de traduction** : Les traductions non anglaises sont assistées par IA (DeepL) avec révision communautaire. Bien que nous nous efforcions d'être précis, des erreurs peuvent subsister. Les locuteurs natifs sont encouragés à [signaler les problèmes](https://github.com/paulortiz199928/awesome-c2pa/issues/new?template=translation.md) ou à soumettre des corrections. La version anglaise reste la référence officielle.

**Navigation rapide** : [Voir toutes les spécifications →](../../docs/README.md)

---

## 🤔 Qu'est-ce que C2PA ?

**C2PA (Coalition for Content Provenance and Authenticity)** est une norme ouverte qui ajoute des métadonnées signées cryptographiquement aux fichiers multimédias, permettant la vérification de l'origine du contenu et de son historique de modification.

**Avantages clés :**
- ✅ Vérifier l'authenticité du contenu et détecter les falsifications
- ✅ Suivre l'historique complet de modification depuis l'original jusqu'à la version actuelle
- ✅ Identifier le contenu généré ou modifié par IA
- ✅ Protéger l'attribution des créateurs et la propriété intellectuelle

**Vous souhaitez approfondir ?**
- 📖 [Guide de démarrage rapide en 5 minutes](quick-start.md) - Démarrez immédiatement
- ❓ [FAQ complète](faq.md) - Plus de 25 questions détaillées
- 📚 [Spécifications techniques](../../docs/README.md) - Plongez dans la norme

---

## ❓ Foire aux questions

Réponses rapides aux questions les plus courantes :

<details>
<summary><b>Qu'est-ce que C2PA et comment fonctionne-t-il ?</b></summary>

C2PA ajoute des métadonnées signées cryptographiquement (« manifests ») aux fichiers multimédias contenant des informations de provenance. Toute falsification brise la signature, rendant les modifications détectables. Il utilise une PKI standard (comme les certificats HTTPS), et non une blockchain.
</details>

<details>
<summary><b>C2PA peut-il être supprimé ? Peut-il détecter les images générées par IA ?</b></summary>

**Suppression** : Oui, par conception. C2PA prouve l'authenticité *lorsqu'il est présent*, plutôt que d'empêcher sa suppression.

**Détection IA** : Pas automatiquement. C2PA enregistre ce que les créateurs déclarent. Les outils d'IA doivent volontairement étiqueter leur production comme « générée par IA » dans les manifests.
</details>

<details>
<summary><b>Quels appareils photo et logiciels prennent en charge C2PA ?</b></summary>

**Appareils photo** : Leica (M11-P, SL3), Sony (Alpha 1, A9 III, A7S III, A7 IV), Nikon (Z6 III prévu pour 2025) peuvent signer des photos au moment de la capture.

**Logiciels** : Adobe Photoshop/Lightroom, Capture One, et de nombreux outils open source.

**Coût** : La norme et les outils sont gratuits. Frais de certificat : environ 50-500 $/an.
</details>

**[→ Voir les 25+ FAQ](faq.md)** couvrant les détails techniques, la confidentialité, la sécurité et l'adoption.

---

## 📚 Ressources officielles

- [Site officiel C2PA](https://c2pa.org/) - Site principal avec actualités et informations
- [Spécifications C2PA](https://c2pa.org/specifications/specifications/2.2/index.html) - Portail de spécifications officielles (v2.2)
- [Organisation GitHub C2PA](https://github.com/c2pa-org) - Dépôts GitHub officiels
- [Content Authenticity Initiative](https://contentauthenticity.org/) - Initiative menée par Adobe soutenant C2PA

---

## 🛠️ Outils et bibliothèques

### Rust

- [c2pa-rs](https://github.com/contentauth/c2pa-rs) - SDK Rust officiel pour créer et valider des manifests C2PA. L'implémentation de référence.

### JavaScript/TypeScript

- [c2pa-node-v2](https://github.com/contentauth/c2pa-node-v2) - Bindings Node.js officiels pour le SDK Rust C2PA
- [c2pa-js](https://github.com/contentauth/c2pa-js) - Bibliothèque JavaScript pour lire les manifests C2PA dans les navigateurs

### Python

- [c2pa-python](https://github.com/contentauth/c2pa-python) - Bindings Python officiels pour le SDK Rust C2PA

### Java

- [c2pa-java](https://github.com/contentauth/c2pa-java) - Bindings Java pour le SDK C2PA

### Autres langages

- [c2pa-c](https://github.com/contentauth/c2pa-c) - Binding C et C++ pour C2PA
- [c2pa-ios](https://github.com/contentauth/c2pa-ios) - SDK C2PA pour iOS
- Les bindings de langages s'étendent - consultez le [GitHub officiel](https://github.com/contentauth/) pour les mises à jour

---

## 🔧 Outils en ligne de commande

- [Outil en ligne de commande C2PA](https://github.com/contentauth/c2pa-rs/tree/main/cli) - Outil en ligne de commande officiel pour créer et inspecter les manifests C2PA
  - Créer, lire et valider du contenu C2PA
  - Multiplateforme : Windows, macOS, Linux
  - Prend en charge les images, vidéos, audio

---

## 🌐 Applications

- [Content Credentials Verify](https://contentcredentials.org/verify) - Outil web officiel pour vérifier le contenu C2PA

---

## 📖 Ressources pédagogiques

### Tutoriels

- [Guide de démarrage rapide C2PA](quick-start.md) - Introduction de 5 minutes à l'implémentation C2PA
- [Documentation développeur C2PA](https://opensource.contentauthenticity.org/docs) - Guide de démarrage et documentation officiels
- [Tutoriel développeur C2PA](https://opensource.contentauthenticity.org/docs/getting-started) - Tutoriel d'implémentation pas à pas

### Vidéos

- [Introduction à Content Authenticity Initiative](https://www.youtube.com/@contentauthenticity) - Chaîne YouTube officielle avec vidéos éducatives
- [Aperçu technique C2PA](https://www.youtube.com/results?search_query=c2pa+technical) - Conférences et présentations techniques
- [Comment fonctionnent les Content Credentials](https://contentauthenticity.org/how-it-works) - Explication visuelle de C2PA en action

### Articles et blogs

- [Site officiel C2PA](https://c2pa.org) - Actualités, mises à jour et ressources techniques
- [Blog Adobe Content Authenticity](https://blog.adobe.com/en/topics/content-authenticity) - Insights sectoriels et cas d'usage
- [Comprendre les manifests C2PA](https://opensource.contentauthenticity.org/docs/manifest) - Plongée technique approfondie

---

## 🎯 Cas d'usage et démos

### Applications sectorielles

- **Actualités et journalisme** : Vérifier l'authenticité des photos et vidéos (essais BBC, Reuters)
- **Fabricants d'appareils photo** : Signature C2PA dans l'appareil (Leica, Nikon, Sony)
- **Réseaux sociaux** : Provenance du contenu sur les plateformes (en exploration)
- **Générateurs d'images IA** : Étiquetage du contenu généré par IA (Midjourney, DALL-E)
- **Photographie de stock** : Prouver la paternité originale (Adobe Stock, Shutterstock)


## 🏢 Organisations et écosystème

### Membres du comité de pilotage

- Adobe
- Arm
- BBC
- Intel
- Microsoft
- Publicis Groupe
- Sony
- Truepic

### Adoptants et partenaires

- **Fournisseurs GenAI** : [OpenAI](https://openai.com/index/understanding-the-source-of-what-we-see-and-hear-online/), [Google](https://blog.google/technology/ai/google-gen-ai-content-transparency-c2pa/), [Meta](https://about.fb.com/news/2024/02/labeling-ai-generated-images-on-facebook-instagram-and-threads)
- **Fabricants d'appareils photo** : Leica, Nikon, Sony, Canon
- **Éditeurs de logiciels** : Adobe, Microsoft, Capture One
- **Organisations de presse** : BBC, New York Times, Reuters
- **Plateformes sociales** : Exploration de l'intégration
- **Autorités de certification** : DigiCert, GlobalSign, et autres

---

## 📰 Actualités et mises à jour

- [Publication de la spécification C2PA v2.2](https://c2pa.org) - Dernière version (2025)
- [Jalons de Content Authenticity Initiative](https://contentauthenticity.org/news) - Mises à jour sur l'adoption sectorielle
- [C2PA sur X/Twitter](https://twitter.com/C2PA_Coalition) - Suivez pour les mises à jour en temps réel

---

## 🤝 Communauté

### Participez

- [Issues GitHub Awesome C2PA](https://github.com/paulortiz199928/awesome-c2pa/issues) - Posez des questions et partagez des idées

### Contribuez à ce projet

Nous accueillons les contributions ! Consultez notre [Guide de contribution](../../CONTRIBUTING.md) pour plus de détails sur :
- Ajout de nouvelles ressources
- Traduction des spécifications
- Amélioration de la documentation
- Signalement de problèmes

---

## 📋 Contribution

Les contributions sont les bienvenues ! Veuillez d'abord lire nos [Directives de contribution](../../CONTRIBUTING.md).

### Comment contribuer

1. **Ajouter des ressources** : Soumettez une PR avec de nouveaux outils, bibliothèques ou articles
2. **Traduire les spécifications** : Aidez à traduire la spécification C2PA dans de nouvelles langues
3. **Corriger les erreurs** : Signalez ou corrigez les erreurs de traduction, les liens brisés ou les informations obsolètes
4. **Améliorer le contenu** : Améliorez les descriptions, ajoutez des exemples ou restructurez les sections

### Normes de qualité

Nous acceptons les ressources qui sont :
- Activement maintenues (mises à jour au cours de la dernière année)
- Bien documentées
- Pertinentes pour la compréhension ou l'implémentation de C2PA
- Open source (préféré) ou librement accessibles

---

## 🙏 Remerciements

- Merci à l'[Organisation C2PA](https://c2pa.org) pour le développement de la norme ouverte
- Merci à la [Content Authenticity Initiative](https://contentauthenticity.org) pour la promotion de l'adoption
- Merci à tous les contributeurs qui aident à maintenir cette ressource

---

**[⬆ Retour au sommaire](#sommaire)**

*Dernière mise à jour : Novembre 2025 | Maintenu par la communauté*
