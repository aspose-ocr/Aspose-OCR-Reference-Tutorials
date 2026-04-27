---
category: general
date: 2026-04-26
description: Kreditkartennummern schnell maskieren mit AsposeAI OCR‑Nachbearbeitung.
  Lernen Sie PCI‑Konformität, Maskierung mit regulären Ausdrücken und Datenbereinigung
  in einer Schritt‑für‑Schritt‑Anleitung.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: de
og_description: Maskieren Sie Kreditkartennummern in OCR‑Ergebnissen mit AsposeAI.
  Dieses Tutorial behandelt PCI‑Konformität, das Maskieren mit regulären Ausdrücken
  und Datenbereinigung.
og_title: Kreditkartennummern maskieren – Vollständiger Leitfaden zur Nachbearbeitung
  von Python‑OCR.
tags:
- OCR
- Python
- security
title: Kreditkartennummern im OCR-Ausgabe maskieren – Vollständiger Python-Leitfaden
url: /de/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kreditkartennummern maskieren – Vollständiger Python‑Leitfaden

Haben Sie jemals **Kreditkartennummern maskieren** müssen in Text, der direkt von einer OCR‑Engine stammt? Sie sind nicht allein. In regulierten Branchen kann die Offenlegung einer vollständigen PAN (Primary Account Number) zu Problemen mit PCI‑Compliance‑Auditoren führen. Die gute Nachricht? Mit ein paar Zeilen Python und dem Post‑Processing‑Hook von AsposeAI können Sie automatisch die mittleren acht Ziffern verbergen und auf der sicheren Seite bleiben.

In diesem Tutorial gehen wir ein reales Szenario durch: OCR auf ein Beleg‑Bild anwenden und dann eine benutzerdefinierte **OCR‑Post‑Processing**‑Funktion einsetzen, die alle PCI‑Daten bereinigt. Am Ende haben Sie ein wiederverwendbares Snippet, das Sie in jeden AsposeAI‑Workflow einbinden können, sowie einige praktische Tipps zum Umgang mit Randfällen und zur Skalierung der Lösung.

## Was Sie lernen werden

- Wie man einen benutzerdefinierten Post‑Processor mit **AsposeAI** registriert.
- Warum ein **Regular‑Expression‑Maskierungs**‑Ansatz sowohl schnell als auch zuverlässig ist.
- Die Grundlagen der **PCI‑Compliance** im Zusammenhang mit Daten‑Sanitisierung.
- Möglichkeiten, das Muster für mehrere Kartenformate oder internationale Nummern zu erweitern.
- Erwartete Ausgabe und wie man überprüft, dass die Maskierung funktioniert hat.

> **Voraussetzungen** – Sie sollten eine funktionierende Python 3‑Umgebung haben, das Aspose.AI‑für‑OCR‑Paket installiert haben (`pip install aspose-ocr`), und ein Beispielbild (z. B. `receipt.png`) besitzen, das eine Kreditkartennummer enthält. Keine weiteren externen Dienste sind erforderlich.

---

## Schritt 1: Definieren Sie einen Post‑Processor, der Kreditkartennummern maskiert

Das Herz der Lösung steckt in einer winzigen Funktion, die das OCR‑Ergebnis erhält, eine **Regular‑Expression‑Maskierungs**‑Routine ausführt und den bereinigten Text zurückgibt.

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**Warum das funktioniert:**  
- Der reguläre Ausdruck `(\d{4})\d{8}(\d{4})` trifft exakt 16 aufeinanderfolgende Ziffern, das gängige Format für Visa, MasterCard und viele andere.  
- Durch das Erfassen der ersten und letzten vier Ziffern (`\1` und `\2`) bewahren wir genügend Informationen für die Fehlersuche, während wir den **PCI‑Compliance**‑Regeln entsprechen, die das Speichern der vollständigen PAN verbieten.  
- Die Ersetzung `\1****\2` verbirgt die sensiblen mittleren acht Ziffern und wandelt `1234567812345678` in `1234****5678` um.

> **Pro‑Tipp:** Wenn Sie 15‑stellige American‑Express‑Nummern unterstützen müssen, fügen Sie ein zweites Muster wie `r'(\d{4})\d{6}(\d{5})'` hinzu und führen beide Ersetzungen nacheinander aus.

---

## Schritt 2: Initialisieren Sie die AsposeAI‑Engine

Bevor wir unseren Post‑Processor anhängen können, benötigen wir eine Instanz der OCR‑Engine. AsposeAI bündelt das OCR‑Modell und eine einfache API für benutzerdefinierte Verarbeitung.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**Warum hier initialisieren?**  
Das einmalige Erzeugen des `AsposeAI`‑Objekts und dessen Wiederverwendung über mehrere Bilder hinweg reduziert den Overhead. Die Engine cached zudem Sprachmodelle, was nachfolgende Aufrufe beschleunigt – praktisch, wenn Sie Stapel von Belegen scannen.

---

## Schritt 3: Registrieren Sie die benutzerdefinierte Maskierungsfunktion

