---
category: general
date: 2026-06-22
description: Erfahren Sie, wie Sie zwischengespeicherte KI‑Modelle mit dem AI‑SDK
  in Python auflisten. Enthält Schritte zum Abrufen des Modell‑Cache‑Verzeichnisses
  und zur effizienten Verwaltung lokaler KI‑Modelle.
draft: false
keywords:
- list cached ai models
- retrieve model cache directory
- list local ai models
- ai sdk python
- manage ai model cache
language: de
og_description: Auflisten von zwischengespeicherten KI‑Modellen mit Python unter Verwendung
  des KI‑SDK. Folgen Sie diesem Schritt‑für‑Schritt‑Tutorial, um das Modell‑Cache‑Verzeichnis
  abzurufen und lokale KI‑Modelle zu verwalten.
og_title: Liste zwischengespeicherter KI-Modelle in Python – Vollständiger Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  headline: List Cached AI Models in Python – Complete Guide
  type: TechArticle
- description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  name: List Cached AI Models in Python – Complete Guide
  steps:
  - name: Import the AI SDK
    text: '```python # Step 1: Import the AI SDK (replace with the actual package
      name if different) import ai ```'
  - name: List All Cached Models
    text: '```python # Step 2: List all models that are cached locally cached_models
      = ai.list_local() print("Cached models:", cached_models) ```'
  - name: Retrieve the Model Cache Directory
    text: '```python # Step 3: Retrieve the directory where the model files are stored
      cache_dir = ai.get_local_path() print("Model cache directory:", cache_dir) ```'
  - name: Empty Cache
    text: If `ai.list_local()` returns an empty list, you might wonder whether the
      SDK is misconfigured. Double‑check the environment variable `AI_CACHE_DIR` (or
      the SDK’s config file) to ensure it points to a writable location.
  - name: Permissions Issues
    text: When accessing `ai.get_local_path()`, a `PermissionError` can surface on
      restrictive systems. The fix is usually to run the script with appropriate user
      rights or to adjust the directory’s ACLs.
  - name: Version Mismatches
    text: 'Sometimes the cache contains an older version of a model while your code
      requests a newer one. The SDK will automatically download the newer version,
      but you can pre‑empt this by inspecting the version tag in the list:'
  - name: Cleaning Up Old Models
    text: 'If you need to free up space, you can delete a specific model folder directly:'
  type: HowTo
- questions:
  - answer: Yes. The SDK abstracts away OS‑specific paths, so `ai.get_local_path()`
      returns a valid string on Linux, macOS, and Windows.
    question: Does this work on all operating systems?
  - answer: The built‑in `list_local()` only reports locally stored artifacts. For
      remote registries you’d use `ai.list_remote()` (if your SDK version provides
      it).
    question: Can I list models from a remote cache?
  - answer: 'Replace the import line with the actual package name, e.g., `import myai
      as ai`. All subsequent calls stay the same because the API contract is consistent
      across implementations. --- ## Conclusion You now have a solid, production‑ready
      method to **list cached AI models** using the **AI SDK Python** '
    question: What if the SDK name isn’t `ai`?
  type: FAQPage
tags:
- python
- ai
- sdk
title: Liste zwischengespeicherter KI-Modelle in Python – Vollständiger Leitfaden
url: /de/python/general/list-cached-ai-models-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zwischengespeicherte KI‑Modelle in Python auflisten – Komplett‑Anleitung

Haben Sie sich schon einmal gefragt, wie Sie **zwischengespeicherte KI‑Modelle** auf Ihrem Rechner auflisten können, ohne in obskuren Ordnern zu wühlen? Sie sind nicht allein. Viele Entwickler stoßen an Grenzen, wenn sie prüfen wollen, welche Modelle bereits lokal gespeichert sind – besonders bei begrenzter Bandbreite oder Offline‑Deployments. In diesem Tutorial zeigen wir Ihnen einen schnellen, unkomplizierten Weg, das AI‑SDK abzufragen, den Cache‑Inhalt auszugeben und genau zu sehen, wo sich die Dateien befinden.

Wir gehen außerdem auf verwandte Themen ein, wie **das Abrufen des Model‑Cache‑Verzeichnisses**, den Umgang mit leeren Caches und bewährte Methoden zum **Verwalten des KI‑Model‑Caches** in Produktions‑Skripten. Am Ende haben Sie ein eigenständiges Snippet, das Sie in jedes Python‑Projekt einbinden können.

## Voraussetzungen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes haben:

- Python 3.8 oder neuer installiert.
- Das AI‑SDK (das `ai`‑Paket) installiert via `pip install ai-sdk` oder aus dem internen Repository Ihrer Organisation.
- Grundlegende Erfahrung im Ausführen von Skripten über die Kommandozeile.

Es werden keine zusätzlichen Bibliotheken benötigt, sodass das Beispiel leichtgewichtig und portabel bleibt.

---

## Zwischengespeicherte KI‑Modelle auflisten – Kurzer Überblick

Das Erste, was Sie tun müssen, ist das SDK zu importieren und seine Hilfsfunktionen aufzurufen. Das SDK stellt zwei praktische Methoden bereit:

1. `ai.list_local()` – gibt eine Python‑Liste von Modell‑Identifikatoren zurück, die bereits im Cache liegen.
2. `ai.get_local_path()` – liefert das absolute Verzeichnis, in dem diese Modelldateien gespeichert sind.

Beide Aufrufe sind synchron und werfen bei Problemen einen klaren `AIError`, was die Fehlerbehandlung unkompliziert macht.

> **Warum diese Funktionen verwenden?**  
> Wenn Sie genau wissen, welche Modelle im Cache sind, vermeiden Sie unnötige Downloads, können Versionskonflikte debuggen und alte Artefakte automatisch bereinigen. Das ist ein kleiner Baustein im größeren **AI SDK Python**‑Workflow, kann Ihnen aber Stunden manueller Dateisystem‑Suche ersparen.

### Schritt 1: Das AI‑SDK importieren

```python
# Step 1: Import the AI SDK (replace with the actual package name if different)
import ai
```

*Warum das wichtig ist:* Durch das Importieren des Pakets werden die zugrunde liegenden C‑Erweiterungen registriert und Konfigurationsdateien (wie Cache‑Pfade) aus Ihrer Umgebung geladen. Wird dieser Schritt übersprungen, wirft bereits der erste SDK‑Aufruf einen `ModuleNotFoundError`.

### Schritt 2: Alle zwischengespeicherten Modelle auflisten

```python
# Step 2: List all models that are cached locally
cached_models = ai.list_local()
print("Cached models:", cached_models)
```

**Was Sie sehen werden:** Wenn Sie drei Modelle gespeichert haben, könnte die Ausgabe etwa so aussehen:

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
```

