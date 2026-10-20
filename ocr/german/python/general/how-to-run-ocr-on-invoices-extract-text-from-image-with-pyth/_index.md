---
category: general
date: 2026-01-07
description: Wie man OCR ausführt und Text aus einem Bild für die Rechnungsverarbeitung
  extrahiert. Lernen Sie, die OCR‑Genauigkeit zu verbessern, ein Bild für OCR zu laden
  und die Rechnungs‑OCR effizient zu verarbeiten.
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: de
og_description: Wie man OCR auf Rechnungen Schritt für Schritt ausführt. Text aus
  Bild extrahieren, OCR‑Genauigkeit verbessern und Bild für OCR mit Aspose AI laden.
og_title: Wie man OCR bei Rechnungen ausführt – Vollständiger Python-Leitfaden
tags:
- OCR
- Python
- Image Processing
title: Wie man OCR auf Rechnungen anwendet – Text aus Bild mit Python extrahieren
url: /de/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR auf Rechnungen ausführt – Text aus Bild mit Python extrahieren

Haben Sie sich jemals gefragt, **wie man OCR** auf einer gescannten Rechnung ausführt und sauberen, durchsuchbaren Text erhält? Sie sind nicht allein. Viele Entwickler stoßen auf Probleme, wenn die rohe OCR‑Ausgabe voller Rechtschreibfehler, fehlerhafter Zeilenumbrüche und fehlender Interpunktion ist. In diesem Tutorial führen wir Sie durch eine Full‑Stack‑Lösung, die nicht nur **Text aus Bild extrahiert**, sondern auch **die OCR‑Genauigkeit** durch Nachbearbeitung mit einem Aspose‑AI‑Modell **verbessert**.

Sie werden sehen, wie man **ein Bild für OCR lädt**, die integrierte Engine ausführt und anschließend eine leichte Rechtschreibprüfung anwendet, die das Ergebnis für nachgelagerte Analysen bereit macht. Am Ende haben Sie ein wiederverwendbares Skript, das in jede Rechnung‑Verarbeitungspipeline integriert werden kann.

> **Was Sie benötigen**  
> * Python 3.9 oder neuer  
> * `aspose-ocr` und `aspose-ai` Pakete (installiert via `pip`)  
> * Ein Rechnungsbild (PNG, JPEG oder TIFF) – wir verwenden `sample_invoice.png` als Beispiel  
> * Optional: eine GPU mit mindestens 4 GB VRAM für schnellere Model‑Inference (das Skript funktioniert auch auf CPU)

---

## Schritt 1: Erforderliche Pakete installieren und Umgebung vorbereiten

