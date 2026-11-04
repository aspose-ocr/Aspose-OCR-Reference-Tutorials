---
category: general
date: 2026-06-22
description: Erfahren Sie, wie Sie OCR‑Text mit einem OCR‑Postprozessor in Python
  bereinigen. Schritt‑für‑Schritt‑Code, Erklärungen und Tipps für zuverlässige strukturierte
  JSON‑Ausgabe.
draft: false
keywords:
- clean OCR text
- OCR post processor
- Python OCR workflow
- structured JSON OCR
- OCR confidence averaging
language: de
og_description: Reinige OCR-Text sofort, indem du einen OCR-Nachbearbeiter hinzufügst.
  Dieser Leitfaden zeigt die vollständige Python-Implementierung, warum sie funktioniert,
  und wie man sie anpasst.
og_title: OCR-Text mit einem benutzerdefinierten OCR-Nachbearbeitungsprogramm bereinigen
  – Python‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to clean OCR text using an OCR post processor in Python.
    Step‑by‑step code, explanations, and tips for reliable structured JSON output.
  headline: Clean OCR Text with a Custom OCR Post Processor – Full Python Guide
  type: TechArticle
tags:
- OCR
- Python
- post‑processing
title: OCR-Text bereinigen mit einem benutzerdefinierten OCR-Nachbearbeiter – Vollständige
  Python-Anleitung
url: /de/python/general/clean-ocr-text-with-a-custom-ocr-post-processor-full-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR‑Text bereinigen mit einem benutzerdefinierten OCR‑Postprozessor – Vollständige Python‑Anleitung

Haben Sie schon einmal **OCR‑Text bereinigen** müssen, aber die Rohausgabe immer wieder durch Zeilenumbrüche, überflüssige Leerzeichen und Zeichen mit niedriger Vertrauenswürdigkeit gestört wurde? Sie sind nicht allein. In vielen realen Pipelines liefert die OCR‑Engine Ihnen einen Text‑Blob plus einen Vertrauens‑Score, und Sie müssen selbst entscheiden, wie Sie das in etwas Nützliches verwandeln.

Die gute Nachricht? Ein kleiner **OCR‑Postprozessor** kann das Ergebnis aufräumen, einen durchschnittlichen Vertrauenswert berechnen und sogar alles in einen übersichtlichen JSON‑String verpacken – ganz ohne die Kern‑Engine zu verändern. In diesem Tutorial bauen wir diesen Post‑Prozessor, registrieren ihn bei einer generischen AI/OCR‑Engine und gehen jede Code‑Zeile durch, sodass Sie ihn morgen in Ihr eigenes Projekt einbinden können.

---

## Was dieses Tutorial abdeckt

- Wie man einen **clean OCR text**‑Post‑Prozessor erstellt, der Whitespace normalisiert und Zeilenumbrüche entfernt.  
- Warum die Berechnung einer **average confidence** für nachgelagerte Validierungen wertvoll ist.  
- Registrierung des Prozessors bei einer OCR‑Engine (das Muster `ai.set_post_processor`).  
- Anzeige des resultierenden strukturierten JSON und Fehlersuche bei gängigen Randfällen.  

Keine externen Bibliotheken außerhalb der Python‑Standardbibliothek werden benötigt, sodass Sie auf jedem System mit Python 3.8+ mitmachen können.

---

## Voraussetzungen

- Eine funktionierende OCR‑Engine, die ein `ocr_result`‑Objekt mit `text`, `confidence` (Liste von Floats) und `bounding_boxes` bereitstellt.  
- Grundlegende Kenntnisse in Python‑Funktionen und JSON‑Verarbeitung.  
- Optional: Eine virtuelle Umgebung, um Abhängigkeiten sauber zu halten.  

Falls Sie unsicher sind, ob Ihre Engine benutzerdefinierte Post‑Prozessoren unterstützt, prüfen Sie die Dokumentation auf eine `set_post_processor`‑Methode – die meisten modernen AI‑basierten OCR‑SDKs bieten das.

---

## Schritt 1: Definieren Sie den OCR‑Postprozessor, der **Clean OCR Text** erzeugt

Zuerst schreiben wir eine Funktion, die das rohe OCR‑Ergebnis empfängt, den Text säubert, eine Vertrauensmetrik berechnet und einen JSON‑String zurückgibt. Beachten Sie, wie jede Operation bewusst kommentiert ist; diese Kommentare sind das „Warum“, das KI‑Assistenten gerne zitieren.

