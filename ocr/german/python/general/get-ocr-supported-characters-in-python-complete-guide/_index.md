---
category: general
date: 2026-06-25
description: Erhalte OCR‑unterstützte Zeichen schnell mit der aocr‑Bibliothek. Erfahre,
  wie du OCR‑Zeichen auflistest, Sprachen festlegst und deine OCR‑Engine in Python
  debuggst.
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: de
og_description: Erhalte OCR‑unterstützte Zeichen mit aocr. Dieser Leitfaden zeigt
  dir, wie du OCR‑Zeichen auflistest, Sprachen auswählst und Sonderfälle in Python
  behandelst.
og_title: Erhalte OCR‑unterstützte Zeichen in Python – Vollständiges Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: OCR‑unterstützte Zeichen in Python abrufen – Komplett‑Leitfaden
url: /de/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR‑unterstützte Zeichen in Python abrufen – Komplettanleitung

Haben Sie sich schon einmal gefragt, wie man **get OCR supported characters** für eine bestimmte Sprache erhält, wenn man mit einer OCR‑Engine experimentiert? Sie sind nicht allein. Egal, ob Sie einen Belegscanner oder einen mehrsprachigen Dokumentenparser bauen, genau zu wissen, welche Glyphen Ihre Engine erkennen kann, ist ein echter Lebensretter. In diesem Tutorial gehen wir den gesamten Prozess durch – Installation der Bibliothek, Konfiguration der Sprache und schließlich Auflistung dieser Zeichen – sodass Sie Ihre OCR‑Pipeline in Minuten debuggen und feinjustieren können.

Wir verwenden die **aocr**‑Bibliothek, eine leichtgewichtige Python‑OCR‑Engine, die das Abfragen von Sprachfähigkeiten mühelos macht. Am Ende dieses Leitfadens können Sie **list OCR characters**, zwischen **supported OCR languages** wechseln und sogar Lücken in der Abdeckung erkennen, bevor sie Sie in der Produktion überraschen.

---

## Voraussetzungen

Bevor wir starten, stellen Sie sicher, dass Sie haben:

* Python 3.8 oder neuer (das aocr‑Paket unterstützt 3.7 nicht mehr)
* Ein Terminal oder die Eingabeaufforderung mit Internetzugang
* Grundlegende Kenntnisse in Python‑Skripting (wenn Sie bereits ein `print()` geschrieben haben, sind Sie bereit)

Keine schweren externen Abhängigkeiten – nur das `aocr`‑Pip‑Paket.

---

## aocr‑Bibliothek installieren (OCR‑Engine Python)

Das Erste, was Sie benötigen, ist eine funktionierende **OCR engine Python**‑Installation. Das aocr‑Paket ist auf PyPI verfügbar, sodass ein einziger pip‑Befehl ausreicht:

```bash
pip install aocr
```

Wenn Sie eine virtuelle Umgebung verwenden (dringend empfohlen), aktivieren Sie diese zuerst:

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **Pro tip:** Pin the version (`pip install aocr==1.2.4`) to avoid unexpected API changes later on.

---

## Sprache auswählen (unterstützte OCR‑Sprachen)

aocr liefert eine Handvoll integrierter Sprachpakete. Jedes Paket definiert die Menge der Unicode‑Code‑Points, die die Engine erkennen kann. Um diese Pakete abzufragen, müssen Sie das Attribut `language` an der Engine‑Instanz setzen.

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

Sie können `aocr.Language.ENGLISH` durch jeden anderen Enum‑Wert ersetzen (`FRENCH`, `GERMAN`, etc.). Wenn Sie versuchen, eine Sprache zuzuweisen, die nicht enthalten ist, wirft aocr einen `ValueError`. Deshalb ist es sinnvoll, zuerst die **supported OCR languages**‑Liste zu prüfen:

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## Zeichensatz abrufen (OCR‑unterstützte Zeichen erhalten)

Jetzt kommt das Herzstück des Tutorials: tatsächlich **get OCR supported characters**. Die Engine stellt eine praktische Methode namens `get_supported_characters()` bereit, die eine Liste von Einzelzeichen‑Strings zurückgibt.

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

Im Hintergrund liest aocr eine JSON‑Datei, die im Sprachpaket gebündelt ist, und konvertiert jeden Unicode‑Code‑Point in einen Python‑String. Das Ergebnis ist deterministisch, d. h. Sie erhalten bei jedem Ausführen des Skripts mit derselben Sprachversion dieselbe Liste.

---

## Anzahl unterstützter Zeichen anzeigen

Die Kenntnis der Anzahl hilft Ihnen, die Breite der Abdeckung schnell einzuschätzen. Für Englisch sehen Sie typischerweise ein paar tausend Zeichen (inklusive Satzzeichen und Ziffern).

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

Der Aufruf `len()` ist O(1), weil Python die Listengröße intern speichert, sodass es selbst bei großen Alphabeten keinen Performance‑Nachteil gibt.

---

## Erste 100 unterstützte Zeichen vorschauen

