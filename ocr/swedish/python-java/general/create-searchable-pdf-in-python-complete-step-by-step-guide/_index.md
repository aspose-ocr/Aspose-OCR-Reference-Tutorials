---
category: general
date: 2026-06-19
description: Skapa sökbar PDF från en bild med Python OCR. Lär dig konvertera OCR
  till PDF, extrahera text från bild och utföra OCR på bild snabbt.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: sv
og_description: Skapa sökbar PDF från en bild med Python OCR. Denna guide visar hur
  man konverterar OCR till PDF, extraherar text från en bild och utför OCR på bilden.
og_title: Skapa sökbar PDF i Python – Fullständig programmeringsgenomgång
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: Skapa sökbar PDF i Python – Komplett steg‑för‑steg‑guide
url: /sv/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa sökbar PDF i Python – Komplett steg‑för‑steg‑guide

Har du någonsin behövt **skapa sökbar PDF** från ett skannat kvitto men inte vetat var du ska börja? Du är inte ensam—många utvecklare stöter på samma hinder när de första gången försöker omvandla en bild av text till en PDF som du faktiskt kan söka i.  

I den här handledningen går vi igenom en praktisk lösning som låter dig **utföra OCR på bild**, omvandla OCR‑resultatet till en **sökbar PDF**, och även hämta den råa texten om du behöver den för vidare bearbetning. Inga onödiga utsvävningar, bara ett fungerande exempel som du kan kopiera‑klistra in i ditt projekt redan idag.

## Vad du kommer att lära dig

- Hur du sätter upp en lättviktig OCR‑motor i Python  
- De exakta stegen för att **konvertera OCR till PDF** och spara den som ett sökbart dokument  
- Sätt att **extrahera text från bild** för efterföljande analys  
- Tips för att hantera vanliga fallgropar som bildorientering och stora filer  
- Ett komplett, körbart skript som du kan anpassa till ditt eget användningsområde

### Förutsättningar

- Python 3.8+ installerat på din maskin  
- Grundläggande kunskap om pip och virtuella miljöer (valfritt men rekommenderat)  
- En bildfil (PNG, JPEG, etc.) som innehåller tydlig, maskinläsbar text  

Om du har detta, låt oss dyka ner.

## Steg 1: Installera det nödvändiga biblioteket

Kodsnutten du såg tidigare använder ett fiktivt `ocr`‑paket, men samma idéer gäller för verkliga bibliotek som **EasyOCR**, **pytesseract** eller **pdfminer.six**. För den här guiden använder vi **EasyOCR** eftersom det är rent Python, stöder många språk och levererar en praktisk PDF‑konverteringsmetod via en hjälpfunktion.

```bash
pip install easyocr pillow
```

> **Proffstips:** Installera i en virtuell miljö (`python -m venv venv && source venv/bin/activate`) för att hålla dina beroenden organiserade.

## Steg 2: Initiera OCR‑motorn – Utför OCR på bild

Nu när biblioteket är redo skapar vi en OCR‑motor och talar om för den att arbeta med engelsk text. Detta är den första platsen där vi **utför OCR på bild**.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

Varför behöver vi ett dedikerat läsar‑objekt? EasyOCR för‑laddar språkmodeller, så att återanvända samma `reader` för flera bilder är mycket effektivare än att initiera om den varje gång.

## Steg 3: Ladda bilden – Extrahera text från bild

Låt oss läsa in bilden i minnet. Detta steg är där vi senare **extraherar text från bild**, men först laddar vi bara in den.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

Om din bild är upp och ner eller sned, överväg att använda Pillow:s `rotate` eller `transpose`‑metoder innan du skickar den till OCR‑motorn. En snabb visuell kontroll kan spara dig timmar av felsökning senare.

## Steg 4: Kör OCR‑motorn och fånga resultaten

Här är kärnan i processen—att skicka bilden till OCR‑motorn och få tillbaka strukturerad data.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

Flaggan `detail=1` ger oss begränsningsrutor, vilket vi kommer att behöva när vi senare **konverterar OCR till PDF**. Om du bara är intresserad av råa strängar, sätt `detail=0`.

## Steg 5: Konvertera OCR‑resultat till en sökbar PDF – Konvertera OCR till PDF

