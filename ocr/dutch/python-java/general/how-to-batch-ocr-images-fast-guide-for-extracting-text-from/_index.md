---
category: general
date: 2026-01-12
description: Hoe je afbeeldingen snel batch‑OCR't en tekst uit JPEG‑bestanden haalt
  in Python. Leer stap‑voor‑stap batchverwerking met een volledig uitvoerbaar voorbeeld.
draft: false
keywords:
- how to batch OCR images
- extract text from JPEG files
language: nl
og_description: Hoe afbeeldingen in batch OCR'en en tekst uit JPEG‑bestanden extraheren.
  Deze gids leidt je door een complete, kant‑klaar Python‑oplossing.
og_title: Hoe afbeeldingen batch-OCR – Snelle Python‑tutorial
tags:
- OCR
- Python
- image processing
title: Hoe batch-OCR op afbeeldingen toepassen – Snelle gids voor het extraheren van
  tekst uit JPEG‑bestanden
url: /nl/python-java/general/how-to-batch-ocr-images-fast-guide-for-extracting-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe batch OCR‑afbeeldingen – Snelle gids voor het extraheren van tekst uit JPEG‑bestanden

Heb je je ooit afgevraagd **hoe je batch OCR‑afbeeldingen** kunt uitvoeren zonder voor elk bestand een apart script te schrijven? Je bent niet de enige. In veel projecten—factuurscanning, archiefdigitalisering of contentmoderatie—moeten we tekst uit tientallen of honderden JPEG‑bestanden in één keer halen. Het goede nieuws is dat je dit kunt doen met slechts een paar regels Python, en dat je een herbruikbare engine krijgt die je in elke pipeline kunt gebruiken.

In deze tutorial laten we je precies zien **hoe je batch OCR‑afbeeldingen** uitvoert, vervolgens lopen we door het extraheren van tekst uit JPEG‑bestanden, het afhandelen van randgevallen en het verifiëren van de output. Aan het einde heb je een zelfstandige script die je op elke map met afbeeldingen kunt uitvoeren, en begrijp je waarom batchverwerking belangrijk is voor prestaties en onderhoudbaarheid.

## Wat je zult leren

- Een eenvoudige OCR‑engine opzetten en configureren voor Engels.  
- Alle JPEG‑bestanden uit een map verzamelen met `pathlib`.  
- De OCR‑engine één keer aanroepen om de hele batch te verwerken.  
- Een voorbeeld van de herkende tekst voor elke afbeelding weergeven.  
- Tips voor het verwerken van grote batches, verschillende talen en veelvoorkomende valkuilen.

**Voorvereisten**: Python 3.8+, de `ocr`‑bibliotheek (of een compatibele wrapper), en een map met JPEG‑afbeeldingen die je wilt analyseren. Er zijn geen externe services nodig—alles draait lokaal.

---

## Stap 1: Initialise de OCR Engine – De kern van hoe batch OCR‑afbeeldingen uit te voeren

Voordat we **batch OCR‑afbeeldingen** kunnen uitvoeren, hebben we een engine nodig die tekst kan lezen. In de meeste bibliotheken maak je een engine‑object aan, stel je eventueel de taal in, en hergebruik je het voor elk bestand.

```python
import ocr
import pathlib

# Create the OCR engine and set it to English (the most common case)
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

*Waarom dit belangrijk is*: Het één keer initialiseren van de engine voorkomt de overhead van het herhaaldelijk laden van taalmodellen. Het geeft je ook één plek om instellingen aan te passen (bijv. DPI, whitelist van tekens) die op de hele batch van toepassing zijn.

> **Pro tip**: Als je van plan bent meertalige documenten te verwerken, schakel dan `ocr.Language.ENGLISH` naar `ocr.Language.MULTI` of laad meerdere taalpakketten voordat de batch start.

---

## Stap 2: Verzamel alle JPEG‑bestanden – Het “Tekst extraheren uit JPEG‑bestanden”‑deel

Nu de engine klaar is, moeten we aangeven op welke afbeeldingen deze moet werken. Het gebruik van `pathlib` maakt de code platformonafhankelijk en beknopt.

```python
# Replace YOUR_DIRECTORY with the path that holds your JPEG files
image_dir = pathlib.Path("YOUR_DIRECTORY/")
image_paths = list(image_dir.glob("*.jpg"))  # only JPEG files, case‑sensitive
```

*Waarom dit belangrijk is*: Door eerst de bestandenlijst te verzamelen, kunnen we de hele collectie in één oproep aan de OCR‑engine voeren—precies waar “hoe batch OCR‑afbeeldingen” om draait. Als je sub‑mappen hebt, kun je `glob("**/*.jpg")` aanpassen om recursief te zoeken.

> **Randgeval**: Als je afbeeldingen gemengde extensies hebben (`.jpeg`, `.JPG`), breid dan het glob‑patroon uit: `image_dir.rglob("*.[jJ][pP][eE]?g")`.

---

## Stap 3: Verwerk de hele batch in één oproep – De echte kracht van batch OCR

De meeste moderne OCR‑bibliotheken bieden een `process_batch`‑methode (of een vergelijkbare naam) die een iterabele van bestandspaden accepteert. Dit is de kern van **hoe je batch OCR‑afbeeldingen** efficiënt uitvoert.

```python
# Process every JPEG file in a single batch operation
ocr_results = ocr_engine.process_batch(image_paths)
```

*Waarom dit belangrijk is*: Een enkele batch‑oproep vermindert het aantal Python‑naar‑C‑overgangen, houdt het taalmodel in het geheugen geladen, en maakt vaak interne parallelisatie mogelijk. Het resultaat is een lijst van objecten—elk met de herkende tekst en vertrouwensscores.

> **Prestatie‑opmerking**: Voor zeer grote batches (duizenden afbeeldingen) kun je overwegen de lijst op te splitsen in kleinere delen (bijv. 200 bestanden) om overmatig geheugenverbruik te voorkomen.

---

## Stap 4: Toon een voorbeeld van de geëxtraheerde tekst – Snelle validatie

Nadat de batch is voltooid, is het handig om een kijkje te nemen naar de eerste paar tekens van elk resultaat. Dit helpt je te bevestigen dat de OCR daadwerkelijk tekst uit je JPEG‑bestanden haalt.

```python
for image_path, ocr_result in zip(image_paths, ocr_results):
    # Show the image name and the first 100 characters of its recognised text
    preview = ocr_result.text[:100].replace("\n", " ").strip()
    print(f"{image_path.name}: {preview}...")