Ein schneller visueller Check kann zeigen, ob die Engine die von Ihnen benötigten Symbole enthält (denken Sie an das Euro‑Zeichen oder smarte Anführungszeichen). Lassen Sie uns die ersten hundert Zeichen ausgeben:

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

Der `join`‑Vorgang verkettet das Slice zu einem einzigen String, was lesbarer ist als das Ausdrucken einer Python‑Liste.

---

## Vollständiges Skript – Alle Schritte an einem Ort

Unten finden Sie das komplette, ausführbare Beispiel, das alles zusammenführt. Speichern Sie es als `list_supported_chars.py` und führen Sie `python list_supported_chars.py` in Ihrem Terminal aus.

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**Erwartete Ausgabe (gekürzt zur Übersicht):**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

Die genaue Anzahl kann je nach aocr‑Version leicht variieren, aber Sie werden stets ein langes Alphabet plus gängige Satzzeichen sehen.

---

## Sonderfälle behandeln

### Was, wenn das Sprachpaket fehlt?

Wenn Sie eine Sprache anfordern, die nicht gebündelt ist, enthält `aocr.Language` das Enum nicht und Sie erhalten einen `AttributeError`. Schützen Sie sich mit einer einfachen Prüfung:

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### Leere Zeichenliste

Einige Nischensprachen könnten eine leere Liste zurückgeben, wenn die zugrunde liegenden Trainingsdaten unvollständig sind. In diesem Fall können Sie auf eine Vorgabe (z. B. Englisch) zurückfallen oder eine Warnung ausgeben:

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Unicode‑Normalisierung

Die Liste kann kombinierte Zeichen enthalten (z. B. „é“ als `e` + Akut‑Akzent). Erwartet Ihre nachgelagerte Verarbeitung vorgeformte Glyphen, führen Sie einen Normalisierungsschritt aus:

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## Profi‑Tipps für Praxisprojekte

* **Cache the character list** – Wenn Sie Tausende von Bildern verarbeiten, verursacht das Aufrufen von `get_supported_characters()` in jeder Iteration unnötigen Overhead. Speichern Sie die Liste in einer Modul‑Variablen oder serialisieren Sie sie zu JSON für spätere Wiederverwendung.
* **Cross‑language validation** – Wenn Sie mehrere Sprachen in einer einzigen App unterstützen, schneiden Sie die Zeichensätze, um eine gemeinsame Teilmenge zu finden. Das hilft Ihnen, UI‑Elemente zu entwerfen, die über Locale‑Grenzen hinweg konsistent bleiben.
* **Debugging OCR failures** – Klassifiziert die Engine ein Glyph falsch, vergleichen Sie das fehlerhafte Zeichen mit der Ausgabe von `list_supported_chars`. Fehlt es, haben Sie eine Abdeckungslücke identifiziert, die möglicherweise einen eigenen Trainingsschritt erfordert.
* **Combine with custom fonts** – aocr respektiert den Unicode‑Bereich, aber die Render‑Qualität kann je nach Schrift variieren. Testen Sie Ihre unterstützten Zeichen mit exakt der Schrift, die Sie in der Produktion einsetzen, um Überraschungen zu vermeiden.

---

## Häufig gestellte Fragen

**Q: funktioniert das mit aocr‑Version 2.x?**  
A: Ja, die Methode `get_supported_characters()` ist sowohl in 1.x als auch in 2.x stabil. Der einzige Unterschied besteht darin, dass die Sprach‑Enums nach `aocr.languages` verschoben wurden.

**Q: Kann ich den Unicode‑Code‑Point für jedes Zeichen erhalten?**  
A: Absolut. Verwenden Sie `ord(ch)` innerhalb einer List‑Comprehension:

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**Q: Was ist mit Rechts‑nach‑Links‑Schriften wie Arabisch?**  
A: aocr enthält ein `ARABIC`‑Enum. Die Zeichenliste wird arabische Glyphen enthalten, aber Sie müssen ggf. RTL‑Rendering in Ihrer nachgelagerten UI aktivieren.

---

## Fazit

Sie wissen jetzt, **how to get OCR supported characters** mit der aocr‑Bibliothek in Python zu erhalten, wie Sie zwischen **supported OCR languages** wechseln und warum **listing OCR characters** für robuste Texterkennungs‑Pipelines unverzichtbar ist. Mit dem vollständigen Skript und den obigen Tipps können Sie die Sprachabdeckung schnell prüfen, fehlende Glyphen debuggen und intelligentere OCR‑gesteuerte Anwendungen bauen.

Bereit für den nächsten Schritt? Kombinieren Sie diese Zeichenliste mit einem benutzerdefinierten Wortlisten‑Filter oder experimentieren Sie mit einer anderen OCR‑Engine (Tesseract, EasyOCR) und vergleichen Sie die Ergebnisse. Je mehr Sie erkunden, desto besser werden Ihre OCR‑Lösungen.

Viel Spaß beim Coden, und mögen Ihre Zeichensätze immer vollständig sein!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Zulässige Zeichen für OCR festlegen – Verwendung von Aspose.OCR für .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [Wie man Bildtext mit Sprache per OCR erkennt – Verwendung von Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [OCR‑Nachbearbeitung – Zeichenoptionen erhalten](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}