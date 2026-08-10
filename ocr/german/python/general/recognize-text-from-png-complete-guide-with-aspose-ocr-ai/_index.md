---
category: general
date: 2026-06-22
description: Texterkennung aus PNG-Dateien mit Aspose OCR in Python. Lerne, OCR‑Bilder
  stapelweise zu verarbeiten und setze GPU‑Schichten für schnelle Verarbeitung.
draft: false
keywords:
- recognize text from png
- batch ocr images
- set gpu layers
- Aspose OCR Python
- GPU acceleration OCR
language: de
og_description: Erkennen Sie Text aus PNG-Dateien mit Aspose OCR in Python. Dieser
  Leitfaden zeigt, wie man Bilder stapelweise OCR verarbeitet und GPU‑Schichten für
  mehr Geschwindigkeit einstellt.
og_title: Texterkennung aus PNG – Schritt‑für‑Schritt Aspose OCR‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  headline: recognize text from png – Complete Guide with Aspose OCR & AI
  type: TechArticle
- description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  name: recognize text from png – Complete Guide with Aspose OCR & AI
  steps:
  - name: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
    text: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
  - name: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
    text: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
  - name: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
    text: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
  - name: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
    text: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
  type: HowTo
tags:
- OCR
- Python
- AsposeAI
title: Text aus PNG erkennen – Komplettanleitung mit Aspose OCR & KI
url: /de/python/general/recognize-text-from-png-complete-guide-with-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Texterkennung aus PNG – Voll‑Featured Aspose OCR & AI Tutorial

Haben Sie jemals **Texte aus PNG**‑Dateien erkennen müssen, waren aber von den Einrichtungdetails verwirrt? Sie sind nicht allein. Egal, ob Sie Belege digitalisieren, Formulare scannen oder Screenshots in durchsuchbaren Text umwandeln – das Beherrschen von batch OCR images in Python kann Ihnen Stunden sparen.  

In diesem Leitfaden gehen wir Schritt für Schritt ein bereit‑zum‑Ausführen‑Beispiel durch, das nicht nur **Texte aus PNG** erkennt, sondern Ihnen auch zeigt, wie Sie **set GPU layers** für einen spürbaren Geschwindigkeitsboost einstellen. Am Ende haben Sie ein eigenständiges Skript, eine klare Erklärung jedes Schrittes und eine Handvoll praktischer Tipps, die Sie einfach kopieren‑und‑einfügen können.

## Was dieses Tutorial abdeckt

- Installation der Aspose OCR‑ und Aspose AI‑Python‑Pakete  
- Konfiguration eines KI‑Modells mit automatischem Download von Hugging Face  
- Erstellung eines kleinen Post‑Processors, der die häufigsten OCR‑Tippfehler korrigiert  
- Ausführen einer **batch OCR images**‑Schleife über einen gesamten Ordner mit PNGs  
- Nutzung der **set GPU layers**‑Option, um Ihre Grafikkarte zu nutzen  
- Sicheres Aufräumen von Ressourcen nach der Verarbeitung  

Keine externen Dienste, keine versteckte Magie – nur reiner Python‑Code, den Sie in eine `.py`‑Datei einfügen und ausführen können.

![Diagram of recognize text from png workflow](workflow.png){alt="Texterkennung aus PNG Workflow-Diagramm"}

## Voraussetzungen

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| Python 3.8+ | Aspose AI’s wheels target recent interpreters |
| Eine CUDA‑kompatible GPU (optional) | Erforderlich, wenn Sie **set GPU layers** für Beschleunigung nutzen möchten |
| Internetzugang beim ersten Lauf | Das Modell wird automatisch von Hugging Face heruntergeladen |
| `pip` installiert | Um die Aspose‑Pakete zu holen |

Wenn Sie das bereits haben, großartig – Sie können sofort loslegen. Wenn nicht, führen Sie die nachstehenden Installationsschritte aus, um die fehlenden Komponenten zu erhalten.

---

## Schritt 1: Aspose OCR‑ und Aspose AI‑Pakete installieren

Zuerst holen wir die Bibliotheken von PyPI. Der untenstehende Befehl lädt sowohl die OCR‑Engine als auch den KI‑Helper in einem Schritt herunter.

```bash
pip install aspose-ocr aspose-ai
```

*Pro‑Tipp:* Verwenden Sie eine virtuelle Umgebung (`python -m venv .venv`), damit die Pakete von Ihrer globalen Python‑Installation isoliert bleiben.

---

