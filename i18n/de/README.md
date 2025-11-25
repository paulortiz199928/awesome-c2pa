# Awesome C2PA [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Eine kuratierte Liste von C2PA (Coalition for Content Provenance and Authenticity) Ressourcen, einschließlich mehrsprachiger Spezifikationen, Tools, Bibliotheken und Lernmaterialien.

**[English](../../README.md) | [简体中文](../zh-Hans/README.md) | [繁體中文](../zh-Hant/README.md) | [日本語](../ja/README.md) | [한국어](../ko/README.md) | Deutsch | [Français](../fr/README.md) | [Русский](../ru/README.md)**

C2PA ist ein offener technischer Standard, der Publishern, Erstellern und Konsumenten die Möglichkeit bietet, die Herkunft verschiedener Medientypen nachzuverfolgen. Im Zeitalter von KI-generierten Inhalten hilft C2PA dabei, die Authentizität und Herkunft von Inhalten zu verifizieren.

## 🌟 Highlights

**🌍 Mehrsprachige offizielle Spezifikationen** - Dieses Projekt bietet die ersten community-getriebenen Übersetzungen der offiziellen C2PA-Spezifikation in mehreren Sprachen und macht C2PA für Entwickler weltweit zugänglich.

**🤝 Helfen Sie, die Übersetzungen zu verbessern** - Unsere Übersetzungen sind KI-unterstützt (DeepL) und befinden sich in der Beta-Phase. Muttersprachler: [Melden Sie Fehler](https://github.com/paulortiz199928/awesome-c2pa/issues/new?template=translation.md), um die Qualität zu verbessern!

## Inhalt

- [Offizielle Spezifikationen (Mehrsprachig)](#-offizielle-spezifikationen-mehrsprachig)
- [Was ist C2PA?](#-was-ist-c2pa)
- [Häufig gestellte Fragen](#-häufig-gestellte-fragen)
- [Offizielle Ressourcen](#-offizielle-ressourcen)
- [Tools & Bibliotheken](#-tools--bibliotheken)
  - [Rust](#rust)
  - [JavaScript/TypeScript](#javascripttypescript)
  - [Python](#python)
  - [Go](#go)
  - [Java](#java)
  - [Andere Sprachen](#andere-sprachen)
- [Kommandozeilen-Tools](#-kommandozeilen-tools)
- [Browser-Erweiterungen & Anwendungen](#-anwendungen)
- [Lernressourcen](#-lernressourcen)
  - [Tutorials](#tutorials)
  - [Videos](#videos)
  - [Artikel & Blogs](#artikel--blogs)
- [Anwendungsfälle & Demos](#-anwendungsfälle--demos)
- [Organisationen & Ökosystem](#-organisationen--ökosystem)
- [Neuigkeiten & Updates](#-neuigkeiten--updates)
- [Community](#-community)
- [Mitwirken](#-mitwirken)

---

## 🌍 Offizielle Spezifikationen (Mehrsprachig)

Die C2PA-Spezifikation Version 2.2 ist in mehreren Sprachen verfügbar. Diese Übersetzungen helfen Entwicklern weltweit, C2PA zu verstehen und in ihre Anwendungen zu implementieren.

| Sprache | Dokument | Status | Methode | Zuletzt aktualisiert |
|----------|----------|--------|--------|--------------|
| 🇬🇧 English | [C2PA Specification 2.2](../../docs/specifications/C2PA_Specification.pdf) | ✅ Offiziell | C2PA Org | Mai 2025 |
| 🇨🇳 简体中文 | [C2PA 规范 2.2](../../docs/specifications/C2PA_Specification_zh-Hans.pdf) | 🔄 Beta | KI + Review | 2025 |
| 🇯🇵 日本語 | [C2PA 仕様 2.2](../../docs/specifications/C2PA_Specification_ja.pdf) | 🔄 Beta | KI + Review | 2025 |
| 🇩🇪 Deutsch | [C2PA Spezifikation 2.2](../../docs/specifications/C2PA_Specification_de.pdf) | 🔄 Beta | KI + Review | 2025 |
| 🇫🇷 Français | [Spécification C2PA 2.2](../../docs/specifications/C2PA_Specification_fr.pdf) | 🔄 Beta | KI + Review | 2025 |
| 🇰🇷 한국어 | Demnächst verfügbar | 🚧 Geplant | - | - |
| 🇪🇸 Español | Demnächst verfügbar | 🚧 Geplant | - | - |
| 🇵🇹 Português | Demnächst verfügbar | 🚧 Geplant | - | - |

> **Hinweis zur Übersetzung**: Nicht-englische Übersetzungen sind KI-unterstützt (DeepL) und werden von der Community überprüft. Obwohl wir uns um Genauigkeit bemühen, können Fehler auftreten. Muttersprachler werden ermutigt, [Probleme zu melden](https://github.com/paulortiz199928/awesome-c2pa/issues/new?template=translation.md) oder Korrekturen einzureichen. Die englische Version bleibt die maßgebliche Referenz.

**Schnellnavigation**: [Alle Spezifikationen anzeigen →](../../docs/README.md)

---

## 🤔 Was ist C2PA?

**C2PA (Coalition for Content Provenance and Authenticity)** ist ein offener Standard, der kryptografisch signierte Metadaten zu Mediendateien hinzufügt und so die Verifizierung der Inhaltsherkunft und des Bearbeitungsverlaufs ermöglicht.

**Hauptvorteile:**
- ✅ Authentizität von Inhalten verifizieren und Manipulationen erkennen
- ✅ Vollständigen Bearbeitungsverlauf vom Original zur aktuellen Version nachverfolgen
- ✅ KI-generierte oder KI-modifizierte Inhalte identifizieren
- ✅ Urheberschaft und geistiges Eigentum schützen

**Möchten Sie tiefer eintauchen?**
- 📖 [5-Minuten-Schnellstartanleitung](quick-start.md) - Sofort loslegen
- ❓ [Vollständige FAQ](faq.md) - Über 25 detaillierte Fragen beantwortet
- 📚 [Technische Spezifikationen](../../docs/README.md) - Tiefgehender Einblick in den Standard

---

## ❓ Häufig gestellte Fragen

Schnelle Antworten auf die häufigsten Fragen:

<details>
<summary><b>Was ist C2PA und wie funktioniert es?</b></summary>

C2PA fügt Mediendateien kryptografisch signierte Metadaten ("Manifeste") mit Herkunftsinformationen hinzu. Jegliche Manipulation bricht die Signatur, wodurch Änderungen erkennbar werden. Es verwendet Standard-PKI (wie HTTPS-Zertifikate), keine Blockchain.
</details>

<details>
<summary><b>Kann C2PA entfernt werden? Kann es KI-generierte Bilder erkennen?</b></summary>

**Entfernung**: Ja, das ist beabsichtigt. C2PA beweist die Authentizität *wenn vorhanden*, anstatt die Entfernung zu verhindern.

**KI-Erkennung**: Nicht automatisch. C2PA zeichnet auf, was Ersteller angeben. KI-Tools müssen ihre Ausgabe freiwillig als "KI-generiert" in Manifesten kennzeichnen.
</details>

<details>
<summary><b>Welche Kameras und Software unterstützen C2PA?</b></summary>

**Kameras**: Leica (M11-P, SL3), Sony (Alpha 1, A9 III, A7S III, A7 IV), Nikon (Z6 III geplant für 2025) können Fotos zum Aufnahmezeitpunkt signieren.

**Software**: Adobe Photoshop/Lightroom, Capture One und viele Open-Source-Tools.

**Kosten**: Der Standard und die Tools sind kostenlos. Zertifikatsgebühren: ~50-500 €/Jahr.
</details>

**[→ Alle 25+ FAQs anzeigen](faq.md)** zu technischen Details, Datenschutz, Sicherheit und Verbreitung.

---

## 📚 Offizielle Ressourcen

- [C2PA Offizielle Website](https://c2pa.org/) - Hauptwebsite mit Neuigkeiten und Informationen
- [C2PA Spezifikationen](https://c2pa.org/specifications/specifications/2.2/index.html) - Offizielles Spezifikationsportal (v2.2)
- [C2PA GitHub Organisation](https://github.com/c2pa-org) - Offizielle GitHub-Repositories
- [Content Authenticity Initiative](https://contentauthenticity.org/) - Von Adobe geleitete Initiative zur Unterstützung von C2PA

---

## 🛠️ Tools & Bibliotheken

### Rust

- [c2pa-rs](https://github.com/contentauth/c2pa-rs) - Offizielles Rust SDK zum Erstellen und Validieren von C2PA-Manifesten. Die Referenzimplementierung.

### JavaScript/TypeScript

- [c2pa-node-v2](https://github.com/contentauth/c2pa-node-v2) - Offizielle Node.js-Bindungen für das C2PA Rust SDK
- [c2pa-js](https://github.com/contentauth/c2pa-js) - JavaScript-Bibliothek zum Lesen von C2PA-Manifesten in Browsern

### Python

- [c2pa-python](https://github.com/contentauth/c2pa-python) - Offizielle Python-Bindungen für das C2PA Rust SDK

### Java

- [c2pa-java](https://github.com/contentauth/c2pa-java) - Java-Bindungen für das C2PA SDK

### Andere Sprachen

- [c2pa-c](https://github.com/contentauth/c2pa-c) - C- und C++-Bindung für C2PA
- [c2pa-ios](https://github.com/contentauth/c2pa-ios) - C2PA SDK für iOS
- Sprachbindungen werden erweitert - prüfen Sie das [offizielle GitHub](https://github.com/contentauth/) für Updates

---

## 🔧 Kommandozeilen-Tools

- [C2PA Kommandozeilen-Tool](https://github.com/contentauth/c2pa-rs/tree/main/cli) - Offizielles Kommandozeilen-Tool zum Erstellen und Prüfen von C2PA-Manifesten
  - Erstellen, Lesen und Validieren von C2PA-Inhalten
  - Plattformübergreifend: Windows, macOS, Linux
  - Unterstützt Bilder, Videos, Audio

---

## 🌐 Anwendungen

- [Content Credentials Verify](https://contentcredentials.org/verify) - Offizielles Web-Tool zur Verifizierung von C2PA-Inhalten
---

## 📖 Lernressourcen

### Tutorials

- [C2PA Schnellstartanleitung](quick-start.md) - 5-Minuten-Einführung in die C2PA-Implementierung
- [C2PA Entwicklerdokumentation](https://opensource.contentauthenticity.org/docs) - Offizieller Einstiegsleitfaden und Dokumentation
- [C2PA Entwickler-Tutorial](https://opensource.contentauthenticity.org/docs/getting-started) - Schritt-für-Schritt-Implementierungsanleitung

### Videos

- [Content Authenticity Initiative Einführung](https://www.youtube.com/@contentauthenticity) - Offizieller YouTube-Kanal mit Lehrvideos
- [C2PA Technischer Überblick](https://www.youtube.com/results?search_query=c2pa+technical) - Konferenzvorträge und technische Präsentationen
- [Wie Content Credentials funktionieren](https://contentauthenticity.org/how-it-works) - Visuelle Erklärung von C2PA in Aktion

### Artikel & Blogs

- [C2PA Offizielle Website](https://c2pa.org) - Neuigkeiten, Updates und technische Ressourcen
- [Adobe Content Authenticity Blog](https://blog.adobe.com/en/topics/content-authenticity) - Einblicke in die Branche und Anwendungsfälle
- [C2PA-Manifeste verstehen](https://opensource.contentauthenticity.org/docs/manifest) - Technischer Tiefgang

---

## 🎯 Anwendungsfälle & Demos

### Branchenanwendungen

- **Nachrichten & Journalismus**: Authentizität von Fotos und Videos verifizieren (BBC, Reuters Testläufe)
- **Kamerahersteller**: Kamerainterne C2PA-Signierung (Leica, Nikon, Sony)
- **Social Media**: Herkunftsnachweis von Inhalten auf Plattformen (in Prüfung)
- **KI-Bildgeneratoren**: Kennzeichnung KI-generierter Inhalte (Midjourney, DALL-E)
- **Stock-Fotografie**: Nachweis der Originalurheberschaft (Adobe Stock, Shutterstock)


## 🏢 Organisationen & Ökosystem

### Mitglieder des Lenkungsausschusses

- Adobe
- Arm
- BBC
- Intel
- Microsoft
- Publicis Groupe
- Sony
- Truepic

### Anwender & Partner

- **GenAI-Anbieter**: [OpenAI](https://openai.com/index/understanding-the-source-of-what-we-see-and-hear-online/), [Google](https://blog.google/technology/ai/google-gen-ai-content-transparency-c2pa/), [Meta](https://about.fb.com/news/2024/02/labeling-ai-generated-images-on-facebook-instagram-and-threads)
- **Kamerahersteller**: Leica, Nikon, Sony, Canon
- **Softwareunternehmen**: Adobe, Microsoft, Capture One
- **Nachrichtenorganisationen**: BBC, New York Times, Reuters
- **Social-Media-Plattformen**: Integration wird geprüft
- **Zertifizierungsstellen**: DigiCert, GlobalSign und andere

---

## 📰 Neuigkeiten & Updates

- [C2PA v2.2 Spezifikation veröffentlicht](https://c2pa.org) - Neueste Version (2025)
- [Content Authenticity Initiative Meilensteine](https://contentauthenticity.org/news) - Updates zur Branchenakzeptanz
- [C2PA auf X/Twitter](https://twitter.com/C2PA_Coalition) - Folgen Sie für Echtzeit-Updates

---

## 🤝 Community

### Mitmachen
- [Awesome C2PA GitHub Issues](https://github.com/paulortiz199928/awesome-c2pa/issues) - Fragen stellen und Ideen teilen

### Zu diesem Projekt beitragen

Wir freuen uns über Beiträge! Siehe unseren [Beitragsleitfaden](../../CONTRIBUTING.md) für Details zu:
- Hinzufügen neuer Ressourcen
- Übersetzen von Spezifikationen
- Verbesserung der Dokumentation
- Melden von Problemen

---

## 📋 Mitwirken

Beiträge sind willkommen! Bitte lesen Sie zuerst unsere [Beitragsrichtlinien](../../CONTRIBUTING.md).

### Wie Sie beitragen können

1. **Ressourcen hinzufügen**: Reichen Sie einen PR mit neuen Tools, Bibliotheken oder Artikeln ein
2. **Spezifikationen übersetzen**: Helfen Sie, die C2PA-Spezifikation in neue Sprachen zu übersetzen
3. **Fehler beheben**: Melden oder beheben Sie Übersetzungsfehler, defekte Links oder veraltete Informationen
4. **Inhalte verbessern**: Beschreibungen verbessern, Beispiele hinzufügen oder Abschnitte umstrukturieren

### Qualitätsstandards

Wir akzeptieren Ressourcen, die:
- Aktiv gepflegt werden (innerhalb des letzten Jahres aktualisiert)
- Gut dokumentiert sind
- Für die C2PA-Implementierung oder das Verständnis relevant sind
- Open Source (bevorzugt) oder frei zugänglich sind

---

## 🙏 Danksagungen

- Dank an die [C2PA Organisation](https://c2pa.org) für die Entwicklung des offenen Standards
- Dank an die [Content Authenticity Initiative](https://contentauthenticity.org) für die Förderung der Verbreitung
- Dank an alle Mitwirkenden, die helfen, diese Ressource zu pflegen

---

**[⬆ Zurück nach oben](#inhalt)**

*Zuletzt aktualisiert: November 2025 | Gepflegt von der Community*
