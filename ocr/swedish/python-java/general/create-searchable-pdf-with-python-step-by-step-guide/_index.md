---
category: general
date: 2026-05-31
description: Skapa sökbar PDF från skannade bilder med Python OCR. Lär dig hur du
  konverterar skannad bild‑PDF, konverterar TIFF till PDF och lägger till ett OCR‑textlager
  på några minuter.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: sv
og_description: Skapa sökbar PDF omedelbart. Den här guiden visar hur du kör OCR,
  konverterar skannad bild‑PDF och lägger till ett OCR‑textlager med ett enda Python‑skript.
og_title: Skapa sökbar PDF med Python – Komplett handledning
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: Skapa sökbar PDF med Python – Steg‑för‑steg‑guide
url: /sv/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa sökbar PDF med Python – Steg‑för‑steg guide

Har du någonsin undrat hur man **skapar sökbar PDF** från en skannad sida utan att jonglera med dussintals verktyg? Du är inte ensam. I många kontorsarbetsflöden hamnar en skannad TIFF eller JPEG på en gemensam enhet, och nästa person måste kopiera‑klistra text manuellt—smärtsamt, felbenäget och tidskrävande.  

I den här handledningen går vi igenom en ren, programmerbar lösning som låter dig **konvertera skannad bild‑PDF**, **konvertera TIFF till PDF**, och **lägga till OCR‑textlager** i ett svep. I slutet har du ett färdigt skript som kör OCR, bäddar in den dolda texten och genererar en sökbar PDF som du kan indexera, söka i eller dela med förtroende.

## Vad du behöver

- Python 3.9+ (någon nyare version fungerar)
- `aspose-ocr` and `aspose-pdf` packages (installerade via `pip install aspose-ocr aspose-pdf`)
- En skannad bildfil (`.tif`, `.png`, `.jpg`, eller till och med en PDF‑sida som bara är en bild)
- En måttlig mängd RAM (OCR‑motorn är lättviktig; även en laptop klarar det)

> **Proffstips:** Om du använder Windows är det enklaste sättet att få paketen att köra kommandot i ett förhöjt PowerShell‑fönster.

```bash
pip install aspose-ocr aspose-pdf
```

Nu när förutsättningarna är avklarade, låt oss dyka ner i koden.

## Steg 1: Skapa en OCR‑motorinstans – *create searchable pdf*

Det första vi gör är att starta OCR‑motorn. Tänk på den som hjärnan som läser varje pixel och omvandlar den till tecken.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **Varför detta är viktigt:** Att initiera motorn bara en gång håller minnesanvändningen låg. Om du skulle anropa `OcrEngine()` i en loop för varje sida, skulle du snabbt få slut på resurser.

## Steg 2: Ladda den skannade bilden – *convert tiff to pdf* & *convert scanned image pdf*

Nästa steg är att rikta motorn mot filen du vill bearbeta. API:et accepterar vilken rasterbild som helst, så en TIFF fungerar lika bra som en JPEG.

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

Om du råkar ha en PDF som bara innehåller en skannad bild, kan du fortfarande använda `load_image` eftersom Aspose automatiskt extraherar den första sidan.

## Steg 3: Förbered PDF‑spara‑alternativ – *add OCR text layer*

Här konfigurerar vi hur den slutgiltiga PDF‑filen ska se ut. Den avgörande flaggan är `create_searchable_pdf`; att sätta den till `True` instruerar biblioteket att bädda in ett osynligt textlager som speglar det visuella innehållet.

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **Vad textlagret gör:** När du öppnar den resulterande filen i Adobe Reader och försöker markera text, ser du de dolda tecknen. Sökmotorer kan också indexera dem—perfekt för efterlevnad eller arkivering.

## Steg 4: Kör OCR och spara – *how to run OCR* i ett enda anrop

Nu händer magin. Ett metodanrop kör igenkänningsmotorn och skriver den sökbara PDF‑filen till disk.

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