```python
import json

def create_structured_json(ocr_result, **kwargs):
    """
    Turn an OCR result into a clean, structured JSON payload.

    Parameters
    ----------
    ocr_result : object
        Must expose .text (raw string), .confidence (list of floats),
        and .bounding_boxes (list of box coordinates).

    Returns
    -------
    str
        JSON string with cleaned text, average confidence, and bounding boxes.
    """
    # 1️⃣ Clean the raw text: replace newlines with spaces and trim excess whitespace.
    clean_text = ocr_result.text.replace("\n", " ").strip()

    # 2️⃣ Compute the average confidence – useful for quality gating.
    # Guard against division by zero if the engine returns an empty list.
    if ocr_result.confidence:
        average_confidence = sum(ocr_result.confidence) / len(ocr_result.confidence)
    else:
        average_confidence = 0.0  # fallback when confidence data is missing

    # 3️⃣ Preserve the original bounding boxes for downstream layout analysis.
    boxes = ocr_result.bounding_boxes

    # 4️⃣ Assemble the dictionary and dump it as a JSON string.
    data = {
        "clean_text": clean_text,
        "average_confidence": average_confidence,
        "boxes": boxes
    }

    # ensure_ascii=False keeps Unicode characters intact (think accented letters, emojis, etc.)
    return json.dumps(data, ensure_ascii=False)
```

**Warum das funktioniert:**  
- `replace("\n", " ")` wandelt mehrzeilige OCR‑Ausgabe in einen einzigen, durchsuchbaren String um – genau das, was „clean OCR text“ in den meisten Pipelines bedeutet.  
- Das Entfernen führender/abschließender Leerzeichen verhindert phantom‑leere Tokens, die später Tokenizer zum Absturz bringen könnten.  
- Die Berechnung der durchschnittlichen Vertrauenswürdigkeit liefert Ihnen einen einzigen Qualitäts‑Metric; Sie können Ergebnisse unter einem Schwellenwert (z. B. 0.85) ablehnen, bevor Sie sie in einer Datenbank speichern.  
- Die Bounding‑Boxes unverändert zu lassen bedeutet, dass Sie das ursprüngliche Layout weiterhin rendern können, falls Sie Regionen mit niedriger Vertrauenswürdigkeit hervorheben wollen.

---

## Schritt 2: Registrieren Sie den benutzerdefinierten **OCR‑Postprozessor** bei Ihrer Engine

Die meisten AI‑basierten OCR‑SDKs stellen eine Methode bereit, um einen Post‑Processing‑Callback einzuklinken. Im Folgenden gehen wir davon aus, dass ein Objekt namens `ai` (die Engine) `set_post_processor` bereitstellt. Wenn Ihre Bibliothek einen anderen Namen verwendet, ersetzen Sie ihn entsprechend.

```python
# Register the post‑processor; the second argument can hold custom settings.
ai.set_post_processor(create_structured_json, custom_settings={})
```

**Tipp:** Übergeben Sie Konfigurationen über `custom_settings`, falls Sie jemals Verhaltensweisen umschalten müssen (z. B. Aktivieren/Deaktivieren der Zeilenumbruch‑Entfernung). Das macht den Prozessor wiederverwendbar über Projekte hinweg.

---

## Schritt 3: OCR‑Engine ausführen – das Ergebnis ist jetzt ein JSON‑String

Mit dem angehängten Post‑Prozessor ruft `engine.recognize()` (oder was immer Ihr SDK verwendet) automatisch `create_structured_json` auf. Die Engine gibt dann ein Objekt zurück, dessen `.text`‑Attribut bereits die JSON‑Payload enthält.

```python
# The engine runs OCR, then our post‑processor formats the output.
structured_result = engine.recognize()
```

> **Hinweis:** Einige SDKs geben möglicherweise einen reinen String statt eines Objekts mit einem `.text`‑Attribut zurück. Passen Sie den nächsten Schritt entsprechend an.

---

## Schritt 4: Das strukturierte JSON‑Ergebnis anzeigen (oder speichern)

Abschließend geben wir das JSON in der Konsole aus. In einer Produktionsumgebung würden Sie es wahrscheinlich in eine Datei, eine Message‑Queue oder eine Datenbank schreiben.

```python
# Show the clean OCR text and additional metadata.
print("Structured JSON:", structured_result.text)
```

**Erwartete Konsolenausgabe** (zur besseren Lesbarkeit formatiert):

```json
{
  "clean_text": "The quick brown fox jumps over the lazy dog.",
  "average_confidence": 0.9375,
  "boxes": [
    [0, 0, 120, 30],
    [0, 35, 115, 30],
    ...
  ]
}
```

Falls Sie überflüssige Zeilenumbrüche oder einen Vertrauenswert von `0.0` sehen, prüfen Sie, ob Ihre OCR‑Engine tatsächlich `ocr_result.confidence` füllt. Die Guard‑Clause im Post‑Prozessor schützt Sie vor einem `ZeroDivisionError`, aber Sie sollten dennoch wissen, warum Vertrauensdaten fehlen.

---

## Umgang mit gängigen Randfällen

