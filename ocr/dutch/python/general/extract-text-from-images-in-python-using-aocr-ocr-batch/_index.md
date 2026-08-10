---
category: general
date: 2026-06-25
description: Tekst extraheren uit afbeeldingen met de Python aocr‑bibliotheek – leer
  batch‑OCR, stel de herkenningsmodus in op gedrukt, en voeg een AI‑postprocessor
  toe.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: nl
og_description: Haal tekst uit afbeeldingen met de Python aocr‑bibliotheek. Deze tutorial
  toont batch‑OCR, afdrukherkenningsmodus en een optionele AI‑nabewerking.
og_title: Tekst uit afbeeldingen halen in Python – Complete aocr batchgids
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Tekst extraheren uit afbeeldingen in Python met aocr OCR Batch
url: /nl/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit afbeeldingen in Python met aocr OCR Batch

Heb je ooit **tekst uit afbeeldingen moeten extraheren** en voelde je je overweldigd door tientallen kleine stappen? Je bent niet de enige. Of je nu gescande formulieren digitaliseert, gegevens van bonnetjes haalt, of een doorzoekbaar archief bouwt, betrouwbare OCR-resultaten op schaal kunnen aanvoelen als het beklimmen van een steile heuvel.

Het goede nieuws? Met de **aocr‑bibliotheek** kun je in slechts een handvol regels een volledige **Python OCR‑batch** opzetten. In deze gids lopen we stap voor stap door het maken van een OCR‑batch, het laden van elke ondersteunde afbeelding uit een map, het kiezen van de juiste **recognition mode printed**, en zelfs het toevoegen van een **AI‑postprocessor** voor die extra nauwkeurigheidsboost. Aan het einde heb je een kant‑klaar script dat tekst uit afbeeldingen haalt en aangeeft hoeveel er per bestand is vastgelegd.

## Wat je zult leren

- Hoe je het `aocr`‑pakket installeert en importeert.  
- Een `OcrBatch` opzetten om duizenden bestanden automatisch te verwerken.  
- De optimale herkenningsmodus kiezen voor gedrukte documenten.  
- (Optioneel) Een AI‑post‑processor koppelen om ruisvolle resultaten op te schonen.  
- Elk bestandspad weergeven naast de lengte van de geëxtraheerde tekst.  
- Tips voor het omgaan met randgevallen zoals niet‑ondersteunde formaten of lege pagina’s.

### Vereisten

- Python 3.8 of nieuwer geïnstalleerd op je machine.  
- Basiskennis van Python‑scripting (loops, imports, enz.).  
- Toegang tot een map met gescande afbeeldingen (PNG, JPG, TIFF, enz.).  

Als je dat hebt, duiken we erin — zonder externe services.

## Stap 1: Installeer de aocr‑bibliotheek

Allereerst. Het `aocr`‑pakket maakt geen deel uit van de standaardbibliotheek, dus moet je het van PyPI halen.

```bash
pip install aocr
```

> **Pro tip:** Gebruik een virtuele omgeving (`python -m venv .venv`) om afhankelijkheden geïsoleerd te houden.  

Zodra het geïnstalleerd is, kun je de kernklassen importeren.

```python
# core imports
import aocr
```

## Stap 2: Maak een OCR‑batch‑instantie

Een `OcrBatch` is de werkpaard die je map doorzoekt en elk afbeeldingsbestand bijhoudt. Beschouw het als een lopende band die afbeeldingen naar de OCR‑engine voert.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

Op dit moment is de batch leeg, maar we vullen hem in de volgende stap.

## Stap 3: Voeg alle ondersteunde afbeeldingen uit een map toe (recursief)

Je hebt waarschijnlijk een geneste mapstructuur — misschien één submap per klant of per maand. De `add_folder`‑methode doorloopt de boom voor je en haalt elke afbeelding op die hij kan lezen.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

Vervang `"YOUR_DIRECTORY/scanned_forms/"` door het echte pad op jouw systeem. Na deze aanroep bevat `ocr_batch.file_paths` een lijst met absolute bestandsnamen, en weet de batch precies hoeveel items hij zal verwerken.

## Stap 4: Kies de herkenningsmodus voor gedrukte tekst

De `aocr`‑engine ondersteunt verschillende modi (handgeschreven, gedrukt, gemengd). Omdat we werken met schone, gedrukte formulieren, stel je de modus overeenkomstig in. Deze kleine vlag kan de nauwkeurigheid dramatisch verbeteren omdat de engine de zware heuristieken voor cursieve scripts overslaat.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **Waarom het belangrijk is:** Gedrukte tekst heeft consistente basislijnen en tekenvormen, waardoor het OCR‑model strakkere teken‑woordenboeken kan toepassen. Als je de modus op “auto” laat staan, kun je extra ruis krijgen bij scans met lage resolutie.

