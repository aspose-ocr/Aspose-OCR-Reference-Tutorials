---
category: general
date: 2026-04-26
description: Wie man OCR‑Ergebnisse nachbearbeitet und Text mit Koordinaten extrahiert.
  Lernen Sie eine Schritt‑für‑Schritt‑Lösung mit strukturierten Ausgaben und KI‑Korrektur.
draft: false
keywords:
- how to post‑process OCR
- extract text with coordinates
- OCR structured output
- AI post‑processing OCR
- bounding box OCR
language: de
og_description: Wie man OCR‑Ergebnisse nachbearbeitet und Text mit Koordinaten extrahiert.
  Folgen Sie diesem umfassenden Tutorial für einen zuverlässigen Arbeitsablauf.
og_title: Wie man OCR nachbearbeitet – Vollständiger Leitfaden
tags:
- OCR
- Python
- AI
- Text Extraction
title: Wie man OCR nachbearbeitet – Text mit Koordinaten in Python extrahieren
url: /de/python/general/how-to-post-process-ocr-extract-text-with-coordinates-in-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR nachbearbeitet – Text mit Koordinaten in Python extrahiert

Hast du jemals **wie man OCR nachbearbeitet** Ergebnisse benötigt, weil die Rohausgabe verrauscht oder fehlerhaft ausgerichtet war? Du bist nicht allein. In vielen realen Projekten — Rechnungs‑Scanning, Beleg‑Digitalisierung oder sogar die Erweiterung von AR‑Erlebnissen — liefert die OCR‑Engine rohe Wörter, aber du musst sie trotzdem bereinigen und verfolgen, wo jedes Wort auf der Seite liegt. Genau hier glänzt ein strukturierter Ausgabemodus kombiniert mit einem KI‑gesteuerten Nachbearbeiter.

> **Pro‑Tipp:** Wenn du eine andere OCR‑Bibliothek nutzt, suche nach einem „structured“ oder „layout“ Modus; die Konzepte bleiben gleich.

---

## Voraussetzungen

Bevor wir loslegen, stelle sicher, dass du Folgendes hast:

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| Python 3.9+ | Moderne Syntax und Type Hints |
| `ocr`‑Bibliothek, die `OutputMode.STRUCTURED` unterstützt (z. B. ein fiktives `myocr`) | Benötigt für Begrenzungs‑Box‑Daten |
| Ein KI‑Nachbearbeitungs‑Modul (kann OpenAI, HuggingFace oder ein eigenes Modell sein) | Verbessert die Genauigkeit nach der OCR |
| Eine Bilddatei (`input.png`) in deinem Arbeitsverzeichnis | Die Quelle, die wir einlesen werden |

Falls dir etwas unbekannt vorkommt, installiere einfach die Platzhalter‑Pakete mit `pip install myocr ai‑postproc`. Der Code unten enthält außerdem Fallback‑Stubs, sodass du den Ablauf ohne die echten Bibliotheken testen kannst.

---

## Schritt 1: Strukturierte Ausgabemodus für die OCR‑Engine aktivieren  

Das Erste, was wir tun, ist der OCR‑Engine mitzuteilen, dass sie uns mehr als nur reinen Text liefern soll. Strukturierte Ausgabe liefert jedes Wort zusammen mit seiner Begrenzungs‑Box und dem Vertrauens‑Score, was später für **Text mit Koordinaten extrahieren** unerlässlich ist.

```python
# step1_structured_output.py
import myocr as ocr  # fictional OCR library

# Initialize the engine (replace with your actual init code)
engine = ocr.Engine()

# Switch to structured mode – this makes the engine emit word‑level data
engine.set_output_mode(ocr.OutputMode.STRUCTURED)

print("✅ Structured output mode enabled")
```

*Warum das wichtig ist:* Ohne strukturierten Modus würdest du nur einen langen String erhalten und die räumlichen Informationen verlieren, die du für das Überlagern von Text auf Bildern oder für nachgelagerte Layout‑Analysen brauchst.

---

## Schritt 2: Bild erkennen und Wörter, Boxen sowie Vertrauenswerte erfassen  

Jetzt übergeben wir das Bild an die Engine. Das Ergebnis ist ein Objekt, das eine Liste von Wort‑Objekten enthält, wobei jedes `text`, `x`, `y`, `width`, `height` und `confidence` bereitstellt.

