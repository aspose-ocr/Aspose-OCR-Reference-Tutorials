---
category: general
date: 2026-06-06
description: Haal tekst uit afbeeldingen en pdf's met Python OCR. Leer hoe je gescande
  documenten snel naar tekst kunt omzetten met asynchrone batchherkenning.
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: nl
og_description: Tekst extraheren uit afbeeldingen en pdf's met Python. Deze stap‑voor‑stap
  gids laat zien hoe je gescande documenten kunt omzetten naar tekst met async OCR.
og_title: Tekst uit PDF-afbeeldingen extraheren – Python OCR‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Tekst extraheren uit PDF‑afbeeldingen – Python‑gids voor het converteren van
  gescande documenten naar tekst
url: /nl/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit afbeeldingen PDF – Python-gids om gescande documenten naar tekst te converteren

Heb je ooit **tekst uit afbeeldingen pdf** moeten **extraheren** zonder uren te hoeven overtypen? In deze gids laten we je zien hoe je **gescande documenten naar tekst** kunt **converteren** met een eenvoudige asynchrone OCR-werkstroom in Python.  

Als je ooit naar een stapel gescande PDF's hebt gekeken en dacht: “Er moet toch een snellere manier zijn,” dan ben je op de juiste plek. We lopen elke regel code door, leggen uit waarom elk onderdeel belangrijk is, en behandelen zelfs een paar randgevallen die je kunt tegenkomen.

## Wat je zult leren

- Hoe je een OCR-engine opzet en de herkennings‑taal instelt.  
- De werking van het voeden van een gemengde lijst van PNG's en PDF's aan een batch‑herkenner.  
- Het asynchroon uitvoeren van de OCR-taak zodat je app responsief blijft.  
- Het ophalen van de resultaten, koppelen aan hun bronbestanden, en het afdrukken van nette output.  

**Voorwaarden**: Python 3.8+, een basisbegrip van `asyncio` of `concurrent.futures`, en een OCR‑bibliotheek die een `OcrEngine`‑klasse exposeert die vergelijkbaar is met die in het voorbeeld (bijv. Aspose.OCR, Tesseract‑wrapper, of een aangepaste wrapper). Geen zware installatie vereist—installeer gewoon de bibliotheek en je bent klaar om te gaan.

