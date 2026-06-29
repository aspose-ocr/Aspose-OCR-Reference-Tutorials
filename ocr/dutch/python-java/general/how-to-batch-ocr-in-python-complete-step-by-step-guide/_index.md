---
category: general
date: 2026-06-28
description: Hoe batch‑OCR uit te voeren met Python. Leer meerdere afbeeldingen OCR’en,
  tekst uit PNG’s extraheren en een afbeelding naar tekst converteren met een volledige
  Python OCR‑tutorial.
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: nl
og_description: Hoe batch‑OCR in Python wordt uitgelegd in de eerste zin. Volg deze
  Python OCR‑tutorial om efficiënt tekst uit PNG‑bestanden te extraheren.
og_title: Hoe batch-OCR in Python uit te voeren – Volledige programmeergids
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Hoe batch‑OCR in Python uit te voeren – Complete stap‑voor‑stap gids
url: /nl/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe batch‑OCR uit te voeren in Python – Complete stapsgewijze gids

Heb je je ooit afgevraagd **hoe je batch‑OCR** kunt uitvoeren op een stapel gescande pagina's zonder een lus te schrijven die je UI blokkeert? Je bent niet de enige. Het verwerken van tientallen PNG‑bestanden één voor één kan aanvoelen als het kijken naar droog verf, vooral wanneer elke afbeelding een seconde of twee nodig heeft om te decoderen.  

In deze tutorial laten we je een schone, niet‑blokkerende manier zien om **meerdere afbeeldingen te OCR‑en** tegelijk, **tekst uit PNG**‑bestanden te halen, en **afbeelding naar tekst te converteren** met een moderne Python OCR‑engine. Aan het einde heb je een kant‑klaar script dat je in elk project kunt plaatsen – perfect voor een snelle *python ocr tutorial* of een productie‑klare batch‑taak.

## Wat je gaat bouwen

- Initialiseer een OCR‑engine en stel de taal in op Latin (of elke andere taal die je nodig hebt).  
- Geef een lijst met afbeeldingspaden (PNG in ons voorbeeld) aan de engine.  
- Start een batch‑operatie die een Future‑achtig object retourneert.  
- Haal alle resultaten gelijktijdig op met een thread‑pool, zodat je hoofdthread vrij blijft.  
- Print de herkende tekst voor elke pagina, netjes gescheiden.

Geen verborgen magie, alleen plain Python en een externe OCR‑bibliotheek (we gebruiken het fictieve `pyocr`‑pakket voor illustratie).  

**Voorvereisten**  
- Python 3.8+ geïnstalleerd.  
- Basiskennis van Python‑functies en `concurrent.futures`.  
- Toegang tot een OCR‑bibliotheek die een `OcrEngine`‑klasse exposeert (bijv. `pip install pyocr`).  

Als je een van deze mist, pak ze dan nu – het is makkelijker dan je denkt.

---

## Hoe batch‑OCR in Python – Kernconcepten

Voordat we in de code duiken, laten we de “waarom” achter elke stap beantwoorden.

1. **Waarom de taal instellen?**  
   De OCR‑nauwkeurigheid stijgt enorm wanneer de engine weet welke tekens verwacht worden. Latin werkt voor Engels, Frans, Spaans, enz. Schakel over naar `Language.Japanese` of `Language.Arabic` indien nodig.

2. **Waarom een batch‑operatie gebruiken?**  
   Een batch‑aanroep laat de engine intern werk plannen, vaak gebruikmakend van native threads of GPU‑versnelling. Het retourneert een handle die je later kunt opvragen, waardoor je niet blokkeert terwijl elke afbeelding wordt verwerkt.

3. **Waarom een ThreadPoolExecutor?**  
   Het Future‑object dat we terugkrijgen is *lazy* – het begint pas resultaten op te halen wanneer we erom vragen. Door een thread‑pool aan `getAll` te geven, laten we Python de tekst van elke pagina parallel ophalen, waardoor de totale runtijd drastisch wordt verkort.

4. **Waarom de resultaten enumereren?**  
   De volgorde van resultaten komt overeen met de volgorde van de invoerpaden, zodat we elk paginanummer veilig kunnen labelen.

Het begrijpen van deze “waarom”‑punten helpt je het patroon aan te passen aan andere bibliotheken of grotere datasets.

## Stap 1: Installeer en importeer vereiste pakketten

Zorg er eerst voor dat de OCR‑bibliotheek geïnstalleerd is. Het voorbeeld gebruikt een generiek `pyocr`‑pakket; vervang het door de bibliotheek die je verkiest (bijv. `pytesseract`, `easyocr`).

```bash
pip install pyocr
```

Importeer nu alles wat we nodig hebben.

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

**Pro tip:** Het gebruik van `Path` uit `pathlib` maakt je script OS‑agnostisch en makkelijker leesbaar.

## Stap 2: Maak de OCR‑engine en stel de taal in

Het maken van de engine is eenvoudig. We zetten deze voor deze demo op Latin.

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