AsposeAI stellt die Methode `set_post_processor` bereit, mit der Sie jede aufrufbare Einheit einbinden können. Wir übergeben unsere `mask_pci`‑Funktion zusammen mit einem optionalen Settings‑Dictionary (vorerst leer).

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**Was im Hintergrund passiert:**  
Wenn Sie später `run_postprocessor` aufrufen, übergibt AsposeAI das rohe OCR‑Ergebnis an `mask_pci`. Die Funktion erhält ein leichtgewichtiges Objekt (`data`), das den erkannten Text enthält, und gibt einen neuen String zurück. Dieses Design lässt das Kern‑OCR unverändert, während Sie **Daten‑Sanitisierungs**‑Richtlinien an einer einzigen Stelle durchsetzen können.

---

## Schritt 4: OCR auf das Beleg‑Bild anwenden

Jetzt, wo die Engine weiß, wie die Ausgabe zu bereinigen ist, übergeben wir ihr ein Bild. Für dieses Tutorial gehen wir davon aus, dass Sie bereits ein `engine`‑Objekt mit den richtigen Sprach‑ und Auflösungseinstellungen konfiguriert haben.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**Tipp:** Wenn Sie kein vorab konfiguriertes Objekt haben, können Sie eines erstellen mit:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

Der Aufruf `recognize_image` liefert ein Objekt zurück, dessen Attribut `text` den rohen, unmaskierten String enthält.

---

## Schritt 5: Registrierten Post‑Processor anwenden

Mit den rohen OCR‑Daten in der Hand geben wir sie an die AI‑Instanz weiter. Die Engine führt automatisch die zuvor registrierte `mask_pci`‑Funktion aus.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**Warum `run_postprocessor` statt eines manuellen Funktionsaufrufs verwenden?**  
Damit bleibt der Workflow konsistent, besonders wenn Sie mehrere Post‑Processor haben (z. B. Rechtschreibprüfung, Spracherkennung). AsposeAI stellt sie in der Reihenfolge ihrer Registrierung in eine Warteschlange, was deterministische Ausgaben garantiert.

---

## Schritt 6: Verifizieren Sie die bereinigte Ausgabe

Zum Schluss geben wir den bereinigten Text aus und prüfen, ob alle Kreditkartennummern korrekt maskiert wurden.

```python
print(final_result.text)
```

**Erwartete Ausgabe** (Auszug):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

Enthielt der Beleg keine Kartennummer, bleibt der Text unverändert – nichts zu maskieren, nichts zu befürchten.

---

## Umgang mit Randfällen und gängigen Variationen

### Mehrere Kartennummern in einem Dokument
Enthält ein Beleg mehr als eine PAN (z. B. eine Treuekarte plus eine Zahlungskarte), führt der reguläre Ausdruck global aus und maskiert automatisch alle Treffer. Kein zusätzlicher Code nötig.

### Nicht‑standardmäßige Formatierung
Manchmal fügt OCR Leerzeichen oder Bindestriche ein (`1234 5678 1234 5678` oder `1234-5678-1234-5678`). Erweitern Sie das Muster, um diese Zeichen zu ignorieren:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

Das hinzugefügte `[ -]?` toleriert optionale Leerzeichen oder Bindestriche zwischen den Ziffernblöcken.

### Internationale Karten
Für 19‑stellige PANs, die in manchen Regionen verwendet werden, können Sie das Muster verbreitern:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

Denken Sie daran, dass **PCI‑Compliance** weiterhin das Maskieren der mittleren Ziffern vorschreibt, unabhängig von der Länge.

### Maskierte Werte protokollieren (optional)
Falls Sie Audit‑Logs benötigen, übergeben Sie ein Flag über `custom_settings` und passen die Funktion an:

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

Anschließend registrieren Sie mit:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## Vollständiges funktionierendes Beispiel (zum Kopieren und Einfügen bereit)

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

Führt man dieses Skript auf einem Beleg aus, der `4111111111111111` enthält, entsteht:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

Damit ist die gesamte Pipeline – vom rohen OCR‑Ergebnis bis zur **Daten‑Sanitisierung** – in wenigen klaren Python‑Zeilen umgesetzt.

---

## Fazit

Wir haben Ihnen gezeigt, wie Sie **Kreditkartennummern** in OCR‑Ergebnissen mithilfe des Post‑Processing‑Hooks von AsposeAI, einer kompakten Regular‑Expression‑Routine und einigen Best‑Practice‑Hinweisen zur **PCI‑Compliance** maskieren können. Die Lösung ist komplett eigenständig, funktioniert mit jedem Bild, das die OCR‑Engine lesen kann, und lässt sich leicht erweitern, um komplexere Kartenformate oder Protokollierungsanforderungen abzudecken.

Bereit für den nächsten Schritt? Kombinieren Sie diese Maske mit einer **Datenbank‑Einfüge‑Routine**, die nur die letzten vier Ziffern zur Referenz speichert, oder integrieren Sie einen **Batch‑Processor**, der über Nacht einen ganzen Ordner mit Belegen scannt. Sie können zudem weitere **OCR‑Post‑Processing**‑Aufgaben erkunden, etwa Adressstandardisierung oder Spracherkennung – jedes folgt dem gleichen Muster, das wir hier verwendet haben.

Haben Sie Fragen zu Randfällen, Performance oder zur Anpassung des Codes für eine andere OCR‑Bibliothek? Hinterlassen Sie einen Kommentar unten, und wir setzen das Gespräch fort. Viel Spaß beim Coden und bleiben Sie sicher!  



![Diagram illustrating how mask credit card numbers works in an OCR pipeline](https://example.com/images/ocr-mask-flow.png "Diagram of OCR post‑processing masking flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}