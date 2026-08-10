---
category: general
date: 2026-06-19
description: Erfahren Sie, wie Sie OCR auf Bildern mit Aspose OCR und KI‑Nachbearbeitung
  in Python durchführen. Enthält automatisch heruntergeladenes Modell, Rechtschreibprüfung
  und GPU‑Beschleunigung.
draft: false
keywords:
- perform OCR on image
- Aspose OCR Python
- AI post‑processor
- auto‑downloaded model
- spellcheck post‑processor
- GPU acceleration
language: de
og_description: Führen Sie OCR auf Bildern mit Aspose OCR und KI‑Nachbearbeitung durch.
  Schritt‑für‑Schritt‑Anleitung mit automatisch heruntergeladenem Modell, Rechtschreibprüfung
  und GPU‑Beschleunigung.
og_title: OCR auf Bild ausführen – Komplettes Python‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  headline: perform OCR on image with Aspose AI – Full Python Guide
  type: TechArticle
- description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  name: perform OCR on image with Aspose AI – Full Python Guide
  steps:
  - name: Initializes the Aspose OCR engine and loads a sample invoice image.
    text: Initializes the Aspose OCR engine and loads a sample invoice image.
  - name: Runs a basic OCR pass and prints the raw text.
    text: Runs a basic OCR pass and prints the raw text.
  - name: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
    text: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
  - name: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
    text: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
  - name: Releases all resources cleanly.
    text: Releases all resources cleanly.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: OCR auf Bild mit Aspose AI durchführen – Vollständiger Python‑Leitfaden
url: /de/python/general/perform-ocr-on-image-with-aspose-ai-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Bild ausführen – Vollständiges Python‑Tutorial

Haben Sie sich jemals gefragt, wie man **OCR auf Bild**‑Dateien ausführen kann, ohne sich mit Dutzenden von Bibliotheken herumzuschlagen? Meiner Erfahrung nach besteht das Hauptproblem meist darin, eine rohe OCR‑Engine zu jonglieren und dann den verrauschten Output zu bereinigen. Zum Glück macht Aspose OCR für Python in Kombination mit seinem KI‑Post‑Processor die gesamte Pipeline zum Kinderspiel.

In diesem Leitfaden führen wir Sie durch ein praktisches End‑to‑End‑Beispiel, das genau zeigt, wie man **OCR auf Bild**‑Daten ausführt, die Genauigkeit mit einem automatisch heruntergeladenen Modell steigert, Rechtschreibprüfung aktiviert und sogar die GPU‑Beschleunigung nutzt, wenn sie verfügbar ist. Sobald Sie fertig sind, haben Sie ein wiederverwendbares Skript, das Sie in jedes Rechnungs‑, Beleg‑Scanning‑ oder Dokument‑Digitalisierungs‑Projekt einbinden können.

## Was Sie erstellen werden

1. Initialisiert die Aspose OCR‑Engine und lädt ein Beispiel‑Rechnungsbild.  
2. Führt einen grundlegenden OCR‑Durchlauf aus und gibt den Rohtext aus.  
3. Konfiguriert **Aspose AI** mit einem **automatisch heruntergeladenen Modell** von Hugging Face.  
4. Führt den **KI‑Post‑Processor** aus (einschließlich eines **Rechtschreib‑Post‑Processors**), um die OCR‑Ausgabe zu bereinigen.  
5. Gibt alle Ressourcen sauber frei.

Keine externen Dienste, keine API‑Schlüssel – nur ein paar Zeilen Python und die Leistung von Aspose.

> **Pro‑Tipp:** Wenn Sie auf einem Rechner mit einer ordentlichen GPU arbeiten, kann das Setzen von `gpu_layers` Sekunden beim Post‑Processing‑Schritt einsparen.

## Voraussetzungen

- Python 3.8 oder neuer (der Code verwendet Typ‑Hints, diese sind jedoch optional).  
- `aspose-ocr` und `aspose-ai` Pakete über `pip` installiert.  
  ```bash
  pip install aspose-ocr aspose-ai
  ```  
