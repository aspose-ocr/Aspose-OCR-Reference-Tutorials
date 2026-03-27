---
category: general
date: 2026-01-12
description: Wie man OCR ausführt und Text aus Rechnungsbildern mit Aspose OCR und
  einem leichten Hugging‑Face‑Modell extrahiert. Erfahren Sie, wie Sie das Modell
  herunterladen, OCR‑Fehler korrigieren und OCR auf dem Bild durchführen.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: de
og_description: Wie man OCR auf Rechnungsbildern ausführt, Text extrahiert und Fehler
  mit einem Hugging Face LLM behebt. Folgen Sie diesem vollständigen Leitfaden für
  fehlerlose Ergebnisse.
og_title: Wie man OCR auf Rechnungsbildern ausführt – Vollständiges Tutorial
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: Wie man OCR auf Rechnungsbildern anwendet – Vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR auf Rechnungsbildern ausführt – Vollständige Schritt‑für‑Schritt‑Anleitung

Haben Sie sich jemals gefragt, **wie man OCR** auf einer gescannten Rechnung ausführt und sauberen, durchsuchbaren Text erhält, ohne Stunden mit der Bereinigung zu verbringen? Sie sind nicht allein. In vielen realen Projekten ist die rohe OCR‑Ausgabe voller Fehlinterpretationen – denken Sie an „O“ statt „0“, „l“ statt „1“ oder sogar ganze Wörter, die durcheinander geraten. Die gute Nachricht? Mit ein paar Zeilen Python können Sie nicht nur **perform OCR on image** Dateien ausführen, sondern auch automatisch **correct OCR errors** mithilfe eines leichten Modells von Hugging Face.

In diesem Tutorial führen wir Sie durch alles, was Sie wissen müssen: vom Laden eines Rechnungsbildes, dem Extrahieren von Rohtext, dem Herunterladen eines quantisierten Modells bis hin zur Verfeinerung des Ergebnisses, sodass Sie eine perfekte Transkription erhalten, die für nachgelagerte Verarbeitung bereit ist. Am Ende können Sie **extract text from invoice** PDFs oder PNGs in einem einzigen, wiederholbaren Skript extrahieren.

## Voraussetzungen & Einrichtung

Before diving in, make sure you have:

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| Python 3.9+ | Moderne Syntax und Typ‑Hinweise |
| `aspose-ocr` package | Stellt den im Beispiel verwendeten `ocr.OcrEngine` bereit |
| `aspose-ai` package | Stellt den `AsposeAI` Post‑Processor bereit |
| Access to a GPU (optional) | Beschleunigt die LLM‑Schichten; sonst funktioniert die CPU einwandfrei |
| Internet connection (first run) | Wird benötigt, um das **download Hugging Face model** automatisch herunterzuladen |

Sie können die erforderlichen Bibliotheken installieren mit:

```bash
pip install aspose-ocr aspose-ai
```

