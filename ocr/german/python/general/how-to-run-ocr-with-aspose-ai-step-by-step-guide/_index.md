---
category: general
date: 2026-02-09
description: Wie man OCR mit Aspose AI und einem Hugging‑Face‑Modell ausführt – lerne,
  das Hugging‑Face‑Modell herunterzuladen, OCR‑Fehler zu korrigieren und GPU‑Speicher
  freizugeben.
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: de
og_description: Wie man OCR mit Aspose AI ausführt, wird im ersten Absatz erklärt
  – entdecken Sie, wie Sie das Hugging‑Face‑Modell herunterladen, OCR‑Fehler korrigieren
  und GPU‑Speicher freigeben.
og_title: Wie man OCR mit Aspose AI ausführt – Komplettanleitung
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: Wie man OCR mit Aspose AI ausführt – Schritt‑für‑Schritt‑Anleitung
url: /de/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR mit Aspose AI ausführt – Komplettanleitung

Haben Sie sich jemals gefragt, **wie man OCR** auf einer gescannten Rechnung ausführt und perfekt saubere Zahlen erhält, ohne Stunden damit zu verbringen, Tippfehler zu korrigieren? Sie sind nicht allein. In vielen real‑world Projekten enthält der Rohtext, der aus einem klassischen OCR‑Engine kommt, immer noch fremde Zeichen, beschädigte Währungssymbole oder verzerrte Ziffern – besonders wenn das Quellbild verrauscht ist.  

Die gute Nachricht ist, dass Sie ein LLM an Aspose OCR anbinden, ein Hugging Face‑Modell on‑the‑fly herunterladen und die KI das Ergebnis für Sie verfeinern lassen können. In diesem Tutorial führen wir Sie durch die gesamte Pipeline, vom Abrufen des Modells (ja, wir zeigen Ihnen, wie Sie **download hugging face model** automatisch **herunterladen**) bis zum Freigeben von GPU‑Ressourcen, wenn Sie fertig sind. Am Ende haben Sie ein reproduzierbares Skript, das **corrects OCR errors**, schnell auf einer bescheidenen GPU läuft und sich selbst aufräumt, damit Sie keinen Speicher verschwenden.

## Was Sie lernen werden

- Konfigurieren Sie Aspose AI, um ein **Qwen2.5‑3B‑Instruct‑GGUF**‑Modell von Hugging Face abzurufen.
- Führen Sie die Standard‑Aspose OCR‑Engine auf einer Bilddatei aus.
- Verwenden Sie einen benutzerdefinierten LLM‑Prompt, der Zahlen und Währungssymbole unverändert lässt.
- Geben Sie GPU‑Speicher mit der integrierten **free gpu memory**‑Routine frei.
- Passen Sie den Workflow für Randfälle wie mehrseitige PDFs oder Low‑End‑GPUs an.

> **Voraussetzungen** – Python 3.9+, `aspose-ocr`‑Paket, Internetzugang für den ersten Modell‑Download und eine GPU mit mindestens 4 GB VRAM (optional, aber empfohlen). Wenn Sie keine GPU haben, fällt das Skript automatisch auf die CPU für die restlichen Schichten zurück.

---

## Wie man OCR ausführt und Ergebnisse verbessert

Unten finden Sie das vollständige, sofort ausführbare Python‑Skript. Speichern Sie es als `ocr_with_ai.py` und ersetzen Sie die Platzhalter‑Pfade durch Ihre eigenen Dateien.

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **Pro‑Tipp:** Der Parameter `gpu_layers` lässt Sie entscheiden, wie viele Transformer‑Layer auf der GPU bleiben. Wenn Sie Out‑of‑Memory‑Fehler erhalten, reduzieren Sie diese Zahl und der Rest läuft auf der CPU – Sie werden später immer noch **free gpu memory** mit `ai.free_resources()` freigeben.

### Erwartete Ausgabe

Das Ausführen des Skripts auf einer Beispiel‑Rechnung liefert etwa Folgendes:

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

Beachten Sie, wie die KI das „O“ in `$1O0.00` zu einer richtigen Null korrigierte, während das Dollarzeichen erhalten blieb. Das ist das Wesentliche von **correct OCR errors** für Finanzdokumente.

---

## Hugging Face‑Modell herunterladen – Was im Hintergrund passiert?

Wenn Sie `allow_auto_download="true"` setzen, prüft der Aspose AI‑Wrapper den `directory_model_path`. Wenn die Modelldateien dort nicht vorhanden sind, greift er auf den Hugging Face‑Hub zu, holt die **int8‑quantized**‑Version von `Qwen2.5‑3B‑Instruct‑GGUF` und speichert sie lokal. Dieser einmalige Download liegt typischerweise unter 2 GB, sodass er selbst auf bescheidenen SSDs machbar ist.

> **Warum int8?** Die Quantisierung auf 8‑Bit reduziert den Speicherverbrauch drastisch – entscheidend, wenn Sie nach der Verarbeitung **free gpu memory** freigeben möchten. Der Kompromiss ist ein winziger Genauigkeitsverlust, aber für die Nachbearbeitung von OCR‑Text ist der Einfluss vernachlässigbar.

