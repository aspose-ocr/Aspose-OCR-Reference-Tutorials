---
category: general
date: 2026-06-25
description: Extrahera text från bilder med Python aocr‑biblioteket – lär dig batch‑OCR,
  sätt igenkänningsläget till tryckt och lägg till en AI‑efterprocessor.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: sv
og_description: Extrahera text från bilder med Python aocr-biblioteket. Denna handledning
  visar batch‑OCR, utskriftsigenkänningsläge och valfri AI‑efterbehandling.
og_title: Extrahera text från bilder i Python – Komplett aocr batchguide
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Extrahera text från bilder i Python med aocr OCR Batch
url: /sv/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bilder i Python med aocr OCR Batch

Har du någonsin behövt **extrahera text från bilder** men känt dig överväldigad av dussintals små steg? Du är inte ensam. Oavsett om du digitaliserar inskannade formulär, hämtar data från kvitton eller bygger ett sökbart arkiv, kan det kännas som att klättra uppför en brant kulle att få pålitliga OCR‑resultat i stor skala.

Den goda nyheten? Med **aocr‑biblioteket** kan du snabbt sätta upp ett komplett **Python OCR‑batch** med bara några få rader kod. I den här guiden går vi igenom hur du skapar ett OCR‑batch, laddar alla stödjade bilder från en mapp, väljer rätt **recognition mode printed**, och till och med kopplar på en **AI‑postprocessor** för extra noggrannhet. När du är klar har du ett färdigt skript som extraherar text från bilder och visar hur mycket som fångades per fil.

## Vad du kommer att lära dig

- Hur du installerar och importerar paketet `aocr`.
- Hur du sätter upp en `OcrBatch` för att automatiskt hantera tusentals filer.
- Hur du väljer det optimala igenkänningsläget för tryckt text.
- (Valfritt) Hur du kopplar på en AI‑post‑processor för att rensa upp brusiga resultat.
- Hur du visar varje filsökväg tillsammans med längden på den extraherade texten.
- Tips för att hantera kantfall som ej stödjade format eller tomma sidor.

### Förkunskaper

- Python 3.8 eller nyare installerat på din maskin.  
- Grundläggande kunskap om Python‑skriptning (loopar, imports osv.).  
- Tillgång till en mapp med inskannade bilder (PNG, JPG, TIFF osv.).  

Om du har detta, så kör vi igång—inga externa tjänster krävs.

## Steg 1: Installera aocr‑biblioteket

Först och främst. Paketet `aocr` är inte en del av standardbiblioteket, så du måste hämta det från PyPI.

```bash
pip install aocr
```

> **Proffstips:** Använd ett virtuellt miljö (`python -m venv .venv`) för att hålla beroenden isolerade.  

När det är installerat kan du importera kärnklasserna.

```python
# core imports
import aocr
```

## Steg 2: Skapa en OCR‑batch‑instans

En `OcrBatch` är arbetshästen som kommer att gå igenom din katalog och hålla reda på varje bildfil. Tänk på den som ett löpband som matar bilder till OCR‑motorn.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

Just nu är batchen tom, men vi fyller den i nästa steg.

## Steg 3: Lägg till alla stödjade bilder från en mapp (rekursivt)

Du har förmodligen en nästlad mappstruktur—kanske en undermapp per kund eller per månad. Metoden `add_folder` går igenom trädet åt dig och plockar in varje bild den kan läsa.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

Byt ut `"YOUR_DIRECTORY/scanned_forms/"` mot den faktiska sökvägen på ditt system. Efter detta anrop innehåller `ocr_batch.file_paths` en lista med absoluta filnamn, och batchen vet exakt hur många objekt den ska bearbeta.

## Steg 4: Välj igenkänningsläge för tryckt text

`aocr`‑motorn stödjer flera lägen (handskriven, tryckt, blandat). Eftersom vi arbetar med rena, tryckta formulär, sätt läget därefter. Denna lilla flagga kan dramatiskt förbättra noggrannheten eftersom motorn hoppar över de tunga heuristiker som behövs för kursiv skrift.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **Varför det spelar roll:** Tryckt text har konsekventa baslinjer och teckenformer, vilket låter OCR‑modellen använda snävare teckendiktionärer. Om du lämnar läget på “auto” kan du få extra brus på lågupplösta skanningar.

