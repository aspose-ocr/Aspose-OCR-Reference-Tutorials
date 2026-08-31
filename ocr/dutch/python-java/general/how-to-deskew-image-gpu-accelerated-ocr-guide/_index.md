---
category: general
date: 2026-01-02
description: Leer hoe je een afbeelding kunt rechtzetten en het contrast van de afbeelding
  kunt verhogen om snel platte tekst te krijgen. Inclusief stapsgewijze Python‑code
  en tips voor het extraheren van tekst.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: nl
og_description: Hoe een afbeelding te deskewen en het contrast te verhogen om platte
  tekst te krijgen. Volledig Python‑voorbeeld met tabelextractie en GPU‑versnelling.
og_title: Hoe een afbeelding rechtzetten – Complete GPU OCR-tutorial
tags:
- OCR
- Python
- Image Processing
title: Hoe een afbeelding rechtzetten – GPU-versnelde OCR-gids
url: /nl/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een afbeelding rechtzetten – GPU‑versnelde OCR‑gids

Heb je je ooit afgevraagd **hoe je een afbeelding rechtzet** wanneer je bonnetjes onder een gekke hoek binnenkomen? Je bent niet de enige; een scheve foto kan een perfect leesbaar bonnetje veranderen in een warboel. Het goede nieuws is dat je met een paar regels Python automatisch kunt rechtzetten, het contrast kunt verhogen en schone platte tekst kunt extraheren—geen handmatige Photoshop nodig.  

In deze tutorial lopen we een compleet, uitvoerbaar voorbeeld door dat niet alleen **hoe je een afbeelding rechtzet** laat zien, maar ook **hoe je het contrast verhoogt**, hoe je **platte tekst krijgt**, en zelfs **hoe je tekst uit tabellen haalt** die de OCR‑engine ontdekt. Aan het einde heb je een zelfstandige script die je in elk project kunt gebruiken.

## Wat je nodig hebt

- Python 3.9+ geïnstalleerd (de code gebruikt type‑hints, dus een recente interpreter helpt)
- De `ocr`‑bibliotheek die `OcrEngine`, `EngineMode`, `ImageProcessingOptions` en `OcrResult` levert (installeren via `pip install ocr‑sdk` – vervang door de daadwerkelijke pakketnaam die je gebruikt)
- Een GPU met compatibele drivers als je de snelheidsboost wilt (optioneel maar aanbevolen)
- Een afbeeldingsbestand dat licht gedraaid of laag‑contrast is, bv. `receipt_skewed.jpg`

> **Pro tip:** Als je geen GPU hebt, wijzig dan `EngineMode.GPU` naar `EngineMode.CPU` en het script werkt nog steeds—alleen iets trager.

## Stapsgewijze implementatie

Hieronder splitsen we de oplossing op in logische blokken. Elk blok heeft een beschrijvende **H2** die ofwel het primaire zoekwoord *hoe je een afbeelding rechtzet* bevat of een van de secundaire zoekwoorden. De code is compleet, voorzien van commentaar, en klaar om te draaien.

### Hoe een afbeelding rechtzetten met GPU‑versnelde OCR

Het eerste wat we doen is de OCR‑engine laten draaien op de GPU en de auto‑rechtzet‑functie inschakelen. Auto‑rechtzetten analyseert de geometrie van de afbeelding en draait deze terug naar de rechte stand.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **Waarom dit belangrijk is:** GPU‑versnelling kan de verwerkingstijd verkorten van seconden naar milliseconden, wat cruciaal is wanneer je tientallen bonnetjes per minuut verwerkt.

### Contrast van de afbeelding verhogen voor betere herkenning

Een laag‑contrast bonnetje is een nachtmerrie voor elk OCR‑systeem. Door het contrast te verhogen geven we de engine duidelijkere randen om mee te werken.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **Hoe je contrast verhoogt:** De `set_contrast_boost`‑methode accepteert een percentage; 30 % is een veilig standaardwaarde die voor de meeste gescande bonnetjes werkt. Als je afbeeldingen extreem donker zijn, verhoog dit dan naar 50 % of experimenteer.

