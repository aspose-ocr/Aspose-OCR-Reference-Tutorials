---
category: general
date: 2026-06-19
description: Maak een doorzoekbare PDF van een afbeelding met Python OCR. Leer hoe
  je OCR naar PDF converteert, tekst uit een afbeelding haalt en snel OCR op een afbeelding
  uitvoert.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: nl
og_description: Maak doorzoekbare PDF van een afbeelding met Python OCR. Deze gids
  laat zien hoe je OCR naar PDF converteert, tekst uit een afbeelding haalt en OCR
  op een afbeelding uitvoert.
og_title: Maak een doorzoekbare PDF in Python – Volledige programmeerhandleiding
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
title: Maak een doorzoekbare PDF in Python – Complete stapsgewijze handleiding
url: /nl/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak doorzoekbare PDF in Python – Complete stapsgewijze gids

Heb je ooit een **create searchable PDF** moeten maken van een gescande bon, maar wist je niet waar je moest beginnen? Je bent niet de enige—veel ontwikkelaars lopen tegen dezelfde muur aan wanneer ze voor het eerst proberen een foto van tekst om te zetten in een PDF die je daadwerkelijk kunt doorzoeken.  

In deze tutorial lopen we een praktische oplossing door die je laat **perform OCR on image**, het OCR‑resultaat omzetten in een **searchable PDF**, en zelfs de ruwe tekst eruit halen als je die nodig hebt voor verdere verwerking. Geen poespas, alleen een werkend voorbeeld dat je vandaag nog kunt copy‑paste in je project.

## Wat je zult leren

- Hoe je een lichtgewicht OCR‑engine in Python instelt  
- De exacte stappen om **convert OCR to PDF** uit te voeren en op te slaan als een doorzoekbaar document  
- Manieren om **extract text from image** te doen voor downstream‑analyse  
- Tips voor het omgaan met veelvoorkomende valkuilen zoals beeldoriëntatie en grote bestanden  
- Een complete, uitvoerbare script die je kunt aanpassen aan je eigen use‑case

### Vereisten

- Python 3.8+ geïnstalleerd op je machine  
- Basiskennis van pip en virtuele omgevingen (optioneel maar aanbevolen)  
- Een afbeeldingsbestand (PNG, JPEG, etc.) dat duidelijke, machinaal leesbare tekst bevat  

Als je die hebt, laten we duiken.

## Stap 1: Installeer de vereiste bibliotheek

De code‑snippet die je eerder zag gebruikt een fictief `ocr`‑pakket, maar dezelfde ideeën gelden voor echte bibliotheken zoals **EasyOCR**, **pytesseract**, of **pdfminer.six**. Voor deze gids gebruiken we **EasyOCR** omdat het pure Python is, veel talen ondersteunt, en een handige PDF‑conversiemethode teruggeeft via een hulpfunctie.

```bash
pip install easyocr pillow
```

> **Pro tip:** Installeer binnen een virtuele omgeving (`python -m venv venv && source venv/bin/activate`) om je afhankelijkheden netjes te houden.

## Stap 2: Initialiseert de OCR‑engine – Perform OCR on Image

Nu de bibliotheek klaar is, maken we een OCR‑engine aan en vertellen we deze om met Engelse tekst te werken. Dit is de eerste plek waar we **perform OCR on image**.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

Waarom hebben we een dedicated reader‑object nodig? EasyOCR laadt taalmodellen vooraf, dus het hergebruiken van dezelfde `reader` voor meerdere afbeeldingen is veel efficiënter dan deze elke keer opnieuw te initialiseren.

## Stap 3: Laad de afbeelding – Extract Text from Image

Laten we de afbeelding in het geheugen laden. Deze stap is waar we later **extract text from image** doen, maar eerst laden we hem alleen.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

Als je afbeelding ondersteboven of scheef staat, overweeg dan om Pillow’s `rotate` of `transpose` methoden te gebruiken voordat je hem naar de OCR‑engine stuurt. Een snelle visuele controle kan je later uren debugging besparen.

## Stap 4: Voer de OCR‑engine uit en vang resultaten op

Dit is de kern van het proces—de afbeelding naar de OCR‑engine sturen en gestructureerde data terugkrijgen.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

De `detail=1`‑vlag geeft ons bounding boxes, die we later nodig hebben wanneer we **convert OCR to PDF**. Als je alleen ruwe strings wilt, stel dan `detail=0` in.

## Stap 5: Converteer OCR‑resultaat naar een searchable PDF – Convert OCR to PDF