## Schritt 2: Aspose AI‑Instanz erstellen und konfigurieren

Die KI‑Komponente liefert der OCR‑Engine den „intelligenten“ Modus. Wir verweisen sie auf das Modell `Qwen/Qwen2.5-3B-Instruct-GGUF`, lassen es bei Bedarf automatisch herunterladen und setzen **set GPU layers** auf 30 (kann später angepasst werden).

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Initialize the AI wrapper
ai = AsposeAI()

# Build a model configuration
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",                     # Grab the model automatically
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Smaller footprint, still accurate
    directory_model_path="YOUR_DIRECTORY/ai_models", # Where the model will live
    gpu_layers=30                                   # <-- set gpu layers for GPU acceleration
)

# Apply the configuration and spin up the model
ai.initialize(model_cfg)
```

**Warum das wichtig ist:**  
- `allow_auto_download` eliminiert den manuellen Schritt, ein ~2 GB‑Modell selbst zu holen.  
- `gpu_layers=30` weist den zugrunde liegenden Transformer an, die ersten 30 Schichten auf der GPU auszuführen, was die Inferenzzeit bei einer kompatiblen GPU deutlich reduziert.  
- Die Verwendung von `int8`‑Quantisierung hält den Speicherverbrauch niedrig, ohne die Genauigkeit stark zu beeinträchtigen.

---

## Schritt 3: Einfachen Post‑Processor definieren, um OCR‑Fehler zu bereinigen

OCR ist nicht perfekt – besonders bei niedrigauflösenden PNGs. Eine schnelle Lösung besteht darin, häufig falsch gelesene Zeichen zu ersetzen. Die folgende Funktion tauscht „0“ gegen „o“ und „1“ gegen „l“, ein Muster, das wir oft bei gescannten Rechnungen sehen.

```python
def fix_common_errors(text, **_):
    """
    Post‑processor that corrects typical OCR mis‑recognitions.
    Feel free to extend this with regexes or custom dictionaries.
    """
    return text.replace("0", "o").replace("1", "l")
```

Wir werden diesen Processor im nächsten Schritt an die KI‑Instanz anhängen, sodass jedes Erkennungsergebnis automatisch durch ihn läuft.

---

## Schritt 4: Post‑Processor und OCR‑Engine verbinden

Jetzt verknüpfen wir alles: die OCR‑Engine, das KI‑Modell und den Post‑Processor.

```python
import ocr  # Aspose OCR module

# Attach the post‑processor
ai.set_post_processor(fix_common_errors, {})

# Spin up the OCR engine and bind the AI
engine = ocr.OcrEngine()
engine.set_ai(ai)
```

**Was im Hintergrund passiert:**  
Der `OcrEngine` delegiert die schwere Arbeit an das von Ihnen konfigurierte KI‑Modell. Nachdem das Modell den Rohtext zurückgibt, ruft Aspose `fix_common_errors` auf, um die Ausgabe zu säubern, bevor Sie sie sehen.

---

## Schritt 5: Batch OCR Images – Jeden PNG in einem Ordner verarbeiten

Hier kommt das Herzstück des Tutorials: eine Schleife, die ein Verzeichnis durchläuft, jede `.png`‑Datei lädt, OCR ausführt und das bereinigte Ergebnis ausgibt. Dieses Muster ist der kanonische Weg, **batch OCR images** effizient zu erledigen.

```python
from pathlib import Path

# Replace with the folder that holds your PNG files
image_folder = Path("YOUR_DIRECTORY")

# Iterate over every PNG file in the folder
for img_path in image_folder.glob("*.png"):
    # Load the image into the engine
    engine.load_image(str(img_path))

    # Perform recognition
    result = engine.recognize()

    # Output the filename and the extracted text
    print(f"[{img_path.name}] → {result.text}")
```

**Erwartete Ausgabe** (Beispiel für einen Beleg):

```
[receipt_001.png] → Total amount: $23.45
[receipt_002.png] → Item: Coffee, Price: $3.50
```

Wenn Sie Dutzende oder Hunderte von Dateien haben, verarbeitet diese Schleife sie nacheinander und verwendet dieselbe KI‑Instanz, um das wiederholte Laden des Modells zu vermeiden.

---

## Schritt 6: Aufräumen – Ressourcen freigeben und Engine entsorgen

Wenn Sie fertig sind, ist es gute Praxis, GPU‑Speicher und andere native Ressourcen freizugeben. Aspose stellt dafür explizite Methoden bereit.

```python
# Release the AI model and any GPU buffers
ai.free_resources()

