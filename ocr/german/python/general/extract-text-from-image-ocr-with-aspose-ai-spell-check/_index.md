---
category: general
date: 2026-05-03
description: Extrahiere Text aus einem Bild mit Aspose OCR und KI‑Rechtschreibprüfung.
  Lerne, wie man ein Bild OCRt, das Bild für OCR lädt, Text aus einer Rechnung erkennt
  und GPU‑Ressourcen freigibt.
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: de
og_description: Text aus Bild mit Aspose OCR und KI‑Rechtschreibprüfung extrahieren.
  Schritt‑für‑Schritt‑Anleitung, wie man ein Bild OCRt, das Bild für OCR lädt und
  GPU‑Ressourcen freigibt.
og_title: Text aus Bild extrahieren – Vollständiger OCR‑ und Rechtschreibprüfungs‑Leitfaden
tags:
- OCR
- Aspose
- AI
- Python
title: Text aus Bild extrahieren – OCR mit Aspose KI‑Rechtschreibprüfung
url: /de/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild extrahieren – Komplett‑OCR‑ & Rechtschreib‑Check‑Leitfaden

Haben Sie schon einmal **Text aus einem Bild extrahieren** müssen, waren sich aber nicht sicher, welche Bibliothek sowohl Geschwindigkeit als auch Genauigkeit liefert? Sie sind nicht allein. In vielen Praxis‑Projekten – denken Sie an Rechnungs‑Verarbeitung, Beleg‑Digitalisierung oder das Scannen von Verträgen – ist das Sauber‑machen von durchsuchbarem Text aus einem Bild die erste Hürde.

Die gute Nachricht: Aspose OCR in Kombination mit einem leichten Aspose AI‑Modell erledigt diese Aufgabe in wenigen Zeilen Python. In diesem Tutorial zeigen wir **wie man ein Bild OCR‑t**, das Bild korrekt lädt, einen integrierten Rechtschreib‑Check‑Post‑Processor ausführt und schließlich **GPU‑Ressourcen freigibt**, damit Ihre Anwendung speichereffizient bleibt.

Am Ende dieses Leitfadens können Sie **Text aus Rechnungs‑Bildern erkennen**, gängige OCR‑Fehler automatisch korrigieren und Ihre GPU für den nächsten Durchlauf sauber halten.

---

## Was Sie benötigen

- Python 3.9 oder neuer (der Code verwendet Typ‑Hints, funktioniert aber auch mit früheren 3.x‑Versionen)
- `aspose-ocr` und `aspose-ai` Pakete (Installation via `pip install aspose-ocr aspose-ai`)
- Eine CUDA‑fähige GPU ist optional; das Skript greift auf die CPU zurück, wenn keine gefunden wird.
- Ein Beispielbild, z. B. `sample_invoice.png`, das in einem Ordner liegt, den Sie referenzieren können.

Keine schweren ML‑Frameworks, keine massiven Modell‑Downloads – nur ein kleines Q4‑K‑M‑quantisiertes Modell, das bequem auf den meisten GPUs passt.

---

## Schritt 1: OCR‑Engine initialisieren – Text aus Bild extrahieren

Zuerst erstellen Sie eine `OcrEngine`‑Instanz und geben an, welche Sprache Sie erwarten. Hier wählen wir Englisch und verlangen reine Textausgabe, was ideal für nachgelagerte Verarbeitung ist.

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**Warum das wichtig ist:** Das Setzen der Sprache begrenzt den Zeichensatz und verbessert die Genauigkeit. Der Nur‑Text‑Modus entfernt Layout‑Informationen, die Sie normalerweise nicht benötigen, wenn Sie einfach nur Text aus einem Bild extrahieren wollen.

---

## Schritt 2: Bild für OCR laden – wie man ein Bild OCR‑t

Jetzt übergeben wir der Engine ein echtes Bild. Der Helfer `Image.load` versteht gängige Formate (PNG, JPEG, TIFF) und abstrahiert Date‑I/O‑Eigenheiten.

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**Tipp:** Wenn Ihre Quellbilder groß sind, sollten Sie sie vor dem Übergeben an die Engine verkleinern; kleinere Abmessungen reduzieren den GPU‑Speicherverbrauch, ohne die Erkennungsqualität zu beeinträchtigen.

---

## Schritt 3: Aspose‑AI‑Modell konfigurieren – Text aus Rechnung erkennen

Aspose AI liefert ein winziges GGUF‑Modell, das Sie automatisch herunterladen können. Das Beispiel nutzt das Repository `Qwen2.5‑3B‑Instruct‑GGUF`, quantisiert zu `q4_k_m`. Außerdem weisen wir die Laufzeit an, 20 Schichten auf der GPU zu reservieren, was Geschwindigkeit und VRAM‑Nutzung ausbalanciert.

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**Im Hintergrund:** Das quantisierte Modell belegt etwa 1,5 GB auf der Festplatte – ein Bruchteil eines Voll‑Präzisions‑Modells, reicht aber aus, um typische OCR‑Rechtschreibfehler zu erkennen.