- Ein Beispielbild (PNG, JPG oder TIFF), das Sie irgendwo referenzieren können, z. B. `sample_invoice.png`.  
- (Optional) Eine CUDA‑fähige GPU und die entsprechenden Treiber, wenn Sie **GPU‑Beschleunigung** wünschen.

Da die Grundlagen nun geschaffen sind, tauchen wir in den Code ein.

![Beispiel für OCR auf Bild](image.png)

## OCR auf Bild – Schritt 1: Initialisieren der OCR‑Engine und Laden des Bildes

Das Erste, was wir benötigen, ist eine OCR‑Engine‑Instanz. Aspose OCR bietet eine saubere, objektorientierte API, die die niedrigstufige Bildvorverarbeitung abstrahiert.

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()
ocr_engine.Language = "en"                     # English; change as needed

# Load the image you want to analyse
ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")
```

**Warum das wichtig ist:**  
Das frühe Festlegen der Sprache teilt der Engine mit, welchen Zeichensatz sie erwarten soll, was die Erkennungs‑Geschwindigkeit und -Genauigkeit verbessern kann. Wenn Sie mit mehrsprachigen Dokumenten arbeiten, wechseln Sie einfach `"en"` zu `"fr"` oder `"de"` nach Bedarf.

## Schritt 2: Grundlegendes OCR ausführen und den Rohtext anzeigen

Jetzt führen wir die Erkennung tatsächlich aus. Das Ergebnis‑Objekt enthält den Rohtext, Konfidenz‑Scores und sogar Begrenzungsrahmen, falls Sie diese später benötigen.

```python
# Run OCR
ocr_result = ocr_engine.Recognize()

# Show the unprocessed output
print("Raw OCR output:")
print(ocr_result.Text)
```

Typische Ausgabe könnte so aussehen (beachten Sie die gelegentlichen Fehlinterpretationen):

```
Raw OCR output:
Inv0ice N0: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00
```

Sie können die Nullen (`0`) sehen, wo die Engine dachte, sie habe ein „O“ gesehen. Dort glänzt der **KI‑Post‑Processor**.

## Aspose AI konfigurieren – automatisch heruntergeladenes Modell und Rechtschreibprüfung

Bevor wir das rohe OCR‑Ergebnis an die KI‑Schicht übergeben, müssen wir Aspose AI mitteilen, welches Modell verwendet werden soll. Die Bibliothek kann automatisch ein Modell von Hugging Face herunterladen, sodass Sie nicht selbst große `.bin`‑Dateien jonglieren müssen.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

# Create a model configuration that auto‑downloads the Qwen2.5‑3B‑Instruct model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"   # reduces RAM usage
model_config.gpu_layers = 20                      # use GPU if available

# Initialise the AI engine with the config
ai_engine = AsposeAI(model_config)

# Enable the built‑in spellcheck post‑processor
ai_engine.set_post_processor("spellcheck", None)
```

**Erklärung der Einstellungen**

| Einstellung | Was es bewirkt | Wann anpassen |
|-------------|----------------|----------------|
| `allow_auto_download` | Ermöglicht Aspose, das Modell beim ersten Lauf automatisch zu holen. | Behalten Sie `true`, es sei denn, Sie haben das Modell für die Offline‑Nutzung vorab heruntergeladen. |
| `hugging_face_repo_id` | Kennung des Modells auf Hugging Face. | Ersetzen Sie es durch ein anderes Modell, wenn Sie ein domänenspezifisches benötigen. |
| `hugging_face_quantization` | Wählt das Quantisierungs‑Level (`int8`, `float16`, etc.). | Verwenden Sie `int8` für Umgebungen mit wenig Speicher; `float16` für höhere Genauigkeit. |
| `gpu_layers` | Anzahl der Transformer‑Schichten, die auf der GPU ausgeführt werden. | Setzen Sie `0` für nur CPU, oder einen Wert bis zur Gesamtzahl der Schichten des Modells (20 für Qwen2.5‑3B). |

## KI‑Post‑Processor auf das OCR‑Ergebnis anwenden

Mit der bereitstehenden Engine füttern wir einfach die rohe OCR‑Ausgabe in die KI‑Pipeline. Der integrierte **Rechtschreib‑Post‑Processor** korrigiert offensichtliche Tippfehler, während das Sprachmodell umformulieren oder fehlende Informationen ergänzen kann, wenn Sie später zusätzliche Prozessoren aktivieren.

