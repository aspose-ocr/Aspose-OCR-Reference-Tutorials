---
category: general
date: 2026-06-25
description: Voorverwerk afbeelding voor OCR en herken tekst uit een gescand document
  met Python. Stapsgewijze tutorial met volledige code.
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: nl
og_description: Verwerk afbeelding voor OCR en herken tekst uit een gescand document
  met Python. Volg deze gedetailleerde, uitvoerbare tutorial.
og_title: Afbeelding voor OCR in Python voorbewerken – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Afbeelding voor OCR in Python voorbewerken – Complete gids
url: /nl/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preprocess Image for OCR in Python – Complete Guide

Heb je je ooit afgevraagd hoe je **preprocess image for OCR** kunt doen zodat de tekst schoon en betrouwbaar wordt? Je bent niet de enige—de meeste ontwikkelaars lopen tegen hetzelfde probleem aan wanneer de gescande pagina scheef staat of het contrast overal verschilt. Het goede nieuws is dat een paar regels Python dat rommel kunnen rechtzetten, de afbeelding kunnen binariseren en je een scherpe, doorzoekbare tekst teruggeven.

In deze tutorial lopen we de exacte stappen door om **preprocess image for OCR** *en* **recognize text from scanned document** bestanden uit te voeren, met behulp van een populaire OCR‑bibliotheek. Aan het einde heb je een kant‑klaar script, begrijp je waarom elke instelling belangrijk is, en weet je hoe je het kunt aanpassen voor lastige randgevallen.

## What You’ll Need

- Python 3.8 of nieuwer (de code werkt ook op 3.10+)
- Een OCR‑pakket dat de klassen `OcrEngine`, `ImagePreProcessingOptions` en `Image` beschikbaar maakt (bijv. de fictieve `ocr`‑module die in het voorbeeld wordt gebruikt)
- Een gescande of gefotografeerde document dat een beetje scheef staat of een laag contrast heeft
- Je favoriete IDE of een eenvoudige terminal—geen zware GUI nodig

Dat is alles. Geen extra binaries, geen Docker‑gymnastiek. Laten we erin duiken.

## Preprocess Image for OCR – Step‑by‑Step

Hieronder staat de kernworkflow opgesplitst in vijf duidelijke fasen. Elke fase bevat **waarom** we het doen, de exacte **code**, en een korte **uitleg** van wat er onder de motorkap gebeurt.

### Step 1: Create an OCR Engine Instance

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Waarom dit belangrijk is:*  
Het `OcrEngine`‑object is de hersenen van de operatie. Het bevat configuraties zoals taalpakketten, vertrouwensdrempels, en—het belangrijkste voor ons—image‑preprocessing‑vlaggen. Het eerst instantieren geeft ons een schone lei om de trucjes die volgen in te schakelen.

### Step 2: Enable Automatic Deskewing and Binarization

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*Waarom dit belangrijk is:*  
- **Deskewing** draait de afbeelding zodat tekstregels horizontaal worden. OCR‑engines hebben moeite wanneer de basislijn meer dan een paar graden helt.  
- **Binarization** zet de afbeelding om naar puur zwart‑wit, waardoor achtergrondruis die karakterclassificatoren kan verwarren, wordt verwijderd.  
Beide opties zijn *automatisch* in veel moderne bibliotheken, maar je moet ze nog steeds inschakelen—vandaar de expliciete toewijzing.

> **Pro tip:** Als je bronafbeeldingen al perfect uitgelijnd zijn, kun je `auto_deskew=False` instellen om een milliseconde verwerkingstijd te besparen.

### Step 3: Load the Skewed Image You Want to Process

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*Waarom dit belangrijk is:*  
De `Image.load`‑methode leest het bestand in het geheugen en verpakt het in een object dat de OCR‑engine begrijpt. Het haalt ook metadata zoals DPI op, wat de standaard schaalfactor voor deskewing kan beïnvloeden.

> **Edge case:** Als de afbeelding een multi‑page TIFF is, moet je over elke pagina itereren of een helper zoals `ocr.MultiPageImage.load` gebruiken. Dezelfde preprocessing‑instellingen gelden voor elke pagina.