## Stap 5: (Optioneel) Voeg een AI‑post‑processor toe

Als je scans lijden onder onscherpte, laag contrast of ongebruikelijke lettertypen, kan een AI‑post‑processor de ruwe OCR‑output opschonen voordat je deze doorgeeft aan downstream‑systemen. De `set_ai_postprocessor`‑methode verwacht een object dat een `process(text: str) -> str`‑interface implementeert.

Hieronder staat een minimaal voorbeeld met een fictieve `SimpleCleaner`‑klasse. In de praktijk kun je een HuggingFace‑transformer, een aangepast taalmodel, of zelfs een regelgebaseerde spell‑checker aansluiten.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

Als je deze stap overslaat, retourneert de batch simpelweg de ruwe OCR‑strings.

## Stap 6: Voer OCR uit op de volledige batch en verzamel resultaten

Nu begint het zware werk. De `run`‑methode loopt over elk bestand, voert de OCR‑engine uit, leidt de output via de optionele AI‑post‑processor, en retourneert een lijst met strings — één per afbeelding.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

Omdat de methode een gewone Python‑lijst teruggeeft, kun je hem behandelen als elke andere collectie — opslaan, naar een CSV schrijven, of invoeren in een database.

## Stap 7: Toon elk bestandspad met de lengte van de geëxtraheerde tekst

Een snelle sanity‑check is om af te drukken hoeveel tekens er uit elk bestand zijn gehaald. Als een pagina leeg is of de OCR faalt, zie je een lengte van `0`.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

Typische output ziet er als volgt uit:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

Het zien van een `0`‑vlag geeft meteen aan welke bestanden een tweede blik nodig hebben (misschien zijn ze corrupt of geen afbeelding).

## Veelvoorkomende randgevallen afhandelen

### 1. Niet‑ondersteunde bestandstypen

`aocr` slaat stilletjes bestanden over die hij niet kan decoderen. Als je vermoedt dat er PDFs of BMP’s tussen zitten, filter ze dan vooraf:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. Grote batches en geheugenverbruik

Het verwerken van duizenden scans met hoge resolutie kan het geheugen doen groeien. Beperk dit door in stukken te verwerken:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. Lege of laag‑contrast pagina’s

Als een pagina minder dan 10 tekens oplevert, wil je die misschien markeren voor handmatige controle:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## Volledig werkend voorbeeld

Alles bij elkaar, hier is een script dat je kunt kopiëren‑plakken en direct kunt uitvoeren. Sla het op als `batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**Verwachte output** (afgekapt voor beknoptheid):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

Voer het uit met:

```bash
python batch_ocr.py
```

Als alles correct is ingesteld, zie je een regel voor elke afbeelding, elk met het aantal tekens van de geëxtraheerde tekst.

## Veelgestelde vragen

**V: Werkt dit met PDFs?**  
A: Niet direct. `aocr` verwerkt alleen rasterafbeeldingen. Converteer PDFs eerst naar PNG/TIFF (bijv. met `pdf2image`).

**V: Kan ik de herkenningsmodus wijzigen naar handgeschreven?**  
A: Zeker — vervang `aocr.RecognitionMode.PRINTED` door `aocr.RecognitionMode.HANDWRITTEN`. Verwacht een tragere uitvoering maar betere resultaten bij cursieve notities.

**V: Wat als ik meertalige ondersteuning nodig heb?**  
A: De bibliotheek wordt geleverd met taalpakketten. Installeer de gewenste taalmodule (`pip install aocr-lang-fr` voor Frans, enz.) en stel `ocr_batch.language = "fr"` in vóór het uitvoeren.

## Volgende stappen en verwante onderwerpen

- **Parallel processing:** Wikkel de batch‑executie in een `concurrent.futures.ThreadPoolExecutor` om meerdere CPU‑kernen te benutten.  
- **Resultaten opslaan:** Schrijf `ocr_results` naar een CSV‑ of SQLite‑database voor downstream‑analyse.  
- **Integratie met cloud‑AI:** Vervang de `SimpleCleaner` door een transformer‑model van HuggingFace voor state‑of‑the‑art spelling‑correctie.  
- **Fine‑tuning aocr:** Als je een eigen lettertype‑set hebt, verken `aocr.Trainer` om de nauwkeurigheid in de gedrukte modus te verbeteren.

---

Dat is het — je hebt nu een solide basis


## Wat moet je hierna leren?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}