---
category: general
date: 2026-11-20
description: Führen Sie OCR auf einem Bild mit Aspose OCR durch und extrahieren Sie
  anschließend den Text aus dem Bild mithilfe des integrierten KI‑Nachbearbeiters.
  Lernen Sie in wenigen Minuten einen vollständigen Python‑Workflow kennen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from image
language: de
lastmod: 2026-11-20
og_description: Führen Sie OCR auf dem Bild mit Aspose OCR durch und extrahieren Sie
  anschließend den Text aus dem Bild mittels KI‑Nachbearbeitung. Folgen Sie dieser
  Schritt‑für‑Schritt‑Python‑Anleitung.
og_image_alt: Diagram showing how to perform OCR on image and extract text from image
  using Aspose
og_title: Führen Sie OCR auf dem Bild aus und extrahieren Sie Text aus dem Bild mit
  Aspose
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Perform OCR on image with Aspose OCR and then extract text from image
    using the built‑in AI post‑processor. Learn a complete Python workflow in minutes.
  headline: Perform OCR on image and extract text from image with Aspose
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI post‑processing
title: OCR auf Bild ausführen und Text aus Bild mit Aspose extrahieren
url: /de/python/general/perform-ocr-on-image-and-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Bild ausführen und Text aus Bild extrahieren mit Aspose

Wenn Sie **perform OCR on image** Dateien in Python benötigen, zeigt Ihnen diese Anleitung eine vollständige End‑to‑End‑Lösung. Durch die Verwendung von Aspose OCR zusammen mit dem Aspose AI‑Post‑Processor können Sie zuverlässig **extract text from image** Dateien extrahieren und das rohe OCR‑Ergebnis mit einem leichten Sprachmodell verbessern.

In diesem Tutorial werden Sie:

* Die Aspose OCR‑Engine einrichten.
* OCR ausführen, um **extract text from image** zu erhalten.
* Optional ein KI‑Modell für die Nachbearbeitung konfigurieren.
* Eine benutzerdefinierte Post‑Processor‑Funktion registrieren.
* Verbesserten Text erzeugen und Ressourcen bereinigen.

Die Schritte funktionieren mit jedem Rasterbild (PNG, JPEG, BMP) und benötigen nur das `aspose-ocr`‑Paket.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

| Anforderung | Warum es wichtig ist |
|-------------|------------------------|
| Python 3.8+ | Erforderlich für das Aspose SDK. |
| `aspose-ocr` pip package | Stellt `AsposeOCR`, `AsposeAI` und Modell‑Konfigurationsklassen bereit. |
| An image file (e.g., `sample_image.png`) | Die Quelle, die Sie **perform OCR on image**. |
| Optional: GPU support | Wenn Sie ein größeres Modell auf einer GPU ausführen möchten, setzen Sie `gpu_layers` entsprechend. |

Installieren Sie das SDK mit:

```bash
pip install aspose-ocr
```

## Schritt 1: OCR auf Bild ausführen

Der erste Vorgang besteht darin, das Bild zu lesen und Rohtext zu erhalten. Dies ist der zentrale **perform OCR on image** Schritt.

```python
from aspose.ocr import AsposeOCR

# Initialise the OCR engine
ocr_engine = AsposeOCR()

# Path to the image you want to process
image_path = "YOUR_DIRECTORY/sample_image.png"

# Execute OCR – this returns the plain text extracted from the image
raw_text = ocr_engine.recognize_image(image_path)

print("Raw OCR result:")
print(raw_text)
```

**Warum das funktioniert:** `AsposeOCR.recognize_image` führt ein vortrainiertes optisches Zeichenerkennungs‑Modell aus, das für Geschwindigkeit und Genauigkeit bei gängigen Schriftarten optimiert ist. Die Methode gibt einen einfachen Unicode‑String zurück, der die Grundlage für jede weitere Verarbeitung bildet.

> **Pro Tipp:** Wenn das Bild mehrere Sprachen enthält, setzen Sie `ocr_engine.language = "eng+spa"` (oder einen anderen unterstützten ISO‑639‑2‑Code), bevor Sie `recognize_image` aufrufen.

