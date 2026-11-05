---
category: general
date: 2026-06-19
description: Hoe PDF te extraheren met OCR in Python – stapsgewijze tutorial over
  het extraheren van tekst uit PDF, het herkennen van tekst uit afbeelding en een
  OCR‑Python‑voorbeeld.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: nl
og_description: Hoe PDF te extraheren met OCR in Python. Leer tekst uit PDF te extraheren,
  tekst uit afbeelding te herkennen en bekijk een volledig OCR‑Python‑voorbeeld.
og_title: Hoe PDF-tekst te extraheren met OCR in Python – Volledige tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Hoe PDF-tekst te extraheren met OCR in Python – Complete gids
url: /nl/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe PDF-tekst te extraheren met OCR in Python – Complete gids

Heb je je ooit afgevraagd **hoe je PDF**-inhoud kunt extraheren wanneer het bestand alleen een gescande afbeelding is? Je bent niet de enige. In veel real‑world projecten—denk aan contracten, facturen of historische archieven—heeft de PDF die je ontvangt geen selecteerbare tekst. Het goede nieuws? Een paar regels Python kunnen die alleen‑afbeeldingspagina's omzetten in doorzoekbare, bewerkbare tekst.

In deze tutorial lopen we een praktisch **OCR Python voorbeeld** door dat een PDF leest, de eerste pagina rendert als een afbeelding, en vervolgens **tekst uit PDF** extraheert met een OCR‑engine. Aan het einde weet je precies hoe je **PDF met OCR kunt lezen**, waarom elke stap belangrijk is, en hoe je de code kunt aanpassen voor documenten met meerdere pagina's of verschillende talen.

## Wat je zult leren

- Installeer en configureer een betrouwbare OCR‑bibliotheek voor Python.  
- Converteer PDF‑pagina's naar afbeeldingen die geschikt zijn voor OCR.  
- **Herken tekst uit afbeelding** en haal schone Unicode‑strings op.  
- Veelvoorkomende valkuilen (low‑resolution PDF's, gedraaide pagina's) en hoe je ze kunt vermijden.  
- Breid het script uit om meerdere pagina's of batchverwerking te verwerken.

**Prerequisites**: Python 3.8+, pip, en een basisbegrip van virtuele omgevingen. Geen eerdere OCR‑ervaring vereist—volg gewoon mee.

---

## ## Hoe PDF-tekst te extraheren met OCR in Python

Deze H2‑kop bevat ons primaire zoekwoord precies waar zoekmachines het graag zien. Laten we meteen in de code duiken.

### Stap 1 – Installeer de vereiste pakketten

Eerst hebben we een OCR‑engine nodig. Het voorbeeld hieronder gebruikt het populaire **ocr**‑pakket (een dunne wrapper rond Tesseract). Als je een andere backend verkiest, blijven de concepten hetzelfde.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Pro tip:** Op Linux heb je ook de Tesseract‑binary nodig: `sudo apt-get install tesseract-ocr`. macOS‑gebruikers kunnen het via Homebrew halen: `brew install tesseract`.

### Stap 2 – Initialiseert de OCR‑engine en stel de taal in

Nu starten we de engine en vertellen we hem om naar Engelse tekens te zoeken. Je kunt `ocr.Language.English` vervangen door elke ondersteunde taalcodes.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Waarom dit belangrijk is:** Het specificeren van de taal verbetert de nauwkeurigheid drastisch omdat de engine taal‑specifieke woordenboeken en tekensmodellen kan toepassen.

### Stap 3 – Laad een PDF‑pagina als afbeelding

OCR werkt op rasterafbeeldingen, niet op PDF‑objecten. De `ocr.Image.from_pdf`‑helper rendert de gekozen pagina naar een bitmap. Pas `page_number` aan voor andere pagina's (0‑gebaseerde indexering).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Edge case:** Als de PDF vector‑graphics bevat in plaats van gescande afbeeldingen, kun je een scherpe rendering krijgen. Voor low‑resolution scans, overweeg de DPI te verhogen: `ocr.Image.from_pdf(..., dpi=300)`.

### Stap 4 – Herken tekst uit de gerenderde afbeelding

Hier is het hart van het **ocr python voorbeeld**. De engine verwerkt de bitmap en retourneert een object dat de geëxtraheerde string bevat.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

Het attribuut `ocr_result.text` bevat de platte‑tekst output, waarbij waar mogelijk regeleinden behouden blijven.

### Stap 5 – Print of sla de geëxtraheerde tekst op

Tot slot geven we het resultaat weer. In een echte applicatie zou je waarschijnlijk naar een bestand of een database schrijven.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

