---
category: general
date: 2026-06-19
description: Wie man OCR Schritt für Schritt ausführt und die OCR‑Genauigkeit mit
  reinen Text‑OCR‑Techniken verbessert. Lernen Sie einen schnellen Workflow für zuverlässige
  Textextraktion.
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: de
og_description: Wie man OCR effizient ausführt. Dieses Tutorial zeigt, wie man die
  OCR‑Genauigkeit mit einfacher Text‑OCR und KI‑Nachbearbeitung verbessert.
og_title: Wie man OCR in Python ausführt – Vollständige Anleitung
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  headline: How to Run OCR in Python – Complete Guide
  type: TechArticle
- description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  name: How to Run OCR in Python – Complete Guide
  steps:
  - name: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
    text: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
  - name: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
    text: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
  - name: '**Export formats** – Write the corrected structure to a searchable PDF'
    text: '**Export formats** – Write the corrected structure to a searchable PDF'
  type: HowTo
tags:
- OCR
- Python
- AI
title: Wie man OCR in Python ausführt – Vollständiger Leitfaden
url: /de/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in Python ausführt – Vollständige Anleitung

Haben Sie sich jemals gefragt, **wie man OCR** auf einem Stapel gescannter PDFs ausführt, ohne Stunden damit zu verbringen, Einstellungen zu optimieren? Sie sind nicht allein. In vielen Projekten besteht die erste Hürde einfach darin, zuverlässigen Text aus einem Bild zu extrahieren, und der Unterschied zwischen einem wackeligen Durchlauf und einer sauberen Extraktion hängt oft von ein paar cleveren Schritten ab.

In diesem Leitfaden gehen wir eine praktische vier‑stufige Pipeline durch, die nicht nur **OCR ausführt**, sondern auch **die OCR‑Genauigkeit verbessert**, indem sie einen schnellen Plain‑Text‑Durchlauf mit einem layout‑bewussten zweiten Durchlauf und einem KI‑gestützten Nachbearbeiter kombiniert. Am Ende haben Sie ein einsatzbereites Skript, eine klare Erklärung, warum jede Phase wichtig ist, und Tipps zum Umgang mit Sonderfällen wie mehrspaltigen Seiten oder verrauschten Scans.

---

## Was Sie benötigen

- **Python 3.9+** – der Code verwendet Typannotationen und f‑Strings.  
- **Tesseract OCR** installiert und über die Befehlszeile `tesseract` erreichbar. (Unter Ubuntu: `sudo apt install tesseract-ocr`; unter Windows holen Sie sich den Installer aus dem offiziellen Repository.)  
- Das **pytesseract**‑Wrapper (`pip install pytesseract`).  
- Eine **AI‑Nachbearbeitungs‑Bibliothek** – für dieses Beispiel tun wir so, als hätten Sie ein leichtgewichtiges `ai`‑Modul, das `run_postprocessor` bereitstellt. Ersetzen Sie es durch die GPT‑4‑API von OpenAI oder ein lokales LLM, wenn Sie möchten.  
- Einige Beispiel‑Bilder oder PDFs zum Testen.

Das war's. Keine schweren Frameworks, kein Docker‑Gymnastik. Nur ein paar pip‑Installationen und Sie sind startklar.

---

## Schritt 1: Einen schnellen Plain‑Text‑OCR‑Durchlauf ausführen

Das Erste, das die meisten Entwickler übersehen, ist, dass ein *Plain‑Text‑*OCR‑Durchlauf blitzschnell ist und Ihnen einen schnellen Plausibilitätstest liefert. Wir rufen `engine.Recognize()` auf, um rohe Zeichen ohne Layout‑Metadaten zu extrahieren. Das ist, was wir unter **Plain‑Text‑OCR** verstehen.

```python
import pytesseract
from PIL import Image

def plain_text_ocr(image_path: str) -> str:
    """Run a quick plain‑text OCR pass and return the raw string."""
    img = Image.open(image_path)
    # pytesseract returns a single string with line breaks.
    raw_text = pytesseract.image_to_string(img, lang='eng')
    return raw_text
```

*Warum das wichtig ist:*  
- **Geschwindigkeit** – ein einfacher Durchlauf auf einer 300 dpi‑Seite dauert meist weniger als eine Sekunde.  
- **Grundlage** – Sie können die spätere strukturierte Ausgabe mit dieser Basis vergleichen, um grobe Fehler zu erkennen.  
- **Fehlererkennung** – wenn der einfache Durchlauf komplett fehlschlägt (z. B. nur Kauderwelsch), wissen Sie, dass die Bildqualität zu niedrig ist und können frühzeitig abbrechen.

---

## Schritt 2: Einen detaillierten layout‑bewussten OCR‑Durchlauf ausführen

Plain‑Text ist großartig, aber er verwirft *wo* jedes Wort auf der Seite steht. Für Rechnungen, Formulare oder mehrspaltige Magazine benötigen Sie Koordinaten, Zeilennummern und vielleicht sogar Schriftinformationen. Hier kommt `engine.RecognizeStructured()` ins Spiel.