Wenn Sie das Modell lieber selbst hosten möchten, legen Sie die `.gguf`‑Dateien einfach in `YOUR_DIRECTORY/Models` ab und Aspose wird sie ohne erneuten Internetzugriff übernehmen.

## Wie man GPU freigibt – Best Practices

GPU‑Ressourcen sind auf vielen Workstations ein gemeinsam genutztes Gut. Das Lebenlassen von Tensoren nach Abschluss Ihres Skripts kann zu „CUDA out of memory“-Fehlern bei nachfolgenden Jobs führen. Der Aufruf `ai.free_resources()` erledigt drei Dinge:

1. **Entfernt den zugrunde liegenden Transformer** – alle GPU‑residenten Gewichte werden freigegeben.
2. **Leert den PyTorch‑Cache** – `torch.cuda.empty_cache()` wird intern aufgerufen.
3. **Löscht temporäre Dateien** – alle während des Downloads erstellten Festplatten‑Caches werden entfernt.

Sie können auch manuell `torch.cuda.empty_cache()` aufrufen, wenn Sie Aspose AI mit anderen PyTorch‑Workloads kombinieren, aber die integrierte Methode ist in der Regel ausreichend.

## Schritt‑für‑Schritt‑Durchgang (H2s mit sekundären Schlüsselwörtern)

### Hugging Face‑Modell automatisch herunterladen

Der Konstruktor `AsposeAIModelConfig` verbirgt die Komplexität der Arbeit mit der Hugging Face‑API. Stellen Sie einfach sicher, dass Sie beim ersten Ausführen des Skripts Internetzugang haben. Danach befindet sich das Modell in `YOUR_DIRECTORY/Models` und nachfolgende Ausführungen starten sofort.

### GPU‑Speicher nach Inferenz freigeben

Wenn Sie dies in einem langfristig laufenden Service (z. B. einer Flask‑API) ausführen, rufen Sie `ai.free_resources()` nach jeder Anfrage auf. Das verhindert Speicherlecks und stellt sicher, dass die nächste Anfrage dieselbe GPU ohne Unterbrechungen wiederverwenden kann.

### OCR‑Fehler mit einem benutzerdefinierten Prompt korrigieren

Unsere Funktion `financial_prompt` gibt ein Dictionary mit einem einzigen Schlüssel `prompt` zurück. Sie können dies an jede Domäne anpassen:

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

Ändern Sie den Funktionsnamen in `ai.set_post_processor(...)` und Sie haben eine **correct OCR errors**‑Pipeline für medizinische Aufzeichnungen.

### Wie man OCR auf mehrseitigen PDFs ausführt

Aspose OCR kann PDFs sofort verarbeiten:

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

Nachdem Sie den Roh‑String erhalten haben, wird derselbe LLM‑Post‑Processor den Text jeder Seite bereinigen. Kein zusätzlicher Code nötig.

### Wenn Sie keine GPU haben – Wie man GPU freigibt (auch ohne eine)

Selbst auf reinen CPU‑Maschinen ist das Aufrufen von `ai.free_resources()` harmlos. Es leert einfach interne Caches, was immer noch RAM freigeben kann. Daher gilt der Hinweis **how to free gpu** universell: immer nach sich selbst aufräumen.

## Häufige Fallstricke & wie wir sie gelöst haben

| Problem | Warum es passiert | Lösung |
|-------|----------------|-----|
| **Out‑of‑Memory auf GPU** | `gpu_layers` ist für Ihre Karte zu hoch eingestellt | Reduzieren Sie `gpu_layers` auf 10 oder 5, lassen Sie den Rest auf der CPU laufen |
| **Modell wird nie heruntergeladen** | Die Unternehmens‑Firewall blockiert HTTPS zu huggingface.co | Laden Sie das Modell manuell in einem anderen Netzwerk herunter und verweisen Sie anschließend `directory_model_path` auf den lokalen Ordner |
| **Zahlen werden beschädigt** | Prompt ist nicht eindeutig genug bezüglich des Beibehaltens von Ziffern | Fügen Sie dem Prompt „preserve all numeric values and currency symbols exactly as they appear“ hinzu |
| `` `free_resources` wirft eine Ausnahme`` | Verwendung einer älteren Aspose OCR‑Version | Aktualisieren Sie auf das neueste `aspose-ocr`‑Paket (pip install --upgrade aspose-ocr) |

## Vollständige Beispiel‑Zusammenfassung

Hier ist das Skript noch einmal, diesmal mit Inline‑Kommentaren, die jede Zeile für die zukünftige Referenz erklären:

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

## Fazit

Wir haben **how to run OCR** mit Aspose behandelt, ein Hugging Face‑Modell bei Bedarf heruntergeladen, einen Prompt erstellt, der **corrects OCR errors** korrigiert, und schließlich **free gpu memory** freigegeben, damit Ihre Workstation reaktionsfähig bleibt. Der gesamte Workflow passt in eine einzige, eigenständige Python‑Datei – keine externen Skripte, keine manuelle Modellverwaltung und keine hängenden GPU‑Allokationen.

Nächste Schritte? Versuchen Sie, den `financial_prompt` zu ersetzen durch ein

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}