![tekst extraheren uit afbeeldingen pdf](https://example.com/placeholder.png "Schermafbeelding van OCR-uitvoer – tekst extraheren uit afbeeldingen pdf")

## Tekst extraheren uit afbeeldingen PDF – OCR-engine instellen

Het eerste wat je nodig hebt is een OCR‑engine‑instantie geconfigureerd voor de taal van je documenten. In ons geval gebruiken we Frans, maar je kunt dit vervangen door elke ondersteunde taal.

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**Waarom dit belangrijk is**: Het van tevoren instellen van de taal verbetert de nauwkeurigheid drastisch. De engine gebruikt taalspecifieke woordenboeken en tekenmodellen; het voeden van de verkeerde taal is een veelvoorkomende bron van onsamenhangende output.

## Bestandslijst voorbereiden – Afbeeldingen en PDF's samen

Onze batch‑herkenner kan zowel rasterafbeeldingen (`.png`, `.jpg`) als PDF‑containers verwerken. Geef gewoon een eenvoudige Python‑lijst met bestandspaden.

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**Tip**: Houd de lijst plat; de engine zal intern elke PDF‑pagina uitpakken naar afbeeldingen vóór herkenning. Als je duizenden bestanden hebt, overweeg dan de lijst op te splitsen in kleinere batches om geheugenpieken te voorkomen.

## Asynchrone batch‑herkenning starten

In plaats van de hoofdthread te blokkeren, starten we de OCR‑taak op de achtergrond. De methode retourneert een `Future` die uiteindelijk een lijst met `OcrResult`‑objecten bevat.

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**Hoe het werkt**: Intern spawnt de engine een thread‑pool (of een async‑taak, afhankelijk van de implementatie). Hierdoor kun je andere taken blijven uitvoeren—zoals een UI bijwerken, meer bestanden ophalen, of voortgang loggen—terwijl de zware verwerking elders plaatsvindt.

## Doe iets nuttigs terwijl OCR draait

Een veelgemaakte fout is om inactief te zitten en de future in een strakke lus te polleren. In plaats daarvan kun je willekeurig ander werk uitvoeren. Voor demonstratie zullen we gewoon een statusregel afdrukken.

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## Resultaten verzamelen zodra de Future voltooid is

Wanneer je klaar bent om de OCR‑output te verzamelen, gebruik je `as_completed` van `concurrent.futures`. Dit patroon werkt of je nu één future of meerdere hebt.

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**Wat je zult zien**: Elk bestandspad gevolgd door de geëxtraheerde platte‑tekstrepresentatie. Voor PDF's bevat `result.text` de samengevoegde tekst van elke pagina.

### Verwachte output (voorbeeld)

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

Als je ontbrekende tekens opmerkt, controleer dan of de ingestelde taal overeenkomt met de documenttaal, en overweeg de afbeeldingen vooraf te verwerken (kantelen corrigeren, contrast verhogen) voordat je ze aan de engine geeft.

## Randgevallen en veelvoorkomende valkuilen

| Situatie | Wat te doen |
|-----------|------------|
| **Gemengde talen** | Voer eerst een taal‑detectie‑pass uit, en instantiateer vervolgens aparte engines per taal. |
| **Grote PDF's (> 100 MB)** | Splits de PDF in afzonderlijke pagina's op schijf (bijv. met `PyPDF2`) en voer ze in als afzonderlijke items. |
| **Niet‑Latijnse scripts** | Zorg ervoor dat de OCR‑bibliotheek het benodigde taalpakket bevat; sommige bibliotheken vereisen dat je extra data‑bestanden downloadt. |
| **Prestatie‑knelpunt** | Verhoog de thread‑pool‑grootte (`engine.set_thread_pool_size(8)`) of schakel over naar een GPU‑versnelde backend indien beschikbaar. |
| **Ontbrekende tekst in lage‑resolutie‑afbeeldingen** | Pre‑process met OpenCV: `cv2.resize`, `cv2.threshold`, en `cv2.medianBlur` om de leesbaarheid te verbeteren. |

## Volledig werkend voorbeeld (klaar om te kopiëren en plakken)

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

Sla dit op als `extract_text_async.py`, vervang `YOUR_DIRECTORY` door het pad naar je bestanden, installeer het OCR‑pakket (`pip install your-ocr-lib`), en voer `python extract_text_async.py` uit. Je zou de console‑output moeten zien die eerder werd geïllustreerd.

## Volgende stappen – verder gaan dan basis‑extractie

- **Post‑processing**: Verwijder extra witruimte, normaliseer Unicode (`unicodedata.normalize`), of voer een spell‑checker uit om OCR‑ruis op te schonen.  
- **Gestructureerde output**: Exporteer resultaten naar CSV, JSON, of direct naar een database voor downstream zoeken.  
- **Parallelle batches**: Als je honderden bestanden hebt, start dan meerdere futures en gebruik een wachtrij om de CPU bezig te houden zonder het geheugen te overbelasten.  
- **Integreren met web‑frameworks**: Koppel dit script aan een Flask‑ of FastAPI‑endpoint om OCR on‑demand als service te bieden.

---

### TL;DR

Je weet nu hoe je **tekst uit afbeeldingen pdf** kunt **extraheren** met een minimale Python‑script die OCR asynchroon uitvoert, waardoor je **gescande documenten naar tekst** kunt **converteren** terwijl je programma responsief blijft. Experimenteer met de taalinstellingen, batch‑groottes en pre‑processing‑trucs om elke laatste teken‑nauwkeurigheid eruit te halen.

Heb je een variant die je wilt delen—misschien OCR op handgeschreven notities of een cloud‑gebaseerde service? Laat een reactie achter, en happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Tekst extraheren uit afbeelding met Aspose OCR – Stapsgewijze gids](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Tekst extraheren uit afbeeldingen met OCR‑bewerking op mappen](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Tekst extraheren uit afbeeldingen met Aspose.OCR – Toegestane tekens](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}