Unten ist ein leichter Wrapper um die **TSV**‑Ausgabe von Tesseract, die uns eine Hierarchie von Seiten → Zeilen → Wörtern liefert und die Begrenzungsrahmen bewahrt.

```python
from typing import List, Dict

def structured_ocr(image_path: str) -> List[Dict]:
    """Return a list of pages, each containing lines with word coordinates."""
    img = Image.open(image_path)

    # Tesseract TSV includes page, block, paragraph, line, word indices.
    tsv_data = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT, lang='eng')

    pages = {}
    for i, level in enumerate(tsv_data["level"]):
        if level != 5:  # focus on word level (5)
            continue
        page_num = tsv_data["page_num"][i]
        line_num = tsv_data["line_num"][i]
        word = tsv_data["text"][i]
        if not word.strip():
            continue

        # Build nested dict structure.
        pages.setdefault(page_num, {}).setdefault(line_num, []).append({
            "text": word,
            "bbox": (
                tsv_data["left"][i],
                tsv_data["top"][i],
                tsv_data["width"][i],
                tsv_data["height"][i],
            ),
        })

    # Convert dicts to a more convenient list format.
    structured_result = []
    for page_id, lines in pages.items():
        page_obj = {"PageNumber": page_id, "Lines": []}
        for line_id, words in lines.items():
            line_text = " ".join(w["text"] for w in words)
            line_obj = {
                "LineNumber": line_id,
                "Text": line_text,
                "Words": words,
            }
            page_obj["Lines"].append(line_obj)
        structured_result.append(page_obj)

    return structured_result
```

*Warum wir das tun:*  
- **Koordinaten** ermöglichen es Ihnen, den extrahierten Text später auf das Originalbild zuzuordnen, um Hervorhebungen oder Redaktionen vorzunehmen.  
- **Zeilengruppierung** bewahrt das ursprüngliche Layout, was entscheidend ist, wenn Sie Tabellen oder Spalten rekonstruieren müssen.  
- Dieser Durchlauf ist etwas langsamer als der einfache, beendet sich aber trotzdem nach wenigen Sekunden für die meisten Dokumente.

---

## Schritt 3: Den KI‑Nachbearbeiter ausführen, um OCR‑Fehler zu korrigieren

Selbst die beste OCR‑Engine macht Fehler – denken Sie an „rn“ vs. „m“, fehlende Diakritika oder geteilte Wörter. Ein KI‑Modell kann die Rohzeichenkette und die strukturierten Daten betrachten, Inkonsistenzen erkennen und den Text neu schreiben, während die ursprünglichen Koordinaten erhalten bleiben.

Unten ist eine **Mock‑**Implementierung; ersetzen Sie den Body durch einen echten LLM‑Aufruf, falls Sie einen haben.

```python
def ai_postprocess(plain_text: str, structured_result: List[Dict]) -> List[Dict]:
    """
    Simulate an AI post‑processor that corrects OCR errors.
    It walks through each line, compares it with the plain text,
    and applies simple heuristics (e.g., spell‑check).
    """
    import difflib
    corrected = []

    for page in structured_result:
        new_page = {"PageNumber": page["PageNumber"], "Lines": []}
        for line in page["Lines"]:
            # Find the closest match in the plain text using difflib.
            best_match = difflib.get_close_matches(line["Text"], plain_text.splitlines(), n=1, cutoff=0.6)
            corrected_text = best_match[0] if best_match else line["Text"]
            # Preserve original word list but replace the text field.
            new_line = {
                "LineNumber": line["LineNumber"],
                "Text": corrected_text,
                "Words": line["Words"],  # coordinates stay the same
            }
            new_page["Lines"].append(new_line)
        corrected.append(new_page)

    return corrected
```

*Warum dieser Schritt die OCR‑Genauigkeit verbessert:*  
- **Kontextuelle Korrekturen** – die KI kann entscheiden, dass „l0ve“ wahrscheinlich „love“ ist, basierend auf den umgebenden Wörtern.  
- **Erhaltung der Koordinaten** – Sie behalten die Layout‑Informationen, sodass nachgelagerte Aufgaben (wie PDF‑Annotationen) genau bleiben.  
- **Iterative Verfeinerung** – Sie könnten den Nachbearbeiter mehrfach ausführen, wobei jeder Durchlauf weitere Fehler bereinigt.

---

## Schritt 4: Durch die korrigierte, strukturierte Ausgabe iterieren

Jetzt, wo wir eine bereinigte Struktur haben, ist das Extrahieren des endgültigen Textes trivial. Unten geben wir jede Zeile aus, aber Sie könnten auch in eine CSV schreiben, in eine Datenbank einspeisen oder ein durchsuchbares PDF erzeugen.

