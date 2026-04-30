---
category: general
date: 2026-04-29
description: Erfahren Sie, wie Sie OCR auf Ihren Scans ausführen, das Hugging‑Face‑Modell
  automatisch nutzen und Text aus Scans mit Aspose OCR in wenigen Minuten erkennen.
draft: false
keywords:
- how to run OCR
- use hugging face model
- recognize text from scans
- download model automatically
language: de
og_description: Wie man OCR auf Scans mit Aspose OCR ausführt, automatisch ein Hugging
  Face‑Modell herunterlädt und sauberen, punktuierten Text erhält.
og_title: Wie man OCR mit Aspose & Hugging Face ausführt – Komplettanleitung
tags:
- OCR
- Aspose
- Hugging Face
- Python
title: Wie man OCR mit Aspose & Hugging Face ausführt – Vollständiger Leitfaden
url: /de/python/general/how-to-run-ocr-with-aspose-hugging-face-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR mit Aspose & Hugging Face ausführt – Komplettanleitung

Haben Sie sich schon einmal gefragt, **wie man OCR** auf einem Stapel gescannter Dokumente ausführt, ohne Stunden mit Feineinstellungen zu verbringen? Sie sind nicht allein. In vielen Projekten müssen Entwickler **Text aus Scans erkennen** und das schnell, doch sie stolpern über Modell‑Downloads und Nachbearbeitung.  

Gute Neuigkeiten: Dieses Tutorial zeigt Ihnen eine sofort einsatzbereite Lösung, die **ein Hugging Face‑Modell verwendet**, es automatisch herunterlädt und Interpunktion hinzufügt, sodass die Ausgabe wie von einem Menschen geschrieben wirkt. Am Ende haben Sie ein Skript, das jedes Bild in einem Ordner verarbeitet und eine saubere `.txt`‑Datei neben jedem Scan ablegt.

## Was Sie benötigen

- Python 3.8+ (der Code verwendet f‑Strings, ältere Versionen reichen nicht)
- `aspose-ocr`‑Paket (Installation via `pip install aspose-ocr`)
- Internetzugang für den erstmaligen Modell‑Download  
- Ein Ordner mit Bild‑Scans (`.png`, `.jpg` oder `.tif`)

Das war’s – keine zusätzlichen Binärdateien, kein manuelles Modell‑Tuning. Lassen Sie uns loslegen.