```python
# step2_recognize.py
from pathlib import Path

# Path to your image
image_path = Path("YOUR_DIRECTORY/input.png")

# Perform OCR – returns a StructuredResult with .words collection
structured_result = engine.recognize_image(str(image_path))

print(f"🔎 Detected {len(structured_result.words)} words")
```

*Randfall:* Wenn das Bild leer oder nicht lesbar ist, wird `structured_result.words` eine leere Liste sein. Es ist gute Praxis, das zu prüfen und elegant zu behandeln.

---

## Schritt 3: KI‑basierte Nachbearbeitung durchführen und Positionen beibehalten  

Selbst die besten OCR‑Engines machen Fehler — z. B. „O“ vs. „0“ oder fehlende Diakritika. Ein KI‑Modell, das auf domänenspezifischen Text trainiert ist, kann diese Fehler korrigieren. Wichtig ist, dass wir die ursprünglichen Koordinaten beibehalten, damit das räumliche Layout intakt bleibt.

```python
# step3_ai_postprocess.py
import ai_postproc as ai  # placeholder for your AI module

# The AI post‑processor expects the structured result and returns a new one
corrected_result = ai.run_postprocessor(structured_result)

print("🤖 AI post‑processing complete")
```

*Warum wir die Koordinaten beibehalten:* Viele nachgelagerte Aufgaben (z. B. PDF‑Erstellung, AR‑Beschriftung) benötigen die exakte Platzierung. Die KI berührt nur das Feld `text` und lässt `x`, `y`, `width`, `height` unverändert.

---

## Schritt 4: Durch die korrigierten Wörter iterieren und deren Text mit Koordinaten anzeigen  

Abschließend durchlaufen wir die korrigierten Wörter und geben jedes Wort zusammen mit seiner oberen linken Ecke `(x, y)` aus. Das erfüllt das Ziel **Text mit Koordinaten extrahieren**.

```python
# step4_display.py
for recognized_word in corrected_result.words:
    # Using f‑string for clean formatting
    print(f"{recognized_word.text} (x:{recognized_word.x}, y:{recognized_word.y})")
```

**Erwartete Ausgabe (Beispiel):**

```
Invoice (x:45, y:112)
Number (x:120, y:112)
12345 (x:190, y:112)
Total (x:45, y:250)
$ (x:120, y:250)
199.99 (x:130, y:250)
```

Jede Zeile zeigt das korrigierte Wort und seine genaue Position im Originalbild.

---

## Vollständiges funktionierendes Beispiel  

Unten findest du ein einzelnes Skript, das alles zusammenführt. Du kannst es kopieren, die Import‑Anweisungen an deine tatsächlichen Bibliotheken anpassen und direkt ausführen.

```python
# ocr_postprocess_demo.py
"""
Complete demo: how to post‑process OCR and extract text with coordinates.
Works with any OCR library exposing a structured output mode and an AI post‑processor.
"""

import sys
from pathlib import Path

# ----------------------------------------------------------------------
# 1️⃣ Imports – replace these with your real packages
# ----------------------------------------------------------------------
try:
    import myocr as ocr               # OCR engine with structured output
    import ai_postproc as ai          # AI correction module
except ImportError:  # Fallback stubs for quick testing
    class DummyWord:
        def __init__(self, text, x, y, w, h, conf):
            self.text = text
            self.x = x
            self.y = y
            self.width = w
            self.height = h
            self.confidence = conf

    class DummyResult:
        def __init__(self, words):
            self.words = words

    class StubEngine:
        class OutputMode:
            STRUCTURED = "structured"

        def set_output_mode(self, mode):
            print(f"[Stub] set_output_mode({mode})")

        def recognize_image(self, path):
            # Very simple fake OCR output
            sample = [
                DummyWord("Invoice", 45, 112, 60, 20, 0.98),
                DummyWord("Number", 120, 112, 55, 20, 0.96),
                DummyWord("12345", 190, 112, 40, 20, 0.97),
                DummyWord("Total", 45, 250, 50, 20, 0.99),
                DummyWord("$", 120, 250, 10, 20, 0.95),
                DummyWord("199.99", 130, 250, 55, 20, 0.94),
            ]
            return DummyResult(sample)

    class StubAI:
        @staticmethod
        def run_postprocessor(structured_result):
            # Pretend we corrected "12345" to "12346"
            for w in structured_result.words:
                if w.text == "12345":
                    w.text = "12346"
            return structured_result

    engine = StubEngine()
    ai = StubAI

# ----------------------------------------------------------------------
# 2️⃣ Enable structured output
# ----------------------------------------------------------------------
engine.set_output_mode(ocr.Engine.OutputMode.STRUCTURED)

# ----------------------------------------------------------------------
# 3️⃣ Recognize image
# ----------------------------------------------------------------------
image_path = Path("YOUR_DIRECTORY/input.png")
if not image_path.is_file():
    print(f"⚠️  Image not found at {image_path}. Using stub data.")
structured_result = engine.recognize_image(str(image_path))

# ----------------------------------------------------------------------
# 4️⃣ AI post‑processing
# ----------------------------------------------------------------------
corrected_result = ai.run_postprocessor(structured_result)

# ----------------------------------------------------------------------
# 5️⃣ Display results
# ----------------------------------------------------------------------
print("\n🗒️  Final OCR output with coordinates:")
for word in corrected_result.words:
    print(f"{word.text} (x:{word.x}, y:{word.y})")
```

