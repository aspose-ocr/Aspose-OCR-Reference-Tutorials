---
category: general
date: 2026-03-28
description: Erfahren Sie, wie Sie OCR auf Bildern ausführen, das Hugging Face‑Modell
  automatisch herunterladen, OCR‑Text bereinigen und ein LLM‑Modell in Python mit
  Aspose OCR Cloud konfigurieren.
draft: false
keywords:
- run OCR on image
- download hugging face model
- clean OCR text
- configure LLM model
language: de
og_description: Führen Sie OCR auf einem Bild aus und bereinigen Sie die Ausgabe mithilfe
  eines automatisch heruntergeladenen Hugging Face‑Modells. Dieser Leitfaden zeigt,
  wie man ein LLM‑Modell in Python konfiguriert.
og_title: OCR auf Bild ausführen – Vollständiges Aspose OCR‑Cloud‑Tutorial
tags:
- OCR
- Python
- LLM
- HuggingFace
title: OCR auf Bild mit Aspose OCR Cloud ausführen – Vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/python/general/run-ocr-on-image-with-aspose-ocr-cloud-full-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Bild ausführen – Komplettes Aspose OCR Cloud Tutorial

Haben Sie jemals OCR auf Bilddateien ausführen müssen, aber die Rohausgabe sah wie ein wirres Durcheinander aus? Meiner Erfahrung nach ist der größte Schmerzpunkt nicht die Erkennung selbst – sondern die Bereinigung. Glücklicherweise ermöglicht Aspose OCR Cloud das Anhängen eines LLM‑Post‑Processors, der *OCR‑Text* automatisch säubert. In diesem Tutorial führen wir Sie durch alles, was Sie benötigen: vom **Herunterladen eines Hugging Face‑Modells** über die Konfiguration des LLMs, das Ausführen der OCR‑Engine bis hin zur abschließenden Verfeinerung des Ergebnisses.

Am Ende dieses Leitfadens haben Sie ein einsatzbereites Skript, das:

1. Ein kompaktes Qwen 2.5‑Modell von Hugging Face abruft (automatisch für Sie heruntergeladen).  
2. Das Modell so konfiguriert, dass ein Teil des Netzwerks auf der GPU und der Rest auf der CPU läuft.  
3. Die OCR‑Engine auf einem Bild einer handschriftlichen Notiz ausführt.  
4. Das LLM verwendet, um den erkannten Text zu bereinigen und Ihnen menschenlesbare Ausgabe zu liefern.

> **Voraussetzungen** – Python 3.8+, `asposeocrcloud`‑Paket, eine GPU mit mindestens 4 GB VRAM (optional aber empfohlen) und eine Internetverbindung für den ersten Modell‑Download.

## Was Sie benötigen

- **Aspose OCR Cloud SDK** – Installation über `pip install asposeocrcloud`.  
- **Ein Beispielbild** – z. B. `handwritten_note.jpg` in einem lokalen Ordner.  
- **GPU‑Unterstützung** – Wenn Sie eine CUDA‑fähige GPU haben, lagert das Skript 30 Schichten aus; andernfalls fällt es automatisch auf die CPU zurück.  
- **Schreibberechtigung** – Das Skript cached das Modell in `YOUR_DIRECTORY`; stellen Sie sicher, dass der Ordner existiert.

## Schritt 1 – LLM‑Modell konfigurieren (Hugging Face‑Modell herunterladen)

Zuerst teilen wir Aspose AI mit, wo das Modell abgerufen werden soll. Die Klasse `AsposeAIModelConfig` übernimmt den Auto‑Download, die Quantisierung und die Zuweisung von GPU‑Schichten.

```python
import asposeocrcloud as ocr
from asposeocrcloud.ai import AsposeAI, AsposeAIModelConfig

# ----------------------------------------------------------------------
# Step 1: Model configuration – this will download the model if it’s missing
# ----------------------------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                           # Enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF", # Repo on Hugging Face
    hugging_face_quantization="int8",                     # Small footprint, fast inference
    gpu_layers=30,                                        # 30 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY"               # Cache folder (optional)
)
```

