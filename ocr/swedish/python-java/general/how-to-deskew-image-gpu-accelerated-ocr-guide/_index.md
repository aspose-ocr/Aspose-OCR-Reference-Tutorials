---
category: general
date: 2026-01-02
description: Lär dig hur du räta upp bilden och ökar bildkontrasten för att snabbt
  få ren text. Inkluderar steg‑för‑steg Python‑kod och tips för att extrahera text.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: sv
og_description: Hur man räta upp en bild och ökar kontrasten för att få ren text.
  Fullt Python‑exempel med tabellutdragning och GPU‑acceleration.
og_title: Hur man räta upp bild – Komplett GPU OCR-handledning
tags:
- OCR
- Python
- Image Processing
title: Hur man räta upp en bild – GPU‑accelererad OCR‑guide
url: /sv/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man räta upp bild – GPU‑accelererad OCR‑guide

Har du någonsin undrat **how to deskew image** när dina kvitton kommer in i en rolig vinkel? Du är inte ensam; ett snedvridet foto kan förvandla ett perfekt läsbart kvitto till ett rörigt kaos. Den goda nyheten är att med några rader Python kan du automatiskt räta upp, öka kontrasten och extrahera ren ren text—utan manuellt Photoshop.  

I den här handledningen går vi igenom ett komplett, körbart exempel som inte bara **how to deskew image** utan också visar **how to boost contrast**, hur man **get plain text**, och till och med **how to extract text** från tabeller som OCR‑motorn upptäcker. I slutet har du ett självständigt skript som du kan lägga in i vilket projekt som helst.

## Vad du behöver

- Python 3.9+ installerat (koden använder typ‑indikatorer, så en nyare interpreter hjälper)
- `ocr`‑biblioteket som tillhandahåller `OcrEngine`, `EngineMode`, `ImageProcessingOptions` och `OcrResult` (installera via `pip install ocr‑sdk` – ersätt med det faktiska paketnamnet du använder)
- Ett GPU med kompatibla drivrutiner om du vill ha hastighetsökning (valfritt men rekommenderas)
- En bildfil som är lite roterad eller har låg kontrast, t.ex. `receipt_skewed.jpg`

> **Pro tip:** Om du inte har ett GPU, ändra bara `EngineMode.GPU` till `EngineMode.CPU` så fungerar skriptet fortfarande—bara lite långsammare.

## Steg‑för‑steg‑implementering

Nedan delar vi upp lösningen i logiska delar. Varje del har en beskrivande **H2** som antingen innehåller huvudnyckelordet *how to deskew image* eller ett av de sekundära nyckelorden. Koden är komplett, kommenterad och klar att köras.

### Hur man räta upp bild med GPU‑accelererad OCR

Det första vi gör är att tala om för OCR‑motorn att köra på GPU och aktivera auto‑deskew‑funktionen. Auto‑deskew analyserar bildens geometri och roterar den tillbaka till upprätt läge.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **Varför detta är viktigt:** GPU‑acceleration kan minska behandlingstiden från sekunder till millisekunder, vilket är avgörande när du hanterar dussintals kvitton per minut.

### Öka bildkontrast för bättre igenkänning

Ett kvitto med låg kontrast är en mardröm för alla OCR‑system. Genom att öka kontrasten ger vi motorn tydligare kanter att arbeta med.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **Hur man ökar kontrast:** Metoden `set_contrast_boost` accepterar en procentsats; 30 % är ett säkert standardvärde som fungerar för de flesta skannade kvitton. Om dina bilder är extremt mörka, öka till 50 % eller experimentera.

### Hämta ren text från den bearbetade bilden

Nu när bilden är rak och ljus, matar vi den till motorn och begär resultatet som ren text.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**Förväntad utskrift** (avkortad för korthet):

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **Hur man får ren text:** Metoden `get_text()` tar bort all layoutinformation och returnerar en ren sträng, som du sedan kan lagra i en databas, skicka till ett API eller föra in i efterföljande analyser.

### Hur man extraherar text från upptäckta tabeller

Ofta innehåller kvitton tabulär data (artiklar, kvantiteter, priser). OCR‑SDK:n kan upptäcka tabeller och låta dig iterera över rader och celler.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**Exempel på tabellutdata**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **Varför extrahera tabeller:** Strukturerad data gör det enkelt att beräkna totalsummor, generera rapporter eller föra in i bokföringsprogram.

### Fullt fungerande skript

När vi sätter ihop allt, här är skriptet du kan kopiera‑klistra in i `deskew_and_ocr.py`:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

Kör det med:

```bash
python deskew_and_ocr.py
```

Du bör se den rensade texten och eventuella upptäckta tabeller skrivas ut i konsolen.

## Vanliga kantfall & hur man hanterar dem

| Situation | What to Do |
|-----------|------------|
| **Bilden är upp och ner** | Öka förtroendet för `set_auto_deskew(True)` genom att också anropa `set_rotation_correction(True)` om SDK:n erbjuder det. |
| **Kontrastökning gör bilden för ljus** | Minska procentsatsen som skickas till `set_contrast_boost` (t.ex. 15 %). |
| **GPU ej tillgänglig** | Byt `EngineMode.GPU` till `EngineMode.CPU`; resten av pipeline förblir oförändrad. |
| **Tabeller missas** | Prova en skanning med högre upplösning eller aktivera `set_table_detection(True)` om biblioteket tillhandahåller det. |

## Nästa steg: Från ren text till strukturerad data

Nu när du vet **how to deskew image**, **how to boost contrast**, och **how to get plain text**, kanske du vill:

- Analysera den rena texten med reguljära uttryck för att extrahera nyckel‑värde‑par (t.ex. `total`, `date`).
- Lagra resultaten i en SQLite‑ eller PostgreSQL‑databas för senare rapportering.
- Koppla skriptet till en serverlös funktion (AWS Lambda, Azure Functions) för att automatiskt bearbeta uppladdningar.

Alla dessa tillägg bygger på samma grund som vi täckte här.

## Slutsats

Vi har gått igenom **how to deskew image** med en GPU‑accelererad OCR‑motor, demonstrerat **how to boost contrast** för skarpare igenkänning, visat exakt **how to get plain text**, och även täckt **how to extract text** från tabeller. Det kompletta, körbara skriptet binder ihop allt, så du kan lägga in det i vilket Python‑projekt som helst och börja hämta ren data från snedvridna, lågkontrast‑foton omedelbart.

Prova det med några av dina egna kvitton, justera kontrastnivån, och låt OCR‑motorn göra det tunga arbetet. Om du stöter på egenheter, gå tillbaka till tabellen med kantfall ovan—de flesta problem är bara ett litet justering bort.

Lycka till med kodningen, och må dina bilder alltid vara raka och ljusa!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}