> **Pro Tipp:** Wenn Sie planen, das LLM auf GPU auszuführen, installieren Sie `torch` mit CUDA‑Unterstützung (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

Jetzt, da die Umgebung bereit ist, gehen wir zum Code über.

---

## Schritt 1 – Initialisieren Sie die OCR‑Engine und laden Sie Ihr Rechnungsbild

Das erste, was Sie tun müssen, ist eine Instanz der OCR‑Engine von Aspose zu erstellen und sie auf die Datei zu richten, die Sie verarbeiten möchten. Dieser Schritt ist die Grundlage von **how to run OCR** für jedes Bild.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Warum das wichtig ist:** `load_image` akzeptiert PNG, JPEG, TIFF und sogar PDF‑Seiten, sodass Sie **perform OCR on image** Daten unabhängig vom Format verarbeiten können.

---

## Schritt 2 – Führen Sie ein einfaches OCR aus, um Rohtext zu erfassen

Sobald das Bild geladen ist, kann die Engine eine rohe Transkription erzeugen. Diese Ausgabe ist oft verrauscht, weshalb wir später einen Korrekturschritt durchführen werden.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

Typische Rohausgabe könnte folgendermaßen aussehen:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

Fallen Ihnen die Nullen (`0`) auf, wo die Ziffer „O“ stehen sollte? Genau das ist die Art von Fehler, die wir später beheben werden.

---

## Schritt 3 – Konfigurieren Sie den KI‑Post‑Processor mit einem leichten LLM

Jetzt holen wir ein **download Hugging Face model** dazu, das klein genug ist, um auf bescheidener Hardware zu laufen, aber leistungsstark genug, um die Sprache von Rechnungen zu verstehen. Das Beispiel verwendet das Qwen 2.5 3B‑Instruct GGUF‑Modell, quantisiert zu `int8` für einen winzigen Speicherbedarf.

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **Warum dieses Modell?** Die `int8`‑Quantisierung reduziert die Datei auf ~1,2 GB, wodurch sie auf den meisten Laptops machbar ist. GPU‑Schichten beschleunigen die Inferenz, aber der Code weicht bei fehlender GPU elegant auf die CPU aus.

---

## Schritt 4 – Führen Sie die LLM‑basierte Korrektur des rohen OCR‑Ergebnisses aus

Mit dem bereitstehenden Modell geben wir den Rohtext in den Post‑Processor ein. Das LLM wird die Transkription neu schreiben, gängige OCR‑Fehler beheben und Zahlen normalisieren.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

Erwartete bereinigte Ausgabe:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

Sie sehen, dass die Nullen wieder in den Buchstaben „O“ umgewandelt wurden und „Am0unt“ jetzt „Amount“ ist. Das ist das Kernstück von **correct OCR errors** automatisch.

---

## Schritt 5 – Ressourcen freigeben und Aufräumen

Große Sprachmodelle können GPU‑Speicher belegen, daher ist es gute Praxis, Ressourcen freizugeben, wenn Sie fertig sind.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

Wenn Sie viele Rechnungen stapelweise verarbeiten möchten, können Sie das Modell geladen lassen und erst am Ende des Skripts freigeben.

## Vollständiges funktionierendes Beispiel

Wenn wir alles zusammenfügen, hier ein einzelnes Skript, das Sie in eine `.py`‑Datei einfügen und ausführen können:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

Das Ausführen des Skripts sollte eine Ausgabe erzeugen, die der zuvor gezeigten „AI‑corrected“-Block ähnelt. Sie können den Bildpfad gern durch andere **extract text from invoice** Dateien im Batch ersetzen.

## Häufig gestellte Fragen & Sonderfälle

### Was, wenn ich keine GPU habe?

Der Parameter `gpu_layers` ist optional. Setzen Sie ihn auf `0` oder lassen Sie ihn weg, und das Modell läuft vollständig auf der CPU. Erwarten Sie eine langsamere Inferenz – etwa 2–3 Sekunden pro Seite auf einem modernen Laptop.

### Meine Rechnungen sind mehrseitige PDFs. Wie gehe ich damit um?

Konvertieren Sie jede Seite in ein separates Bild (z. B. mit `pdf2image`) und iterieren Sie über die Seiten mit demselben Skript. Die OCR‑Engine kann jedes Bild unabhängig verarbeiten, und das LLM korrigiert jeden Textblock.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### Der Modell‑Download schlägt hinter einer Firewall fehl?

Laden Sie das Modell manuell vom Hugging Face Model Hub herunter, entpacken Sie es in einen lokalen Ordner und verweisen Sie `hugging_face_repo_id` auf den lokalen Pfad:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### Wie genau ist die Korrektur?

Bei typischen englischsprachigen Rechnungen korrigiert das LLM >95 % der gängigen OCR‑Fehlinterpretationen. Komplexe handschriftliche Notizen können weiterhin eine manuelle Überprüfung erfordern.

## Tipps & Tricks für den Produktionseinsatz

- **Batch processing:** Schritt 2‑4 in eine Funktion einbetten und eine Liste von Dateipfaden übergeben. Verwenden Sie dieselbe `AsposeAI`‑Instanz erneut, um das Laden des Modells zu vermeiden.
- **Logging:** Ersetzen Sie `print` durch das Python‑`logging`‑Modul, um sowohl rohe als auch korrigierte Ausgaben für Prüfpfade zu erfassen.
- **Error handling:** Umgeben Sie den OCR‑Aufruf mit `try/except`‑Blöcken. Wenn ein Bild fehlschlägt, protokollieren Sie den Dateinamen und fahren fort.
- **Performance tuning:** Experimentieren Sie mit `gpu_layers`. Mehr Schichten auf der GPU beschleunigen die Inferenz, erhöhen jedoch den VRAM‑Verbrauch.

## Fazit

Wir haben **how to run OCR** auf Rechnungsbildern von Anfang bis Ende behandelt und gezeigt, wie man **perform OCR on image**, **download Hugging Face model** und **correct OCR errors** automatisch ausführt. Das vollständige Skript demonstriert einen praktischen Workflow, den Sie in jede Python‑basierte Automatisierungspipeline einbinden können.

Nächste Schritte? Versuchen Sie, die Pipeline zu erweitern, um **extract key fields** (Rechnungsnummer, Datum, Gesamtsumme) mithilfe regulärer Ausdrücke auf dem korrigierten Text zu extrahieren, oder füttern Sie die bereinigte Ausgabe in eine Datenbank für durchsuchbare Datensätze. Sie können auch mit anderen leichten LLMs von Hugging Face experimentieren, falls Sie eine andere Sprache oder domänenspezifisches Wissen benötigen.

Viel Spaß beim Programmieren, und möge Ihr OCR‑Ergebnis stets kristallklar sein!

![wie man OCR auf einem Rechnungsbild ausführt](ocr_invoice_example.png "wie man OCR auf Rechnung ausführt")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}