```

*Waarom dit belangrijk is*: Een korte preview laat je duidelijke fouten (bijv. lege output, onleesbare tekens) opmerken zonder elk bestand te openen. Als je systematische problemen ziet, kun je de engine‑instellingen aanpassen en de batch opnieuw uitvoeren.

> **Veelvoorkomende valkuil**: Het vergeten te strippen van newline‑karakters kan de preview rommelig maken. De regel `replace("\n", " ")` maakt het schoon.

---

## Volledig werkend voorbeeld – Alle stappen gecombineerd

Hieronder staat het volledige script dat je kunt kopiëren‑plakken, het pad naar de map kunt aanpassen, en kunt uitvoeren. Het demonstreert de volledige **hoe batch OCR‑afbeeldingen** workflow van begin tot eind.

```python
import ocr
import pathlib

def batch_ocr_jpeg(folder: str):
    """
    Process all JPEG files in `folder` and print a 100‑character preview
    of the recognised text for each image.
    """
    # Step 1 – Initialise OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – Gather JPEG paths
    img_dir = pathlib.Path(folder)
    jpeg_paths = list(img_dir.glob("*.jpg"))  # add more patterns if needed

    if not jpeg_paths:
        print("No JPEG files found in the specified directory.")
        return

    # Step 3 – Batch process
    results = engine.process_batch(jpeg_paths)

    # Step 4 – Display previews
    for path, res in zip(jpeg_paths, results):
        preview = res.text[:100].replace("\n", " ").strip()
        print(f"{path.name}: {preview}...")

if __name__ == "__main__":
    # Replace with the path containing your JPEG images
    batch_ocr_jpeg("YOUR_DIRECTORY/")
```

**Verwachte output** (voorbeeld):

```
invoice_001.jpg: Invoice #001  Date: 2024-03-15  Total: $1,245.00  Bill To: Acme Corp...
receipt_202.jpg: Receipt 202  Store: QuickMart  Total: $45.67  Date: 03/12/2024...
...
```

Als de preview betekenisvolle tekst toont, heb je succesvol **tekst uit JPEG‑bestanden** geëxtraheerd met een batch‑aanpak.

---

## Grote batches verwerken en geavanceerde scenario's

### Grote werklasten chunken

Bij het verwerken van duizenden afbeeldingen kan geheugen een knelpunt worden. Splits de lijst in kleinere chunks:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(jpeg_paths, 200):  # 200 files per batch
    results = engine.process_batch(chunk)
    # process results as shown earlier
```

### Talen wisselen

Als je documenten Frans of Spaans bevatten, wijzig dan de taal vóór de batch:

```python
engine.language = ocr.Language.FRENCH  # or ocr.Language.SPANISH
```

### Resultaten opslaan op schijf

In plaats van af te drukken, wil je misschien elk OCR‑resultaat naar een `.txt`‑bestand schrijven:

```python
output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for path, res in zip(jpeg_paths, results):
    txt_path = output_dir / f"{path.stem}.txt"
    txt_path.write_text(res.text, encoding="utf-8")
```

---

## Conclusie

Je weet nu **hoe je batch OCR‑afbeeldingen** kunt uitvoeren en betrouwbaar **tekst uit JPEG‑bestanden** kunt extraheren met een compacte Python‑script. Door de engine één keer te initialiseren, alle JPEG‑paden te verzamelen, ze in één batch te verwerken en de output te previewen, bereik je zowel snelheid als eenvoud. Vanaf hier kun je de workflow uitbreiden—meertalige ondersteuning toevoegen, resultaten in een database opslaan, of het script integreren in een grotere document‑verwerkings‑pipeline.

Klaar voor de volgende stap? Probeer de `ocr`‑bibliotheek te vervangen door Tesseract, experimenteer met verschillende beeld‑pre‑processing (drempeldetectie, schalen), of voer de geëxtraheerde tekst in een natural‑language‑processing‑model voor automatische categorisatie. De mogelijkheden zijn eindeloos, en je hebt een solide basis om op voort te bouwen.

Veel plezier met coderen, en moge je OCR‑batches altijd foutloos zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}