---
category: general
date: 2026-06-25
description: Laad een afbeelding voor OCR en voer OCR uit op een PNG met een stap‑voor‑stap
  Python‑tutorial met aocr. Leer debuggen, loggen en best practices.
draft: false
keywords:
- load image for OCR
- perform OCR on PNG
- aocr logging setup
- OCR debugging Python
- image preprocessing OCR
language: nl
og_description: Laad afbeelding voor OCR en voer OCR uit op PNG met aocr. Deze gids
  leidt je door logging, het laden van afbeeldingen en herkenning met volledige code.
og_title: Afbeelding laden voor OCR – Stapsgewijze Python‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Load image for OCR and perform OCR on PNG with a step‑by‑step Python
    tutorial using aocr. Learn debugging, logging, and best practices.
  headline: Load Image for OCR – Complete Guide to Perform OCR on PNG Files
  type: TechArticle
- questions:
  - answer: Usually not. `aocr` handles PNG natively, but if the image is huge (>10
      MP) you might want to downscale first to speed up processing.
    question: Do I need to convert the PNG to another format?
  - answer: Rotate the log after each run or limit the level to `INFO` once you’re
      confident the pipeline works.
    question: What if the logger file grows too large?
  - answer: Absolutely. Just call `ocr_png` for each file; the function creates a
      fresh logger each time, keeping logs isolated.
    question: Can I process multiple images in a loop?
  - answer: Yes – `engine.result` also contains `boxes` and `confidences`. Explore
      the `aocr` docs for `result.boxes` if you need layout information.
    question: Is there a way to get bounding boxes instead of plain text?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Afbeelding laden voor OCR – Complete gids voor het uitvoeren van OCR op PNG‑bestanden
url: /nl/python/general/load-image-for-ocr-complete-guide-to-perform-ocr-on-png-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Afbeelding Laden voor OCR – Complete Gids voor OCR op PNG-bestanden

Heb je ooit **load image for OCR** moeten doen maar wist je niet hoe je juiste debugging moet opzetten? Je bent niet de enige. In veel projecten is de eerste hindernis het PNG in de engine krijgen terwijl je toch kunt zien wat er onder de motorkap gebeurt.  

In deze tutorial lopen we je stap voor stap alles door wat je nodig hebt om **perform OCR on PNG** bestanden te gebruiken met de `aocr` library – van het instellen van een logger voor gedetailleerde output tot het daadwerkelijk herkennen van tekst. Aan het einde heb je een herbruikbaar script dat je in elk Python‑project kunt plaatsen, en begrijp je waarom elk onderdeel belangrijk is.

## Wat je zult leren

- Hoe je de `aocr` logger initialiseert zodat je elke stap kunt volgen.
- De exacte code om **load image for OCR** te gebruiken met `aocr.OcrEngine`.
- Hoe je het logniveau configureert om gedetailleerde debug‑informatie te krijgen.
- Het draaien van de engine om **perform OCR on PNG** uit te voeren en de resultaten op te halen.
- Tips voor het omgaan met veelvoorkomende valkuilen zoals ontbrekende bestanden of niet‑ondersteunde formaten.

Ervaring met `aocr` is niet vereist; alleen een werkende Python 3‑installatie en een afbeelding die je wilt lezen. Laten we beginnen.

![voorbeeld van afbeelding laden voor OCR](assets/load-image-ocr.png "Illustratie van het laden van een afbeelding voor OCR in Python")

## Vereisten

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| Python 3.8+ | `aocr` richt zich op moderne interpreters en gebruikt type‑hints. |
| `aocr` library geïnstalleerd (`pip install aocr`) | Zonder het pakket bestaan de klassen die we gebruiken niet. |
| Een PNG‑afbeelding die je wilt lezen | De tutorial richt zich op **perform OCR on PNG**, dus een PNG is essentieel. |
| Schrijfrechten voor een log‑directory | De logger moet `ocr_debug.log` aanmaken. |

