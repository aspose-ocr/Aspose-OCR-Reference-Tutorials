---
category: general
date: 2026-04-26
description: Hoe je documenten in batch OCR't en tekst uit scans haalt in Python.
  Leer stap‑voor‑stap batchverwerking met OcrEngine voor JSON‑output.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: nl
og_description: Hoe je batch‑OCR uitvoert op je gescande bestanden en tekst uit scans
  haalt in één script. Complete code, tips en afhandeling van randgevallen.
og_title: Hoe batch-OCR uit te voeren – Snelle Python-gids
tags:
- OCR
- Python
- Automation
title: Hoe batch-OCR – Tekst efficiënt uit scans extraheren
url: /nl/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe batch-OCR uit te voeren – Tekst uit scans efficiënt extraheren

Heb je je ooit afgevraagd **hoe je batch-OCR** kunt toepassen op een berg gescande PDF's zonder je verstand te verliezen? Je bent niet de enige—ontwikkelaars vragen voortdurend, *“Hoe kan ik tekst uit scans in één keer extraheren?”* Het goede nieuws is dat een paar regels Python die saaie klus kunnen omtoveren tot een soepel, geautomatiseerd pipeline. In deze tutorial lopen we stap voor stap door een complete, kant‑klaar oplossing die **tekst uit scans** extraheert, de resultaten opslaat als JSON, en je aan het einde een snelle sanity‑check geeft. Geen externe services, geen tovenarij—gewoon pure Python, de `OcrEngine`‑klasse, en een beetje map‑beheer.

## Wat je na afloop hebt

- Een volledig functioneel script dat **batch-OCR** uitvoert over elke map met afbeeldingen.
- Duidelijke uitleg over *waarom* elke regel bestaat, niet alleen *wat* hij doet.
- Tips voor het omgaan met lege mappen, niet‑afbeeldingsbestanden en grote batches.
- Een manier om te verifiëren dat de JSON‑output daadwerkelijk de geëxtraheerde tekst bevat.

### Vereisten (het absolute minimum)

| Vereiste | Waarom het belangrijk is |
|-------------|----------------|
| Python 3.8+ | Moderne syntaxis & type‑hints |
| `OcrEngine` library (or a compatible wrapper) | Kern‑OCR‑functionaliteit |
| A directory with scanned image files (PNG, JPG, TIFF) | Invoergegevens |
| Write permissions for the output folder | JSON‑resultaten opslaan |

Als je deze al hebt, geweldig—laten we erin duiken.

![how to batch OCR workflow](image-placeholder.png){alt="workflow voor batch OCR"}

## Stap 1 – Initialiseer de OCR‑engine (hoe batch-OCR)

Voordat we iets kunnen verwerken, hebben we een OCR‑engine‑instance nodig. Beschouw het als het “brein” dat elke afbeelding leest en tekst genereert. Het één keer initialiseren en hergebruiken gedurende de hele batch is het meest efficiënte patroon.

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **Waarom dezelfde instantie hergebruiken?**  
> Het creëren van een nieuwe engine voor elk bestand zou telkens zware modellen in het geheugen laden, waardoor de batch drastisch vertraagt. Eén instantie houdt het model in RAM en laat je duizenden afbeeldingen verwerken zonder merkbare vertraging.

## Stap 2 – Verwijs naar je scans‑map (tekst uit scans extraheren)

Je scans staan ergens op de schijf. Laten we het script vertellen waar ze te vinden zijn. Het gebruik van absolute paden voorkomt “bestand niet gevonden” verrassingen wanneer het script vanuit een andere werkmap wordt gestart.

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **Pro tip:**  
> Als je op Windows werkt, werken schuine strepen (`/`) prima met `os.path.abspath`, zodat je backslashes niet hoeft te escapen.

## Stap 3 – Kies waar de JSON‑resultaten naartoe moeten

Je wilt waarschijnlijk een nette map voor de OCR‑resultaten. Het scheiden van output en bron maakt het later gemakkelijk om op te ruimen of de JSON in een andere pipeline te voeren.

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **Waarom de map programmatisch aanmaken?**  
> Het garandeert dat het script niet crasht als de map ontbreekt, en `exist_ok=True` maakt de operatie idempotent—voer het script meerdere keren uit zonder fouten.

## Stap 4 – Voer het batch‑proces uit (hoe batch-OCR)

Nu het hart van de zaak: `ocr_engine` instrueren om door elk bestand in `input_dir` te lopen, OCR uit te voeren, en JSON weg te schrijven naar `output_dir`. De `format="json"`‑vlag vertelt de engine om het resultaat te serialiseren in een gestructureerde vorm die downstream‑tools waarderen.

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### Wat gebeurt er onder de motorkap?