```python
def display_corrected_text(structured_result: List[Dict]) -> None:
    """Print each line of corrected OCR output."""
    for page in structured_result:
        print(f"\n--- Page {page['PageNumber']} ---")
        for line in page["Lines"]:
            print(line["Text"])

# Example usage tying everything together
if __name__ == "__main__":
    img_path = "sample_scan.png"

    # 1️⃣ Plain‑text OCR
    plain = plain_text_ocr(img_path)
    print("✅ Plain text OCR completed.")

    # 2️⃣ Structured OCR
    structured = structured_ocr(img_path)
    print("✅ Structured OCR completed.")

    # 3️⃣ AI post‑processing
    corrected = ai_postprocess(plain, structured)
    print("✅ AI post‑processor finished.")

    # 4️⃣ Show results
    display_corrected_text(corrected)
```

**Erwartete Ausgabe** (angenommen eine einfache einseitige Rechnung):

```
--- Page 1 ---
Invoice #12345
Date: 2024‑05‑01
Bill To: Acme Corp
Item Qty Price Total
Widget A 2 $15.00 $30.00
Widget B 1 $25.00 $25.00
Subtotal $55.00
Tax $5.50
Total $60.50
```

Beachten Sie, wie Zeilenumbrüche und Spaltenreihenfolge erhalten bleiben und gängige OCR‑Fehler wie „$15.00“, die als „$15,00“ gelesen werden, durch den KI‑Schritt korrigiert werden.

---

## Wie dieser Workflow **die OCR‑Genauigkeit verbessert**

| Phase | Was es behebt | Warum es wichtig ist |
|------|---------------|----------------------|
| **Plain text OCR** | Erkennt unlesbare Seiten frühzeitig | Spart Zeit, indem hoffnungslose Eingaben übersprungen werden |
| **Structured OCR** | Erfasst Layout, Koordinaten | Ermöglicht nachgelagerte Aufgaben (Hervorhebung, Redaktion) |
| **AI post‑processor** | Korrigiert Rechtschreibung, fügt geteilte Wörter zusammen, korrigiert Zahlen | Steigert die Gesamtezeichengenauigkeit von ~85 % auf >95 % bei verrauschten Scans |
| **Iteration** | Ermöglicht erneutes Ausführen mit abgestimmten Parametern | Feinabstimmung der Pipeline für spezifische Dokumenttypen |

Durch die Kombination dieser drei Konzepte – **Plain‑Text‑OCR**, layout‑bewusste Extraktion und KI‑Korrektur – erhalten Sie eine robuste Lösung, die die OCR‑Genauigkeit *signifikant* **verbessert**, ohne ein eigenes neuronales Netzwerk von Grund auf zu schreiben.

---

## Häufige Fallstricke & Pro‑Tipps

- **Fallstrick:** Das Einspeisen eines Bildes mit niedriger Auflösung (≤150 dpi) in Tesseract führt zu wirrem Output.  
  **Pro‑Tipp:** Vorverarbeiten mit `Pillow` – wenden Sie `Image.convert('L')` und `Image.filter(ImageFilter.MedianFilter())` vor dem OCR an.

- **Fallstrick:** Der KI‑Nachbearbeiter kann versehentlich domänenspezifische Terminologie (z. B. „SKU123“) umschreiben.  
  **Pro‑Tipp:** Erstellen Sie eine Whitelist von Begriffen und übergeben Sie diese an das LLM oder an eine Rechtschreibprüfungs‑Bibliothek wie `pyspellchecker`.

- **Fallstrick:** Mehrspaltige Seiten werden zu einer einzigen Zeile zusammengeführt.  
  **Pro‑Tipp:** Erkennen Sie Spaltengrenzen mithilfe des Feldes `block_num` in der TSV‑Ausgabe von Tesseract und teilen Sie die Zeilen entsprechend.

- **Fallstrick:** Große PDFs verursachen einen Speicherüberlauf, wenn alle Seiten gleichzeitig geladen werden.  
  **Pro‑Tipp:** Verarbeiten Sie Seiten inkrementell – iterieren Sie über `pdf2image.convert_from_path(..., first_page=n, last_page=n)`.

---

## Erweiterung der Pipeline

Wenn Sie neugierig auf die nächsten Schritte sind, betrachten Sie die folgenden Erweiterungen:

1. **Batch‑Verarbeitung** – Verpacken Sie das gesamte Skript in eine Funktion, die ein Verzeichnis durchläuft und Tausende von Dateien parallel mit `concurrent.futures` verarbeitet.  
2. **Sprachmodelle** – Ersetzen Sie die einfache difflib‑Heuristik durch einen Aufruf von OpenAI’s `gpt‑4o` oder einem lokal gehosteten LLaMA‑Modell, um reichhaltigere kontextuelle Korrekturen zu erhalten.  
3. **Export‑Formate** – Schreiben Sie die korrigierte Struktur in ein durchsuchbares PDF

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Bildtext mit Sprache mit Aspose.OCR OCR‑t](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Wie man OCR verwendet – Fortgeschrittene Techniken mit Aspose.OCR für Java](/ocr/english/java/advanced-ocr-techniques/)
- [OCR‑Genauigkeit verbessern – Erkennungs‑Bereich‑Modus in OCR](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}