Het uitvoeren van het script zou iets moeten weergeven als:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

Dat is een volledige **extract text from pdf** workflow met OCR.

---

## ## Herken tekst uit afbeelding – Nauwkeurigheid aanpassen

Als je alleen geïnteresseerd bent in **recognize text from image** (bijvoorbeeld een JPEG van een bon), kun je de PDF‑conversiestap overslaan:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Tips voor betere resultaten:**

- **Pre‑process** de afbeelding: converteer naar grijswaarden, pas drempeling toe, of deskew. Pillow maakt dit eenvoudig.
- **Increase DPI** tijdens PDF‑rendering: hogere resolutie geeft de OCR‑engine meer detail.
- **Enable OCR engine’s config** voor paginasegmentatie (`ocr_engine.config = "--psm 6"` voor uniforme blokken).

## ## PDF met OCR lezen – Meerdere pagina's verwerken

De meeste contracten beslaan meerdere pagina's. Over elke pagina itereren is eenvoudig:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

Deze functie **reads PDF with OCR**, voegt de output samen en voegt een duidelijke paginabreak‑markering toe. Je kunt vervolgens `full_text` in een zoekindex voeren of opslaan als een `.txt`‑bestand.

## ## Veelvoorkomende valkuilen en hoe ze op te lossen

| Symptoom | Waarschijnlijke oorzaak | Oplossing |
|----------|--------------------------|-----------|
| Vervormde tekens, veel `?` | Verkeerde taal of ontbrekende taal‑databestanden | Installeer het juiste Tesseract‑taalpakket (`tesseract-ocr-<lang>`) en stel `ocr_engine.language` in. |
| Ontbrekende regels of afgekorte woorden | Lage DPI (onder 150) | Render de PDF op 300 DPI of hoger (`dpi=300`). |
| Tekst is gedraaid of ondersteboven | Gescante pagina niet rechtop | Gebruik `ocr.Image.deskew(page_image)` vóór herkenning. |
| Trage verwerking bij grote PDF's | Pagina's sequentieel verwerken op één thread | Paralleliseer met `concurrent.futures.ThreadPoolExecutor`. |

## ## Het OCR Python voorbeeld uitbreiden

- **Export to PDF/A**: Na extractie kun je de tekst terug inbedden in een doorzoekbare PDF met `reportlab` of `pypdf2`.
- **Language detection**: Gebruik `langdetect` op de OCR‑output om `ocr_engine.language` dynamisch te wisselen.
- **Batch processing**: Loop door een map met `os.listdir` en pas `extract_all_pages` toe op elk bestand.

## ## Verwachte output en verificatie

Wanneer je het script uitvoert op een duidelijke, Engelstalige scan, zou je een schoon tekstblok met juiste interpunctie moeten zien. Verifieer door:

1. Een paar regels vergelijken met de originele gescande afbeelding.  
2. Een eenvoudige woordtelling uitvoeren (`len(ocr_result.text.split())`) om te zorgen dat de output niet leeg is.  
3. Optioneel de resultaten doorvoeren naar een spell‑checker zoals `pyspellchecker` om OCR‑fouten te vinden.

## Conclusie

We hebben **how to extract PDF** inhoud behandeld wanneer traditionele parsing faalt, een volledig **ocr python example** gedemonstreerd, en uitgelegd hoe je **recognize text from image** en **read PDF with OCR** kunt toepassen voor zowel enkel‑pagina als multi‑pagina scenario's. Met de bovenstaande code‑fragmenten kun je nu elke gescande PDF omzetten in doorzoekbare, bewerkbare tekst—geen handmatig overtypen meer.

Volgende stappen? Probeer de taal te wisselen naar Spaans (`ocr.Language.Spanish`) of experimenteer met beeld‑pre‑processing technieken om de nauwkeurigheid te verhogen. Als je een document‑managementsysteem bouwt, overweeg dan om de geëxtraheerde tekst te indexeren met Elasticsearch voor razendsnelle zoekopdrachten.

Heb je vragen of loop je tegen een eigenzinnige PDF aan? Laat een reactie achter, en happy coding!  

![Hoe PDF te extraheren met OCR in Python](image.png "Hoe PDF te extraheren met OCR in Python")

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Tekst extraheren uit afbeelding met Aspose OCR – Stapsgewijze gids](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [PDF-tekst herkennen – OCR‑operaties met Aspose.OCR voor Java](/ocr/english/java/ocr-operations/)
- [Afbeeldingstekst extraheren C# met taalkeuze met behulp van Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}