## Steg 5: (Valfritt) Koppla på en AI‑post‑processor

Om dina skanningar lider av oskärpa, låg kontrast eller ovanliga typsnitt, kan en AI‑post‑processor rensa upp den råa OCR‑utdata innan du skickar den vidare till efterföljande system. Metoden `set_ai_postprocessor` förväntar sig ett objekt som implementerar ett `process(text: str) -> str`‑gränssnitt.

Nedan är ett minimalt exempel med en fiktiv `SimpleCleaner`‑klass. I praktiken kan du ansluta en HuggingFace‑transformer, en anpassad språkmodell eller till och med en regelbaserad stavningskontroll.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

Om du hoppar över detta steg returnerar batchen helt enkelt de råa OCR‑strängarna.

## Steg 6: Kör OCR på hela batchen och samla resultat

Nu börjar det tunga arbetet. Metoden `run` loopar över varje fil, kör OCR‑motorn, skickar utdata genom den valfria AI‑post‑processorn och returnerar en lista med strängar—en per bild.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

Eftersom metoden returnerar en vanlig Python‑lista kan du behandla den som vilken annan samling som helst—spara den, skriv den till en CSV eller mata in den i en databas.

## Steg 7: Visa varje filsökväg med längden på den extraherade texten

En snabb kontroll är att skriva ut hur många tecken som extraherades från varje fil. Om en sida är tom eller OCR‑processen misslyckades ser du en längd på `0`.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

Typisk utskrift ser ut så här:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

Att se en `0`‑flagga direkt visar vilka filer som behöver en andra granskning (kanske är de korrupta eller inte ens bilder).

## Hantera vanliga kantfall

### 1. Ej stödjade filtyper

`aocr` hoppar tyst över filer den inte kan avkoda. Om du misstänker att du har PDF‑ eller BMP‑filer blandade, filtrera dem i förväg:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. Stora batcher och minnesanvändning

Att köra tusentals högupplösta skanningar kan blåsa upp minnesförbrukningen. Minska detta genom att bearbeta i portioner:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. Tomma eller lågkontrast‑sidor

Om en sida ger färre än 10 tecken kan du vilja flagga den för manuell granskning:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## Fullt fungerande exempel

Sammanställt allt ovan, här är ett skript du kan kopiera‑klistra och köra direkt. Spara det som `batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**Förväntad utskrift** (avkortad för korthet):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

Kör det med:

```bash
python batch_ocr.py
```

Om allt är korrekt konfigurerat ser du en rad för varje bild, där varje rad rapporterar teckenantalet för den extraherade texten.

## Vanliga frågor

**Q: Fungerar detta på PDF‑filer?**  
A: Inte direkt. `aocr` hanterar endast rasterbilder. Konvertera PDF‑filer till PNG/TIFF först (t.ex. med `pdf2image`).

**Q: Kan jag byta igenkänningsläge till handskriven?**  
A: Absolut—byt bara `aocr.RecognitionMode.PRINTED` mot `aocr.RecognitionMode.HANDWRITTEN`. Förvänta dig längre körtid men bättre resultat på kursiv handskrift.

**Q: Vad händer om jag behöver flerspråkigt stöd?**  
A: Biblioteket levereras med språkpaket. Installera önskat språkmodul (`pip install aocr-lang-fr` för franska osv.) och sätt `ocr_batch.language = "fr"` innan du kör.

## Nästa steg och relaterade ämnen

- **Parallell bearbetning:** Wrappa batch‑exekveringen i en `concurrent.futures.ThreadPoolExecutor` för att utnyttja flera CPU‑kärnor.  
- **Spara resultat:** Skriv `ocr_results` till en CSV‑fil eller SQLite‑databas för vidare analys.  
- **Integrera med moln‑AI:** Byt ut `SimpleCleaner` mot en transformer‑modell från HuggingFace för toppmodern stavningskorrigering.  
- **Fin‑tuna aocr:** Om du har ett eget teckensnitt, utforska `aocr.Trainer` för att förbättra noggrannheten i tryckt‑läge.

---

Det var allt—nu har du en solid grund


## Vad bör du lära dig härnäst?


Följande handledningar täcker närliggande ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i egna projekt.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}