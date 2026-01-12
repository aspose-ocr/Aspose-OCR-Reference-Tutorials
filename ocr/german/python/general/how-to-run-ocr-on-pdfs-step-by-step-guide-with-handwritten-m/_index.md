---
category: general
date: 2026-01-12
description: Wie man OCR auf PDFs mit Aspose OCR ausführt, PDF‑OCR lädt, den handschriftlichen
  OCR‑Modus aktiviert und ein Hugging Face OCR‑Modell für die Nachbearbeitung integriert.
draft: false
keywords:
- how to run OCR
- load pdf OCR
- handwritten OCR mode
- hugging face OCR model
language: de
og_description: Wie man OCR auf PDFs mit Aspose OCR ausführt, den handschriftlichen
  OCR‑Modus aktiviert und die Genauigkeit mit einem Hugging‑Face‑OCR‑Modell steigert.
og_title: Wie man OCR auf PDFs ausführt – Komplettanleitung
tags:
- OCR
- Python
- Aspose
- Hugging Face
title: Wie man OCR auf PDFs ausführt – Schritt‑für‑Schritt‑Leitfaden mit Handschrifterkennung
url: /de/python/general/how-to-run-ocr-on-pdfs-step-by-step-guide-with-handwritten-m/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR auf PDFs ausführt – Vollständiges Tutorial

Haben Sie sich jemals gefragt, **wie man OCR** auf einem mehrsprachigen PDF mit unordentlicher Handschrift ausführt? Sie sind nicht allein. In vielen realen Projekten – denken Sie an die Digitalisierung von Rechnungen oder die Archivierung historischer Briefe – reicht die reine Textextraktion nicht aus. Dieser Leitfaden zeigt Ihnen genau, wie man OCR auf PDFs ausführt, PDF OCR lädt, in den **handwritten OCR mode** wechselt und dann die Ergebnisse mit einem **Hugging Face OCR‑Modell** für Rechtschreib‑ und Grammatik‑Korrekturen verfeinert.

Wir gehen alles durch, was Sie benötigen: von der Installation des Aspose OCR Cloud SDK über die Konfiguration der GPU‑Beschleunigung bis hin zum Einbinden eines leichten Qwen‑Modells von Hugging Face. Am Ende haben Sie ein einsatzbereites Skript, das Sie in jedes Python‑Projekt einbinden können.

> **Voraussetzungen**  
> • Python 3.9 oder neuer  
> • Eine Aspose OCR Cloud‑Lizenz (als Umgebungsvariable gesetzt)  
> • Optional: eine CUDA‑kompatible GPU für schnellere Inferenz  

---

## Was dieses Tutorial abdeckt

- Aktivieren der Aspose OCR‑Lizenz aus der Umgebung  
- Laden eines PDFs mit `load_pdf OCR` und Aktivieren des **handwritten OCR mode**  
- Ausführen von strukturiertem OCR, um Block‑Level‑Text und Sprachdaten zu erhalten  
- Einrichten eines **Hugging Face OCR‑Modells** (Qwen 2.5‑3B‑Instruct) für die Nachverarbeitung  
- Anwenden von Rechtschreib‑ und Gramm‑Korrekturen Block für Block  
- Bereinigen von KI‑Ressourcen, um Speicherlecks zu vermeiden  

Wenn Sie jemals eine Standard‑OCR‑Engine ausprobiert haben und bei handschriftlichen Notizen Kauderwelsch erhalten haben, ist das Flag **handwritten OCR mode** der Wendepunkt, den Sie vermisst haben. Und dank des Hugging Face‑Modells erhalten Sie zudem eine professionelle Verfeinerung, ohne Ihre Python‑Umgebung zu verlassen.