EasyOCR biedt geen directe PDF‑schrijver, maar we kunnen de PDF zelf samenstellen met Pillow en de `reportlab`‑bibliotheek. Om de tutorial lichtgewicht te houden, gebruiken we `fpdf2`, waarmee we de originele afbeelding kunnen embedden en onzichtbare tekst kunnen overlayen.

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

Wat is er net gebeurd? We plaatsten de gescande afbeelding als de zichtbare laag, en schreven vervolgens de herkende woorden erboven met witte tekst die opgaat in de witte achtergrond. Zoektools lezen nog steeds de verborgen laag, dus wordt de PDF **searchable** zonder de visuele weergave te wijzigen.

## Stap 6: Sla de PDF‑bytes op – Convert Image to PDF

Als je de PDF liever in het geheugen verwerkt (bijv. versturen via een API), kun je de bytes vastleggen in plaats van direct naar schijf te schrijven.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

Die regel toont de klassieke **convert image to PDF** workflow: je begint met een afbeelding, voert OCR uit, overlayt tekst, en geeft uiteindelijk een PDF‑stream uit.

## Stap 7: Verifieer het resultaat – Snelle controles

Nadat je het script hebt uitgevoerd, open `receipt_searchable.pdf` in een PDF‑viewer en probeer de zoekbalk (Ctrl + F). Typ een woord waarvan je weet dat het in de bon staat—als het naar de juiste plek springt, heb je succesvol **create searchable pdf**!  

Als de zoekopdracht mislukt, controleer dan:

1. De OCR‑vertrouwensscores (`conf`‑waarden). Een lage confidence kan betekenen dat de afbeelding onscherp is.  
2. Bounding‑box coördinaten—soms rapporteert EasyOCR ze in een andere oriëntatie.  
3. Dat de PDF‑viewer niet is ingesteld op ‘alleen afbeelding’-modus (zeldzaam, maar sommige viewers hebben die optie).

## Volledig werkend script

Alles samengevoegd, hier is het volledige, kant‑klaar Python‑bestand:

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

Sla dit op als `searchable_pdf.py`, vervang de `YOUR_DIRECTORY`‑placeholders door echte paden, en voer uit:

```bash
python searchable_pdf.py
```

Je zou een bevestigingsbericht moeten zien en een gloednieuwe searchable PDF in je map.

## Veelgestelde vragen & randgevallen

**Wat als de afbeelding in kleur is?**  
EasyOCR werkt met zowel grijswaarden als kleurenafbeeldingen, maar omzetten naar grijswaarden (`pil_image.convert("L")`) kan soms de nauwkeurigheid verbeteren bij ruisende scans.

**Kan ik multi‑page PDF’s verwerken?**  
Ja—loop over elke paginabeeld, voer de OCR‑stappen uit, en voeg elke pagina toe aan hetzelfde `FPDF`‑object. Vergeet niet de cursor te resetten (`self.add_page()`) voor elke nieuwe afbeelding.

**Is er een manier om de originele tekstlaag te behouden in plaats van onzichtbare witte tekst?**  
Als je een echte “text‑under‑image” PDF nodig hebt (bijv. voor toegankelijkheid), overweeg dan `pdfminer` of `pikepdf` te gebruiken om een verborgen tekstlaag met juiste PDF‑tags in te sluiten. Dat is geavanceerder, maar het principe blijft hetzelfde: achtergrondafbeelding + overlay‑tekst.

**Wat als de OCR‑confidence laag is?**  
Je kunt woorden met lage confidence filteren:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## Samenvatting – Wat we hebben bereikt

We begonnen met een eenvoudige afbeelding van een bon, **performed OCR on image**, haalden de herkende strings op, en uiteindelijk **create searchable pdf** die zich gedraagt als elk professioneel gescande document. Het proces besloeg elk secundair trefwoord—**convert OCR to PDF**, **extract text from image**, **convert image to PDF**, en **perform OCR on image**—zodat je nu een herbruikbare toolbox hebt voor elk vergelijkbaar project.

### Volgende stappen

- Experimenteer met andere talen door hun ISO‑codes door te geven aan `easyocr.Reader(['en', 'es'])`.  
- Vervang EasyOCR door Tesseract als je een volledig offline oplossing nodig hebt; de rest van de pijplijn blijft hetzelfde.  
- Voeg OCR‑confidence visualisatie toe (teken bounding boxes op de afbeelding) om problematische scans te debuggen.  

Heb je een twist die je wilt delen? Laat een reactie achter, fork


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}