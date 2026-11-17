---
category: general
date: 2026-05-31
description: Leer hoe je OCR-gebied van interesse gebruikt om een afbeelding te laden
  voor OCR en tekst uit een rechthoek te extraheren, perfect voor het herkennen van
  het bedrag op een factuur.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: nl
og_description: Beheers het OCR-gebied van interesse om een afbeelding voor OCR te
  laden, tekst uit een rechthoek te extraheren en tekst van een factuur te herkennen
  in één tutorial.
og_title: OCR-regio van belang – Stapsgewijze Python-gids
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
title: OCR‑regio van belang – Tekst extraheren uit een rechthoek in Python
url: /nl/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Region of Interest – Tekst extraheren uit rechthoek in Python

Heb je je ooit afgevraagd hoe je **ocr region of interest** een specifiek deel van een gescande factuur kunt verwerken zonder de hele pagina aan de engine te voeren? Je bent niet de eerste die naar een wazige bon staart en zich afvraagt: “Hoe haal ik het bedrag eruit dat ergens rechtsonder staat?” Het goede nieuws is dat je de OCR‑bibliotheek precies kunt vertellen waar hij moet kijken, waardoor zowel snelheid als nauwkeurigheid enorm toenemen.

In deze gids lopen we een compleet, uitvoerbaar voorbeeld door dat laat zien hoe je **load image for OCR**, een **region of interest** definieert, en vervolgens **extract text from rectangle** toepast om uiteindelijk **recognize text from invoice** te doen en de klassieke vraag “hoe haal je het bedrag eruit” te beantwoorden. Geen vage verwijzingen—alleen concrete code, duidelijke uitleg, en een paar pro‑tips die je eerder had willen weten.

---

## Wat je gaat bouwen

1. Laadt een factuurafbeelding van de schijf.  
2. Markeert een rechthoekige ROI waar het totale bedrag zich bevindt.  
3. Voert OCR alleen binnen die ROI uit.  
4. Print de opgeschoonde bedrag‑string.  

Dit werkt met elke OCR‑bibliotheek die ROI ondersteunt—hier gebruiken we een fictief maar representatief `SimpleOCR`‑pakket dat populaire tools zoals Tesseract of EasyOCR nabootst. Voel je vrij om het te vervangen; de concepten blijven hetzelfde.

---

## Vereisten

- Python 3.8+ geïnstalleerd (`python --version` moet ≥3.8 tonen).  
- Een via pip te installeren OCR‑pakket (bijv. `pip install simpleocr`).  
- Een factuurafbeelding (PNG of JPEG) geplaatst in een map die je kunt refereren.  
- Basiskennis van Python‑functies en -klassen (niets geavanceerd).

Als je die al hebt, prima—laten we erin duiken. Zo niet, haal dan eerst de afbeelding; de rest van de stappen is onafhankelijk van de feitelijke bestandsinhoud.

---

## Stap 1: Afbeelding laden voor OCR

Het eerste wat elke OCR‑workflow nodig heeft, is een bitmap om van te lezen. De meeste bibliotheken bieden een eenvoudige `load_image`‑methode die een bestandspad accepteert. Zo doe je het met onze `SimpleOCR`‑engine:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** Gebruik absolute paden of `os.path.join` om “bestand niet gevonden” verrassingen te vermijden wanneer je het script vanuit een andere werkmap uitvoert.

---

## Stap 2: OCR Region of Interest definiëren

In plaats van de engine de hele pagina te laten scannen, vertellen we hem *exact* waar het bedrag staat. Dit is de **ocr region of interest** stap, en het is de sleutel tot betrouwbare extractie, vooral wanneer het document rommelige kopteksten of voetteksten bevat.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

Waarom die getallen? `x` en `y` zijn pixel‑offsets vanaf de linkerbovenhoek, terwijl `width` en `height` de afmetingen van de doos beschrijven. Als je het niet zeker weet, open de afbeelding in een editor, zet een liniaal aan en noteer de coördinaten. Veel IDE’s laten zelfs de cursorpositie zien tijdens het zweven.

---

## Stap 3: Tekst extraheren uit rechthoek

Nu de ROI is ingesteld, vragen we de engine om **recognize text from invoice** maar beperkt tot de rechthoek die we zojuist hebben toegevoegd. De aanroep retourneert een result‑object dat doorgaans de ruwe string, vertrouwensscores en soms begrenzingskaders bevat.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

Achter de schermen iterereert `recognize()` over elke ROI, snijdt dat deel uit, voert het OCR‑model uit en voegt de resultaten samen. Daarom kan het definiëren van een strakke **extract text from rectangle**‑regio seconden schelen in de verwerkingstijd voor batch‑taken.