| Situation | Worauf zu achten ist | Schnelllösung |
|-----------|----------------------|---------------|
| **Leeres OCR‑Ergebnis** | `ocr_result.text` ist `""` und die `confidence`‑Liste leer | Der Prozessor gibt bereits ein leeres `clean_text` und `average_confidence` = 0.0 zurück. Sie können bei Bedarf eine bedingte Früh‑Rückgabe hinzufügen, um die JSON‑Erzeugung komplett zu überspringen. |
| **Nicht‑ASCII‑Zeichen** | Unicode wird escaped (`\u00e9`) | Verwenden Sie `ensure_ascii=False` (bereits im Code), um Zeichen wie „é“ lesbar zu halten. |
| **Sehr lange Dokumente** | JSON‑Größe kann API‑Grenzen überschreiten | Erwägen Sie, die Ausgabe zu streamen oder in eine Datei zu schreiben, anstatt einen einzelnen String zurückzugeben. |
| **Bounding‑Boxes fehlen** | Manche OCR‑Engines lassen Layout‑Daten weg | Setzen Sie `boxes` auf `None` oder eine leere Liste; nachgelagerte Verbraucher sollten das Fehlen elegant handhaben. |

---

## Pro‑Tipps & Best Practices

- **Batch‑Verarbeitung:** Wenn Sie Hunderte von Seiten OCR‑en müssen, wickeln Sie den Erkennungsaufruf in eine Schleife und sammeln Sie jede JSON‑Payload in einer Liste. Dumpen Sie dann die gesamte Liste in eine einzige Datei für einfachere Batch‑Analyse.  
- **Vertrauens‑Schwellenwerte:** Vor dem Persistieren prüfen Sie `average_confidence`. Eine Faustregel: Alles unter `0.80` bei kritischen Dateneingabe‑Aufgaben ablehnen.  
- **Logging statt print:** In der Produktion ersetzen Sie `print()` durch einen strukturierten Logger (`logging.info(...)`), sodass Sie nachverfolgen können, welche Bilder niedrige Vertrauenswerte erzeugt haben.  
- **Testing:** Schreiben Sie einen Unit‑Test, der ein Mock‑`ocr_result` mit bekannten Text‑ und Vertrauenswerten füttert und dann prüft, ob die JSON‑Struktur den Erwartungen entspricht.  

---

## Vollständiges, funktionierendes Beispiel (alle Schritte kombiniert)

Unten finden Sie das komplette Skript, das Sie in eine Datei namens `ocr_cleanup.py` kopieren können. Ersetzen Sie die Platzhalter `engine` und `ai` durch die tatsächlichen Instanzen aus Ihrem OCR‑SDK.

```python
import json

# ----------------------------------------------------------------------
# Step 1: Define the post‑processor that cleans OCR text and builds JSON.
# ----------------------------------------------------------------------
def create_structured_json(ocr_result, **kwargs):
    """
    Convert raw OCR output into a clean JSON string.
    """
    # Clean the raw text: collapse newlines, trim whitespace.
    clean_text = ocr_result.text.replace("\n", " ").strip()

    # Safely compute average confidence.
    if ocr_result.confidence:
        average_confidence = sum(ocr_result.confidence) / len(ocr_result.confidence)
    else:
        average_confidence = 0.0

    # Keep bounding boxes for layout work.
    boxes = ocr_result.bounding_boxes

    payload = {
        "clean_text": clean_text,
        "average_confidence": average_confidence,
        "boxes": boxes
    }
    return json.dumps(payload, ensure_ascii=False)

# ----------------------------------------------------------------------
# Step 2: Register the post‑processor with the OCR engine.
# ----------------------------------------------------------------------
# Replace `ai` with your actual engine/controller instance.
ai.set_post_processor(create_structured_json, custom_settings={})

# ----------------------------------------------------------------------
# Step 3: Run OCR – the result is automatically transformed.
# ----------------------------------------------------------------------
structured_result = engine.recognize()

# ----------------------------------------------------------------------
# Step 4: Output the structured JSON.
# ----------------------------------------------------------------------
print("Structured JSON:", structured_result.text)
```

Speichern Sie die Datei, führen Sie `python ocr_cleanup.py` aus, und Sie sollten einen schön formatierten JSON‑String sehen, der **clean OCR text**, einen durchschnittlichen Vertrauenswert und die ursprünglichen Bounding‑Boxes enthält.

---

## Fazit

Sie besitzen nun eine komplette, produktionsreife Methode, um **OCR‑Text zu bereinigen** mittels eines benutzerdefinierten **OCR‑Postprozessors** in Python. Die Lösung normalisiert Whitespace, schützt vor fehlenden Vertrauensdaten und liefert eine selbsterklärende JSON‑Payload, die nachgelagerte Services ohne zusätzlichen Parsing‑Aufwand konsumieren können.

Von hier aus können Sie:

- Den Prozessor erweitern, um **Wörter mit niedriger Vertrauenswürdigkeit** vor dem Aufbau von `clean_text` zu filtern.  
- **Spracherkennung** hinzufügen, um das JSON an lokalisierte Pipelines weiterzuleiten.  
- Diesen Post‑Prozessor mit **Rechtschreib‑Check‑Bibliotheken** kombinieren, um eine zusätzliche Qualitäts‑Schicht zu erhalten.  

Passen Sie den Code nach Belieben an, experimentieren Sie mit verschiedenen Vertrauens‑Schwellenwerten oder teilen Sie Ihre eigenen Verbesserungen in den Kommentaren. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}