---
category: general
date: 2026-03-28
description: Hoe ROI OCR'en in Python – Leer hoe je preprocessing‑opties kunt instellen
  voor nauwkeurige tekstextractie uit specifieke afbeeldingsgebieden.
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: nl
og_description: Hoe ROI OCR'en in Python – Deze gids laat zien hoe je preprocessing
  instelt voor betrouwbare tekstextractie uit gedefinieerde beeldgebieden.
og_title: Hoe ROI OCR'en in Python – Hoe de preprocessing in te stellen
tags:
- OCR
- Python
- Aspose
title: How to OCR ROI in Python – How to set preprocessing
url: /nl/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe ROI OCR’en in Python – Hoe preprocessing in te stellen

Heb je je ooit afgevraagd **hoe je ROI OCR’t** in een ruisachtig factuurbeeld zonder de hele pagina in het geheugen te laden? Je bent niet de enige. In veel real‑world projecten hebben we slechts een handvol velden nodig—klantnaam, adres, totalen—dus het scannen van het volledige document is overbodig.  

Het goede nieuws? Met Aspose OCR kun je de engine precies vertellen **waarnaar gezocht moet worden** en zelfs eerst de afbeelding laten opschonen. In deze tutorial lopen we **hoe je preprocessing**‑opties instelt, Regions of Interest (ROI’s) definieert, en schone tekst haalt in slechts een paar regels Python.

Aan het einde van deze gids heb je een kant‑klaar script dat specifieke blokken uit elke factuur, bon of formulier extraheert. Geen extra tools nodig, alleen Aspose OCR en een beetje Python‑logica.

---

## Wat je nodig hebt

- **Python 3.8+** (de code werkt met elke recente versie)  
- **Aspose OCR for Python via .NET** – installeren met `pip install aspose-ocr`  
- Een voorbeeldafbeelding (bijv. `invoice.png`) geplaatst in een map die je kunt refereren  
- Basiskennis van Python‑functies en object‑georiënteerde syntaxis  

Als je dit al hebt, geweldig—laten we direct naar de code gaan.

---

![how to OCR ROI diagram showing ROI boxes on an invoice image](ocr-roi.png "Voorbeeld van hoe ROI OCR’en")  
*Alt‑tekst: diagram dat laat zien hoe ROI‑vakken op een factuurafbeelding worden weergegeven*

---

## Stap 1 – Initialiseer de OCR‑engine (Hoe ROI OCR’en)

Voordat we de engine kunnen vertellen *waar* te zoeken, hebben we een instantie van de OCR‑processor nodig. Dit object bevat alle configuratie en voert de herkenningsstap uit.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*Waarom dit belangrijk is*: De `OcrEngine`‑klasse abstraheert het zware werk (lettertype‑detectie, lay‑outanalyse, enz.). Door één enkele engine te maken, vermijd je het herinitialiseren van zware bronnen voor elke afbeelding, wat de prestaties soepel houdt.

---

## Stap 2 – Laad je bronafbeelding (Hoe ROI OCR’en)

Aspose Storage maakt het laden van afbeeldingen moeiteloos. Geef het pad op, en je krijgt een `Image`‑object dat klaar is voor verwerking.

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*Tip*: Als je met streams werkt (bijv. afbeeldingen geüpload via een web‑API), kun je een `BytesIO`‑object doorgeven aan `Image.load` in plaats van een bestandspad.

---

## Stap 3 – Definieer de Regions of Interest (ROI’s)

Nu beantwoorden we de kernvraag **hoe je ROI OCR’t**: we vertellen de engine de exacte rechthoeken die de gegevens bevatten waarin we geïnteresseerd zijn. Elke ROI wordt gedefinieerd door de linkerbovenhoek (`x`, `y`) en de afmetingen (`width`, `height`).

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*Waarom ROI’s gebruiken?*  
- **Snelheid** – De engine slaat irrelevante delen van de afbeelding over.  
- **Nauwkeurigheid** – Door je te concentreren op een klein gebied, kan ruis elders de herkenner niet verwarren.  
- **Flexibiliteit** – Je kunt zoveel ROI’s toevoegen als nodig; de engine retourneert een lijst met resultaten in dezelfde volgorde.

---

## Stap 4 – Hoe preprocessing in te stellen voor betere OCR‑nauwkeurigheid

Afbeeldingen direct van scanners of telefoons hebben vaak scheefstand, laag contrast of ongelijke belichting. Aspose OCR biedt een `PreprocessingOptions`‑object waarmee je veelvoorkomende correcties kunt inschakelen vóór de herkenning.

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*Hoe dit helpt*:  
- **Deskew** verwijdert de helling die karaktervormen onduidelijk maakt.  
- **Binarize** vermindert kleurnois, waardoor de OCR‑engine een schoon binair beeld krijgt.  
- **Contrast** versterkt zwakke strepen, wat vooral nuttig is voor vervaagde bonnen.