---

## Schritt 4: AsposeAI initialisieren und den Rechtschreib‑Check‑Post‑Processor anhängen

Aspose AI enthält einen fertigen Rechtschreib‑Check‑Post‑Processor. Durch das Anhängen wird jedes OCR‑Ergebnis automatisch bereinigt.

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**Warum den Post‑Processor nutzen?** OCR‑Engines lesen häufig „Invoice“ als „Invo1ce“ oder „Total“ als „T0tal“. Der Rechtschreib‑Check läuft ein leichtes Sprachmodell über den Roh‑String und korrigiert diese Fehler, ohne dass Sie ein eigenes Wörterbuch schreiben müssen.

---

## Schritt 5: Rechtschreib‑Check‑Post‑Processor auf das OCR‑Ergebnis anwenden

Mit allem verkabelt, liefert ein einziger Aufruf den korrigierten Text. Wir geben sowohl die Original‑ als auch die bereinigte Version aus, damit Sie die Verbesserung sehen können.

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

Typische Ausgabe für eine Rechnung könnte so aussehen:

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

Beachten Sie, wie „Invo1ce“ in das korrekte Wort „Invoice“ umgewandelt wurde. Das ist die Kraft des integrierten KI‑Rechtschreib‑Checks.

---

## Schritt 6: GPU‑Ressourcen freigeben – GPU‑Ressourcen sicher freigeben

Wenn Sie das in einem langlebigen Service (z. B. einer Web‑API, die Dutzende Rechnungen pro Minute verarbeitet) ausführen, müssen Sie den GPU‑Kontext nach jedem Batch freigeben. Andernfalls entstehen Speicher‑Leaks und schließlich „CUDA out of memory“-Fehler.

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**Pro‑Tipp:** Rufen Sie `free_resources()` in einem `finally`‑Block oder einem Context‑Manager auf, sodass er immer ausgeführt wird, selbst wenn eine Ausnahme auftritt.

---

## Vollständiges funktionierendes Beispiel

Alle Bausteine zusammen ergeben ein eigenständiges Skript, das Sie in jedes Projekt einbinden können.

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

Speichern Sie die Datei, passen Sie den Pfad zu Ihrem Bild an und führen Sie `python extract_text_from_image.py` aus. Sie sollten den bereinigten Rechnungstext in der Konsole sehen.

---

## Häufig gestellte Fragen (FAQ)

**F: Funktioniert das auf reinen CPU‑Maschinen?**  
A: Absolut. Wird keine GPU erkannt, fällt Aspose AI auf CPU‑Ausführung zurück, ist jedoch langsamer. Sie können die CPU erzwingen, indem Sie `model_cfg.gpu_layers = 0` setzen.

**F: Was, wenn meine Rechnungen in einer anderen Sprache als Englisch vorliegen?**  
A: Ändern Sie `ocr_engine.language` auf den entsprechenden Enum‑Wert (z. B. `aocr.Language.Spanish`). Das Rechtschreib‑Check‑Modell ist mehrsprachig, aber Sie erhalten möglicherweise bessere Ergebnisse mit einem sprachspezifischen Modell.

**F: Kann ich mehrere Bilder in einer Schleife verarbeiten?**  
A: Ja. Platzieren Sie die Lade‑, Erkennungs‑ und Post‑Processing‑Schritte einfach in einer `for`‑Schleife. Denken Sie daran, `ocr_ai.free_resources()` nach der Schleife oder nach jedem Batch aufzurufen, wenn Sie dieselbe AI‑Instanz wiederverwenden.

**F: Wie groß ist der Modell‑Download?**  
A: Etwa 1,5 GB für die quantisierte `q4_k_m`‑Version. Nach dem ersten Lauf wird er zwischengespeichert, sodass nachfolgende Ausführungen sofort starten.

---

## Fazit

In diesem Tutorial haben wir gezeigt, wie man **Text aus Bild extrahiert** mit Aspose OCR, ein kleines KI‑Modell konfiguriert, einen Rechtschreib‑Check‑Post‑Processor anwendet und sicher **GPU‑Ressourcen freigibt**. Der Workflow deckt alles ab – vom Laden des Bildes bis zum Aufräumen – und liefert Ihnen eine zuverlässige Pipeline für **Text aus Rechnung erkennen**‑Szenarien.

Nächste Schritte? Ersetzen Sie den Rechtschreib‑Check durch ein benutzerdefiniertes Entity‑Extraction‑Modell

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}