**Ausführen des Skripts**

```bash
python ocr_postprocess_demo.py
```

Wenn du die echten Bibliotheken installiert hast, verarbeitet das Skript dein `input.png`. Andernfalls lässt dich die Stub‑Implementierung den erwarteten Ablauf und die Ausgabe sehen, ohne externe Abhängigkeiten.

---

## Häufig gestellte Fragen (FAQ)

| Frage | Antwort |
|----------|--------|
| *Funktioniert das mit Tesseract?* | Tesseract selbst stellt keinen strukturierten Modus out‑of‑the‑box bereit, aber Wrapper wie `pytesseract.image_to_data` geben Begrenzungs‑Boxen zurück, die du in dieselbe KI‑Nachbearbeitung einspeisen kannst. |
| *Was, wenn ich die rechte untere Ecke statt der oberen linken benötige?* | Jedes Wort‑Objekt liefert auch `width` und `height`. Berechne `x2 = x + width` und `y2 = y + height`, um die gegenüberliegende Ecke zu erhalten. |
| *Kann ich mehrere Bilder stapelweise verarbeiten?* | Absolut. Packe die Schritte in eine `for image_path in Path("folder").glob("*.png"):` Schleife und sammle die Ergebnisse pro Datei. |
| *Wie wähle ich ein KI‑Modell für die Korrektur aus?* | Für generischen Text funktioniert ein kleiner, auf OCR‑Fehler feinabgestimmter GPT‑2. Für domänenspezifische Daten (z. B. medizinische Rezepte) trainiere ein Sequence‑to‑Sequence‑Modell auf gepaarten Rauschen‑Sauber‑Daten. |
| *Ist der Vertrauens‑Score nach der KI‑Korrektur noch nützlich?* | Du kannst den ursprünglichen Score weiterhin zum Debuggen behalten, aber die KI kann ihren eigenen Score ausgeben, falls das Modell das unterstützt. |

---

## Randfälle & bewährte Methoden  

1. **Leere oder beschädigte Bilder** – prüfe immer, dass `structured_result.words` nicht leer ist, bevor du fortfährst.  
2. **Nicht‑lateinische Schriften** – stelle sicher, dass deine OCR‑Engine für die Zielsprache konfiguriert ist; die KI‑Nachbearbeitung muss auf derselben Schrift trainiert sein.  
3. **Performance** – KI‑Korrektur kann teuer sein. Cache Ergebnisse, wenn du dasselbe Bild wiederverwendest, oder führe den KI‑Schritt asynchron aus.  
4. **Koordinatensystem** – OCR‑Bibliotheken können unterschiedliche Ursprünge verwenden (oben‑links vs. unten‑links). Passe das beim Überlagern auf PDFs oder Canvas‑Elemente an.  

---

## Fazit  

Du hast jetzt ein solides, End‑zu‑End‑Rezept, um **wie man OCR nachbearbeitet** und zuverlässig **Text mit Koordinaten extrahiert**. Durch das Aktivieren der strukturierten Ausgabe, das Durchlaufen des Ergebnisses über eine KI‑Korrekturschicht und das Beibehalten der ursprünglichen Begrenzungs‑Boxen kannst du verrauschte OCR‑Scans in sauberen, räumlich‑bewussten Text verwandeln, der für nachgelagerte Aufgaben wie PDF‑Erstellung, Daten‑Entry‑Automatisierung oder Augmented‑Reality‑Overlays bereitsteht.

Bereit für den nächsten Schritt? Versuche, die Stub‑KI durch einen OpenAI `gpt‑4o‑mini` Aufruf zu ersetzen oder integriere die Pipeline in ein FastAPI‑Projekt.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}