![Diagramm zum OCR‑Ablauf](https://example.com/ocr-workflow.png "wie man OCR ausführt")

*Image alt text: Diagramm zum OCR‑Ablauf*

---

## Schritt 1: Erforderliche Pakete installieren

Stellen Sie zunächst sicher, dass das Aspose OCR Cloud SDK und die Bibliothek `transformers` installiert sind. Führen Sie das Folgende in Ihrem Terminal aus:

```bash
pip install aspose-ocr-cloud transformers huggingface-hub
```

> **Pro‑Tipp:** Wenn Sie GPU‑Beschleunigung nutzen möchten, installieren Sie zusätzlich `torch` mit CUDA‑Support (`pip install torch==2.2.0+cu121 -f https://download.pytorch.org/whl/torch_stable.html`).

---

## Schritt 2: Aktivieren der Aspose OCR‑Lizenz

Das Aktivieren der Lizenz aus einer Umgebungsvariable hält Ihren Schlüssel außerhalb der Quellcode‑Kontrolle. Setzen Sie `ASPOSE_OCR_LICENSE` in Ihrer Shell und rufen Sie dann `activate_from_env()` auf:

```python
import asposeocrcloud as ocr

# Pull the license string from the ASPOSE_OCR_LICENSE environment variable
ocr.activate_from_env()
```

> Warum das wichtig ist: Ohne eine gültige Lizenz fällt das SDK in einen Testmodus, der die Seitenzahl begrenzt und die GPU‑Nutzung deaktiviert.

---

## Schritt 3: Initialisieren der OCR‑Engine im Handwritten‑Modus

Wir erstellen ein `OcrEngine`, aktivieren die GPU (falls verfügbar) und fordern explizit den **handwritten OCR mode** an. Dieser Modus passt das zugrunde liegende neuronale Netzwerk an, um besser mit kursiven Strichen umzugehen.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Enable GPU acceleration – optional but speeds up large PDFs dramatically
ocr_engine.set_use_gpu(True)

# Switch to handwritten recognition mode for better accuracy on cursive text
ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)
```

> **Hinweis:** Wenn Sie keine GPU haben, funktioniert `set_use_gpu(False)` weiterhin; die Engine fällt auf die CPU zurück.

---

## Schritt 4: PDF laden und strukturiertes OCR ausführen

Jetzt laden wir tatsächlich **PDF OCR**. Die Methode `load_image` akzeptiert PDF, TIFF, JPG usw. Strukturiertes OCR liefert Blöcke, die sowohl den Rohtext als auch die erkannte Sprache enthalten.

```python
# Replace the path with your own PDF location
pdf_path = "YOUR_DIRECTORY/multilingual_handwritten.pdf"
ocr_engine.load_image(pdf_path)

# Perform structured OCR – returns a hierarchy of blocks
structured_result = ocr_engine.recognize_structured()
```

Die Liste `structured_result.blocks` könnte etwa so aussehen (gekürzt zur Übersicht):

```python
[
    Block(text="Bonjour le monde", language="fr"),
    Block(text="Hello world", language="en"),
    Block(text="こんにちは世界", language="ja")
]
```

---

## Schritt 5: Konfigurieren eines Hugging Face OCR‑Modells für die Nachverarbeitung

Wir verwenden das **Qwen 2.5‑3B‑Instruct**‑Modell von Hugging Face, quantisiert zu `int8` für einen kleinen Speicherbedarf. Der Wrapper `AsposeAIModelConfig` dem Aspose‑AI‑Post‑Processor mit, wie das Modell heruntergeladen und ausgeführt wird.

```python
from asposeocrcloud import AsposeAI, AsposeAIModelConfig

model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25,                # Number of transformer layers to keep on GPU
    allow_auto_download="true"   # Auto‑download the model if not cached
)

spell_corrector = AsposeAI()
spell_corrector.set_post_processor("spell_corrector", model_cfg)
```

> **Warum dieses Modell?** Qwen 2.5‑3B‑Instruct bietet ein gutes Gleichgewicht zwischen Geschwindigkeit und Qualität. Die `int8`‑Quantisierung reduziert den RAM‑Verbrauch auf ca. 4 GB, sodass es auf den meisten modernen Laptops machbar ist.

---

## Schritt 6: Rechtschreibprüfung Block für Block anwenden

Wir iterieren über jeden OCR‑Block, übergeben ihn dem KI‑Post‑Processor und geben den korrigierten Text zusammen mit der erkannten Sprache aus. Das ist das Kernstück der **load PDF OCR → post‑process**‑Pipeline.

```python
for block in structured_result.blocks:
    # Run the correction; `run_postprocessor` returns an object with a .text attribute
    corrected = spell_corrector.run_postprocessor(block)
    print(f"[{block.language}] {corrected.text}")
