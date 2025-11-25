# C2PA Schnellstartanleitung

Starten Sie in 5 Minuten mit C2PA! Diese Anleitung hilft Ihnen, C2PA-signierte Inhalte zu verstehen, zu verifizieren und zu erstellen.

## 📋 Inhaltsverzeichnis

1. [C2PA verstehen](#c2pa-verstehen)
2. [C2PA-Inhalte verifizieren](#c2pa-inhalte-verifizieren)
3. [C2PA-Inhalte erstellen](#c2pa-inhalte-erstellen)
4. [Nächste Schritte](#nächste-schritte)

---

## C2PA verstehen

### Was Sie wissen müssen

**C2PA** fügt ein kryptografisch signiertes "Manifest" zu Ihren Mediendateien hinzu, das Folgendes enthält:
- **Wer**: Identität des Erstellers/Bearbeiters
- **Was**: Durchgeführte Aktionen (erstellt, bearbeitet, KI-generiert)
- **Wann**: Zeitstempel
- **Wie**: Verwendete Tools und Einstellungen
- **Von**: Quellmaterialien (Zutaten)

### Schlüsselkonzepte in 30 Sekunden

```
Originalfoto → [C2PA-Manifest hinzufügen] → Signiertes Foto
                     ↓
              Enthält Metadaten:
              • Ersteller: John Doe
              • Kamera: Nikon Z9
              • Datum: 2025-11-21
              • GPS: 37.7749°N, 122.4194°W
              • Signatur: ✓ Gültig
```

Bei Bearbeitung:
```
Signiertes Foto → [In Photoshop bearbeiten] → Neues signiertes Foto
                                                    ↓
                                             Neues Manifest verweist auf
                                             Original als "Zutat"
```

**Ergebnis**: Vollständige Herkunftskette vom Original zur aktuellen Version.

---

## C2PA-Inhalte verifizieren

### Methode 1: Online-Tool (Am einfachsten)

**Keine Installation erforderlich!**

1. Besuchen Sie https://contentcredentials.org/verify
2. Ziehen Sie ein beliebiges Bild/Video/Dokument per Drag & Drop
3. Zeigen Sie Herkunftsinformationen an:
   - Ersteller-Identität
   - Bearbeitungsverlauf
   - Signaturstatus
   - Originalinhalt (falls verfügbar)

**Probieren Sie es jetzt** mit Beispielbildern von: https://contentauthenticity.org/examples

### Methode 2: Browser-Erweiterung

**Für automatische Verifizierung beim Surfen:**

1. Installieren Sie die [Content Credentials-Erweiterung](https://chrome.google.com/webstore)
   - Verfügbar für Chrome, Edge, Brave
2. Surfen Sie normal
3. Erweiterung erkennt automatisch C2PA-Inhalte
4. Klicken Sie auf das Symbol, um Herkunftsdetails anzuzeigen

### Methode 3: Kommandozeile

**Für Entwickler und Power-User:**

#### c2patool installieren

```bash
# macOS/Linux (mit Cargo)
cargo install c2patool

# macOS (mit Homebrew)
brew install c2patool

# Windows
# Herunterladen von: https://github.com/contentauth/c2patool/releases
```

#### Datei verifizieren

```bash
# Grundlegende Verifizierung
c2patool photo.jpg

# Detaillierte JSON-Ausgabe
c2patool photo.jpg --detailed

# Manifest in JSON-Datei speichern
c2patool photo.jpg --output manifest.json

# Mehrere Dateien prüfen
c2patool *.jpg
```

#### Beispielausgabe

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

### Methode 4: Programmatisch

**Verifizierung in Ihre App integrieren:**

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

## C2PA-Inhalte erstellen

### Methode 1: Unterstützte Software verwenden

**Kein Programmieren erforderlich:**

#### Adobe Photoshop/Lightroom

1. Öffnen Sie ein Bild in Photoshop/Lightroom
2. Gehen Sie zu **Bearbeiten → Content Credentials**
3. Füllen Sie Ersteller-Informationen aus
4. Speichern Sie die Datei → C2PA-Manifest wird automatisch hinzugefügt

#### Kameras mit integriertem C2PA

- **Nikon Z9/Z8**: In Kameraeinstellungen aktivieren → Fotos werden bei Aufnahme signiert
- **Leica M11-P/SL3**: Automatische Signierung aktiviert
- **Sony Alpha-Serie**: Über Firmware-Update aktivieren

### Methode 2: Kommandozeile (c2patool)

#### Voraussetzungen

Sie benötigen ein Signaturzertifikat:

**Zum Testen (selbstsigniert):**
```bash
# Test-Zertifikat generieren (nicht vertrauenswürdig für Validatoren)
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes
```

**Für Produktion:**
- Zertifikat von vertrauenswürdiger CA kaufen (DigiCert, GlobalSign usw.)
- C2PA-Schlüsselnutzungsanforderungen angeben

#### Manifest erstellen

`manifest.json` erstellen:

```json
{
  "claim_generator": "meine-app/1.0",
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

#### Datei signieren

```bash
# Mit Ihrem Zertifikat signieren
c2patool photo.jpg \
  --manifest manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output signed_photo.jpg

# Überprüfen, ob es funktioniert hat
c2patool signed_photo.jpg
```

### Methode 3: Programmatisch

#### Rust

```rust
use c2pa::{Builder, SigningAlg};

fn main() -> Result<(), Box<dyn std::error::Error>> {
    let mut builder = Builder::from_file("input.jpg")?;

    // Ersteller-Assertion hinzufügen
    builder.add_assertion("stds.schema-org.CreativeWork",
        r#"{"author": [{"name": "John Doe"}]}"#)?;

    // Signieren und speichern
    let signer = get_signer(); // Ihr Zertifikat/Schlüssel
    builder.sign("output.jpg", signer)?;

    Ok(())
}
```

#### JavaScript/Node.js

```javascript
const c2pa = require('c2pa-node');

async function sign(inputPath, outputPath) {
  const manifest = {
    claim_generator: 'meine-app/1.0',
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
    cert: 'path/to/cert.pem',
    key: 'path/to/key.pem'
  };

  await c2pa.sign(inputPath, outputPath, manifest, signer);
  console.log('Erfolgreich signiert!');
}

sign('input.jpg', 'output.jpg');
```

#### Python

```python
from c2pa import Builder, Signer

# Builder erstellen
builder = Builder.from_file('input.jpg')

# Assertions hinzufügen
builder.add_assertion('stds.schema-org.CreativeWork', {
    'author': [{'name': 'John Doe'}]
})

# Signieren
signer = Signer('cert.pem', 'key.pem')
builder.sign('output.jpg', signer)

print('Erfolgreich signiert!')
```

### Methode 4: Signierte Inhalte bearbeiten (Herkunft bewahren)

Beim Bearbeiten von C2PA-signierten Inhalten verweisen Sie auf das Original als "Zutat":

```bash
# Bearbeiten und Kette bewahren
c2patool edited_photo.jpg \
  --parent original_photo.jpg \
  --manifest edit_manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output final_photo.jpg
```

Das neue Manifest verweist auf `original_photo.jpg` als Zutat und bewahrt so die vollständige Historie.

---

## Nächste Schritte

### Mehr erfahren

**Die Spezifikation verstehen:**
- [English](../../docs/specifications/C2PA_Specification.pdf)
- [中文](../../docs/specifications/C2PA_Specification_zh-Hans.pdf)
- [日本語](../../docs/specifications/C2PA_Specification_ja.pdf)
- [Deutsch](../../docs/specifications/C2PA_Specification_de.pdf)

**Tools erkunden:**
- [Tools & Bibliotheken](README.md#tools--bibliotheken) - SDKs für alle gängigen Sprachen
- [Offizielle Dokumentation](https://opensource.contentauthenticity.org/docs)

**Häufige Fragen:**
- [FAQ](faq.md) - Über 25 häufig gestellte Fragen
- [GitHub Discussions](https://github.com/c2pa-org/../../docs/specifications/discussions)

### Tutorials & Beispiele

**Offizielle Tutorials:**
- [C2PA Entwickler-Tutorial](https://opensource.contentauthenticity.org/docs/tutorial)
- [Manifeste erstellen](https://opensource.contentauthenticity.org/docs/manifest/guide)
- [Assertion-Referenz](https://opensource.contentauthenticity.org/docs/manifest/assertions)

**Code-Beispiele:**
- [c2pa-rs Beispiele](https://github.com/contentauth/c2pa-rs/tree/main/sdk/examples)
- [c2pa-node Beispiele](https://github.com/contentauth/c2pa-node/tree/main/examples)
- [c2pa-python Beispiele](https://github.com/contentauth/c2pa-python/tree/main/examples)

### Produktionsbereitstellung

**Vor dem Go-Live:**

1. **Produktionszertifikat erhalten**
   - Von vertrauenswürdiger CA kaufen (DigiCert, GlobalSign usw.)
   - C2PA-kompatible Schlüsselnutzung sicherstellen
   - Kosten: ~50-500 €/Jahr

2. **Sichere Schlüsselspeicherung**
   - Hardware-Sicherheitsmodul (HSM) für private Schlüssel verwenden
   - Oder Cloud-HSM (AWS CloudHSM, Azure Key Vault)
   - Niemals Schlüssel in Quellcodeverwaltung committen

3. **Gründlich testen**
   - Signaturen mit mehreren Validatoren verifizieren
   - Auf verschiedenen Dateiformaten testen
   - Plattformübergreifende Kompatibilität prüfen

4. **Überwachen & Warten**
   - Zertifikatsrotation implementieren
   - Auf Widerrufe überwachen
   - SDKs aktuell halten

### Integration in Ihre Anwendung

**Wichtige Integrationspunkte:**

```
Ihr App-Workflow:

1. Inhaltserstellung/-Upload
   ↓
2. [C2PA-Manifest hinzufügen] ← Ihr Integrationspunkt
   ↓
3. Mit Zertifikat signieren
   ↓
4. Signierten Inhalt speichern/veröffentlichen
   ↓
5. [Optional] Bei Anzeige verifizieren ← Weiterer Integrationspunkt
```

**Typische Integrationszeit:**
- Einfache Verifizierung: 1-2 Tage
- Grundlegende Signierung: 3-5 Tage
- Vollständige Produktionsbereitstellung: 2-4 Wochen

### Zertifikate erhalten

**Testen (Kostenlos):**
- Selbstsignierte Zertifikate
- Nur für Entwicklung geeignet
- Nicht vertrauenswürdig für Validatoren

**Produktion:**
- **DigiCert**: https://www.digicert.com/
- **GlobalSign**: https://www.globalsign.com/
- **Entrust**: https://www.entrust.com/
- Zertifikate mit C2PA-Schlüsselnutzungserweiterungen anfordern

### Der Community beitreten

**Hilfe erhalten:**
- [GitHub Issues](https://github.com/c2pa-org/../../docs/specifications/issues) - Fehlerberichte
- [GitHub Discussions](https://github.com/c2pa-org/../../docs/specifications/discussions) - Fragen
- [C2PA Website](https://c2pa.org) - Offizielle Ressourcen

**Beitragen:**
- [awesome-c2pa](README.md) - Ressourcen hinzufügen, Dokumentation übersetzen
- [C2PA Implementierungen](https://github.com/contentauth) - Code beitragen
- [Content Authenticity Initiative](https://contentauthenticity.org) - Der Bewegung beitreten

---

## Schnellreferenzkarte

### Inhalt verifizieren
```bash
c2patool image.jpg
```

### Inhalt signieren
```bash
c2patool input.jpg \
  --manifest manifest.json \
  --signer-cert cert.pem \
  --signer-key key.pem \
  --output signed.jpg
```

### Von Web prüfen
```
https://contentcredentials.org/verify
```

### Häufige Manifest-Vorlage
```json
{
  "claim_generator": "app-name/version",
  "assertions": [
    {
      "label": "stds.schema-org.CreativeWork",
      "data": {
        "author": [{"name": "Name des Erstellers"}]
      }
    }
  ]
}
```

---

## Problembehandlung

### "No C2PA data found"
- Datei hat möglicherweise kein C2PA-Manifest
- Metadaten wurden möglicherweise entfernt
- Versuchen Sie ein anderes Dateiformat

### "Invalid signature"
- Datei nach Signierung geändert
- Zertifikat widerrufen oder abgelaufen
- Vertrauenskette unterbrochen

### "Certificate not trusted"
- Verwendung selbstsigniertes Zertifikat (bei Tests zu erwarten)
- CA nicht in Vertrauensliste
- Bei Bedarf benutzerdefinierte Vertrauensanker hinzufügen

### Leistungsprobleme
- C2PA fügt ~10-50 KB pro Manifest hinzu (minimal)
- Signierung dauert < 1 Sekunde für typische Dateien
- Verifizierung ist nahezu sofort

---

**Bereit zu starten?** Wählen Sie oben Ihre Methode und legen Sie los!

**Fragen?** Siehe [FAQ](faq.md) oder [öffnen Sie ein Issue](https://github.com/paulortiz199928/awesome-c2pa/issues).

---

*Zuletzt aktualisiert: November 2025*
