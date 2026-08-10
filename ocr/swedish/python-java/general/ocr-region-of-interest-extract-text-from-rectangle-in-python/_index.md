---
category: general
date: 2026-05-31
description: Lär dig hur du använder ett intresseområde för OCR för att ladda en bild
  för OCR och extrahera text från en rektangel, perfekt för att känna igen belopp
  på en faktura.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: sv
og_description: Behärska OCR‑intresseområdet för att ladda bild för OCR, extrahera
  text från en rektangel och känna igen text från en faktura i en enda handledning.
og_title: OCR‑intresseområde – steg‑för‑steg Python‑guide
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR-område av intresse – Extrahera text från rektangel i Python
url: /sv/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Region of Interest – Extrahera text från rektangel i Python

Har du någonsin funderat på hur du **ocr region of interest** en specifik del av en skannad faktura utan att mata in hela sidan i motorn? Du är inte den första som stirrar på ett suddigt kvitto och tänker: “Hur extraherar jag beloppet som ligger någonstans i nedre högra hörnet?” Den goda nyheten är att du kan tala om för OCR‑biblioteket exakt var det ska leta, vilket dramatiskt ökar både hastighet och noggrannhet.

I den här guiden går vi igenom ett komplett, körbart exempel som visar hur du **load image for OCR**, definierar en **region of interest**, och sedan **extract text from rectangle** för att slutligen **recognize text from invoice** och svara på den klassiska frågan “hur extraherar man belopp”. Inga vaga referenser – bara konkret kod, tydliga förklaringar och några pro‑tips du önskar att du hade känt till tidigare.

---

## Vad du kommer att bygga

I slutet av den här tutorialen har du ett litet Python‑skript som:

1. Laddar en fakturabild från disk.  
2. Markerar en rektangulär ROI där totalbeloppet finns.  
3. Kör OCR endast inom den ROI:n.  
4. Skriver ut den rensade beloppssträngen.  

Allt detta fungerar med vilket OCR‑bibliotek som helst som stödjer ROI – här använder vi ett fiktivt men representativt `SimpleOCR`‑paket som efterliknar populära verktyg som Tesseract eller EasyOCR. Byt gärna ut det; koncepten förblir desamma.

---

## Förutsättningar

- Python 3.8+ installerat (`python --version` bör visa ≥3.8).  
- Ett pip‑installabelt OCR‑paket (t.ex. `pip install simpleocr`).  
- En fakturabild (PNG eller JPEG) placerad i en mapp du kan referera till.  
- Grundläggande kunskap om Python‑funktioner och -klasser (inget avancerat).

Om du redan har detta, bra – låt oss dyka ner. Om inte, hämta bilden först; resten av stegen är oberoende av själva filinnehållet.

---

## Steg 1: Load Image for OCR

Det första som någon OCR‑arbetsflöde behöver är en bitmap att läsa från. De flesta bibliotek exponerar en enkel `load_image`‑metod som accepterar en filsökväg. Så här gör du med vår `SimpleOCR`‑motor:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** Använd absoluta sökvägar eller `os.path.join` för att undvika “file not found”-överraskningar när du kör skriptet från en annan arbetskatalog.

---

## Steg 2: Define OCR Region of Interest

Istället för att låta motorn skanna hela sidan, talar vi om exakt var beloppet sitter. Detta är **ocr region of interest**‑steget, och det är nyckeln till pålitlig extraktion, särskilt när dokumentet innehåller brusiga rubriker eller sidfötter.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

Varför just de siffrorna? `x` och `y` är pixel‑offsets från det övre vänstra hörnet, medan `width` och `height` beskriver lådans storlek. Om du är osäker, öppna bilden i någon redigerare, aktivera en linjal och notera koordinaterna. Många IDE:er låter dig till och med skriva ut muspekarens position när du hovrar.

---

## Steg 3: Extract Text from Rectangle

Nu när ROI:n är satt ber vi motorn att **recognize text from invoice** men begränsat till den rektangel vi just lagt till. Anropet returnerar ett resultatobjekt som vanligtvis innehåller den råa strängen, förtroendesiffror och ibland avgränsningsrutor.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

