---
category: general
date: 2026-01-12
description: Voer OCR snel uit op PNG‑bestanden met Python. Leer hoe je tekst uit
  een afbeelding en factuur kunt extraheren, en hoe je een afbeelding kunt laden voor
  OCR met Aspose.OCR.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: nl
og_description: Voer OCR direct uit op PNG. Deze gids laat zien hoe je tekst uit een
  afbeelding en factuur kunt extraheren, de afbeelding kunt laden voor OCR, en de
  resultaten kunt opslaan als JSON en CSV.
og_title: Voer OCR uit op PNG – Volledige Python‑tutorial
tags:
- OCR
- Python
- Image Processing
title: OCR uitvoeren op PNG – Complete Python-gids om tekst uit afbeeldingen te halen
url: /nl/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR uitvoeren op PNG – Complete Python-gids om tekst uit afbeeldingen te extraheren

Heb je ooit **run OCR on PNG** bestanden nodig gehad, maar wist je niet welke bibliotheek je schone, gestructureerde resultaten zou geven? Je bent niet de enige. In veel real‑world projecten—denk aan factuurautomatisering of kassabon‑scannen— is de eerste stap om **extract text from image** bestanden te verwerken, en PNG is een veelgebruikt formaat omdat het verliesvrije kwaliteit behoudt.

In deze tutorial lopen we een hands‑on voorbeeld door met het Aspose.OCR Python‑pakket. Aan het einde van de gids weet je hoe je **load image for OCR** kunt uitvoeren, elke regel tekst kunt ophalen, die data kunt omzetten naar een net JSON‑object, en zelfs kunt exporteren naar CSV voor downstream verwerking. Geen poespas, alleen een praktische, kant‑klaar oplossing.

## Wat je zult leren

- Hoe de Aspose.OCR bibliotheek te installeren en importeren.  
- De exacte stappen om **run OCR on PNG** uit te voeren en het result object te verwerken.  
- Manieren om **extract text from invoice** bestanden te extraheren en de output te formatteren als JSON of CSV.  
- Tips voor het omgaan met afbeeldingen met laag contrast, meertalige documenten en confidence scores.  
- Een complete copy‑and‑paste code‑voorbeeld dat je vandaag kunt uitvoeren.

> **Prerequisite:** Python 3.8+ en een basiskennis van pip. Als je nog nooit Aspose hebt gebruikt, maak je geen zorgen—deze gids behandelt alles wat je nodig hebt om te beginnen.

---

## Stap 1 – Installeer Aspose.OCR en bereid je omgeving voor

Voordat we **run OCR on PNG** kunnen uitvoeren, moet de bibliotheek aanwezig zijn op je systeem.

```bash
pip install aspose-ocr
```

> **Pro tip:** Gebruik een virtuele omgeving (`python -m venv venv`) om afhankelijkheden geïsoleerd te houden. Het voorkomt versieconflicten als je met meerdere projecten werkt.

Na installatie importeer je de modules die we nodig hebben:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

Hier importeren we `asposeocr` voor het zware werk en de ingebouwde `json` bibliotheek voor latere serialisatie.

## Stap 2 – Maak de OCR‑engine en stel de taal in

De OCR‑engine is het kernonderdeel dat daadwerkelijk de pixels leest. Voor de meeste Engelse facturen wil je het Engelse taalpakket gebruiken:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Why this matters:** Het specificeren van de taal beperkt de tekenset, wat de nauwkeurigheid verhoogt en de verwerking versnelt. Als je ooit meertalige facturen moet verwerken, verwissel je gewoon `ocr.Language.ENGLISH` door de juiste enum.

## Stap 3 – Laad de afbeelding voor OCR

Nu gaan we **load image for OCR**. De `Image.load` methode accepteert een bestandspad en werkt met PNG, JPEG, BMP en meer.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Edge case:** Als de PNG ongewoon groot is (meer dan 5 MB), overweeg dan eerst te verkleinen om het geheugenverbruik redelijk te houden. Pillow kan dat in één regel doen:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

## Stap 4 – OCR uitvoeren op PNG en het resultaat vastleggen