---

## Stap 4: Hoe het bedrag te extraheren – Output opschonen

OCR is niet perfect; je krijgt vaak vreemde spaties, regeleinden of zelfs verkeerd gelezen tekens (denk aan “S” vs “5”). Een snelle `strip()` en een kleine regex lossen meestal het probleem op voor monetaire waarden.

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

> **Waarom dit belangrijk is:** Als je het bedrag in een database of een betalingsgateway wilt invoeren, heb je een voorspelbaar formaat nodig. Het verwijderen van witruimte en het filteren van niet‑numerieke tekens voorkomt fouten later in de keten.

---

## Stap 5: Recognize Text from Invoice – Volledig script

Alles bij elkaar, hier is het volledige, kant‑klaar script. Sla het op als `extract_amount.py` en voer `python extract_amount.py` uit.

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

### Verwachte output

```
Amount: 1,245.67
```

Als de ROI niet goed uitgelijnd is, zie je misschien iets als `Amount: 1245.6S`—let op de vreemde “S”. Pas de rechthoekcoördinaten aan en voer opnieuw uit totdat de output er schoon uitziet.

---

## Veelvoorkomende valkuilen & randgevallen

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **ROI te klein** | De bedragtekst wordt afgesneden, wat leidt tot gedeeltelijke herkenning. | Vergroot `width`/`height` met ~10‑20 % en test opnieuw. |
| **Onjuiste DPI** | Scans met lage resolutie (≤150 dpi) verminderen de OCR‑nauwkeurigheid. | Resample de afbeelding naar 300 dpi vóór het laden, of vraag de scanner om een hogere DPI. |
| **Meerdere valuta's** | Regex pakt de eerste numerieke groep, die een factuurnummer kan zijn. | Verfijn de regex om naar valutasymbolen (`$`, `€`, `£`) vóór de cijfers te zoeken. |
| **Gedraaide facturen** | OCR‑engines gaan uit van rechtopstaande tekst; gedraaide pagina's breken de herkenning. | Pas een rotatiecorrectie toe (`ocr_engine.rotate(90)`) vóór het toevoegen van ROI. |
| **Ruis op achtergrond** | Schaduwen of stempels verwarren het model. | Pre‑process met een eenvoudige drempel (`cv2.threshold`) of gebruik een denoise‑filter. |

Het vroeg aanpakken van deze randgevallen bespaart je later uren aan debuggen.

---

## Pro‑tips voor real‑world projecten

- **Batchverwerking:** Loop over een map met facturen, bereken ROI dynamisch (bijv. op basis van sjabloondetectie), en sla resultaten op in CSV.  
- **Sjabloonmatching:** Als je verschillende factuurlay-outs verwerkt, onderhoud dan een JSON‑map van `template_id → ROI‑coördinaten`. Wissel ROI op basis van een snelle lay‑out‑classifier.  
- **Parallelle uitvoering:** Gebruik `concurrent.futures.ThreadPoolExecutor` om meerdere OCR‑instanties gelijktijdig uit te voeren—ideaal voor high‑volume back‑office pipelines.  
- **Vertrouwensfiltering:** De meeste OCR‑resultaten bevatten een vertrouwensscore. Verwijder resultaten onder een drempel (bijv. 85 %) en markeer ze voor handmatige controle.

---

## Conclusie

We hebben alles behandeld wat je nodig hebt om **ocr region of interest**, **load image for OCR**, **extract text from rectangle**, en uiteindelijk **recognize text from invoice** uit te voeren om de klassieke **how to extract amount**‑vraag te beantwoorden. Het script is compact, maar toch flexibel genoeg om zich aan te passen aan verschillende documentformaten, talen en OCR‑back‑ends.

Nu je de basis onder de knie hebt, overweeg het uitbreiden van de workflow: voeg barcode‑scanning toe, integreer met een PDF‑parser, of stuur het geëxtraheerde bedrag naar een boekhoud‑API. De mogelijkheden zijn eindeloos, en met een goed gedefinieerde ROI krijg je altijd snellere, schonere resultaten.

Als je tegen een probleem aanloopt, laat dan een reactie achter—veel succes met OCRen!

![ocr region of interest voorbeeld](https://example.com/ocr_roi_example.png "ocr region of interest voorbeeld")


## Wat kun je hierna leren?

- [Hoe tekst uit afbeelding te extraheren door rechthoeken voor OCR voor te bereiden](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Tekst uit afbeelding extraheren Java met Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Tekst uit afbeelding extraheren – OCR-optimalisatie met Aspose.OCR voor .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}