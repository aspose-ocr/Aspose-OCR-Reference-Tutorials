---
category: general
date: 2026-06-25
description: Haal tekst uit een afbeelding met Python OCR. Leer hoe je een afbeelding
  laadt voor OCR, OCR uitvoert in Python, en een bon converteert naar JSON in een
  paar eenvoudige stappen.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: nl
og_description: Tekst uit afbeelding halen met Python OCR. Deze tutorial leidt je
  stap voor stap door het laden van een afbeelding voor OCR, het uitvoeren van OCR
  in Python en het omzetten van een bon naar JSON.
og_title: Tekst uit afbeelding halen in Python – Volledige OCR-gids
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Tekst extraheren uit afbeelding in Python – Volledige OCR-gids
url: /nl/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeelding extraheren in Python – Volledige OCR-gids

Heb je ooit **tekst uit een afbeelding moeten extraheren** maar wist je niet waar te beginnen? In deze tutorial laten we je zien hoe je **een afbeelding laadt voor OCR**, **OCR uitvoert in Python**, en **een bon converteert naar JSON**—alles met slechts een handvol code‑regels.

Als je ooit een bon‑scanapp, een uitgaven‑tracker, of gewoon automatisering van gegevensinvoer hebt gebouwd, zul je zien waarom het beheersen van deze workflow een echte game‑changer is. Aan het einde heb je een werkend script dat een foto van een bon leest en een nette JSON‑payload oplevert, klaar voor downstream‑services.

## Wat je zult leren

We behandelen elke stap, van het installeren van de `aocr`‑bibliotheek tot het verwerken van het ruwe resultaat. Specifiek leer je hoe je:

1. **Een OCR‑engine‑instantie maakt** – het startpunt voor alle herkenningswerk.  
2. **Een afbeelding laadt voor OCR** – vertel de engine welk bestand gelezen moet worden.  
3. **Het exportformaat kiest** – JSON of XML, we kiezen JSON omdat het makkelijker te consumeren is.  
4. **De herkenning uitvoert** – daadwerkelijk OCR in Python toepast.  
5. **Het resultaat afdrukt of opslaat** – converteer de bon naar JSON en bekijk de output.

Er is geen voorafgaande ervaring met OCR vereist; alleen een basis‑Python‑installatie en een afbeeldingsbestand (een bon, een flyer, wat je maar nodig hebt).  

---

![Diagram dat de stroom van tekstextractie uit een afbeelding met Python OCR toont](extract-text-from-image-python-ocr.png){alt="diagram dat de stroom van tekstextractie uit een afbeelding met Python OCR toont"}

## Tekst uit afbeelding – Stap‑voor‑stap Python OCR

Hieronder staat het volledige, kant‑klaar script. Kopieer‑en‑plak het gerust in een bestand genaamd `receipt_ocr.py` en voer `python receipt_ocr.py` uit.

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### Waarom dit werkt

- **Engine‑instantie** – `aocr.OcrEngine()` omvat al het zware werk (model‑laden, pre‑processing, enz.).  
- **Afbeelding laden** – `engine.load_image()` vertelt de bibliotheek precies welke bitmap geanalyseerd moet worden; je kunt JPEG, PNG of zelfs meer‑pagina‑PDF’s gebruiken.  
- **Exportformaat** – Door `engine.export_format` in te stellen op `aocr.ExportFormat.JSON` wordt het resultaat een gestructureerde string, perfect voor API’s die JSON verwachten.  
- **Herkenningsaanroep** – `engine.recognize()` voert de neurale‑net‑inference op de achtergrond uit; het retourneert een JSON‑string met gedetecteerde tekstblokken, vertrouwensscores en lay‑outinformatie.  

---

## Afbeelding laden voor OCR met aocr

Als je je afvraagt of de afbeelding speciale pre‑processing nodig heeft, is het korte antwoord **nee**—`aocr` handelt de meeste gangbare gevallen (contrast‑aanpassing, deskewing) automatisch af. Je kunt echter de nauwkeurigheid verbeteren door:

- De afbeelding minimaal 300 dpi te maken.  
- Onrelevante randen bij te snijden.  
- Vooraf te converteren naar grijstinten (optioneel, `engine.load_image()` doet dit voor je).

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*Pro tip:* Als de bon veel ruis bevat, kan de bovenstaande extra stap de **perform OCR in Python**‑nauwkeurigheid merkbaar verhogen.

---

## Exportformaat kiezen en bon converteren naar JSON

Je vraagt je misschien af: “Waarom niet gewoon platte tekst?” Omdat JSON de hiërarchische structuur (regels, woorden, begrenzingsvakjes) behoudt. Dit maakt het veel makkelijker om later velden zoals *totaalbedrag* of *datum* te mappen.

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

Wanneer je het script uitvoert, zal `json_result` er ongeveer zo uitzien (verkort voor de leesbaarheid):

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

Je hebt nu een **convert receipt to JSON**‑payload die je rechtstreeks kunt invoeren in een database, een REST‑endpoint, of een machine‑learning‑model.

---

## Herkenning uitvoeren en resultaten ophalen

De laatste stap—het daadwerkelijk uitvoeren van OCR—is zo simpel als `recognize()` aanroepen. Achter de schermen doet de bibliotheek:

1. De afbeelding door een voorgetraind convolutioneel netwerk sturen.  
2. De netwerkaoutput decoderen naar leesbare tekens.  
3. Alles verpakken in het gekozen formaat (JSON in ons geval).

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

Als je de output wilt opslaan in plaats van af te drukken, schrijf je deze simpelweg naar een bestand:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*Edge case:* Sommige bonnen bevatten niet‑ASCII‑tekens (bijv. “€” ). Zorg ervoor dat je het bestand opent met UTF‑8‑codering, zoals hierboven getoond, om vervormde tekst te voorkomen.

---

## Volledig werkend voorbeeld (Alle stappen in één script)

Alles bij elkaar gebracht, hier is het definitieve script dat je end‑to‑end kunt uitvoeren:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

Voer het uit met:

```bash
python receipt_ocr.py
```

Je zou een bevestigingsregel moeten zien en, in dezelfde map, een `receipt_output.json`‑bestand met de gestructureerde data.

---

## Conclusie

Je weet nu **hoe je tekst uit een afbeelding kunt extraheren** met Python, hoe je **een afbeelding laadt voor OCR**, hoe je **OCR uitvoert in Python**, en hoe je **een bon converteert naar JSON** voor downstream‑consumptie. Deze end‑to‑end‑flow is lichtgewicht, vereist alleen het `aocr`‑pakket, en kan in elke automatiserings‑pipeline worden geïntegreerd.

Wat nu? Probeer het exportformaat te wijzigen naar XML, experimenteer met verschillende pre‑processing‑technieken, of bouw een kleine Flask‑API die een geüploade bon accepteert en direct de JSON‑payload teruggeeft. De mogelijkheden zijn eindeloos zodra je de basis onder de knie hebt.

Vragen of een probleem? Laat een reactie achter, en happy coding!

## Wat kun je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Tekst uit afbeelding extraheren met Aspose OCR – Stap‑voor‑stap gids](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Tekst uit afbeelding – OCR‑optimalisatie met Aspose.OCR voor .NET](/ocr/english/net/ocr-optimization/)
- [Hoe een tabel uit een afbeelding te extraheren met Aspose.OCR voor .NET](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}