Met de engine klaar en de afbeelding geladen, is het tijd om **run OCR on PNG** uit te voeren en het gestructureerde resultaat op te halen.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

Het `ocr_result` object bevat een collectie van `OcrRegion` items, elk met de herkende tekst en een confidence‑score (0‑100). Hier krijg je de gedetailleerde data die nodig is om **extract text from invoice** regels te extraheren.

## Stap 5 – Converteer het resultaat naar JSON en print het mooi

De meeste downstream systemen houden van JSON, dus we zetten de OCR‑output om in een mooi geformatteerde string.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### Voorbeeldoutput

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

Let op hoe elke regel een confidence‑metriek bevat—perfect om lage‑confidence items te filteren als je van plan bent **extract text from invoice** automatisch te extraheren.

## Stap 6 – Sla de OCR‑data op als CSV (één regel per tekst + confidence)

CSV is ideaal voor spreadsheets of snelle data‑imports. Aspose biedt een one‑liner om alles naar een CSV‑bestand te dumpen.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

De gegenereerde CSV ziet er als volgt uit:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

Je kunt het nu openen in Excel, Google Sheets, of invoeren in een database.

## Bonus – Omgaan met low‑confidence tekst en multi‑page PDF's

### Filteren op confidence

Als je alleen regels met hoge zekerheid wilt, filter dan de JSON voordat je deze wegschrijft:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### Multi‑page documenten

Aspose.OCR maakt automatisch een nieuw `page`‑item aan voor elke pagina in een multi‑page PNG of PDF. Loop door `ocr_data["pages"]` om ze allemaal te verwerken—geen extra code nodig.

## Volledig werkend voorbeeld

Hieronder staat het **complete script** dat je kunt kopiëren, plakken en direct kunt uitvoeren. Vervang `YOUR_DIRECTORY` door de map die je PNG‑bestand bevat.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

Voer het script uit met `python run_ocr.py` en je ziet de JSON‑dump in de console, een CSV‑bestand op schijf, en een gefilterde lijst van high‑confidence items.

## Veelgestelde vragen

**Q: Kan ik dit gebruiken om tekst te extraheren uit een gescande kassabon in plaats van een factuur?**  
A: Absoluut. Hetzelfde workflow geldt—wijs gewoon `image_path` naar je kassabon‑PNG. Als de kassabon een andere taal gebruikt, wissel je `engine.language` overeenkomstig.

**Q: Wat als mijn PNG gedraaide tekst bevat?**  
A: Aspose.OCR detecteert automatisch de oriëntatie, maar voor hardnekkige gevallen kun je de afbeelding handmatig roteren met Pillow voordat je deze aan de engine geeft.

**Q: Heb ik een betaalde licentie nodig voor Aspose.OCR?**  
A: De bibliotheek biedt een gratis evaluatiemodus met een watermerk op de output. Voor productiegebruik heb je een licentie nodig, die je kunt verkrijgen via de Aspose‑website.

## Conclusie

We hebben alles behandeld wat je nodig hebt om **run OCR on PNG** bestanden te gebruiken met Python: het installeren van de SDK, het laden van de afbeelding, het extraheren van gestructureerde tekst, en het opslaan van het resultaat als JSON of CSV. Of je nu **extract text from image** wilt voor een simpel script of **extract text from invoice** voor een geautomatiseerde boekhoud‑pipeline, de bovenstaande stappen geven je een solide, productie‑gereed fundament.

Vervolgens kun je het volgende verkennen:

- Het integreren van de CSV‑output met een database voor bulk‑factuuropslag.  
- Het toevoegen van post‑processing met reguliere expressies om data, bedragen of btw‑nummers te extraheren.  
- Het gebruiken van de `ocr_engine.recognize_barcode` functie als je facturen QR‑codes bevatten.

Probeer het, pas de confidence‑drempels aan, en zie hoe je document‑verwerkingsworkflow een fluitje van een cent wordt. Heb je meer vragen of een coole use‑case om te delen? Laat een reactie achter—happy OCRing!

![run OCR on PNG example](run-ocr-on-png.png "run OCR on PNG – visual example of OCR result")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}