Als je een van deze mist, installeer ze dan nu – het duurt maar een minuut.

```bash
pip install aocr
```

## Stap 1: Afbeelding Laden voor OCR – Logger Initialiseren

Voordat je de afbeelding aanraakt, stel je een logger in. Debuggen van OCR kan een nachtmerrie zijn als je blind bent voor wat de engine doet. De `aocr.Logging`‑klasse schrijft alles naar een bestand, en door het niveau op `DEBUG` te zetten zie je elke interne aanroep.

```python
import aocr

# Create a logger instance
ocr_logger = aocr.Logging()
# Choose where the log file will live – adjust the path to suit your project
ocr_logger.set_output_file("logs/ocr_debug.log")

# DEBUG gives you the most detail; you can switch to INFO for less noise
ocr_logger.set_level(aocr.LoggingLevel.DEBUG)
```

**Waarom dit belangrijk is:**  
Als de OCR‑engine het bestand niet kan vinden of het afbeeldingsformaat niet wordt ondersteund, legt de logger de stack‑trace van de uitzondering vast. Dat bespaart je later eindeloos giswerk.

## Stap 2: OCR op PNG Uitvoeren – Engine Configureren

Nu de logger klaar is, koppel je deze aan de OCR‑engine. Deze stap verbindt de twee zodat elke engine‑actie wordt geregistreerd.

```python
# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
# Plug the logger into the engine
ocr_engine.logging = ocr_logger
```

**Pro tip:**  
Je kunt dezelfde `ocr_engine`‑instantie hergebruiken voor meerdere afbeeldingen. Vergeet alleen niet eventuele vorige staat te wissen als je een batch verwerkt.

## Stap 3: Afbeelding Laden voor OCR – PNG‑bestand Voeden

Dit is de kern van de tutorial: daadwerkelijk **load image for OCR**. De `load_image`‑methode accepteert een bestandspad; hij decodeert intern de PNG naar een bitmap die de engine kan begrijpen.

```python
# Path to the PNG you want to read
image_path = "samples/invoice.png"

# Load the image – this is where we “load image for OCR”
ocr_engine.load_image(image_path)
```

### Randgevallen om in de gaten te houden

1. **Bestand Niet Gevonden** – Als het pad onjuist is, werpt `aocr` een `FileNotFoundError`. De logger noteert dit, maar je kunt het ook opvangen:

   ```python
   try:
       ocr_engine.load_image(image_path)
   except FileNotFoundError as e:
       print(f"❌ Could not locate {image_path}: {e}")
       raise
   ```

2. **Niet‑Ondersteund Formaat** – Hoewel PNG breed wordt ondersteund, kan een beschadigd bestand `UnsupportedFormatError` veroorzaken. Overweeg in dat geval de afbeelding met Pillow naar een schone PNG te converteren voordat je laadt.

## Stap 4: OCR op PNG Uitvoeren – Herkenning Starten

Nu de afbeelding in het geheugen staat, kun je eindelijk **perform OCR on PNG**. De `recognize`‑methode start de pipelines van de engine (pre‑processing, segmentatie, classificatie) en vult het result‑object.

```python
# Execute the OCR process
ocr_engine.recognize()
```

Na deze oproep bevat de engine de herkende tekst. Je kunt er toegang toe krijgen via het `result`‑attribuut:

```python
# Retrieve the plain text output
recognized_text = ocr_engine.result.text
print("📝 OCR Result:")
print(recognized_text)
```

**Waarom je het resultaat moet controleren:**  
Sommige OCR‑engines geven lege strings terug voor beelden met weinig contrast. Het resultaat meteen zien laat je beslissen of je moet pre‑processen (bijv. contrast verhogen) voordat je opnieuw draait.

## Stap 5: Alles Samenvatten – Een Herbruikbare Functie

