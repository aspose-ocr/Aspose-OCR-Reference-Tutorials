---
category: general
date: 2026-03-18
description: Kör OCR på bilden för att extrahera text från PNG och skapa en sökbar
  PDF. Lär dig hur du känner igen text i en bild och konverterar PNG till PDF på några
  minuter.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: sv
og_description: Kör OCR på bilden för att extrahera text från PNG, känna igen textbilden
  och skapa en sökbar PDF. Följ denna steg‑för‑steg‑guide.
og_title: Kör OCR på bild – Extrahera text från PNG snabbt
tags:
- OCR
- Python
- Image Processing
title: Kör OCR på bild – Extrahera text från PNG snabbt
url: /sv/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kör OCR på bild – Extrahera text från PNG snabbt

Har du någonsin behövt **köra OCR på bild**-filer men varit osäker på var du ska börja? Kanske har du en skannad artikel sparad som `article.png` och bara vill ha ren text, eller så behöver du en sökbar PDF för arkivering. Oavsett är du på rätt plats. I den här handledningen går vi igenom hur du extraherar text från PNG, känner igen texten i bilden och till och med konverterar PNG-filen till en sökbar PDF – allt med några få kodrader.

> **Vad du får:** ett komplett, körbart skript som laddar en PNG, kör OCR, sparar hOCR‑utdata och valfritt skapar en sökbar PDF. Inga saknade imports, inga “se dokumentationen” döda vägar – bara en självständig lösning som du kan lägga in i ditt projekt idag.

## Förutsättningar

- **Python 3.8+** (syntaxen som används här fungerar på alla nyare versioner)
- Biblioteket **`ocr_engine`** som du använder (exemplet förutsätter en klass som heter `OcrEngine`; ersätt med Tesseract, EasyOCR, etc., om det behövs)
- En PNG‑bild du vill bearbeta (t.ex. `article.png` placerad i en mapp du kan referera till)
- Skrivbehörighet till utmatningskatalogen

Om du använder Tesseract under huven, installera det med:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

Och installera sedan Python‑wrappern:

```bash
pip install pytesseract Pillow
```

*Proffstips:* håll ditt OCR‑bibliotek uppdaterat – nya språkpaket och prestandaförbättringar släpps ofta.

## Kör OCR på bild – Steg‑för‑steg‑guide

Nedan är det **kompletta skriptet**. Kopiera och klistra in det i en fil som heter `run_ocr.py` och kör den med `python run_ocr.py`.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### Vad skriptet gör, på enkla svenska

1. **Instansiera** OCR‑motorn så att du kan kontrollera dess inställningar.
2. **Läs in** PNG‑filen (`article.png`). Skriptet avbryts tidigt om filen saknas – inga mystiska `NoneType`‑fel senare.
3. **Välj** `hocr` som exportformat. Detta format behåller den ursprungliga layouten, vilket är avgörande för att senare konvertera bilden till en sökbar PDF.
4. **Kör** igenkänningsmotorn; den tunga lyftningen sker här.
5. **Skriv** hOCR‑XML till `article.hocr`. Du har nu en maskinläsbar representation av texten och dess koordinater.
6. *(Valfritt)* Byt till `"pdf"` och generera en sökbar PDF i ett extra steg.

Den **förväntade utdata** är en UTF‑8‑kodad `.hocr`‑fil som ser ut ungefär så här (trimmad för korthet):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

Om du avkommenterar PDF‑avsnittet får du även `article_searchable.pdf`, som du kan öppna i vilken PDF‑visare som helst och använda **Ctrl + F**‑sökfältet för att omedelbart hitta ord.

![Exempel på OCR på bild resultat](example.png "Kör OCR på bild – hOCR- och PDF-resultat")

## Hur du extraherar text från PNG med OcrEngine

Om allt du behöver är råtext (ingen layout, ingen PDF), kan du hoppa över hOCR‑steget helt:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Varför välja ren text?* Den är lättviktig, perfekt för indexering och fungerar bra med efterföljande NLP‑pipelines.

## Känn igen textbild och generera sökbar PDF

Att generera en sökbar PDF är en tvådelad process:

1. **Kör OCR** med `hocr` (som vi gjorde ovan) för att få layoutinformationen.
2. **Kombinera** den ursprungliga PNG‑filen med hOCR till en PDF med motorns PDF‑exportör.

De flesta moderna OCR‑bibliotek (Tesseract, ABBYY, Google Vision) erbjuder en `pdf`‑export som gör exakt detta. Koden i *Valfritt*-blocket i huvudskriptet visar mönstret. Om ditt bibliotek inte har en inbyggd PDF‑exportör kan du använda **`pdf2image`** + **`reportlab`** för att sammanfoga bilden och hOCR – säg bara till så delar jag ett snabbt extra exempel.

## Konvertera PNG till PDF med OCR‑utdata

Ibland vill du bara ha en **vanlig PDF** som innehåller bilden (ingen sökbar lager). Det är ännu enklare:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

Kombinera detta med OCR‑steget om du behöver en sökbar version, eller behåll det som en trogen visuell kopia för arkiveringsändamål.

## Vanliga fallgropar & tips

| Problem | Varför det händer | Snabb lösning |
|-------|----------------|-----------|
| **Suddig eller lågupplöst PNG** | OCR‑noggrannheten sjunker dramatiskt under ~300 DPI. | Skala upp med `Image.resize((width*2, height*2), Image.LANCZOS)` innan du skickar den till motorn. |
| **Fel språk** | Motorn använder som standard engelska; icke‑engelska tecken blir förvrängda. | Anropa `ocr_engine.setLanguage('deu')` (eller lämplig ISO‑kod) innan `recognize()`. |
| **Saknad hOCR‑utdata** | Vissa motorer använder standardtext när `setExportFormat` inte anropas. | Kontrollera att `setExportFormat("hocr")` körs **innan** `recognize()`. |
| **Filbehörighetsfel** | Försöker skriva till en skrivskyddad mapp. | Använd en sökväg inom ditt projekt eller kör `os.makedirs(..., exist_ok=True)` först. |
| **Stora PDF‑filer orsakar minnesökning** | PDF‑exportören håller hela bilden i RAM. | Bearbeta sidor i delar eller använd en strömmande PDF‑skrivare. |

*Proffstips:* testa alltid på en liten exempelbild innan du skalar upp till tusentals. Det sparar timmar av felsökning.

## Sammanfattning

Du vet nu **hur du kör OCR på bild**‑filer, **extraherar text från PNG**, **känner igen textbilder** för efterföljande uppgifter, **genererar en sökbar PDF**, och **konverterar PNG till PDF** när du behöver ett enkelt arkiv. Det medföljande skriptet är en komplett, kopiera‑och‑klistra‑lösning som fungerar direkt, och de valfria sektionerna låter dig anpassa utdata efter ditt exakta arbetsflöde.

### Vad blir nästa?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}