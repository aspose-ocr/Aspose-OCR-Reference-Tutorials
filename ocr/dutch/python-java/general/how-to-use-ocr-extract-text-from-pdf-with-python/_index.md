---
category: general
date: 2026-04-26
description: hoe OCR te gebruiken op gescande PDF's, tekst uit PDF te extraheren,
  OCR op PDF uit te voeren en gescande PDF om te zetten naar doorzoekbare bestanden
  in een paar stappen.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: nl
og_description: 'hoe OCR te gebruiken in Python: leer hoe je tekst uit PDF kunt extraheren,
  OCR op PDF kunt uitvoeren en gescande PDF''s kunt omzetten in doorzoekbare documenten.'
og_title: hoe OCR te gebruiken – Snelle gids om tekst uit PDF te extraheren
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Hoe OCR te gebruiken – Tekst extraheren uit PDF met Python
url: /nl/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hoe OCR te gebruiken – Tekst extraheren uit PDF met Python

Heb je je ooit afgevraagd **hoe je OCR kunt gebruiken** om tekst uit een gescand contract, bon of e‑book te halen? Je bent niet de enige. In veel real‑world projecten is de PDF die je ontvangt slechts een afbeelding, en zonder OCR kun je de inhoud niet doorzoeken, indexeren of analyseren.  

In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat laat zien **hoe je OCR kunt gebruiken**, hoe je **tekst uit PDF kunt extraheren**, en waarom je mogelijk **gescande PDF**‑bestanden wilt **converteren naar doorzoekbare** documenten. We behandelen ook de subtiele kunst van **PDF laden als afbeelding** zodat de OCR‑engine elke pagina duidelijk kan zien.

> **Snelle preview:** Aan het einde heb je een script dat een meer‑pagina PDF laadt, OCR op elke pagina uitvoert, en de herkende tekst afdrukt – zonder externe services.

## Wat je nodig hebt

- Python 3.9+ (elke recente versie werkt)
- `aocr`‑pakket (of een compatibele OCR‑bibliotheek die `OcrEngine` en `Image.load` biedt)
- Een gescande PDF‑bestand dat je wilt verwerken (bijv. `contract.pdf`)
- Een bescheiden hoeveelheid RAM (≈ 200 MB per 100‑pagina PDF is meestal voldoende)

Als je de OCR‑bibliotheek nog niet hebt geïnstalleerd, voer dan uit:

```bash
pip install aocr
```

> **Pro tip:** Gebruik een virtuele omgeving om je afhankelijkheden netjes te houden.

## Stap 1: PDF laden als afbeelding – Het eerste puzzelstuk

Voordat OCR kan plaatsvinden, moet de PDF worden weergegeven als een afbeelding. Hier komt het secundaire trefwoord **pdf laden als afbeelding** van pas.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Waarom dit belangrijk is:* `aocr.Image.load` rastert intern elke PDF‑pagina naar een bitmap die de OCR‑engine kan begrijpen. Als je deze stap overslaat en de ruwe PDF invoert, zal de engine een fout geven omdat hij pixeldata verwacht, geen vectordata.

> **Opmerking:** Het pad kan absoluut of relatief zijn. Zorg ervoor dat het bestand leesbaar is; anders krijg je een `FileNotFoundError`.

## Stap 2: OCR uitvoeren op PDF – Pixels omzetten in tekens

Nu de PDF als afbeelding bestaat, kunnen we eindelijk **OCR uitvoeren op PDF**. Het volgende fragment verwerkt elke pagina in één keer:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*Wat gebeurt er onder de motorkap?* `process_all_pages` doorloopt de gerasterde pagina's, past het OCR‑model toe, en retourneert een lijst met resultaatobjecten — één per pagina. Elk resultaat bevat de herkende tekst, vertrouwensscores en begrenzingskaders (als je die later nodig hebt).

## Stap 3: Tekst extraheren uit PDF – De strings eruit halen

