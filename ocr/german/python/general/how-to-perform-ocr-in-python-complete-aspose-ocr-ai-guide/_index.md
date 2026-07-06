---
category: general
date: 2026-06-25
description: Erfahren Sie, wie Sie OCR in Python durchführen und entdecken Sie die
  beste Methode, ein Bild für OCR zu laden, um dann die Genauigkeit mit der Aspose
  KI‑Nachbearbeitung zu steigern.
draft: false
keywords:
- how to perform OCR
- load image for OCR
- Aspose OCR Python
- AI post‑processor OCR
- OCR accuracy improvement
- Python image processing OCR
language: de
og_description: Wie führt man OCR in Python durch? Folgen Sie diesem Leitfaden, um
  ein Bild für OCR zu laden, die Grund­erkennung auszuführen und die Ergebnisse mit
  Aspose AI‑Nachbearbeitung zu verbessern.
og_title: Wie man OCR in Python ausführt – Vollständiges Aspose OCR‑ und KI‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  headline: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  type: TechArticle
- description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  name: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  steps:
  - name: Expected Output
    text: '``` === Raw OCR === Inv0ice #12345 Date: 2023-08-15 Total: $1,23O'
  - name: What if I don’t have a GPU?
    text: Set `model_config.gpu_layers = 0` and optionally increase `model_config.context_size`
      to 2048 for better CPU performance. The model will run slower, but you still
      get the same quality of correction.
  - name: My image is rotated—will `load_image` handle it?
    text: 'Aspose OCR automatically detects orientation, but for extremely skewed
      scans you may want to pre‑rotate using Pillow:'
  - name: How do I process multiple files in a folder?
    text: Wrap the whole pipeline in a `for` loop and store each `enhanced_text` in
      a list or write directly to a CSV. Remember to call `ocr_ai.free_resources()`
      **once** after the loop, not after each file—re‑initialising the model repeatedly
      is wasteful.
  - name: Can I swap the language model?
    text: Absolutely. Just change `model_config.hugging_face_repo_id` to any GGUF‑compatible
      model on Hugging Face (e.g., `Meta/Llama-3.2-1B-Instruct-GGUF`). Keep the quantization
      setting consistent with your hardware.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: Wie man OCR in Python durchführt – Vollständiger Aspose OCR‑ und KI‑Leitfaden
url: /de/python/general/how-to-perform-ocr-in-python-complete-aspose-ocr-ai-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in Python durchführt – Vollständiger Aspose OCR‑&‑KI‑Leitfaden

Haben Sie sich jemals gefragt, **wie man OCR** in Python durchführt, ohne sich mit Low‑Level‑Bildtricks herumzuschlagen? Sie sind nicht allein. In diesem Tutorial führen wir Sie durch das Laden eines Bildes für OCR, die reine Textextraktion und das Verfeinern der Ausgabe mit Asposes KI‑Post‑Processor. Am Ende haben Sie ein einsatzbereites Skript, das verrauschte Scans in sauberen, durchsuchbaren Text verwandelt – ohne zusätzliche Dienste.

Wir decken alles ab, von der Installation des SDK bis zum Freigeben von Ressourcen in langfristig laufenden Anwendungen. Wenn Sie jemals versucht haben, **load image for OCR** zu verwenden und ein wirres Durcheinander erhalten haben, ist dieser Leitfaden das Gegenmittel. Sie werden sehen, warum die Kombination von traditionellem OCR mit einem Sprachmodell Ergebnisse liefert, die aussehen, als wären sie von einem Menschen getippt.

## Voraussetzungen

Bevor wir loslegen, stellen Sie sicher, dass Sie Folgendes haben:

- Python 3.9 oder neuer (der Code verwendet Typannotationen, die ältere Interpreter nicht mögen)
- Eine aktive Aspose OCR‑Lizenz oder eine kostenlose Testversion (die Community‑Edition funktioniert für Evaluierungen)
- Eine GPU mit mindestens 4 GB VRAM, wenn Sie das KI‑Modell beschleunigen möchten (optional, aber praktisch)
- Ein Beispielbild, z. B. `sample_invoice.png`, an einem Ort, den Sie referenzieren können

Wenn Ihnen irgendeiner dieser Punkte unbekannt ist, keine Panik – die Installation des SDK ist ein Einzeiler, und die GPU‑Einstellungen können später deaktiviert werden.