Bevor wir **ein Bild für OCR laden** können, müssen wir sicherstellen, dass die notwendigen Bibliotheken verfügbar sind. Die Aspose OCR‑Engine wird mit einem einfachen Python‑Wrapper geliefert, während der KI‑Nachbearbeiter auf einem quantisierten Hugging Face‑Modell basiert.

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **Pro‑Tipp:** Wenn Sie GPU‑Beschleunigung nutzen möchten, installieren Sie `torch` mit CUDA‑Support (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

---

## Schritt 2: Rechnungsbild laden

Das Laden des Bildes ist unkompliziert, aber es ist erwähnenswert, warum wir den Pfad explizit als Rohstring (`r"..."`) setzen. Das verhindert versehentliche Escape‑Zeichen‑Probleme bei Windows‑Pfaden.

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*Warum das wichtig ist:* Durch die Verwendung von `ocr.Image.load` wird garantiert, dass das Bild gemäß Asposes optimalen Vorgaben vorverarbeitet wird (Binarisierung, Entzerrung), was bereits **die OCR‑Genauigkeit** verbessert, bevor irgendeine KI‑Magie einsetzt.

---

## Schritt 3: Eingebaute OCR‑Engine ausführen

Jetzt führen wir tatsächlich **OCR aus** und erfassen den Rohtext. Dieser Schritt zeigt die typische Ausgabe, die Sie von einem einfachen OCR‑Durchlauf erhalten – oft ein Durcheinander von Zeilenumbrüchen und gelegentlichen Rechtschreibfehlern.

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**Typische Rohausgabe** (aus Platzgründen gekürzt):

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Sie werden vielleicht bemerken, dass „Invoice“ als „Invo1ce“ erscheint oder dass Interpunktion fehlt. Hier kommt der KI‑Nachbearbeiter ins Spiel.

---

## Schritt 4: Aspose‑KI‑Modell konfigurieren

Das KI‑Modell, das wir verwenden werden, ist **Qwen2.5‑3B‑Instruct‑GGUF**, ein leichtgewichtiges, anweisungs‑getunetes LLM, das komfortabel auf einer Mittelklasse‑GPU läuft. Die nachstehende Konfiguration teilt Aspose mit, wo das Modell abgerufen wird, wie viele Schichten auf der GPU verbleiben und welche Kontextgröße für die Verarbeitung langer Absätze verwendet wird.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **Warum diese Konfiguration?**  
> * `gpu_layers=30` balanciert Geschwindigkeit und Speicher – die meisten Inferenzvorgänge laufen auf der GPU, während die restlichen Schichten auf der CPU bleiben, um OOM‑Fehler zu vermeiden.  
> * `context_size=4096` stellt sicher, dass das Modell die gesamte Rechnung auf einmal sehen kann, wodurch das Abschneiden wichtiger Felder verhindert wird.

---

## Schritt 5: Einfachen Rechtschreib‑Nachbearbeiter erstellen

Wir verpacken den KI‑Aufruf in einer kleinen Funktion namens `simple_spell_check`. Der Prompt ist bewusst knapp: „Correct spelling and punctuation:“ gefolgt vom rohen OCR‑Text. Das Modell gibt eine bereinigte Version zurück.

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**Wie es funktioniert:** `ai.run_prompt` sendet den Prompt an das lokal geladene LLM, das dann einen einzelnen String mit korrigierter Rechtschreibung, richtiger Interpunktion und einem natürlicheren Zeilenumbruch‑Layout zurückgibt.

---

## Schritt 6: Nachbearbeiter auf den rohen OCR‑Text anwenden

Jetzt geschieht die Magie. Wir geben die rohe OCR‑Ausgabe in unseren Nachbearbeiter ein und drucken das verbesserte Ergebnis.

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**Beispiel für verbesserten Output**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Beachten Sie die korrigierte Schreibweise von „Invoice“, die korrekte Verwendung von Doppelpunkten und konsistente Zeilenumbrüche – genau das, was Sie für zuverlässiges nachgelagertes Parsen benötigen.

---

## Schritt 7: Ressourcen bereinigen

Sowohl die OCR‑Engine als auch das KI‑Modell reservieren native Ressourcen. Es ist gute Praxis, sie freizugeben, wenn Sie fertig sind insbesondere in langfristig laufenden Diensten.

```python
ai.free_resources()
engine.dispose()
```

---

## Vollständiges Skript – Bereit zum Einfügen

Unten finden Sie das vollständige, ausführbare Skript, das alle Schritte miteinander verknüpft. Speichern Sie es als `invoice_ocr.py`, ersetzen Sie `YOUR_DIRECTORY` durch den Ordner, der Ihr Rechnungsbild enthält, und führen Sie es mit `python invoice_ocr.py` aus.

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

Führen Sie das Skript aus und Sie sehen sowohl den lauten rohen OCR‑Dump als auch die polierte Version mit **verbesserter OCR‑Genauigkeit** nebeneinander.

---

## Häufig gestellte Fragen & Sonderfälle

### 1. Was ist, wenn mein Rechnungsbild ein mehrseitiges PDF ist?

Aspose OCR kann PDF‑Seiten direkt laden. Ersetzen Sie die Zeile zum Laden des Bildes durch:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

Iterieren Sie `page_index`, um jede Seite nacheinander zu verarbeiten.

### 2. Meine GPU hat nicht genug Speicher – kann ich nur die CPU verwenden?

Absolut. Setzen Sie `gpu_layers=0` in der `AsposeAIModelConfig`. Das Modell läuft dann vollständig auf der CPU, was langsamer, aber für Low‑End‑Hardware sicher ist.

### 3. Wie gehe ich mit nicht‑englischen Rechnungen um?

Tauschen Sie die Modell‑Repository‑ID gegen ein sprachspezifisches Modell aus, z. B. `"mistralai/Mistral-7B-Instruct-v0.2"` für mehrsprachige Unterstützung. Der Rest der Pipeline bleibt unverändert.

### 4. Kann ich mehrere Nachbearbeiter verketten (z. B. Daten formatieren, Summen extrahieren)?

Ja. `ai.set_post_processor` akzeptiert eine Liste von Callables. Zum Beispiel:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

---

## Leistungstipps & bewährte Methoden

| Tipp | Warum es hilft |
|-----|----------------|
| **Mehrere Rechnungen stapeln** – laden Sie sie in eine Liste und verarbeiten Sie sie in einer Schleife. | Reduziert den Overhead des Python‑Interpreters und hält das KI‑Modell im Speicher warm. |
| **Modell cachen** – vermeiden Sie wiederholte Aufrufe von `initialize` in einem Web‑Service. | Das Laden des Modells kann ~30 Sekunden dauern; Caching liefert sofortige Antworten. |
| **Große Bilder auf 1500 px Breite verkleinern** vor OCR. | Kleinere Bilder beschleunigen sowohl OCR als auch KI‑Inference, ohne die Genauigkeit zu beeinträchtigen. |
| **Setzen Sie `allow_auto_download="false"` in der Produktion** – liefern Sie das Modell mit Ihrer Bereitstellung. | Garantiert deterministische Startzeiten und vermeidet Netzwerkprobleme. |

---

## Fazit

Wir haben behandelt, **wie man OCR** auf Rechnungen ausführt, vom Laden des Bildes bis zur Verfeinerung des Ergebnisses mit einer KI‑basierten Rechtschreibprüfung. Wenn Sie diesen Schritten folgen, können Sie zuverlässig **Text aus Bild extrahieren**, **die OCR‑Genauigkeit verbessern** und nahtlos **Rechnungs‑OCR** in jedem Python‑basierten Workflow verarbeiten.

Probieren Sie es mit verschiedenen Rechnungs‑Layouts aus – vielleicht ein handschriftlicher Beleg oder ein gescannter Vertrag. Die gleiche Pipeline passt sich mit minimalen Anpassungen an und beweist, dass eine gut strukturierte OCR + KI‑Kombination ein vielseitiges Werkzeug für jedes Dokument‑Automatisierungsprojekt ist.

Wenn Ihnen diese Anleitung geholfen hat, teilen Sie sie mit Kolleg*innen oder geben Sie dem Repository, das die Aspose‑Pakete hostet, einen Stern.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}