Met OCR‑resultaten in de hand wordt het extraheren van platte tekst triviaal. We itereren over de pagina's en printen de output, waarmee we het secundaire trefwoord **tekst extraheren uit pdf** demonstreren.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Verwachte output** (ingekort voor beknoptheid):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

Als je de tekst in één enkele string nodig hebt, concateneer je eenvoudigweg:

```python
full_text = "\n".join(r.text for r in page_results)
```

Nu heb je met succes **tekst uit PDF geëxtraheerd** met OCR.

## Stap 4: Gescande PDF converteren – Maak hem doorzoekbaar

Veel downstream‑tools (zoals Elasticsearch of SharePoint) verwachten een doorzoekbare PDF in plaats van een platte‑tekst dump. Je kunt de OCR‑output terug in de originele PDF embedden, waardoor je effectief **gescande PDF** **converteert naar een doorzoekbare** versie.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*Waarom de moeite waard?* Een doorzoekbare PDF behoudt de originele lay-out en afbeeldingen, terwijl tekstselectie en indexering mogelijk zijn – een win‑win voor zowel mensen als machines.

## Veelvoorkomende valkuilen & randgevallen

### Multi‑page PDF's groter dan het geheugen

Als je PDF honderden pagina's heeft, kan het in één keer laden het RAM uitputten. De `aocr`‑bibliotheek ondersteunt lazy loading:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

Verwerk vervolgens pagina's één voor één:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### Scans van lage kwaliteit

De OCR‑nauwkeurigheid daalt drastisch bij wazige of laag‑contrast scans. Overweeg voorafverwerking voordat je de afbeelding aan de engine geeft:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### Taalondersteuning

Standaard gaat de engine uit van Engels. Om **OCR uitvoeren op PDF** in een andere taal, stel je de taalcode in:

```python
ocr_engine.language = "spa"  # Spanish
```

Zorg ervoor dat het bijbehorende taalmodel geïnstalleerd is.

## Volledig werkend voorbeeld

Alles samenvoegend, hier is een zelfstandige script die je in een bestand genaamd `ocr_pdf.py` kunt plaatsen en direct kunt uitvoeren:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

Voer het als volgt uit:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

Je ziet de tekst in de console afgedrukt, en als je `-o` hebt opgegeven, verschijnt er een doorzoekbare PDF naast het originele bestand.

## Pro‑tips & best practices

- **Batchverwerking:** Bij het verwerken van tientallen PDF's, wikkel je de bovenstaande logica in een lus en log je het succes/failure van elk bestand.
- **Vertrouwensfiltering:** Elk `page_result` bevat een vertrouwensmetriek. Verwijder of markeer pagina's met lage vertrouwensscore voor handmatige controle.
- **Parallelisme:** Als je CPU meerdere cores heeft, overweeg dan `concurrent.futures` te gebruiken om pagina's parallel te verwerken — let wel op het geheugenverbruik.
- **Versie-lock:** De `aocr` API kan evolueren. Pin de versie in `requirements.txt` (bijv. `aocr==2.3.1`) om brekende wijzigingen te voorkomen.

## Conclusie

We hebben doorlopen **hoe je OCR kunt gebruiken** om **tekst uit PDF te extraheren**, **OCR uitvoeren op PDF**, **PDF te laden als afbeelding**, en zelfs **gescande PDF** te **converteren naar een doorzoekbaar** formaat. De code is compleet, de uitleg behandelt zowel het *wat* als het *waarom*, en je hebt nu een herbruikbaar patroon voor elk project dat met op afbeeldingen gebaseerde PDF's werkt.

Wat is het volgende? Probeer de geëxtraheerde tekst in een natural‑language pipeline te voeren, indexeer de doorzoekbare PDF's met Elasticsearch, of experimenteer met verschillende OCR‑back‑ends zoals Tesseract of Azure Computer Vision. De mogelijkheden zijn eindeloos, en de tools liggen binnen handbereik.

Veel plezier met coderen, en moge je PDF's altijd doorzoekbaar zijn! 

![voorbeeld van hoe OCR te gebruiken](/images/ocr_workflow.png "hoe OCR te gebruiken")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}