## Schritt 2: AI‑Post‑Processor initialisieren

Aspose AI stellt eine leichte Nachbearbeitungsschicht bereit, die OCR‑Fehler bereinigen, Interpunktion korrigieren oder benutzerdefinierte Geschäftslogik anwenden kann.

```python
from aspose.ocr import AsposeAI

# Initialise the AI post‑processor with default logging
ai_processor = AsposeAI()
```

**Warum Sie es benötigen:** Roh‑OCR erkennt häufig Zeichen falsch (z. B. „0“ vs „O“). Der KI‑Schritt verfeinert das Ergebnis und macht das **extract text from image** Ergebnis zuverlässiger für nachgelagerte Aufgaben wie Indexierung oder Analytik.

## Schritt 3: (Optional) KI‑Modell konfigurieren

Sie können den Prozessor auf ein bestimmtes Hugging Face‑Modell verweisen, automatische Downloads aktivieren oder die CPU‑Ausführung erzwingen. Dieser Schritt ist optional, aber nützlich, wenn Sie deterministisches Verhalten wünschen.

```python
from aspose.ocr import AsposeAIModelConfig

# Create a configuration object
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"          # Download model if missing
model_config.hugging_face_repo_id = "openai/gpt2"   # Small, fast model
model_config.gpu_layers = 0                        # Use CPU; set >0 for GPU

# Apply the configuration to the AI processor
ai_processor.configure(model_config)
```

**Erklärung:**  
* `allow_auto_download` erspart Ihnen die manuelle Modellverwaltung.  
* `hugging_face_repo_id` wählt ein Modell aus; `gpt2` ist ein guter Kompromiss zwischen Größe und Qualität für die Korrektur kurzer Texte.  
* `gpu_layers` steuert, wie viele Transformer‑Layer auf der GPU laufen; `0` erzwingt reine CPU‑Ausführung, was auf allen Maschinen sicher ist.

## Schritt 4: Benutzerdefinierte Nachbearbeitungsfunktion registrieren

Aspose AI ermöglicht das Einbinden einer beliebigen aufrufbaren Funktion, die den Roh‑OCR‑String erhält und eine transformierte Version zurückgibt. Unten ist ein einfaches Beispiel, das alles in Großbuchstaben umwandelt.

```python
def my_post_processor(text):
    """
    Custom post‑processor that transforms the OCR result.
    Replace this logic with your own business rules.
    """
    return text.upper()

# Register the function with the AI processor
ai_processor.set_post_processor(my_post_processor, custom_settings=None)
```

**Wann anpassen:** Verwenden Sie eine benutzerdefinierte Funktion, wenn Sie domänenspezifische Bereinigungen benötigen, z. B. das Entfernen vertraulicher Kennungen, das Normalisieren von Daten oder das Anwenden von regex‑basierten Korrekturen. Das KI‑Modell wird *nach* dieser Funktion ausgeführt, sodass Sie deterministische Regeln mit probabilistischen Verbesserungen kombinieren können.

## Schritt 5: OCR‑Ergebnis mit dem AI‑Post‑Processor verbessern

Jetzt führen Sie die komplette Pipeline aus: Der Roh‑OCR‑Text wird zuerst durch Ihre benutzerdefinierte Funktion geleitet, dann durch das KI‑Modell, und schließlich erhalten Sie das verfeinerte Ergebnis.

```python
# Run the AI post‑processor on the raw OCR text
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("\nOriginal OCR :")
print(raw_text)
print("\nAI‑enhanced   :")
print(enhanced_text)
```

**Was Sie sehen sollten:**  
Wenn das ursprüngliche Bild „Hello world“ enthielt, könnte die Konsole Folgendes anzeigen:

```
Original OCR :
Hello world

AI‑enhanced   :
HELLO WORLD
```

In einem realen Szenario würde das KI‑Modell Rechtschreibfehler korrigieren, fehlende Interpunktion hinzufügen oder Zeilenumbrüche neu formatieren, sodass Sie ein saubereres **extract text from image** Ergebnis erhalten, das bereit für Speicherung oder Analyse ist.