`recognize`‑metoden returnerar ett statusobjekt som du kan inspektera för fel, men för de flesta enkla scenarier är det enkla anropet ovan tillräckligt.

### Förväntad utdata

Att köra skriptet skriver ut:

```
PDF saved as searchable PDF.
```

Om du öppnar `scanned_page_searchable.pdf` kommer du märka att du kan markera text, kopiera‑klistra den, och till och med köra en `Ctrl+F`‑sökning. Det är kännetecknet för ett **create searchable pdf**‑arbetsflöde.

## Fullt fungerande skript

Nedan är det kompletta, färdiga skriptet. Byt bara ut platshållar‑sökvägarna mot dina faktiska filplatser.

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

Spara detta som `create_searchable_pdf.py` och kör:

```bash
python create_searchable_pdf.py
```

## Vanliga frågor & kantfall

### 1️⃣ Kan jag bearbeta flersidiga PDF‑filer?

Ja. Använd `ocr_engine.load_image("file.pdf")` och loopa sedan över varje sida med `ocr_engine.recognize(pdf_save_options, page_number)`. Biblioteket genererar automatiskt en flersidig sökbar PDF.

### 2️⃣ Vad händer om min källfil är en högupplöst TIFF (300 dpi+)?

Högre DPI ger bättre OCR‑noggrannhet men också större minnesanvändning. Om du får ett `MemoryError`, skala ner bilden först:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ Hur ändrar jag språket för OCR?

Ställ in `language`‑egenskapen på motorn innan du laddar bilden:

```python
ocr_engine.language = "fra"   # French
```

En fullständig lista över stödda språkkoder finns i Aspose‑dokumentationen.

### 4️⃣ Vad händer om jag måste behålla den ursprungliga bildkvaliteten?

`PdfSaveOptions`‑klassen har en `compression`‑egenskap. Sätt den till `PdfCompression.None` för att bevara rasterdata exakt som den var.

```python
pdf_save_options.compression = "None"
```

## Tips för produktionsklar distribution

- **Batch‑bearbetning:** Packa in kärnlogiken i en funktion som accepterar en lista med filsökvägar. Logga varje lyckat/misslyckat resultat till en CSV för revisionsspår.
- **Parallellism:** Använd `concurrent.futures.ThreadPoolExecutor` för att köra OCR på flera kärnor. Kom bara ihåg att varje tråd behöver sin egen `OcrEngine`‑instans.
- **Säkerhet:** Om du hanterar känsliga dokument, kör skriptet i en sandlådemiljö och radera de temporära filerna omedelbart efter bearbetning.

## Slutsats

Du vet nu hur man **skapar sökbar PDF**‑filer från skannade bilder med ett koncist Python‑skript. Genom att initiera en OCR‑motor, ladda en TIFF (eller någon raster), konfigurera `PdfSaveOptions` för att **lägga till OCR‑textlager**, och slutligen anropa `recognize`, blir hela **convert scanned image pdf**‑ och **convert TIFF to PDF**‑pipeline ett enda, repeterbart kommando.

Nästa steg? Prova att kedja detta skript med en fil‑övervakare så att varje ny skanning som läggs i en mapp automatiskt blir sökbar. Eller experimentera med olika OCR‑språk för att stödja flerspråkiga arkiv. Himlen är gränsen när du kombinerar OCR med PDF‑generering.

Har du fler frågor om **how to run OCR** i andra språk eller ramverk? Lämna en kommentar nedan, och lycka till med kodandet! 

![Diagram som visar flödet från skannad bild → OCR‑motor → sökbar PDF (create searchable pdf)](searchable-pdf-flow.png "Diagram för skapa sökbar pdf flöde")


## Vad bör du lära dig härnäst?

- [Hur man OCR‑ar PDF i .NET med Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Konvertera bilder till PDF C# – Spara flersidigt OCR‑resultat](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Hur man OCR‑ar bildtext med språk med Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}