```python
# Enhance the OCR result using the AI post‑processor
enhanced_result = ai_engine.run_postprocessor(ocr_result)

# Display the cleaned‑up text
print("\nAI‑enhanced OCR output:")
print(enhanced_result.Text)
```

Erwartete Ausgabe nach dem Rechtschreib‑Schritt:

```
AI‑enhanced OCR output:
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

Beachten Sie, wie die Nullen in korrekte Buchstaben umgewandelt wurden und das falsch geschriebene „Am0unt“ zu „Amount“ wurde. Der **KI‑Post‑Processor** funktioniert, indem er den Rohtext durch das ausgewählte Modell schickt, das dann eine verfeinerte Version basierend auf seinem Training zurückgibt.

### Sonderfälle & Tipps

- **Bilder mit niedriger Auflösung**: Wenn die OCR‑Engine Schwierigkeiten hat, erwägen Sie, das Bild zuerst hochzuskalieren (`Pillow` kann helfen) oder `ocr_engine.ImagePreprocessingOptions` zu erhöhen.  
- **Nicht‑lateinische Schriften**: Ändern Sie `ocr_engine.Language` zum entsprechenden ISO‑Code (`"zh"` für Chinesisch, `"ar"` für Arabisch).  
- **GPU nicht erkannt**: Die Einstellung `gpu_layers` fällt stillschweigend auf CPU zurück, wenn keine kompatible GPU gefunden wird, sodass Sie keine zusätzliche Fehlerbehandlung benötigen.  
- **Modellgrößen‑Grenzen**: Das Qwen2.5‑3B‑Modell ist ca. 4 GB komprimiert; stellen Sie sicher, dass Ihre Festplatte genügend Platz für den automatischen Download hat.

## Ressourcen freigeben – sauberer Shutdown

Aspose‑Objekte halten native Handles, daher ist es gute Praxis, sie freizugeben, wenn Sie fertig sind. Das verhindert Speicherlecks, besonders in langlaufenden Diensten.

```python
# Free AI resources
ai_engine.free_resources()

# Dispose of the OCR engine
ocr_engine.Dispose()
```

Sie können das gesamte Skript in einen `try…finally`‑Block einbetten, wenn Sie eine explizite Aufräumung bevorzugen.

## Vollständiges Skript – zum Kopieren‑Einfügen bereit

Unten finden Sie das gesamte Programm, das bereit ist, ausgeführt zu werden, nachdem Sie `YOUR_DIRECTORY` durch den Pfad zu Ihrem Bild ersetzt haben.

```python
# -*- coding: utf-8 -*-
"""
Full example: perform OCR on image using Aspose OCR + AI post‑processor.
Author: Your Name
Date: 2026‑06‑19
"""

from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = OcrEngine()
    ocr_engine.Language = "en"
    ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Basic OCR
    ocr_result = ocr_engine.Recognize()
    print("Raw OCR output:")
    print(ocr_result.Text)

    # 3️⃣ Configure Aspose AI with auto‑downloaded model
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "int8"
    model_cfg.gpu_layers = 20   # GPU acceleration if available

    ai_engine = AsposeAI(model_cfg)
    ai_engine.set_post_processor("spellcheck", None)   # enable spellcheck

    # 4️⃣ AI post‑processing
    enhanced = ai_engine.run_postprocessor(ocr_result)
    print("\nAI‑enhanced OCR output:")
    print(enhanced.Text)

    # 5️⃣ Clean up
    ai_engine.free_resources()
    ocr_engine.Dispose()

if __name__ == "__main__":
    main()
```

Führen Sie es aus mit:

```bash
python perform_ocr_on_image.py
```

Sie sollten die rohen und bereinigten Ausgaben in der Konsole sehen.

## Conclusion


## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Text aus Bild extrahieren mit Aspose OCR – Schritt‑für‑Schritt‑Anleitung](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Bildtext in C# extrahieren mit Sprachauswahl mittels Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Bild zu Text konvertieren – OCR auf Bild von URL ausführen](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}