Je kunt met deze vlaggen experimenteren—schakel er één uit en kijk of de output verandert. Dat is de essentie van **hoe preprocessing in te stellen** op een effectieve manier.

---

## Stap 5 – Voer OCR alleen binnen de gedefinieerde ROI’s uit

Met de engine, afbeelding, ROI’s en preprocessing klaar, is het tijd om `recognize` aan te roepen. De methode retourneert een `OcrResult`‑object dat een `regions`‑collectie bevat—elk item komt overeen met de ROI‑volgorde die we hebben opgegeven.

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*Achter de schermen*: De engine cropt elke ROI, past de preprocessing‑pipeline toe, en draait het herkenningsmodel op het opgeschoonde fragment. Omdat we een lijst hebben doorgegeven, behoudt het resultaat dezelfde volgorde, waardoor nabewerking eenvoudig is.

---

## Stap 6 – Lees en gebruik de geëxtraheerde tekst (Hoe ROI OCR’en)

Itereer tenslotte over de `regions`‑lijst en print—of sla op—de herkende strings. Het `Region`‑object exposeert een `text`‑eigenschap die het Unicode‑resultaat bevat.

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**Verwachte output (voorbeeld)**:

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

Als de tekst er onduidelijk uitziet, kijk dan opnieuw naar **hoe preprocessing in te stellen**: misschien `contrast` verhogen of `binarize` uitschakelen voor gekleurde logo’s.

---

## Veelvoorkomende valkuilen en pro‑tips

| Probleem | Waarom het gebeurt | Oplossing (Hoe preprocessing in te stellen) |
|----------|--------------------|--------------------------------------------|
| Scheve tekst verschijnt als onzin | `deskew` uitgeschakeld of afbeelding te sterk gedraaid | Schakel `preprocessing_options.deskew = True` in |
| Cijfers worden punten of vreemde strepen | Laag contrast of agressieve binarisatie | Verlaag `contrast` (bijv. `1.2`) of zet `binarize = False` |
| ROI‑coördinaten liggen een paar pixels mis | Andere DPI of scanner‑schaling | Gebruik een tool (bijv. Paint.NET) om exacte pixelposities te meten, of voeg een kleine marge (`+5` pixels) toe aan elke ROI |
| Leeg resultaat voor een regio | ROI buiten de afbeeldingsgrenzen | Controleer afbeeldingsdimensies: `source_image.width`, `source_image.height` |

---

## De oplossing uitbreiden (Hoe ROI OCR’en in verschillende scenario’s)

- **Dynamische ROI’s**: Als je facturen variabele lay‑outs hebben, kun je eerst een snelle volledige‑pagina OCR uitvoeren om sleutelwoorden (“Customer:”, “Address:”) te vinden en vervolgens ROI’s on‑the‑fly berekenen.  
- **Batchverwerking**: Plaats de bovenstaande stappen in een functie en loop over een map met afbeeldingen. Hergebruik dezelfde `ocr_engine`‑instantie om het geheugenverbruik laag te houden.  
- **Exporteren naar JSON**: In plaats van te printen, bouw een dictionary en dump deze met `json.dumps`; dit maakt downstream‑integratie (bijv. invoeren in een ERP‑systeem) triviaal.

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

---

## Conclusie

Je hebt nu een compleet, uitvoerbaar voorbeeld dat **hoe je ROI OCR’t** in Python laat zien, terwijl je **hoe preprocessing in te stellen** beheerst voor optimale nauwkeurigheid. Door de engine te beperken tot de exacte rechthoeken die je nodig hebt en de afbeelding vooraf op te schonen, krijg je snellere, schonere resultaten—perfect voor factuur‑automatisering, formulier‑digitalisering, of elke situatie waarin slechts een deel van de pagina van belang is.

Klaar voor de volgende stap? Probeer de ROI‑coördinaten aan te passen voor een ander documenttype, of experimenteer met extra preprocessing‑vlaggen zoals `sharpen` of `noise_reduction`. De flexibiliteit van Aspose OCR betekent dat je de pipeline kunt afstemmen op praktisch elke beeldkwaliteit.

Als je tegen een probleem aanloopt, controleer dan de console‑output voor lege regio’s en bekijk de preprocessing‑instellingen opnieuw. Veel programmeerplezier, en moge je OCR altijd accuraat zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}