1. **Bestandsdetectie** – De engine scant `input_folder` recursief en negeert verborgen bestanden.
2. **Bestandsvalidatie** – Alleen ondersteunde afbeeldingsextensies (`.png`, `.jpg`, `.tif`, etc.) worden aan het OCR‑model gevoed.
3. **OCR‑uitvoering** – Elke afbeelding wordt naar de OCR‑engine gestuurd; tekst, vertrouwensscores en lay-outgegevens worden vastgelegd.
4. **JSON‑serialisatie** – Het resultaat wordt weggeschreven naar een bestand met dezelfde basisnaam maar een `.json`‑extensie in `output_folder`.

> **Afhandeling van randgevallen:**  
> - **Lege map:** De engine logt “No files found” en keert netjes terug.  
> - **Beschadigde afbeelding:** Hij slaat het bestand over, registreert een foutmelding in een `batch_errors.log`, en gaat door.  
> - **Grote batch (10k+ bestanden):** Het geheugenverbruik blijft laag omdat elke afbeelding onafhankelijk wordt verwerkt.

## Stap 5 – Bevestig dat de conversie voltooid is

Een eenvoudige `print`‑statement geeft directe feedback in de console. Voor productiepipelines kun je dit vervangen door een logging‑call of een e‑mailnotificatie.

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

Wanneer je die regel ziet, kun je veilig de `json_output`‑map inspecteren. Elk JSON‑bestand zal er ongeveer zo uitzien:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

Je kunt deze JSON‑bestanden nu invoeren in een database, een zoekindex, of een andere downstream‑analytics‑tool.

## Veelgestelde vragen (en snelle antwoorden)

**Q: Wat als ik PDF's moet verwerken in plaats van afbeeldingen?**  
A: Converteer elke PDF‑pagina eerst naar een afbeelding (bijv. met `pdf2image`) en plaats de resulterende PNG/JPG‑bestanden in `input_dir`. De batch‑OCR‑logica blijft ongewijzigd.

**Q: Kan ik het uitvoerformaat wijzigen naar platte tekst?**  
A: Zeker. Vervang `format="json"` door `format="txt"` en de engine schrijft een `.txt`‑bestand dat alleen de geëxtraheerde tekst bevat.

**Q: Mijn scans staan in meerdere sub‑mappen—zal het script recursief zoeken?**  
A: Ja. `batch_process` doorloopt standaard de mapboom. Als je een platte output wilt, stel `flatten=True` in (indien de bibliotheek dit ondersteunt) of verwerk de JSON‑bestandsnamen achteraf.

**Q: Hoe ga ik om met niet‑Latijnse scripts?**  
A: Initialise `OcrEngine` met een taalparameter, bijv. `OcrEngine(lang="spa+eng")`. De batch‑lus zelf vereist geen aanpassingen.

## Pro‑tips & veelvoorkomende valkuilen

- **Batch‑grootte is belangrijk:** Als je CPU‑pieken ziet, beperk het proces met een eenvoudige `time.sleep(0.1)` tussen bestanden.
- **Logging:** Vervang de `print`‑call door Python’s `logging`‑module om tijdstempels en foutniveaus vast te leggen.
- **Bestandsnaam‑conflicten:** Als twee scans dezelfde basisnaam hebben maar in verschillende sub‑mappen staan, zullen de JSON‑bestanden elkaar overschrijven. Voeg een hash van het relatieve pad toe aan de uitvoernaam om dit te voorkomen.
- **Geheugenlekken:** Sommige OCR‑back‑ends houden native resources vast. Roep `ocr_engine.close()` aan het einde van je script aan als de bibliotheek een opruimmethode biedt.

## Volledig script – Klaar om te kopiëren & plakken

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**Verwachte console‑output**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

Je kunt de JSON verifiëren door een willekeurig bestand in `json_output` te openen met een teksteditor of door het in Python te laden:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

Je zou de ruwe OCR‑geëxtraheerde tekst in de console moeten zien verschijnen.

## Afronding

We hebben zojuist **hoe je batch-OCR** kunt toepassen op een volledige map met gescande afbeeldingen en **tekst uit scans** kunt extraheren naar schone, machine‑leesbare JSON‑bestanden. De aanpak is opzettelijk simpel: initialiseert de engine één keer, wijs een map aan, en laat de bibliotheek het zware werk doen. Vanaf hier kun je:

- Plug the JSON

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}