Bakom kulisserna itererar `recognize()` över varje ROI, beskär den delen, kör OCR‑modellen och sammanfogar resultaten. Detta är varför en väl avgränsad **extract text from rectangle**‑region kan spara sekunder på bearbetningstid för batchjobb.

---

## Steg 4: How to Extract Amount – Clean the Output

OCR är inte perfekt; du får ofta oönskade mellanslag, radbrytningar eller felaktigt lästa tecken (tänk “S” vs “5”). En snabb `strip()` och ett litet regex‑mönster löser vanligtvis problemet för monetära värden.

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Why this matters:** Om du planerar att skicka beloppet till en databas eller en betalningsgateway behöver du ett förutsägbart format. Att ta bort whitespace och filtrera icke‑numeriska tecken förhindrar fel längre ner i kedjan.

---

## Steg 5: Recognize Text from Invoice – Full Script

Sätter vi ihop allt får du det kompletta, körklara skriptet. Spara det som `extract_amount.py` och kör `python extract_amount.py`.

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Förväntad output

```
Amount: 1,245.67
```

Om ROI:n är feljusterad kan du se något i stil med `Amount: 1245.6S` – notera den stray “S”. Justera rektangelkoordinaterna och kör igen tills outputen ser ren ut.

---

## Vanliga fallgropar & kantfall

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| **ROI för liten** | Beloppstexten klipps av, vilket leder till partiell igenkänning. | Utöka `width`/`height` med ~10‑20 % och testa igen. |
| **Fel DPI** | Lågresolution‑skanningar (≤150 dpi) minskar OCR‑noggrannheten. | Resampla bilden till 300 dpi innan du laddar, eller be skannern om högre DPI. |
| **Flera valutor** | Regex fångar den första numeriska gruppen, vilket kan vara ett fakturanummer. | Förfina regex‑mönstret för att leta efter valutasymboler (`$`, `€`, `£`) före siffrorna. |
| **Rotera fakturor** | OCR‑motorer förutsätter upprätt text; roterade sidor bryter igenkänning. | Applicera en rotationskorrigering (`ocr_engine.rotate(90)`) innan du lägger till ROI. |
| **Bakgrundsbrus** | Skuggor eller stämplar förvirrar modellen. | Förbehandla med ett enkelt tröskelvärde (`cv2.threshold`) eller använd ett brusreduceringsfilter. |

Att ta itu med dessa kantfall tidigt sparar dig timmar av felsökning senare.

---

## Pro‑tips för verkliga projekt

- **Batch‑behandling:** Loopa över en mapp med fakturor, beräkna ROI dynamiskt (t.ex. baserat på mall‑detektion), och lagra resultat i CSV.  
- **Mall‑matchning:** Om du hanterar flera fakturamallar, håll en JSON‑karta över `template_id → ROI‑koordinater`. Byt ROI baserat på en snabb layout‑klassificerare.  
- **Parallell körning:** Använd `concurrent.futures.ThreadPoolExecutor` för att köra flera OCR‑instanser samtidigt – perfekt för högvolym‑backoffice‑pipelines.  
- **Förtroendefiltrering:** De flesta OCR‑resultat innehåller en confidence‑score. Kasta bort resultat under en tröskel (t.ex. 85 %) och flagga dem för manuell granskning.

---

## Slutsats

Vi har gått igenom allt du behöver för att **ocr region of interest**, **load image for OCR**, **extract text from rectangle**, och slutligen **recognize text from invoice** för att svara på den klassiska frågan **how to extract amount**. Skriptet är kompakt, men ändå tillräckligt flexibelt för att anpassas till olika dokumentformat, språk och OCR‑bakgrunder.

Nu när du behärskar grunderna, fundera på att utöka arbetsflödet: lägg till streckkodsskanning, integrera med en PDF‑parser, eller skicka det extraherade beloppet till ett bokförings‑API. Himlen är gränsen, och med en väl definierad ROI får du alltid snabbare, renare resultat.

Om du stöter på problem, lämna en kommentar nedan – lycka till med OCR‑andet!

![ocr region of interest example](https://example.com/ocr_roi_example.png "ocr region of interest example")


## Vad bör du lära dig härnäst?

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}