### Step 4: Perform OCR on the Pre‑processed Image

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*Waarom dit belangrijk is:*  
Op dit punt past de engine de eerder ingeschakelde deskew‑ en binarisatiestappen toe, en draait vervolgens zijn neurale netwerk (of klassieke Tesseract‑achtige pipeline) op de opgeschoonde bitmap. Het geretourneerde `result`‑object bevat doorgaans de platte tekst, vertrouwensscores, en soms positionele data voor elk woord.

> **Wat als de tekst nog steeds onduidelijk is?**  
Controleer de afbeeldingsresolutie: OCR werkt het beste bij 300 dpi of hoger. Als je bron lager is, overweeg dan om op te schalen vóór het laden, of vraag de originele scan op bij de documentbron.

### Step 5: Output the Recognized Text

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*Waarom dit belangrijk is:*  
`result.text` is een platte‑stringrepresentatie van alles wat de engine kon lezen. Het afdrukken is handig voor snelle debugging; in een echte app zou je het waarschijnlijk naar een `.txt`‑bestand, een database, of een downstream NLP‑pipeline schrijven.

---

## Recognize Text from Scanned Document – Going Beyond the Basics

Nu de basis‑pipeline werkt, laten we een paar veelvoorkomende variaties verkennen die je kunt tegenkomen wanneer je **recognize text from scanned document** afbeeldingen in de praktijk probeert.

### 1. Handling Multiple Languages

Als je document zowel Engels als Frans bevat, configureer dan de engine vóór stap 1:

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

De meeste OCR‑engines accepteren ISO‑639‑2‑codes; het laden van extra taalpakketten voegt een kleine overhead toe maar verbetert de nauwkeurigheid op meertalige pagina's dramatisch.

### 2. Fine‑Tuning Binarization Thresholds

Automatische binarisatie werkt in de meeste gevallen, maar sommige oude fotokopieën hebben een aangepaste drempel nodig:

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

Experimenteer met waarden tussen 120 en 220 totdat de achtergrond verdwijnt zonder vage tekens te wissen.

### 3. Extracting Layout Information

Soms heb je meer nodig dan ruwe tekst—je wilt weten waar elke alinea zich op de pagina bevindt. Veel engines bieden een `result.blocks`‑collectie:

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

Dit is van onschatbare waarde voor het reconstrueren van tabellen of het behouden van kolomvolgorde.

### 4. Processing a Batch of Files

Als je een map vol gescande PDF’s hebt die naar JPEG’s zijn geconverteerd, wikkel dan de hele flow in een lus:

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

De lus hergebruikt dezelfde `engine`‑instantie, wat efficiënter is dan deze voor elk bestand opnieuw te creëren.

### 5. Dealing with Low‑Resolution Scans

Scans met lage resolutie (< 150 dpi) leveren vaak wazige tekens op. Een snelle remedie is om met een hoogwaardige algoritme op te schalen voordat je de afbeelding aan de OCR‑engine geeft:

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

Opschalen creëert geen details uit het niets, maar de binarisatiestap kan werken met scherpere randen, wat een bescheiden verbetering oplevert.

---

## Expected Output

Het uitvoeren van het oorspronkelijke vijf‑stappen‑script op een matig scheve, 300 dpi scan zou iets moeten afdrukken als:

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

Als je onduidelijke tekens ziet, controleer dan de preprocessing‑vlaggen, afbeeldingsresolutie en taalconfiguratie.

---

## Conclusion

We hebben alles behandeld wat je nodig hebt om **preprocess image for OCR** en **recognize text from scanned document** bestanden te gebruiken met Python. Beginnend met een verse engine‑instantie, schakelden we automatische deskewing en binarisatie in, laadden een scheve afbeelding, voerden de herkenning uit, en drukten de schone tekst af. Onderweg verkenden we meertalige ondersteuning, handmatige drempelaanpassingen, layout‑extractie, batchverwerking, en oplossingen voor lage resolutie.

Probeer het script op je eigen scans—misschien een stapel bonnetjes, een handgeschreven formulier, of een oude krantenknipsel. Zodra je er vertrouwd mee bent, kun je PDF‑generatie toevoegen of de output in een zoekindex voeren. De mogelijkheden zijn eindeloos.

**Klaar voor de volgende uitdaging?** Bekijk onze tutorials over *“Extract Tables from Scanned PDFs with Python”* en *“Train Custom OCR Models with TensorFlow”* om je document‑automatiseringstoolbox verder uit te breiden.

Happy coding, and may your OCR always be crisp!

## What Should You Learn Next?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}