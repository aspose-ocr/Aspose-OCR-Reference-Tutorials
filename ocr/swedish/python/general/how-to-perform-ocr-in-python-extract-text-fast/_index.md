---
category: general
date: 2026-03-26
description: Lär dig hur du utför OCR i Python och enkelt extraherar text från en
  bild, läser text från en skanning eller extraherar text från en faktura med en enkel
  OcrEngine.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: sv
og_description: Hur utför man OCR i Python? Den här guiden visar dig hur du extraherar
  text från en bild, läser text från en skanning och extraherar text från en faktura
  på några minuter.
og_title: Hur man utför OCR i Python – Extrahera text snabbt
tags:
- OCR
- Python
- Image Processing
title: Hur man utför OCR i Python – Extrahera text snabbt
url: /sv/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man utför OCR i Python – Extrahera text snabbt

Har du någonsin undrat **hur man utför OCR** på ett skannat kvitto eller en suddig PDF? Du är inte ensam. I många projekt dyker behovet av att **extrahera text från bild** upp förr eller senare, och den vanliga “skriv allt för hand”-metoden är helt enkelt inte skalbar.  

I den här handledningen kommer du att se ett komplett, färdigt‑att‑köra exempel som visar **hur man använder OCR** för att läsa text från en skanning, hämta data från en faktura och till och med hantera automatisk skevkorrektion—allt med bara några rader Python.

## Vad du kommer att lära dig

Vi går igenom allt du behöver veta:

* De exakta beroenden och importeringar som krävs.
* Hur man skapar och konfigurerar en `OcrEngine`‑instans.
* Sätt att **extrahera text från bild**, **läsa text från skanning**, och **extrahera text från faktura** med samma motor.
* Vanliga fallgropar (fel språk, saknade filer, stora bilder) och hur man undviker dem.
* Förväntad output så att du kan verifiera att OCR:n lyckades.

Inga externa dokumentationslänkar behövs—allt är självständigt, så du kan kopiera‑klistra koden och se resultat omedelbart.

## Förutsättningar

Innan vi dyker ner, se till att du har:

* Python 3.8+ installerat (paketet `ocr` fungerar med vilken nyare version som helst).
* `ocr`‑biblioteket tillgängligt (`pip install ocr‑engine` – ersätt med det faktiska paketnamnet om det är annorlunda).
* En bildfil du vill bearbeta – för demonstrationen använder vi `invoice.png` som ligger i en mapp som heter `YOUR_DIRECTORY`.

Det är allt. Om du redan har detta, är du redo att köra.

## Steg 1: Installera och importera OCR‑modulen

Först och främst: vi behöver OCR‑biblioteket. Om du inte har installerat det ännu, kör följande kommando i din terminal:

```bash
pip install ocr-engine
```

Nu importerar vi modulen i vårt skript.

```python
# Step 1: Import the OCR module
import ocr
```

> **Pro tip:** Håll ditt virtuella miljö rent; det förhindrar versionskonflikter när du senare lägger till andra bild‑behandlingspaket.

## Steg 2: Skapa och konfigurera OCR‑motorn

Att skapa motorn är lika enkelt som att anropa dess konstruktor, men den verkliga kraften ligger i att konfigurera den korrekt. Vi kommer att sätta språket till engelska och slå på automatisk skevkorrektion, vilket är viktigt när man hanterar skannade fakturor som inte är perfekt justerade.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

Varför aktivera `auto_skew`? Många skannrar producerar bilder som är några grader sned. Utan korrigering kan motorn missa tecken, vilket förvandlar en helt läsbar faktura till nonsens.

## Steg 3: Utför OCR på din målbild

Nu matar vi bildfilen i motorn. Metoden `recognize_image` returnerar ett objekt som innehåller den råa texten samt förtroendesiffror (om biblioteket tillhandahåller dem).

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

Om du arbetar med ett **läsa text från skanning**‑scenario, ersätt helt enkelt sökvägen med den skannade PDF:en konverterad till PNG eller JPEG. Samma anrop fungerar för alla bildformat som det underliggande biblioteket stödjer.

## Steg 4: Inspektera och använd den extraherade texten

Låt oss skriva ut den råa OCR‑utdata. I en verklig fakturabehandlingspipeline skulle du förmodligen parsra denna sträng, extrahera radposter, totalsummor och datum, men för nu räcker en snabb titt för att bekräfta att OCR:n lyckades.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**Förväntad output (avkortad för korthet):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

Om outputen ser förvrängd ut, dubbelkolla att bilden är klar och att `engine.language` matchar dokumentets språk.

## Steg 5: Hantera vanliga edge‑cases

### Stora bilder

Att bearbeta en 5000 × 5000 pixel‑skanning kan vara minneskrävande. Ett snabbt sätt att mildra detta är att skala ner bilden innan den skickas till motorn:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### Flera språk

Om du behöver **extrahera text från bild** som innehåller både engelska och spanska, kan du ange en lista med språk:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

Motorn kommer att försöka känna igen tecken från båda uppsättningarna.

### Felhantering

Anta aldrig att filen finns. Omge anropet med ett try‑except‑block för att ge ett vänligt meddelande:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## Visuell referens

Nedan är en skärmdump av exempel­fakturan vi använde i demonstrationen. Lägg märke till den lilla lutningen—precis vad `auto_skew` rättar till.

![how to perform OCR on an invoice](/images/ocr-example.png)

*Alt text:* hur man utför OCR på en fakturabild som visar automatisk skevkorrektion.

## Fullt, körbart exempel

När vi sätter ihop allt, här är ett enda skript du kan köra från kommandoraden. Det täcker installation, konfiguration, felhantering och ett enkelt efterbearbetningssteg som skriver den extraherade texten till en fil som heter `output.txt`.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

Att köra `python full_ocr_demo.py` kommer att skriva ut den extraherade texten till konsolen och lagra den i `output.txt`. Därifrån kan du använda reguljära uttryck, CSV‑skrivare eller någon annan logik du behöver för **extrahera text från faktura**‑automatisering.

## Slutsats

Du har nu ett solidt, end‑to‑end‑svar på **hur man utför OCR** i Python. Genom att skapa en `OcrEngine`, konfigurera språk och skevkorrektion, och hantera några praktiska edge‑cases, kan du på ett pålitligt sätt **extrahera text från bild**, **läsa text från skanning**, och **extrahera text från faktura** utan att leta igenom spridd dokumentation.

Vad blir nästa steg? Prova att mata in en batch av filer i en loop, experimentera med olika språk, eller anslut outputen till ett PDF‑genereringsbibliotek för att skapa sökbara PDF‑filer. Himlen är gränsen, och koden du just såg är en robust startplattform.

Har du frågor om ett specifikt filformat eller behöver hjälp med att justera förtroendetrösklar? Lämna en kommentar nedan—glad att hjälpa dig finjustera din OCR‑pipeline!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}