## Schritt 1: Aspose OCR und Abhängigkeiten installieren

Öffnen Sie ein Terminal und führen Sie aus:

```bash
pip install aspose-ocr
pip install aspose-ocr-ai
```

Das erste Paket liefert Ihnen `aspose.ocr`, das zweite fügt die KI‑Post‑Processor‑Hilfsmittel hinzu. Beide sind reine Python‑Wheels, sodass Sie nichts selbst kompilieren müssen.

## Schritt 2: Bild für OCR laden und die Engine initialisieren

Jetzt **load image for OCR** mit Asposes `OcrEngine`. Stellen Sie sich das vor wie das Übergeben eines Blatt Papiers an einen sehr gewissenhaften Schreiber, der jedes Zeichen liest.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Initialise the basic OCR engine
ocr_engine = aocr.OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

# Perform a plain OCR scan – this returns a raw string
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)
```

> **Warum das wichtig ist:** Der Aufruf `load_image` ist die Brücke zwischen Ihrem Dateisystem und der OCR‑Engine. Wenn der Pfad falsch ist, erhalten Sie einen `FileNotFoundError`, bevor irgendeine Erkennung überhaupt beginnt. Überprüfen Sie stets die Verzeichnis­trennzeichen, besonders unter Windows vs. macOS/Linux.

## Schritt 3: Aspose KI‑Post‑Processor einrichten

Aspose AI kann ein Sprachmodell von Hugging Face herunterladen, lokal zwischenspeichern und Inferenz auf Ihrer GPU (oder CPU) ausführen. Im Folgenden konfigurieren wir ein leichtgewichtiges 3‑Milliarden‑Parameter‑Modell, das auf den meisten modernen Laptops passt.

```python
# Initialise the AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()

# Allow the SDK to fetch the model automatically
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"

# Use half of the GPU layers – balances speed and VRAM usage
model_config.gpu_layers = 20
model_config.context_size = 1024

# Load (or download) the model now
ocr_ai.initialize(model_config)
```

> **Tipp:** Wenn Sie nur eine CPU‑Maschine haben, setzen Sie `gpu_layers = 0`. Das Modell läuft dann immer noch, nur etwas langsamer. Die `int8`‑Quantisierung hält den Speicherverbrauch klein, während sie die meisten Genauigkeiten des Modells bewahrt.

## Schritt 4: Einen benutzerdefinierten Post‑Processor registrieren

Das KI‑Modell benötigt einen Prompt, der ihm sagt, was zu tun ist. Hier bitten wir es, wie ein OCR‑Korrekturleser zu agieren, Rechtschreibfehler zu beheben, zerbrochene Wörter zu verbinden und Artefakte zu entfernen.

```python
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    # Temperature 0.0 makes the output deterministic
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

# Hook the custom processor into the AI pipeline
ocr_ai.set_post_processor(correction_processor, custom_settings=None)
```

> **Warum ein benutzerdefinierter Processor?** Der Standard‑Post‑Processor könnte zusätzliche Erklärungen oder Formatierungen hinzufügen, die Sie nicht benötigen. Indem wir unsere eigene Funktion bereitstellen, halten wir die Ausgabe strikt auf den bereinigten Text, was perfekt für nachgelagerte Indexierung oder Datenbankspeicherung ist.

## Schritt 5: Die KI‑verbesserte OCR‑Pipeline ausführen

Jetzt geben wir die rohe OCR‑Ausgabe an die KI‑Schicht weiter. Die Engine ruft unseren `correction_processor` auf, der wiederum mit dem Sprachmodell kommuniziert.

```python
# Apply the AI post‑processor to the raw OCR result
enhanced_text = ocr_ai.run_postprocessor(raw_text)

