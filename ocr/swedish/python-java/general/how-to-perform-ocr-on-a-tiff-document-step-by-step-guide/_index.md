---
category: general
date: 2026-01-12
description: Hur man utför OCR snabbt och exakt. Lär dig att köra OCR på dokument,
  extrahera text från tiff, ladda bild för OCR och ställa in OCR-språk i Python.
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: sv
og_description: Hur man utför OCR i Python. Denna handledning visar hur du kör OCR
  på ett dokument, extraherar text från tiff, laddar bild för OCR och ställer in OCR-språk.
og_title: Hur man utför OCR på ett TIFF‑dokument – Komplett guide
tags:
- OCR
- Python
- Image Processing
title: Hur man utför OCR på ett TIFF‑dokument – steg‑för‑steg‑guide
url: /sv/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man utför OCR på ett TIFF-dokument – Komplett guide

Har du någonsin undrat **hur man utför OCR** på en skannad TIFF-fil utan att spendera timmar på att leta efter rätt bibliotek? Du är inte ensam. Många utvecklare stöter på problem när de behöver extrahera text från tiff-bilder, särskilt när prestanda och språkinställningar spelar roll.

I den här handledningen går vi igenom allt du behöver veta: från att installera OCR‑paketet, ladda bilden för OCR, ange OCR‑språket, till slut **köra OCR på dokumentet** och hämta ren text. I slutet har du ett färdigt skript som du kan släppa in i vilket projekt som helst.

> **Proffstips:** Även om exemplet använder en generisk `ocr`‑modul, gäller samma koncept för Tesseract, EasyOCR eller någon modern OCR‑motor som exponerar ett Python‑API.

---

## Vad du behöver

- Python 3.8+ (någon nyare version fungerar)
- Ett OCR‑bibliotek som tillhandahåller en `OcrEngine`‑klass (exemplet använder ett fiktivt `ocr`‑paket; ersätt det med ditt riktiga)
- En fler‑sidig TIFF‑fil som du vill bearbeta (vi kallar den `big_document.tif`)
- En maskin med minst 4 CPU‑kärnor om du planerar att ange trådräkning

Inga externa tjänster, inga moln‑nycklar – bara lokal kod som körs på sekunder.

![exempel på hur man utför OCR](/images/ocr-example.png "hur man utför OCR på ett TIFF-dokument")

*Bildtext: hur man utför OCR på ett TIFF-dokument – förhandsgranskning av extraherad text.*

---

## Steg 1: Installera och importera OCR‑biblioteket

Först och främst: skaffa biblioteket till din maskin. De flesta OCR‑paket finns på PyPI, så ett enkelt `pip install` löser det.

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

Nu importerar vi de klasser du behöver. Om du använder Tesseract skulle import‑raden se annorlunda ut, men resten av koden förblir densamma.

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*Varför detta är viktigt:* Att importera rätt symboler tidigt förhindrar namnrymdskrockar senare och gör skriptet lättare att läsa.

---

## Steg 2: Skapa och konfigurera OCR‑motorn (ange OCR‑språk)

Att konfigurera motorn är där du **anger OCR‑språk** för korrekt igenkänning. Engelska är standard, men du kan byta till franska, tyska eller till och med flerspråkigt läge med en enda rad.

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **Varför 4 trådar?** De flesta moderna bärbara datorer har minst fyra kärnor, och att begränsa trådräkningen hindrar OCR‑processen från att ta hela maskinens resurser – särskilt användbart när skriptet körs på en delad server.

Om du behöver ett annat språk, ersätt bara `ocr.Language.ENGLISH` med `ocr.Language.FRENCH`, `ocr.Language.SPANISH` osv.

---

## Steg 3: Ladda bild för OCR (Load Image for OCR)

Nu **laddar vi bild för OCR**. Metoden `Image.load` läser TIFF‑filen till minnet och hanterar automatiskt fler‑sidiga dokument.

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*Edge case:* Om filen är enorm kan du få slut på RAM. I så fall kan du överväga att ladda en sida i taget med `Image.load_page(page_number)` (om biblioteket stödjer det).

---

## Steg 4: Kör OCR på dokumentet

Med motorn redo och bilden laddad är det dags att **köra OCR på dokumentet**. Metoden `process` gör det tunga arbetet och returnerar ett resultatobjekt.

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

Bakom kulisserna delar motorn upp bilden i textblock, kör igenkänningsmodellen och sätter ihop resultaten. Anropet är blockande, vilket betyder att skriptet väntar tills hela TIFF‑filen är bearbetad – perfekt för batch‑jobb.

---

## Steg 5: Extrahera text från TIFF och verifiera resultatet

Till sist **extraherar vi text från tiff** genom att läsa attributet `text` i resultatet. Låt oss skriva ut de första 200 tecknen som en snabb kontroll.

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**Förväntat resultat (exempel):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

Om du behöver hela texten, använd helt enkelt `ocr_result.text`. För vidare bearbetning kan du skriva den till en `.txt`‑fil:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

---

## Fullt fungerande exempel

Sätter vi ihop allt får du ett färdigt skript. Byt ut platshållar‑paketnamnet mot det du faktiskt har installerat.

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

Kör skriptet med:

```bash
python ocr_tiff_example.py
```

Du bör se en förhandsgranskning skriven till konsolen och en fil med namnet `extracted_text.txt` som innehåller hela transkriptionen.

---

## Vanliga frågor & kantfall

- **Vad händer om TIFF‑filen innehåller flera sidor?**  
  De flesta OCR‑motorer behandlar varje sida som en separat bild internt. `ocr_result.text` kommer att innehålla ett radbrytning mellan sidorna. Om du behöver hantera varje sida separat, iterera med `Image.load_page(page_number)`.

- **Kan jag bearbeta en PNG eller JPEG istället för TIFF?**  
  Absolut. Metoden `Image.load` accepterar vanligtvis alla format som stöds av Pillow eller det underliggande biblioteket. Byt bara filändelsen.

- **Min text är förvrängd – bör jag byta språk?**  
  Ja. Steget **ange OCR‑språk** är avgörande för icke‑engelska dokument. Se till att språkpaketet är installerat (t.ex. `tesseract‑lang‑fra` för franska).

- **Slutar jag få slut på minne?**  
  Minska `set_memory_limit` eller bearbeta sidor en‑och‑en. Vissa motorer låter dig också skala ner bilden innan igenkänning.

---

## Slutsats

Där har du det – en kortfattad, fullt funktionell guide om **hur man utför OCR** på en TIFF‑fil med Python. Vi har gått igenom allt från installation av biblioteket, konfigurering av motorn (inklusive **ange OCR‑språk**), **ladda bild för OCR**, **köra OCR på dokumentet**, och slutligen **extrahera text från tiff**.  

Känn dig fri att experimentera: justera trådräkningen, byt språk, eller mata OCR‑resultatet in i en naturlig‑språk‑pipeline. Himlen är gränsen när du har bemästrat grunderna.

Har du fler frågor? Lämna en kommentar nedan, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}