## Schritt 6: Ressourcen nach Abschluss freigeben

Sowohl die OCR‑Engine als auch der AI‑Post‑Processor reservieren native Ressourcen. Durch explizites Freigeben dieser Ressourcen werden Speicherlecks vermieden, insbesondere in langfristig laufenden Diensten.

```python
# Clean up native resources
ai_processor.free_resources()
```

Wenn Sie `ocr_engine` ebenfalls mit einem schweren Backend instanziiert haben, könnten Sie `ocr_engine.dispose()` (falls verfügbar) auf dieselbe Weise aufrufen.

## Häufige Variationen und Randfälle

| Situation | Empfohlene Anpassung |
|-----------|------------------------|
| **Large PDFs with many pages** | Durchlaufen Sie jede Seite, rufen Sie `recognize_image` für jede gerasterte Seite auf und fassen Sie die Ergebnisse zusammen. |
| **GPU‑enabled environment** | Setzen Sie `model_config.gpu_layers` auf die Anzahl der Layer, die Sie auf der GPU haben möchten (z. B. `4`). Stellen Sie sicher, dass CUDA‑Treiber installiert sind. |
| **Non‑English text** | Ändern Sie `ocr_engine.language` auf den entsprechenden Sprachcode und wählen Sie ggf. ein sprachspezifisches Hugging Face‑Modell aus. |
| **Very noisy scans** | Verarbeiten Sie das Bild vor dem Aufruf von `recognize_image` mit OpenCV (Rauschen entfernen, Schwellenwert setzen). |
| **Need to keep original casing** | Ersetzen Sie die `my_post_processor`‑Funktion durch einen No‑Op oder eine differenziertere Regel anstelle von `text.upper()`. |

## Vollständiges funktionierendes Beispiel

Wenn Sie alles zusammenführen, finden Sie hier ein einzelnes Skript, das Sie unverändert ausführen können (ersetzen Sie `YOUR_DIRECTORY/sample_image.png` durch Ihren tatsächlichen Dateipfad):

```python
from aspose.ocr import AsposeOCR, AsposeAI, AsposeAIModelConfig

# 1️⃣ Perform OCR on image
ocr_engine = AsposeOCR()
image_path = "YOUR_DIRECTORY/sample_image.png"
raw_text = ocr_engine.recognize_image(image_path)

# 2️⃣ Initialise the AI post‑processor
ai_processor = AsposeAI()

# 3️⃣ (Optional) Configure the AI model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "openai/gpt2"
model_config.gpu_layers = 0            # CPU execution
ai_processor.configure(model_config)

# 4️⃣ Register a custom post‑processor (example: uppercase)
def my_post_processor(text):
    return text.upper()

ai_processor.set_post_processor(my_post_processor, custom_settings=None)

# 5️⃣ Enhance the OCR result
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("Original OCR :", raw_text)
print("AI‑enhanced   :", enhanced_text)

# 6️⃣ Release resources
ai_processor.free_resources()
```

Das Ausführen dieses Skripts gibt sowohl die Roh‑OCR‑Ausgabe als auch die KI‑verbesserte Version aus und zeigt, wie Sie **perform OCR on image** Dateien zuverlässig **extract text from image** in einem einzigen, reproduzierbaren Workflow verarbeiten können.

## Fazit

Sie wissen jetzt, wie Sie **perform OCR on image** Dateien mit Aspose OCR durchführen und anschließend **extract text from image** mithilfe des integrierten AI‑Post‑Processors extrahieren. Das Tutorial behandelte:

* Initialisierung der OCR‑Engine.
* Ausführen von OCR, um Rohtext zu erhalten.
* (Optional) Konfiguration eines leichten Hugging Face‑Modells.
* Hinzufügen einer

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Extract Text Image with Aspose OCR & AI – Full Step‑by‑Step Guide](/ocr/english/python/general/extract-text-image-with-aspose-ocr-ai-full-step-by-step-guid/)
- [How to Correct OCR Errors – Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image Python – Complete Aspose OCR Guide](/ocr/english/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}