# Dispose of the OCR engine to close native handles
engine.dispose()
```

Wird dieser Schritt übersprungen, können verwaiste GPU‑Speicherbereiche zurückbleiben, was beim nächsten Skriptlauf zu Out‑of‑Memory‑Fehlern führen kann.

---

## Bonus: GPU‑Layers für unterschiedliche Hardware anpassen

Der von Ihnen zuvor gesetzte `gpu_layers`‑Wert ist ein guter Kompromiss für viele moderne GPUs, aber Sie müssen ihn eventuell anpassen:

| GPU‑Speicher (GB) | Empfohlene `gpu_layers` |
|-------------------|--------------------------|
| 4 GB oder weniger | 10‑15                    |
| 6‑8 GB            | 20‑30                    |
| 12 GB+            | 35‑45 (oder höher)       |

Überschreiten Sie den GPU‑Speicher, fällt die Engine automatisch auf die CPU für die restlichen Schichten zurück, sodass Sie nicht abstürzen – nur langsamer. Experimentieren Sie gern und überwachen Sie die Auslastung mit `nvidia‑smi`.

---

## Häufige Stolperfallen & wie man sie vermeidet

1. **Modell‑Download schlägt fehl** – Stellen Sie sicher, dass Ihre Umgebung `https://huggingface.co` erreichen kann. Ein Firmen‑Proxy benötigt evtl. eine Konfiguration (`https_proxy`‑Umgebungsvariable).  
2. **GPU nicht erkannt** – Prüfen Sie, ob die `torch`‑Bibliothek (als Abhängigkeit installiert) die GPU sieht: `import torch; print(torch.cuda.is_available())`. Gibt sie `False` zurück, installieren Sie das CUDA‑kompatible PyTorch‑Wheel.  
3. **Falscher Bildpfad** – `Path.glob("*.png")` ist unter Linux case‑sensitive. Verwenden Sie `*.PNG` oder `*.png` entsprechend, oder ergänzen Sie `pathlib.Path(...).rglob("*.[pP][nN][gG]")` für mehr Sicherheit.  
4. **Post‑Processor korrigiert zu viel** – Das einfache Ersetzen kann legitime „0“-Zeichen in „o“ verwandeln. Testen Sie an einer repräsentativen Stichprobe und passen Sie die Logik bei Bedarf an.

---

## Vollständiges funktionierendes Beispiel (Copy‑Paste‑bereit)

```python
# recognize_text_from_png_batch.py
# -------------------------------------------------
# Author: Your Name
# Date:   2026‑06‑22
# -------------------------------------------------
from pathlib import Path
import ocr                      # Aspose OCR module
from aspose_ai import AsposeAI, AsposeAIModelConfig

# ----- Step 1: AI configuration -----
ai = AsposeAI()
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    directory_model_path="YOUR_DIRECTORY/ai_models",
    gpu_layers=30               # <-- set gpu layers
)
ai.initialize(model_cfg)

# ----- Step 2: Post‑processor -----
def fix_common_errors(text, **_):
    """Replace typical OCR mis‑reads."""
    return text.replace("0", "o").replace("1", "l")

ai.set_post_processor(fix_common_errors, {})

# ----- Step 3: OCR engine -----
engine = ocr.OcrEngine()
engine.set_ai(ai)

# ----- Step 4: Batch processing -----
image_folder = Path("YOUR_DIRECTORY")
for img_path in image_folder.glob("*.png"):
    engine.load_image(str(img_path))
    result = engine.recognize()
    print(f"[{img_path.name}] → {result.text}")

# ----- Step 5: Cleanup -----
ai.free_resources()
engine.dispose()
```

Führen Sie es aus mit:

```bash
python recognize_text_from_png_batch.py
```

Sie sollten für jede PNG‑Datei den Dateinamen gefolgt vom extrahierten Text sehen, exakt wie zuvor demonstriert.

---

## Fazit

Wir haben gerade einen kompletten, produktionsreifen Workflow durchlaufen, um **Texte aus PNG**‑Dateien mit Aspose OCR und Aspose AI in Python zu **recognize text from png**. Durch das Bündeln der Schritte in ein sauberes Skript können Sie mühelos **batch OCR images** durchführen, und dank der `set gpu layers`


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Wie man Batch OCR Images mit List in Aspose.OCR für .NET verwendet](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Text aus Bildern mit OCR‑Operation auf Ordnern extrahieren](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Wie man Bildtext mit Sprache mittels Aspose.OCR OCR‑t](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}