Door de onderdelen in één functie te combineren, kun je deze gemakkelijk aanroepen vanuit andere scripts of een webservice. Dit toont ook hoe je **load image for OCR** en **perform OCR on PNG** in één nette package kunt gebruiken.

```python
def ocr_png(image_path: str, log_dir: str = "logs") -> str:
    """
    Load a PNG image, run aocr OCR, and return the extracted text.
    
    Parameters
    ----------
    image_path : str
        Full path to the PNG file.
    log_dir : str, optional
        Directory where the debug log will be written.
    
    Returns
    -------
    str
        The plain‑text OCR result.
    """
    import os
    import aocr

    # Ensure the log directory exists
    os.makedirs(log_dir, exist_ok=True)

    # ---------- Logging ----------
    logger = aocr.Logging()
    logger.set_output_file(os.path.join(log_dir, "ocr_debug.log"))
    logger.set_level(aocr.LoggingLevel.DEBUG)

    # ---------- Engine ----------
    engine = aocr.OcrEngine()
    engine.logging = logger

    # ---------- Load Image ----------
    try:
        engine.load_image(image_path)
    except Exception as exc:
        logger.error(f"Failed to load image {image_path}: {exc}")
        raise

    # ---------- Recognize ----------
    engine.recognize()
    return engine.result.text

# Example usage
if __name__ == "__main__":
    txt = ocr_png("samples/invoice.png")
    print("\n--- Extracted Text ---\n")
    print(txt)
```

Het uitvoeren van het script genereert een gedetailleerd `ocr_debug.log` in de `logs`‑map, en print vervolgens de herkende tekst naar de console. Je hebt nu een **perform OCR on PNG**‑utility die je elders kunt importeren.

## Veelgestelde Vragen & Valkuilen

- **Moet ik de PNG naar een ander formaat converteren?**  
  Meestal niet. `aocr` verwerkt PNG natively, maar als de afbeelding enorm is (>10 MP) wil je misschien eerst verkleinen om de verwerking te versnellen.

- **Wat als het logger‑bestand te groot wordt?**  
  Roteer de log na elke run of beperk het niveau tot `INFO` zodra je zeker bent dat de pipeline werkt.

- **Kan ik meerdere afbeeldingen in een lus verwerken?**  
  Zeker. Roep gewoon `ocr_png` aan voor elk bestand; de functie maakt elke keer een nieuwe logger aan, waardoor logs geïsoleerd blijven.

- **Is er een manier om begrenzingsvakken te krijgen in plaats van platte tekst?**  
  Ja – `engine.result` bevat ook `boxes` en `confidences`. Bekijk de `aocr`‑documentatie voor `result.boxes` als je lay‑outinformatie nodig hebt.

## Conclusie

Je weet nu hoe je **load image for OCR** en **perform OCR on PNG** kunt gebruiken met de `aocr` library, inclusief een robuuste logging‑configuratie die debuggen pijnloos maakt. De voorbeeldfunctie omvat de volledige workflow, zodat je deze in elk project kunt plaatsen en direct tekst kunt extraheren.

Volgende stappen? Probeer de engine verschillende beeldtypen (JPEG, TIFF) te voeren om te zien hoe de nauwkeurigheid verandert, of experimenteer met pre‑processing technieken zoals drempelwaardes om resultaten op ruisende scans te verbeteren. En als je benieuwd bent naar het extraheren van gestructureerde data (tabellen, formulieren), bekijk dan de `aocr`‑secties over lay‑outanalyse – ze passen goed bij wat je net hebt gebouwd.

Veel plezier met coderen, en moge je OCR‑pipelines altijd foutloos zijn!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Tekst Extracten uit Afbeelding met Aspose OCR – Stapsgewijze Gids](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Hoe een Afbeelding OCR‑en – OCR op Afbeelding Uitvoeren in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Tekst Extracten uit Afbeelding – OCR‑optimalisatie met Aspose.OCR voor .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}