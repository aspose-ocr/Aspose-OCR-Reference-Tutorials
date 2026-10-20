---
category: general
date: 2026-03-18
description: Ein grundlegendes OCR‑Python‑Tutorial zeigt, wie man TIFF in Text konvertiert,
  Bild‑OCR lädt, GPU‑Schichten einstellt und führende Nullen mit Aspose AI korrigiert.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: de
og_description: Ein grundlegendes OCR‑Python‑Tutorial führt Sie durch das Konvertieren
  von TIFF‑Dateien in sauberen Text, das Laden von Bildern, das Einstellen von GPU‑Schichten
  und das Korrigieren führender Nullen.
og_title: Grundlegendes OCR Python – TIFF in Text konvertieren
tags:
- OCR
- Python
- AI
- Aspose
title: Grundlegendes OCR in Python – TIFF in Text umwandeln
url: /de/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – TIFF in Text konvertieren mit KI‑Nachbearbeitung

Suchen Sie nach einer Möglichkeit, **basic ocr python** auf Ihren gescannten Dokumenten durchzuführen? In diesem Leitfaden zeigen wir, wie man eine TIFF‑Datei in sauberen, durchsuchbaren Text konvertiert, indem man Aspose OCR und einen KI‑Nachbearbeiter verwendet.  

Falls Sie jemals Schwierigkeiten hatten, **TIFF in Text zu konvertieren**, weil die Rohausgabe voller Tippfehler oder seltsamer Symbole ist, sind Sie nicht allein. Wir zeigen Ihnen außerdem, wie Sie **load image OCR** verwenden, die Engine anpassen, um **set GPU layers** zu setzen, und sogar **fix leading zeroes** beheben, die häufig in Rechnungsnummern vorkommen.

## Was Sie lernen werden

- Wie man die Aspose OCR‑Engine für gedruckte Dokumente initialisiert.  
- Die genauen Schritte, um **load image OCR** aus einer TIFF‑Datei zu laden und Rohtext zu erhalten.  
- Konfiguration eines KI‑Modells, automatischer Download und **setting GPU layers** für schnellere Inferenz.  
- Einbindung der integrierten Rechtschreibprüfung plus einer benutzerdefinierten Funktion, die **fixes leading zeroes**.  
- Bereinigung des OCR‑Ergebnisses und korrektes Freigeben von Ressourcen.  

Am Ende dieses Tutorials haben Sie ein einzelnes, wiederverwendbares Python‑Skript, das jede TIFF‑Datei in aufbereiteten, durchsuchbaren Text umwandelt – ohne manuelles Kopieren und Einfügen.

### Voraussetzungen

- Python 3.8+ auf Ihrem Rechner installiert.  
- `aspose-ocr`‑Paket (`pip install aspose-ocr`).  
- Optional: eine GPU mit mindestens 4 GB VRAM, wenn Sie **set GPU layers** nutzen möchten; andernfalls fällt der Code automatisch auf die CPU zurück.  

---

## basic ocr python – Bild laden und Text erkennen

Das Erste, was wir tun müssen, ist **load image OCR**, damit die Engine die Pixel lesen kann. Asposes `OcrEngine` unterstützt viele Formate, aber hier konzentrieren wir uns auf TIFF, da es das häufigste Format für gescannte Rechnungen ist.

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Pro Tipp:** Wenn Sie mit mehrseitigen TIFFs arbeiten, verarbeitet Aspose automatisch jede Seite nacheinander, sodass Sie keine zusätzlichen Schleifen benötigen.

Jetzt, wo das Bild geladen ist, führen wir einen grundlegenden Erkennungslauf durch.

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

Sie werden etwas Ähnliches sehen:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Fallen Ihnen die *Nullen* vor den Buchstaben auf? Das ist ein klassisches OCR‑Artefakt, das wir später bereinigen werden.

![basic ocr python Arbeitsablauf](/images/ocr-workflow.png "basic ocr python Arbeitsablaufdiagramm")

---

## Schritt 2: TIFF in Text konvertieren – KI‑Nachbearbeiter vorbereiten

Roh‑OCR ist nützlich, aber die meisten Produktions‑Pipelines benötigen eine aufbereitete Version. Aspose stellt einen `AsposeAI`‑Wrapper bereit, der ein Modell von Hugging Face herunterladen, auf der GPU ausführen und automatisch Rechtschreibprüfung anwenden kann.  

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### Warum `set GPU layers` wichtig ist

Der Parameter `gpu_layers` gibt dem zugrunde liegenden GGUF‑Modell an, wie viele Transformer‑Layer auf der GPU verbleiben sollen. Mehr Layer = schnellere Inferenz, aber höherer VRAM‑Verbrauch. Wenn Sie einen bescheidenen Laptop verwenden, reduzieren Sie den Wert auf `10` oder lassen Sie ihn ganz weg, um auf der CPU zu bleiben.  