**Warum das wichtig ist** – Die Quantisierung auf `int8` reduziert den Speicherverbrauch drastisch (≈ 4 GB gegenüber 12 GB). Das Aufteilen des Modells zwischen GPU und CPU ermöglicht das Ausführen eines 3‑Milliarden‑Parameter‑LLM selbst auf einer bescheidenen RTX 3060. Wenn Sie keine GPU haben, setzen Sie `gpu_layers=0` und das SDK hält alles auf der CPU.

> **Tipp:** Der erste Durchlauf lädt ~ 1,5 GB herunter, geben Sie also ein paar Minuten und eine stabile Verbindung.

## Schritt 2 – AI‑Engine mit der Modellkonfiguration initialisieren

Jetzt starten wir die Aspose AI‑Engine und übergeben ihr die gerade erstellte Konfiguration.

```python
# ----------------------------------------------------------------------
# Step 2: Initialise the AI engine – pulls the model if needed
# ----------------------------------------------------------------------
ocr_ai = AsposeAI()
ocr_ai.initialize(model_config)  # This call blocks until the model is ready
```

**Was im Hintergrund passiert** – Das SDK prüft `directory_model_path` auf ein vorhandenes Modell. Wenn es eine passende Version findet, wird sie sofort geladen; andernfalls wird die GGUF‑Datei von Hugging Face heruntergeladen, entpackt und die Inferenz‑Pipeline vorbereitet.

## Schritt 3 – OCR‑Engine erstellen und den AI‑Post‑Processor anhängen

Die OCR‑Engine übernimmt das schwere Heben beim Erkennen von Zeichen. Durch das Anhängen von `ocr_ai.run_postprocessor` aktivieren wir **sauberen OCR‑Text** automatisch nach der Erkennung.

```python
# ----------------------------------------------------------------------
# Step 3: Build the OCR engine and bind the LLM post‑processor
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=None)
```

**Warum einen Post‑Processor verwenden?** Roh‑OCR enthält oft Zeilenumbrüche an falschen Stellen, falsch erkannte Interpunktion oder fremde Symbole. Das LLM kann die Ausgabe in korrekte Sätze umschreiben, Rechtschreibung korrigieren und sogar fehlende Wörter ableiten – im Wesentlichen wird ein Rohdump in polierten Prosa verwandelt.

## Schritt 4 – OCR auf einer Bilddatei ausführen

Nachdem alles verbunden ist, ist es Zeit, ein Bild an die Engine zu übergeben.

```python
# ----------------------------------------------------------------------
# Step 4: Load the image and run OCR
# ----------------------------------------------------------------------
input_image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
raw_result = ocr_engine.recognize(input_image)   # Returns an OcrResult object
```

**Randfall:** Wenn das Bild groß ist (> 5 MP), möchten Sie es möglicherweise zuerst verkleinern, um die Verarbeitung zu beschleunigen. Das SDK akzeptiert ein Pillow‑`Image`‑Objekt, sodass Sie bei Bedarf mit `PIL.Image.thumbnail()` vorverarbeiten können.

## Schritt 5 – Die KI den erkannten Text bereinigen lassen und beide Versionen anzeigen

Zum Schluss rufen wir den zuvor angehängten Post‑Processor auf. Dieser Schritt zeigt den Unterschied zwischen *vor* und *nach* der Bereinigung.

```python
# ----------------------------------------------------------------------
# Step 5: Clean the OCR output using the LLM and display both results
# ----------------------------------------------------------------------
cleaned_result = ocr_engine.run_postprocessor(raw_result)

print("=== Before AI ===")
print(raw_result.text)

print("\n=== After AI ===")
print(cleaned_result.text)
```

### Erwartete Ausgabe