```

### Erwartete Ausgabe

```
[fr] Bonjour le monde
[en] Hello world
[ja] こんにちは世界
```

Wenn das ursprüngliche OCR Rechtschreibfehler wie „Helllo wrold“ enthielt, würde das Modell die korrigierte Version ausgeben.

---

## Schritt 7: KI‑Ressourcen bereinigen

Löschen Sie immer den GPU‑Speicher, wenn Sie fertig sind. Der Aufruf `free_resources()` entlädt das Modell und leert den CUDA‑Cache.

```python
spell_corrector.free_resources()
```

---

## Häufige Fallstricke & wie man sie vermeidet

| Problem | Symptom | Lösung |
|---------|----------|--------|
| **GPU nicht erkannt** | `set_use_gpu(True)` fällt stillschweigend auf CPU zurück | CUDA‑Treiber prüfen (`nvidia-smi`) und das korrekte `torch`‑Wheel installieren |
| **Modell‑Download schlägt fehl** | `allow_auto_download` wirft einen Netzwerkfehler | Stellen Sie sicher, dass ausgehendes HTTPS erlaubt ist, oder laden Sie die GGUF‑Datei manuell herunter und setzen `hugging_face_repo_id` auf den lokalen Pfad |
| **Handschriftlicher Text immer noch unleserlich** | Niedrige Vertrauenswerte in `structured_result` | Erhöhen Sie `set_recognition_mode` auf `HANDWRITTEN` (bereits geschehen) und erwägen Sie eine Vorverarbeitung des PDFs mit Bildschärfung (`opencv`) vor dem OCR |
| **Speicher‑Ausnahme auf GPU** | `RuntimeError: CUDA out of memory` | Reduzieren Sie `gpu_layers` (z. B. auf 10) oder wechseln Sie zur CPU‑Inference (`set_use_gpu(False)`) |

---

## Erweiterung des Workflows

- **Batch‑Verarbeitung:** Verpacken Sie das gesamte Skript in eine Funktion, die eine Liste von PDF‑Pfaden akzeptiert und die korrigierten Ausgaben in separate `.txt`‑Dateien schreibt.  
- **Benutzerdefinierte Vokabulare:** Wenn Ihr Fachgebiet spezialisierte Terminologie verwendet (z. B. medizinische Abkürzungen), feintunen Sie das Hugging Face‑Modell mit einem kleinen Datensatz.  
- **Alternative Modelle:** Ersetzen Sie `Qwen/Qwen2.5-3B-Instruct-GGUF` durch `mistralai/Mistral-7B-Instruct-v0.2`, wenn Sie ein größeres Kontextfenster benötigen.

---

## Fazit

Sie wissen jetzt **wie man OCR** auf PDFs ausführt, PDF OCR lädt, den **handwritten OCR mode** aktiviert und die Genauigkeit mit einem **Hugging Face OCR‑Modell** steigert. Das komplette Skript – Lizenzaktivierung, GPU‑aktivierte Engine, strukturiertes OCR, KI‑Nachverarbeitung und Aufräumen – deckt jeden Schritt ab, den ein Entwickler typischerweise fragt, von „Was, wenn ich keine GPU habe?“ bis „Wie gebe ich Ressourcen frei?“.  

Probieren Sie es mit Ihren eigenen Dokumenten aus, experimentieren Sie mit verschiedenen Modellen oder integrieren Sie die Pipeline in einen größeren Dokumenten‑Verarbeitungs‑Service. Sobald Sie diese Kombination aus Aspose OCR und Hugging Face KI gemeistert haben, sind Ihrer Kreativität keine Grenzen gesetzt.

**Nächste Schritte**

- Probieren Sie denselben Workflow mit gescannten Bildern (`.png`, `.jpg`) aus, um zu sehen, wie die Engine reagiert.  
- Erkunden Sie die Aspose OCR **layout analysis**‑Funktionen für die Tabellenerkennung.  
- Vertiefen Sie sich in Hugging Face‑Quantisierungstechniken, um die Modellgröße noch weiter zu reduzieren.

Viel Spaß beim OCR‑Hacken!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}