### Platte tekst krijgen van de verwerkte afbeelding

Nu de afbeelding recht en helder is, voeren we deze in de engine en vragen we om het platte‑tekstresultaat.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**Verwachte output** (verkort voor de leesbaarheid):

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **Hoe je platte tekst krijgt:** De `get_text()`‑methode verwijdert alle lay‑outinformatie en retourneert een schone string, die je vervolgens kunt opslaan in een database, naar een API kunt sturen, of kunt gebruiken in downstream‑analytics.

### Hoe tekst uit gedetecteerde tabellen extraheren

Bonnetjes bevatten vaak tabelgegevens (artikelen, aantallen, prijzen). De OCR‑SDK kan tabellen detecteren en je laten itereren over rijen en cellen.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**Voorbeeld van tabeloutput**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **Waarom tabellen extraheren:** Gestructureerde data maakt het triviaal om totalen te berekenen, rapporten te genereren, of te voeden aan boekhoudsoftware.

### Volledig werkend script

Alles samengevoegd, hier is het script dat je kunt kopiëren‑plakken in `deskew_and_ocr.py`:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

Voer het uit met:

```bash
python deskew_and_ocr.py
```

Je zou de opgeschoonde tekst en eventuele gedetecteerde tabellen in de console moeten zien.

## Veelvoorkomende randgevallen & hoe ze op te lossen

| Situatie | Wat te doen |
|-----------|------------|
| **Afbeelding staat ondersteboven** | Verhoog de `set_auto_deskew(True)`‑confidence door ook `set_rotation_correction(True)` aan te roepen als de SDK dit biedt. |
| **Contrastverhoging maakt de afbeelding te helder** | Verlaag het percentage dat aan `set_contrast_boost` wordt doorgegeven (bijv. 15 %). |
| **GPU niet beschikbaar** | Schakel `EngineMode.GPU` over naar `EngineMode.CPU`; de rest van de pijplijn blijft ongewijzigd. |
| **Tabellen worden gemist** | Probeer een hogere resolutie scan of schakel `set_table_detection(True)` in als de bibliotheek dit ondersteunt. |

## Volgende stappen: Van platte tekst naar gestructureerde data

Nu je weet **hoe je een afbeelding rechtzet**, **hoe je contrast verhoogt**, en **hoe je platte tekst krijgt**, wil je misschien:

- De platte tekst parsen met reguliere expressies om sleutel‑waardeparen te extraheren (bijv. `total`, `date`).
- De resultaten opslaan in een SQLite‑ of PostgreSQL‑database voor latere rapportage.
- Het script koppelen aan een serverless‑functie (AWS Lambda, Azure Functions) om uploads automatisch te verwerken.

Al deze uitbreidingen bouwen voort op dezelfde basis die we hier hebben behandeld.

## Conclusie

We hebben stap voor stap **hoe je een afbeelding rechtzet** met een GPU‑versnelde OCR‑engine doorgenomen, **hoe je contrast verhoogt** voor scherpere herkenning, je precies laten zien **hoe je platte tekst krijgt**, en zelfs behandeld **hoe je tekst uit tabellen extraheren**. Het complete, uitvoerbare script verbindt alles, zodat je het in elk Python‑project kunt drop‑en en meteen schone data uit scheve, laag‑contrast foto’s kunt halen.

Probeer het met een paar eigen bonnetjes, pas het contrastniveau aan, en laat de OCR het zware werk doen. Als je tegen eigenaardigheden aanloopt, kijk dan nog eens naar de tabel met randgevallen—de meeste problemen zijn slechts een kleine aanpassing verwijderd.

Happy coding, en moge je afbeeldingen altijd recht en helder zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}