Ist der Cache leer, erhalten Sie eine leere Liste:

```
Cached models: []
```

> **Pro‑Tipp:** Packen Sie den Aufruf in einen `try/except`‑Block, falls das SDK nicht korrekt initialisiert ist.

```python
try:
    cached_models = ai.list_local()
except ai.AIError as e:
    print("Failed to list cached models:", e)
    cached_models = []
```

### Schritt 3: Das Model‑Cache‑Verzeichnis abrufen

```python
# Step 3: Retrieve the directory where the model files are stored
cache_dir = ai.get_local_path()
print("Model cache directory:", cache_dir)
```

Typische Ausgabe auf einem Unix‑ähnlichen System:

```
Model cache directory: /home/you/.cache/ai/models
```

Unter Windows sehen Sie möglicherweise etwas wie `C:\Users\you\AppData\Local\ai\models`. Dieses Verzeichnis zu kennen ist entscheidend, wenn Sie den **KI‑Model‑Cache** manuell verwalten möchten – etwa um alte Versionen zu entfernen oder Dateien auf ein gemeinsames Laufwerk zu kopieren.

---

## Visuelle Zusammenfassung

![Diagram showing how to list cached AI models, retrieve their names, and locate the cache directory](https://example.com/images/list-cached-ai-models.png)

*Alt‑Text:* Diagramm, das den Prozess zum **Auflisten zwischengespeicherter KI‑Modelle** mit dem AI‑SDK in Python veranschaulicht.

---

## Edge Cases und häufige Stolperfallen

### Leerer Cache

Gibt `ai.list_local()` eine leere Liste zurück, fragen Sie sich vielleicht, ob das SDK falsch konfiguriert ist. Überprüfen Sie die Umgebungsvariable `AI_CACHE_DIR` (oder die SDK‑Konfigurationsdatei), um sicherzustellen, dass sie auf ein beschreibbares Verzeichnis zeigt.

```python
if not cached_models:
    print("No models are cached. Consider downloading a model first.")
```

### Berechtigungsprobleme

Beim Zugriff auf `ai.get_local_path()` kann auf restriktiven Systemen ein `PermissionError` auftreten. Die Lösung besteht meist darin, das Skript mit den entsprechenden Benutzerrechten auszuführen oder die ACLs des Verzeichnisses anzupassen.

### Versionskonflikte

Manchmal enthält der Cache eine ältere Version eines Modells, während Ihr Code eine neuere verlangt. Das SDK lädt automatisch die neuere Version herunter, Sie können jedoch vorbeugen, indem Sie das Versions‑Tag in der Liste prüfen:

```python
for model in cached_models:
    if "v2" not in model:
        print(f"Model {model} may be outdated.")
```

### Alte Modelle bereinigen

Möchten Sie Speicher freigeben, können Sie einen bestimmten Modellordner direkt löschen:

```python
import shutil, os

def purge_model(model_name):
    path = os.path.join(cache_dir, model_name)
    if os.path.isdir(path):
        shutil.rmtree(path)
        print(f"Purged {model_name} from cache.")
    else:
        print(f"{model_name} not found in cache.")
```

Der Aufruf `purge_model('bert-base-uncased')` entfernt dieses Modell und gibt Festplattenspeicher frei.

---

## Komplettes Skript zum Kopieren‑und‑Einfügen

Unten finden Sie ein sofort ausführbares Skript, das alle Schritte kombiniert, grundlegende Fehlerbehandlung enthält und eine freundliche Zusammenfassung ausgibt.

```python
#!/usr/bin/env python3
"""
Complete example: list cached AI models and show cache directory.
"""

import ai
import os
import sys
import shutil

def main():
    try:
        # Retrieve cached model list
        cached = ai.list_local()
        print("Cached models:", cached)

        # Retrieve cache directory
        cache_dir = ai.get_local_path()
        print("Model cache directory:", cache_dir)

        # Summarize status
        if not cached:
            print("\n⚠️  No models are currently cached.")
        else:
            print("\n✅  Found {} model(s) in cache.".format(len(cached)))

        # Optional: ask user if they want to purge an old model
        if cached:
            to_purge = input("\nEnter a model name to purge (or press Enter to skip): ").strip()
            if to_purge:
                purge_path = os.path.join(cache_dir, to_purge)
                if os.path.isdir(purge_path):
                    shutil.rmtree(purge_path)
                    print(f"🗑️  Purged {to_purge} from cache.")
                else:
                    print(f"❌  Model {to_purge} not found in cache.")
    except ai.AIError as err:
        print("AI SDK error:", err, file=sys.stderr)
        sys.exit(1)
    except Exception as exc:
        print("Unexpected error:", exc, file=sys.stderr)
        sys.exit(1)

if __name__ == "__main__":
    main()
```

**Erwartete Ausgabe (wenn der Cache gefüllt ist):**

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
Model cache directory: /home/you/.cache/ai/models

✅  Found 3 model(s) in cache.

Enter a model name to purge (or press Enter to skip):
```

Führen Sie das Skript mit `python list_models.py` aus und Sie wissen sofort, was auf Ihrer Festplatte liegt.

---

## Häufig gestellte Fragen

**F: Funktioniert das auf allen Betriebssystemen?**  
A: Ja. Das SDK abstrahiert betriebssystemspezifische Pfade, sodass `ai.get_local_path()` einen gültigen String unter Linux, macOS und Windows zurückgibt.

**F: Kann ich Modelle aus einem Remote‑Cache auflisten?**  
A: Die eingebaute `list_local()` meldet nur lokal gespeicherte Artefakte. Für entfernte Registries verwenden Sie `ai.list_remote()` (sofern Ihre SDK‑Version das unterstützt).

**F: Was, wenn das SDK nicht `ai` heißt?**  
A: Ersetzen Sie die Import‑Zeile durch den tatsächlichen Paketnamen, z. B. `import myai as ai`. Alle nachfolgenden Aufrufe bleiben gleich, weil der API‑Vertrag über Implementierungen hinweg konsistent ist.

---

## Fazit

Sie verfügen jetzt über eine solide, produktionsreife Methode, um **zwischengespeicherte KI‑Modelle** mit der **AI SDK Python**‑Bibliothek aufzulisten, das **Model‑Cache‑Verzeichnis** zu ermitteln und sogar alte Dateien zu bereinigen. Dieses Wissen hilft Ihnen, Ihre Umgebung sauber zu halten, redundante Downloads zu vermeiden und Versionsprobleme mühelos zu debuggen.

Bereit für den nächsten Schritt? Versuchen Sie, das Skript zu erweitern, sodass fehlende Modelle automatisch heruntergeladen werden, oder integrieren Sie es in eine CI‑Pipeline, die den Cache‑Zustand vor jedem Build prüft. Das Erkunden von **Strategien zum Verwalten des KI‑Model‑Caches** macht Ihre KI‑gestützten Anwendungen schneller und zuverlässiger.

Viel Spaß beim Coden, und mögen Ihre Caches schlank bleiben!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren Projekten erkunden können.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}