![wie man OCR ausführt Beispiel](https://example.com/ocr-demo.png "wie man OCR ausführt Beispiel")

## Schritt 1: Aspose OCR‑Klassen importieren & Umgebung einrichten

Wir beginnen damit, die notwendigen Klassen aus der Aspose OCR‑Bibliothek zu holen. Alles zu Beginn zu importieren hält das Skript übersichtlich und macht fehlende Abhängigkeiten leicht erkennbar.

```python
# Step 1: Import Aspose OCR classes
import os
from aspose.ocr import OcrEngine, AsposeAI, AsposeAIModelConfig
```

*Warum das wichtig ist*: `OcrEngine` übernimmt die schwere Arbeit, während `AsposeAI` uns ermöglicht, ein großes Sprachmodell für eine intelligentere Nachbearbeitung anzuschließen. Wenn Sie den Import weglassen, kompiliert der Rest des Codes nicht – also nicht vergessen.

## Schritt 2: Ein GPU‑bewusstes Hugging Face‑Modell konfigurieren  

Jetzt teilen wir Aspose mit, wo das Modell heruntergeladen werden soll und wie viele Schichten auf der GPU laufen sollen. Das Flag `allow_auto_download="true"` übernimmt für Sie den **automatischen Modell‑Download**.

```python
# Step 2: Configure a GPU‑aware AI model (replace with your own model folder)
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=40,                     # use GPU for faster inference
    directory_model_path=r"YOUR_DIRECTORY/models"
)
```

> **Pro‑Tipp**: Wenn Sie keine GPU haben, setzen Sie `gpu_layers=0`. Das Modell fällt dann auf die CPU zurück, was langsamer ist, aber trotzdem funktioniert.

### Warum ein Hugging Face‑Modell wählen?

Hugging Face hostet eine riesige Sammlung sofort einsetzbarer LLMs. Durch den Verweis auf `Qwen/Qwen2.5-3B-Instruct-GGUF` erhalten Sie ein kompaktes, instruktions‑feinabgestimmtes Modell, das Interpunktion hinzufügen, Abstände korrigieren und sogar kleinere OCR‑Fehler beheben kann. Das ist die praktische Umsetzung von **use hugging face model**.

## Schritt 3: KI‑Engine initialisieren und Interpunktions‑Nachbearbeitung aktivieren  

Die KI‑Engine ist nicht nur für schicke Chats gedacht – hier hängen wir einen *Interpunktions‑Adder* an, der die rohe OCR‑Ausgabe säubert.

```python
# Step 3: Initialise the AI engine and enable punctuation post‑processing
ai_engine = AsposeAI()
ai_engine.set_post_processor("punctuation_adder", {})
```

*Was passiert?* Der Aufruf `set_post_processor` registriert einen eingebauten Nachbearbeiter, der nach Abschluss der OCR‑Engine läuft. Er nimmt den rohen String und fügt Kommas, Punkte und Großbuchstaben an den richtigen Stellen ein, sodass der finale Text deutlich lesbarer wird.

## Schritt 4: OCR‑Engine erstellen und KI‑Engine anhängen  

Die Verknüpfung von KI‑Engine und OCR‑Engine liefert ein einzelnes Objekt, das sowohl Zeichen lesen als auch das Ergebnis veredeln kann.

```python
# Step 4: Create the OCR engine and attach the AI engine
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_engine)
```

Wenn Sie diesen Schritt überspringen, funktioniert die OCR weiterhin, aber Sie verlieren den Interpunktions‑Boost – die Ausgabe sieht dann aus wie ein Strom von Wörtern.

## Schritt 5: Jede Bilddatei in einem Ordner verarbeiten  

Hier kommt das Herzstück des Tutorials. Wir iterieren über jedes Bild, führen OCR aus, wenden die Nachbearbeitung an und schreiben den bereinigten Text in eine nebeneinander liegende `.txt`‑Datei.

```python
# Step 5: Run OCR on each image in a folder, post‑process the result, and save the text
scans_folder = r"YOUR_DIRECTORY/scans"
for image_file in os.listdir(scans_folder):
    # Filter only supported image types
    if not image_file.lower().endswith(('.png', '.jpg', '.tif')):
        continue

    image_path = os.path.join(scans_folder, image_file)

    # Recognise text from the image
    ocr_result = ocr_engine.recognize(image_path)

    # Apply the punctuation post‑processor
    ocr_result = ocr_engine.run_postprocessor(ocr_result)

    # Show a brief confidence summary
    print(f"{image_file} – confidence {ocr_result.confidence:.2%}")

    # Save the cleaned text next to the source image
    txt_path = image_path + ".txt"
    with open(txt_path, "w", encoding="utf-8") as txt_file:
        txt_file.write(ocr_result.text)
```

### Was Sie erwarten können

Beim Ausführen des Skripts erscheint etwa Folgendes:

```
invoice_001.png – confidence 96.73%
receipt_2024.tif – confidence 94.12%
```

Jede Zeile gibt den Vertrauens‑Score aus (ein schneller Gesundheits‑Check) und erstellt `invoice_001.png.txt`, `receipt_2024.tif.txt` usw., die interpunktierten, menschenlesbaren Text enthalten.

### Sonderfälle & Variationen

- **Scans in anderen Sprachen**: Ändern Sie `hugging_face_repo_id` zu einem mehrsprachigen Modell (z. B. `microsoft/Multilingual-LLM-GGUF`).
- **Große Stapel**: Verpacken Sie die Schleife in einen `concurrent.futures.ThreadPoolExecutor` für parallele Verarbeitung, achten Sie jedoch auf GPU‑Speichergrenzen.
- **Eigene Nachbearbeitung**: Ersetzen Sie `"punctuation_adder"` durch Ihr eigenes Skript, wenn Sie domänenspezifische Bereinigungen benötigen (z. B. das Entfernen von Rechnungsnummern).

## Schritt 6: Ressourcen aufräumen  

Wenn der Job beendet ist, verhindert das Freigeben von Ressourcen Speicher‑Leaks – besonders wichtig, wenn Sie das in einem langlebigen Service ausführen.

```python
# Step 6: Release resources
ai_engine.free_resources()
ocr_engine.dispose()
```

Das Ignorieren dieses Schrittes kann GPU‑Speicher belegen und nachfolgende Läufe sabotieren.

## Zusammenfassung: OCR End‑to‑End ausführen  

In nur wenigen Zeilen haben wir gezeigt, **wie man OCR** auf einem Ordner mit Scans ausführt, **ein Hugging Face‑Modell** nutzt, das sich beim ersten Mal selbst herunterlädt, und **Text aus Scans erkennt** mit automatisch hinzugefügter Interpunktion. Das komplette Skript ist bereit zum Kopieren, Pfade anpassen und Ausführen.

## Nächste Schritte & verwandte Themen  

- **Batch‑Nachbearbeitung**: Erkunden Sie `ocr_engine.run_batch_postprocessor` für noch schnellere Massenverarbeitung.  
- **Alternative Modelle**: Probieren Sie die `openai/whisper`‑Familie, wenn Sie neben OCR auch Sprache‑zu‑Text benötigen.  
- **Integration mit Datenbanken**: Speichern Sie den extrahierten Text in SQLite oder Elasticsearch für durchsuchbare Archive.  

Experimentieren Sie gern – tauschen Sie das Modell aus, passen Sie `gpu_layers` an oder fügen Sie Ihre eigene Nachbearbeitung hinzu. Die Flexibilität von Aspose OCR kombiniert mit dem Modell‑Hub von Hugging Face bildet ein vielseitiges Fundament für jedes Dokument‑Digitalisierungsprojekt.

---

*Viel Spaß beim Coden! Wenn Sie auf ein Problem stoßen, hinterlassen Sie einen Kommentar unten oder werfen Sie einen Blick in die Aspose OCR‑Dokumentation für weiterführende Konfigurationsoptionen.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}