```
=== Before AI ===
Th1s 1s a h@ndwr1tt3n n0te.  It c0nta1ns m1st@k3s, l1n3 br3aks, & sp3c!@l ch@r@ct3rs.

=== After AI ===
This is a handwritten note. It contains mistakes, line breaks, and special characters.
```

Beachten Sie, wie das LLM:

- Häufige OCR‑Fehler korrigiert hat (`Th1s` → `This`).  
- Fremde Symbole entfernt hat (`&` → `and`).  
- Zeilenumbrüche in korrekte Sätze normalisiert hat.

## 🎨 Visueller Überblick (OCR‑Workflow auf Bild ausführen)

![Run OCR on image workflow](run_ocr_on_image_workflow.png "Diagram showing the run OCR on image pipeline from model download to cleaned output")

Das obige Diagramm fasst die gesamte Pipeline zusammen: **Hugging Face‑Modell herunterladen → LLM konfigurieren → AI initialisieren → OCR‑Engine → AI‑Post‑Processor → OCR‑Text bereinigen**.

## Häufige Fragen & Pro‑Tipps

### Was, wenn ich keine GPU habe?

Setzen Sie `gpu_layers=0` in `AsposeAIModelConfig`. Das Modell läuft dann vollständig auf der CPU, was langsamer, aber dennoch funktionsfähig ist. Sie können auch zu einem kleineren Modell wechseln (z. B. `Qwen/Qwen2.5-1.5B‑Instruct‑GGUF`), um die Inferenzzeit angemessen zu halten.

### Wie ändere ich später das Modell?

Aktualisieren Sie einfach `hugging_face_repo_id` und führen Sie `ocr_ai.initialize(model_config)` erneut aus. Das SDK erkennt die Versionsänderung, lädt das neue Modell herunter und ersetzt die zwischengespeicherten Dateien.

### Kann ich den Prompt des Post‑Processors anpassen?

Ja. Übergeben Sie ein Dictionary an `custom_settings` mit einem Schlüssel `prompt_template`. Zum Beispiel:

```python
custom_prompt = {
    "prompt_template": "Correct the following OCR text and keep line breaks:\n{ocr_text}"
}
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=custom_prompt)
```

### Sollte ich den bereinigten Text in einer Datei speichern?

Definitiv. Nach der Bereinigung können Sie das Ergebnis in einer `.txt`‑ oder `.json`‑Datei für die Weiterverarbeitung schreiben:

```python
with open("cleaned_note.txt", "w", encoding="utf-8") as f:
    f.write(cleaned_result.text)
```

## Fazit

Wir haben Ihnen gerade gezeigt, wie Sie **OCR auf Bilddateien** mit Aspose OCR Cloud ausführen, automatisch ein **Hugging Face‑Modell herunterladen**, die **LLM‑Modelleinstellungen** fachkundig **konfigurieren** und schließlich **OCR‑Text** mit einem leistungsstarken LLM‑Post‑Processor bereinigen. Der gesamte Prozess passt in ein einziges, leicht auszuführendes Python‑Skript und funktioniert sowohl auf GPU‑fähigen als auch auf reinen CPU‑Maschinen.

Wenn Sie mit dieser Pipeline vertraut sind, experimentieren Sie gern mit:

- **Verschiedene LLMs** – probieren Sie `meta-llama/Meta-Llama-3-8B‑Instruct‑GGUF` für ein größeres Kontextfenster.  
- **Batch‑Verarbeitung** – iterieren Sie über einen Ordner mit Bildern und aggregieren Sie die bereinigten Ergebnisse in einer CSV.  
- **Benutzerdefinierte Prompts** – passen Sie die KI an Ihre Domäne an (rechtliche Dokumente, medizinische Notizen usw.).

Passen Sie den Wert `gpu_layers` nach Belieben an, tauschen Sie das Modell aus oder fügen Sie Ihren eigenen Prompt ein. Der Himmel ist die Grenze, und der Code, den Sie jetzt haben, ist die Startrampe.

Viel Spaß beim Programmieren, und möge Ihr OCR‑Ausgabe stets sauber sein! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}