EasyOCR erbjuder ingen direkt PDF‑skrivare, men vi kan själva sätta ihop PDF‑filen med Pillow och `reportlab`‑biblioteket. För att hålla handledningen lättviktig använder vi `fpdf2`, som låter oss bädda in den ursprungliga bilden och överlagra osynlig text.

```bash
pip install fpdf2
```

```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

Vad hände just nu? Vi placerade den skannade bilden som det synliga lagret, och skrev sedan de igenkända orden ovanpå med vit text som smälter in i den vita bakgrunden. Sökapparater läser fortfarande det dolda lagret, så PDF‑filen blir **sökbar** utan att ändra det visuella utseendet.

## Steg 6: Spara PDF‑byten – Konvertera bild till PDF

Om du föredrar att hantera PDF‑filen i minnet (t.ex. skicka den via ett API), kan du fånga bytena istället för att skriva direkt till disk.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

Den raden demonstrerar det klassiska **konvertera bild till PDF**‑flödet: du börjar med en bild, kör OCR, överlagrar text och slutligen genererar ett PDF‑ström.

## Steg 7: Verifiera resultatet – Snabba kontroller

Efter att du kört skriptet, öppna `receipt_searchable.pdf` i någon PDF‑visare och testa sökrutan (Ctrl + F). Skriv in ett ord du vet finns på kvittot—om det hoppar till rätt ställe har du lyckats **skapa sökbar pdf**!  

Om sökningen misslyckas, dubbelkolla:

1. OCR‑konfidenspoängen (`conf`‑värden). Låg konfidens kan betyda att bilden är suddig.  
2. Koordinaterna för begränsningsrutorna—ibland rapporterar EasyOCR dem i en annan orientering.  
3. Att PDF‑visaren inte är inställd på “endast bild”‑läge (sällsynt, men vissa visare har den möjligheten).

## Fullt fungerande skript

När allt sätts ihop, här är den kompletta, körklara Python‑filen:

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

Spara den som `searchable_pdf.py`, ersätt `YOUR_DIRECTORY`‑platshållarna med faktiska sökvägar, och kör:

```bash
python searchable_pdf.py
```

Du bör se ett bekräftelsemeddelande och en helt ny sökbar PDF i din mapp.

## Vanliga frågor & kantfall

**Vad händer om bilden är i färg?**  
EasyOCR fungerar både med gråskala‑ och färgbilder, men att konvertera till gråskala (`pil_image.convert("L")`) kan ibland förbättra noggrannheten på brusiga skanningar.

**Kan jag hantera flersidiga PDF‑filer?**  
Ja—loopa över varje sidbild, kör OCR‑stegen och lägg till varje sida i samma `FPDF`‑objekt. Glöm inte att återställa markören (`self.add_page()`) för varje ny bild.

**Finns det ett sätt att behålla det ursprungliga textlagret istället för osynlig vit text?**  
Om du behöver ett riktigt “text‑under‑bild”‑PDF (t.ex. för tillgänglighet), överväg att använda `pdfminer` eller `pikepdf` för att bädda in ett dolt textlager med korrekta PDF‑taggar. Det är mer avancerat, men principen är densamma: bakgrundsbild + överlagrad text.

**Vad gör jag om OCR‑konfidensen är låg?**  
Du kan filtrera bort ord med låg konfidens:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## Sammanfattning – Vad vi uppnådde

Vi började med en enkel bild av ett kvitto, **utförde OCR på bild**, extraherade de igenkända strängarna och slutligen **skapade sökbar pdf** som beter sig som vilket professionellt skannat dokument som helst. Processen täckte varje sekundärt nyckelord—**konvertera OCR till PDF**, **extrahera text från bild**, **konvertera bild till PDF**, och **utföra OCR på bild**—så du nu har en återanvändbar verktygslåda för liknande projekt.

### Nästa steg

- Experimentera med andra språk genom att skicka deras ISO‑koder till `easyocr.Reader(['en', 'es'])`.  
- Byt ut EasyOCR mot Tesseract om du behöver en helt offline‑lösning; resten av pipeline förblir densamma.  
- Lägg till visualisering av OCR‑konfidens (rita begränsningsrutor på bilden) för att felsöka problematiska skanningar.  

Har du ett eget knep du vill dela? Kommentera gärna, fork

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}