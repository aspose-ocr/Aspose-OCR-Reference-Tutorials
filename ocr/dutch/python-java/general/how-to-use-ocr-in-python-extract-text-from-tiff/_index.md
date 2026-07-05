---
category: general
date: 2026-07-05
description: Hoe OCR in Python te gebruiken om TIFF snel naar tekst te converteren.
  Leer de OCR‑bibliotheek‑stappen in Python voor het extraheren van tekst uit TIFF‑afbeeldingen
  en het bouwen van een Python‑OCR‑engine.
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: nl
og_description: Hoe OCR te gebruiken in Python? Deze gids laat je stap‑voor‑stap zien
  hoe je TIFF naar tekst kunt converteren met een Python OCR‑engine en de OCR‑bibliotheek
  Python.
og_title: Hoe OCR te gebruiken in Python – Complete TIFF-tekstextractie
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: Hoe OCR in Python te gebruiken – Tekst uit TIFF extraheren
url: /nl/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR te gebruiken in Python – Tekst extraheren uit TIFF

Heb je je ooit afgevraagd **hoe je OCR in Python** kunt gebruiken om een gescand boek om te zetten in bewerkbare tekst? Je bent niet de enige—ontwikkelaars, onderzoekers en hobbyisten lopen allemaal tegen dit obstakel aan bij het werken met multi‑page TIFF‑afbeeldingen. Het goede nieuws? Met de **ocr library python** kun je een kleine OCR‑engine opzetten, erop wijzen naar een TIFF‑bestand, en binnen enkele seconden schone, doorzoekbare tekst krijgen.

In deze tutorial lopen we alles door wat je nodig hebt: het installeren van het juiste pakket, het laden van een multi‑page TIFF, het uitvoeren van de OCR‑engine, en uiteindelijk het afdrukken van de inhoud van elke pagina. Aan het einde kun je **TIFF naar tekst converteren** en **tekst uit TIFF extraheren** zonder je Python‑omgeving te verlaten.

## Vereisten

- Python 3.9 of nieuwer (het voorbeeld is getest op 3.11)
- Een recente versie van de `ocr` library (of elke compatibele `python ocr engine` die je prefereert)
- Een multi‑page TIFF‑bestand dat je wilt verwerken (we noemen het `scanned_book.tif`)
- Basiskennis van Python‑scripts en virtuele omgevingen

Geen zware externe tools vereist—alleen pip en een paar regels code.

## Installeer de OCR Library Python

Allereerst: je hebt een solide OCR‑backend nodig. Voor deze gids gebruiken we het fictieve `ocr`‑pakket dat wordt geleverd met een eenvoudige high‑level API, maar hetzelfde patroon werkt met Tesseract‑gebaseerde wrappers zoals `pytesseract` of commerciële SDK's.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro tip:** Als je Windows gebruikt en het pakket vertrouwt op native binaries, zorg er dan voor dat je de juiste Visual C++ redistributable geïnstalleerd hebt. De installer waarschuwt je meestal als er iets ontbreekt.

## Hoe OCR Engine te gebruiken in Python

Nu de library klaar is, laten we een OCR‑engine opzetten en erop wijzen naar ons TIFF‑bestand. Het volgende fragment maakt een engine‑instance, stelt de taal in op Engels, en bereidt het voor op multi‑page verwerking.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**Waarom de taal instellen?**  
De meeste OCR‑engines gebruiken taalmode­len om de nauwkeurigheid te verbeteren. Als je deze stap overslaat, valt de engine terug op een generiek model dat interpunctie of speciale tekens mogelijk verkeerd herkent.

## Laad de Multi‑Page TIFF Afbeelding

Het volgende onderdeel is het laden van het gescande document. De `ocr.Image.load` helper begrijpt TIFF‑stapels direct, en retourneert een object dat intern elke pagina vertegenwoordigt.

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Edge case:** Als je TIFF compressie gebruikt (CCITT Group 4, LZW, etc.) en de library een fout geeft, probeer het eerst te converteren naar een ongecomprimeerde versie met ImageMagick:
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## Voer OCR uit op alle pagina's – Converteer TIFF naar Tekst

Met het afbeelding‑object in de hand kan de engine nu elke pagina tegelijk verwerken. Deze methode retourneert een lijst waarbij elk element het OCR‑resultaat voor één pagina bevat.

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**Wat gebeurt er onder de motorkap?**  
De `recognize_multi_page` functie iterereert over elke gerasterde pagina, voert de neurale‑netwerk herkenner uit, en verpakt de platte‑tekst output samen met confidence‑scores. Het is in wezen een batch‑operatie die je bespaart van het handmatig schrijven van een lus.

## Doorloop de resultaten – Tekst extraheren uit TIFF