De `setLanguage`‑aanroep is optioneel voor sommige engines, maar het is een goede gewoonte. Het vertelt het OCR‑model zich te richten op de tekenset die je nodig hebt, wat zowel snelheid als nauwkeurigheid verbetert.

## Stap 3: Lijst de afbeeldingsbestanden om te verwerken (tekst uit PNG halen)

Verzamel alle PNG‑bestanden die je wilt converteren. Het gebruik van `Path.glob` betekent dat je een hele map kunt toevoegen zonder het script te bewerken.

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

**Waarom dit belangrijk is:** Door de lijst te sorteren garanderen we een deterministische volgorde, waardoor later elk resultaat overeenkomt met het juiste paginanummer.

## Stap 4: Start een batch‑OCR‑operatie (afbeelding naar tekst converteren)

Nu geven we de lijst aan de engine. De methode retourneert een Future‑achtig container die we later zullen opvragen.

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

Onder de motorkap kan de engine eigen worker‑threads of zelfs een GPU‑pipeline opstarten. Het enige waar we om geven is dat we een handle (`batch_future`) hebben die weet hoe de individuele resultaten op te halen.

## Stap 5: Haal alle resultaten gelijktijdig op (OCR meerdere afbeeldingen)

Hier is waar we het werk echt *batchen*. Door een `ThreadPoolExecutor` aan `getAll` te geven, wordt de tekst van elke pagina in zijn eigen thread opgehaald.

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

Je kunt `max_workers` afstemmen op basis van je CPU‑kernen of de aanbevelingen van de OCR‑bibliotheek. Meer workers ≠ altijd sneller – houd je CPU‑gebruik in de gaten.

## Stap 6: Output de herkende tekst (Python OCR tutorial finale)

Print tenslotte de tekst van elke pagina. Het `Result`‑object biedt `getText()` – pas aan als je bibliotheek een andere methodenaam gebruikt.

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**Verwachte output (voorbeeld)**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

Als een afbeelding faalt, voegen de meeste engines een lege string in of gooien een uitzondering – je kunt de lus in een `try/except`‑blok plaatsen om randgevallen netjes af te handelen.

## Volledig script – klaar om uit te voeren

Hieronder staat het volledige, zelfstandige script. Kopieer‑en plak het in een bestand genaamd `batch_ocr.py`, pas `YOUR_DIRECTORY` aan, en voer `python batch_ocr.py` uit.

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

Sla op, voer uit, en zie de console vullen met de geëxtraheerde tekst. Simpel, snel, en volledig asynchroon.

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **Geen output** – lege strings | De OCR‑engine kon geen tekst vinden (afbeelding te ruisachtig) | Pre‑process afbeeldingen: binariseren, rechtzetten, of DPI verhogen |
| **`FileNotFoundError`** | Verkeerd mappad of ontbrekende PNG‑bestanden | Controleer `YOUR_DIRECTORY` en zorg dat bestanden eindigen op `.png` |
| **Hoge CPU‑belasting** | `max_workers` te hoog ingesteld voor je machine | Verlaag `max_workers` of schakel GPU‑versnelling in indien ondersteund |
| **Unicode-rammel** | Engine standaard op een andere taal ingesteld | Roep `engine.setLanguage(Language.Latin)` (of passend) aan vóór batch‑OCR |

Deze vroeg aanpakken bespaart je uren debugging.

## De tutorial uitbreiden – volgende stappen

- **OCR meerdere afbeeldingen** in andere formaten (JPEG, TIFF) – wijzig gewoon het glob‑patroon.  
- **Tekst uit PNG halen** en deze invoeren in een zoekindex (bijv. Elasticsearch).  
- **Afbeelding naar tekst converteren** voor PDF‑generatie met `reportlab` of `PyPDF2`.  
- **Paralleliseer over machines** met `multiprocessing` of een taak‑queue zoals Celery voor enorme datasets.  

Elk van deze onderwerpen bouwt natuurlijk voort op de **python ocr tutorial** die je zojuist hebt voltooid.

## Conclusie

We hebben stap voor stap **hoe je batch‑OCR** uitvoert op een verzameling PNG‑bestanden, de kracht van een batch‑georiënteerde API gedemonstreerd, en laten zien hoe je **tekst uit PNG** haalt met een thread‑pooled aanpak. Het volledige script hierboven is productie‑klaar, en je hebt nu een solide basis voor elk OCR‑intensief Python‑project.

Probeer het uit, pas de taalinstellingen aan, en vervang `pyocr` eventueel door `pytesseract` – het patroon blijft hetzelfde. Heb je vragen of wil je een cool use‑case delen? Laat een reactie achter, en laten we het gesprek voortzetten.

*Veel plezier met coderen!*

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Tekst uit afbeelding halen met Aspose OCR – Stapsgewijze gids](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Tekst uit afbeeldingen halen met OCR‑operatie op mappen](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Hoe batch‑OCR afbeeldingen met lijst in Aspose.OCR voor .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}