print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)
```

Sie sollten eine deutliche Verbesserung sehen: fehlende Zeichen werden wiederhergestellt, häufige OCR‑Fehlinterpretationen wie „0“ vs. „O“ werden korrigiert, und Zeilenumbrüche werden logischer.

## Schritt 6: Aufräumen – Ressourcen freigeben

Wenn Sie dies innerhalb eines Web‑Services oder eines langfristig laufenden Daemons ausführen möchten, ist das Freigeben des GPU‑Speichers entscheidend. Das Vergessen des Aufrufs `free_resources` kann nach einigen hundert Anfragen zu „out‑of‑memory“-Abstürzen führen.

```python
ocr_ai.free_resources()
```

Das war’s – Ihre komplette OCR‑Pipeline ist jetzt produktionsreif.

## Vollständige Skript‑Zusammenfassung

Unten finden Sie das vollständige, ausführbare Beispiel. Kopieren Sie es in eine Datei namens `ocr_with_ai.py`, passen Sie den Bildpfad an und führen Sie `python ocr_with_ai.py` aus.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Step 1: Load image for OCR and perform basic recognition
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)

# Step 2: Initialise the Aspose AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"
model_config.gpu_layers = 20          # half of GPU layers
model_config.context_size = 1024
ocr_ai.initialize(model_config)

# Step 3: Register custom correction processor
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

ocr_ai.set_post_processor(correction_processor, custom_settings=None)

# Step 4: Run AI post‑processor on raw OCR output
enhanced_text = ocr_ai.run_postprocessor(raw_text)
print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)

# Step 5: Release resources (important for long‑running apps)
ocr_ai.free_resources()
```

### Erwartete Ausgabe

```
=== Raw OCR ===
Inv0ice #12345
Date: 2023-08-15
Total: $1,23O

=== AI‑enhanced OCR ===
Invoice #12345
Date: 2023-08-15
Total: $1,230
```

Beachten Sie, wie „Inv0ice“ zu „Invoice“ wird und das lose „O“ nach dem Betrag verschwindet. Das ist die KI, die ihre Magie wirkt.

## Häufige Fragen & Randfälle

### Was, wenn ich keine GPU habe?

Setzen Sie `model_config.gpu_layers = 0` und erhöhen Sie optional `model_config.context_size` auf 2048 für bessere CPU‑Leistung. Das Modell läuft langsamer, aber Sie erhalten immer noch dieselbe Korrekturgüte.

### Mein Bild ist gedreht – wird `load_image` das handhaben?

Aspose OCR erkennt die Orientierung automatisch, aber bei extrem schiefen Scans möchten Sie eventuell vorher mit Pillow rotieren:

```python
from PIL import Image
img = Image.open("sample.png")
rotated = img.rotate(90, expand=True)
rotated.save("rotated.png")
ocr_engine.load_image("rotated.png")
```

### Wie verarbeite ich mehrere Dateien in einem Ordner?

Umwickeln Sie die gesamte Pipeline in eine `for`‑Schleife und speichern Sie jedes `enhanced_text` in einer Liste oder schreiben Sie direkt in eine CSV. Denken Sie daran, `ocr_ai.free_resources()` **einmal** nach der Schleife aufzurufen, nicht nach jeder Datei – das wiederholte Neu‑initialisieren des Modells ist verschwenderisch.

```python
import os

for filename in os.listdir("invoices"):
    if filename.lower().endswith(".png"):
        ocr_engine.load_image(os.path.join("invoices", filename))
        raw = ocr_engine.recognize()
        clean = ocr_ai.run_postprocessor(raw)
        # Save or index `clean`
```

### Kann ich das Sprachmodell austauschen?

Absolut. Ändern Sie einfach `model_config.hugging_face_repo_id` zu einem beliebigen GGUF‑kompatiblen Modell auf Hugging Face (z. B. `Meta/Llama-3.2-1B-Instruct-GGUF`). Halten Sie die Quantisierungseinstellung konsistent mit Ihrer Hardware.

## Pro‑Tipps & Fallstricke

- **Pro‑Tipp:** Setzen Sie `temperature=0.0` für deterministische Korrekturen. Höhere Temperaturen können kreative, aber falsche Änderungen einführen.
- **Achten Sie auf:** Extrem lange Dokumente (> 5000 Zeichen). Das Kontextfenster des Modells ist im Beispiel auf 1024 Tokens begrenzt; teilen Sie den Text vor dem Senden an die KI in Absätze auf.
- **Sicherheitshinweis:** Wenn Sie dies in einer regulierten Umgebung ausführen, stellen Sie sicher, dass die Modell‑Download‑URL auf der Whitelist steht. Das `allow_auto_download`‑Flag kann

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält komplette, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}