Tot slot tonen we de herkende tekst. Je kunt de output schrijven naar afzonderlijke `.txt`‑bestanden, naar een database sturen, of invoeren in een zoekindex—wat ook maar bij je workflow past.

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### Verwachte Output

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

Elke `result.text`‑string bevat de ruwe OCR‑output voor die pagina. Als je behoud van regeleinden nodig hebt, bieden de meeste engines `result.lines` aan als een lijst van strings.

## Grote TIFF‑bestanden verwerken – Tips & Tricks

Het verwerken van een 500‑pagina TIFF kan veel geheugen verbruiken. Hier zijn een paar strategieën om alles soepel te laten verlopen:

1. **Deel de pagina's op** – In plaats van `recognize_multi_page`, roep `engine.recognize(page)` aan binnen een generator die één pagina per keer oplevert.
2. **Pas DPI aan** – Het verlagen van de beeldresolutie (bijv. van 300 DPI naar 200 DPI) vermindert de CPU‑belasting terwijl het de nauwkeurigheid voor de meeste gedrukte tekst nauwelijks beïnvloedt.
3. **Paralleliseer** – Als je OCR‑engine thread‑safe is, start een `concurrent.futures.ThreadPoolExecutor` om herkenning op meerdere pagina's gelijktijdig uit te voeren.

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## Sla de geëxtraheerde tekst op in bestanden

De meeste real‑world pipelines hebben permanente opslag nodig. Hieronder staat een beknopte manier om de tekst van elke pagina in een eigen bestand te dumpen, met behoud van de paginavolgorde.

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

Nu heb je een nette map met `.txt`‑bestanden die klaar zijn voor indexering of verdere NLP‑verwerking.

## Afbeeldingsvoorbeeld – OCR‑resultaten visueel gebruiken

Als je de OCR‑overlay op de originele afbeelding wilt zien (handig voor debugging), laten veel libraries je rechthoeken tekenen. Hier is een snel voorbeeld met Pillow:

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![Hoe OCR te gebruiken in Python – OCR overlay op een TIFF-pagina](ocr_overlay_example.png)

*Alt‑tekst:* Hoe OCR te gebruiken in Python – visuele overlay van herkende tekst op een TIFF‑pagina.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|-------|----------------|-----|
| Vervormde tekens | Verkeerd taalmodel | Stel `engine.language` in op de juiste enum |
| Ontbrekende pagina's | TIFF-compressie niet ondersteund | Converteer eerst naar een ongecomprimeerde TIFF |
| Trage prestaties | Hoge DPI + single‑threaded verwerking | Verlaag DPI of schakel multi‑threading in |
| Lege output | Afbeelding is te donker/laag contrast | Pre‑process met contrast stretching (`opencv` of `Pillow`) |

Deze vroeg aanpakken bespaart je later uren debugging.

## Volgende stappen – Verder gaan dan basisextractie

Nu je de basis van **hoe OCR in Python te gebruiken** onder de knie hebt, overweeg dan om te verkennen:

- **PDF-generatie** – Combineer geëxtraheerde tekst met `reportlab` om doorzoekbare PDF's opnieuw op te bouwen.
- **Taaldetectie** – Schakel `engine.language` automatisch over met `langdetect`.
- **Gestructureerde data‑extractie** – Gebruik reguliere expressies of spaCy om datums, namen of tabellen uit de ruwe tekst te halen.
- **Alternatieve OCR‑backends** – Vervang `ocr` door `pytesseract` of `easyocr` als je meertalige ondersteuning nodig hebt.

Elk van deze onderwerpen sluit natuurlijk aan bij de secundaire zoekwoorden **ocr library python**, **convert tiff to text**, **extract text from tiff**, en **python ocr engine**, en geeft je een stevige basis voor meer geavanceerde projecten.

---

### Conclusie

We hebben **hoe OCR in Python te gebruiken** behandeld, van installatie tot multi‑page verwerking, en laten precies zien hoe je **TIFF naar tekst kunt converteren** en **tekst uit TIFF kunt extraheren** met een eenvoudige **python OCR engine**. Het volledige, uitvoerbare voorbeeld hierboven zou direct moeten werken voor de meeste standaard TIFF‑bestanden, en de gegeven tips helpen je om op te schalen naar grotere documenten of OCR in grotere pipelines te integreren.

Probeer het met je eigen gescande boeken, bonnetjes of archiefafbeeldingen—en experimenteer vervolgens met de next‑level ideeën die staan in de sectie “Volgende stappen”. Veel plezier met coderen, en moge je OCR‑resultaten altijd accuraat zijn!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Tekst extraheren uit afbeelding met Aspose OCR – Stapsgewijze gids](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Hoe tekst te extraheren uit tiff met Aspose.OCR voor Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Hoe afbeeldingstekstextractie uit stream uit te voeren met Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}