---

## Schritt 3: Rechtschreibprüfung anwenden und **fix leading zeroes**

Aspose AI wird mit einer integrierten Rechtschreibprüfung geliefert, die die meisten englischen Rechtschreibfehler erkennt. Domänenspezifische Korrekturen – wie das Ersetzen einer führenden `0` durch ein `O` bei Rechnungs‑Codes – erfordern jedoch einen benutzerdefinierten Nachbearbeiter.

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **Warum das funktioniert:** Der reguläre Ausdruck sucht nach einer Wortgrenze (`\b`), einer Null, gefolgt von exakt drei Großbuchstaben. Er ersetzt dann die Null durch den Buchstaben „O“. Sie können das Muster für andere Eigenheiten erweitern (z. B. `0[0-9]{2}` für falsch gelesene Zahlen).  

---

## Schritt 4: OCR‑Ergebnis mit dem KI‑Nachbearbeiter bereinigen

Jetzt kombinieren wir alles: den Rohstring aus **basic ocr python**, die Rechtschreibprüfung und unsere Null‑Korrektur. Die Methode `run_postprocessor` gibt eine bereinigte Version zurück, die für nachgelagerte Systeme bereit ist.

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

Typische Ausgabe nach dem Nachbearbeiter:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Sie können sehen, dass die führende Null in ein `O` umgewandelt wurde und häufige Rechtschreibfehler korrigiert sind. Der Text ist nun geeignet, um in einer Suchmaschine indiziert oder in eine Datenextraktions‑Pipeline eingespeist zu werden.  

---

## Schritt 5: KI‑Ressourcen freigeben – GPU zufrieden halten

Wenn Sie mehrere OCR‑Aufgaben in einem langlaufenden Service ausführen, ist es gute Praxis, den GPU‑Speicher des Modells nach Abschluss freizugeben.

```python
ocr_ai.free_resources()
```

Das Überspringen dieses Schrittes kann zu „out‑of‑memory“-Fehlern bei nachfolgenden Aufrufen führen, insbesondere wenn **set GPU layers** auf einen hohen Wert gesetzt ist.  

---

## Optionale Varianten & Randfälle

| Situation | Was zu ändern ist |
|-----------|-------------------|
| **Handwritten documents** | Verwenden Sie `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` anstelle von `PRINTED`. |
| **No GPU available** | Setzen Sie `gpu_layers=0` oder lassen Sie das Argument weg; das Modell läuft auf der CPU (langsamer, aber sicher). |
| **Different language** | Tauschen Sie die Hugging Face‑Repo‑ID gegen ein sprachspezifisches Modell aus, z. B. `microsoft/Florence-2-base`. |
| **Batch processing** | Packen Sie die Schritte in eine `for file in glob("*.tif"):`‑Schleife und sammeln Sie die Ergebnisse in einer Liste oder CSV. |
| **More complex zero patterns** | Erweitern Sie `invoice_fix` mit zusätzlichen Regexes, z. B. `r"\b0+([A-Z]{2,})\b"` für mehrere führende Nullen. |

---

## Fazit

Wir haben gerade eine **basic ocr python**‑Pipeline abgeschlossen, die eine TIFF lädt, Rohtext extrahiert und diesen dann mit einem KI‑Modell bereinigt, während **setting GPU layers** für die Leistung verwendet werden. Der benutzerdefinierte Nachbearbeiter zeigt, wie man **fix leading zeroes** durchführt – ein kleines, aber oft übersehenes Detail, das nachgelagerte Analysen beeinträchtigen kann.  

Fühlen Sie sich frei zu experimentieren: probieren Sie eine andere Quantisierung (`float16` für höhere Genauigkeit), tauschen Sie die Rechtschreibprüfung gegen ein domänenspezifisches Wörterbuch aus oder verketten Sie mehrere benutzerdefinierte Korrekturen. Das Muster bleibt gleich – laden, erkennen, KI konfigurieren, nachbearbeiten und aufräumen.  

**Nächste Schritte**, die Sie erkunden könnten, umfassen:

- Integration der bereinigten Ausgabe in eine Datenbank oder einen Elasticsearch‑Index.  
- Verwendung desselben Ansatzes, um **convert TIFF to text** für mehrsprachige PDFs zu nutzen.  
- Hinzufügen einer UI mit Flask oder FastAPI, damit nicht‑technische Benutzer Dateien hochladen und sofort bereinigten Text erhalten können.  

Viel Spaß beim Programmieren, und mögen Ihre OCR‑Ergebnisse stets klar und ohne Null‑Probleme sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}