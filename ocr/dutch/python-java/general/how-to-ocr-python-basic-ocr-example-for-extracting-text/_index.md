---
category: general
date: 2026-04-26
description: 'hoe OCR in Python: Leer tekst uit een afbeelding te extraheren en een
  TIFF‑bestand te lezen met Python met een basis‑OCR‑voorbeeld. Snelle, uitvoerbare
  code inbegrepen.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: nl
og_description: 'hoe OCR in Python: Een stapsgewijze gids die laat zien hoe je tekst
  uit een afbeelding haalt, een TIFF‑bestand in Python leest en gescande afbeeldings­tekst
  converteert met een eenvoudig, uitvoerbaar script.'
og_title: hoe OCR in Python – Basis OCR-voorbeeld voor het extraheren van tekst
tags:
- OCR
- Python
- Image Processing
title: hoe OCR met Python – Basis OCR‑voorbeeld voor het extraheren van tekst
url: /nl/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hoe ocr python – Basis OCR-voorbeeld voor het extraheren van tekst

Heb je je ooit afgevraagd **how to ocr python** wanneer je een gescande TIFF op je bureau hebt liggen? Je bent niet de enige die naar een hoop afbeeldingsbestanden staart en zich afvraagt: “Hoe haal ik de woorden hieruit?” Het goede nieuws is dat het omzetten van een afbeelding naar platte tekst een fluitje van een cent is met de juiste bibliotheek en een paar duidelijke stappen.

In deze tutorial lopen we een **basic OCR example** stap voor stap door die een TIFF‑bestand leest, de tekst extraheert en deze naar de console print. Aan het einde weet je precies hoe je **extract text from image** bestanden kunt verwerken, hoe je de eigenaardigheden van TIFF‑formaten aanpakt, en wat je moet aanpassen als je **convert scanned image text** naar iets bruikbaars wilt omzetten. Geen verborgen magie—gewoon rechttoe rechtaan Python die je kunt copy‑paste en vandaag nog kunt uitvoeren.

## Wat je nodig hebt

- Python 3.9+ geïnstalleerd (de nieuwste stabiele release is het beste).
- Een via pip te installeren OCR‑bibliotheek. Voor deze gids gebruiken we een fictief `aocr`‑pakket dat populaire tools zoals Tesseract nabootst; je kunt het later vervangen door `pytesseract` of `easyocr`.
- Een TIFF‑afbeelding die je wilt verwerken – noem deze `input.tiff` en plaats hem in een map die je in de code zult refereren.
- Basiskennis van de commandoregel (alleen om het pakket te installeren).

Dat is alles. Geen zware afhankelijkheden, geen Docker‑containers, slechts een paar regels code.

## Stap 1 – Installeer en importeer afhankelijkheden (how to ocr python)

Eerst, haal het OCR‑pakket. Open een terminal en voer uit:

```bash
pip install aocr
```

Als je de voorkeur geeft aan een echte bibliotheek, vervang `aocr` door `pytesseract` en installeer de Tesseract‑engine apart.

Importeer nu wat we nodig hebben. De `Path`‑klasse van `pathlib` biedt ons een nette manier om met bestandspaden te werken op verschillende besturingssystemen.

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*Waarom `Path` gebruiken?* Omdat het de schuine strepen (`/` vs `\`) abstraheert en je mappen kunt samenvoegen zonder je zorgen te maken over het onderliggende besturingssysteem. Dat kleine detail bespaart vaak hoofdpijn wanneer je later het script naar een CI‑server verplaatst.

## Stap 2 – Maak een OCR‑engine‑instantie (basic ocr example)

Vervolgens start je de OCR‑engine. Beschouw `OcrEngine` als het brein dat de afbeelding leest en tekens uitspuwt.

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

De meeste OCR‑bibliotheken laten je hier taal, DPI of vertrouwensdrempels aanpassen. Voor dit **basic OCR example** blijven we bij de standaardinstellingen, maar je kunt later `ocr_engine.config` verkennen als je meertalige documenten moet verwerken.

## Stap 3 – Laad je TIFF‑afbeelding (read tiff file python)

Hier komt het **read tiff file python**‑gedeelte om de hoek kijken. TIFF‑bestanden kunnen meerdere pagina’s bevatten, maar `Image.load` pakt standaard de eerste pagina—perfect voor een enkel‑pagina scan.

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

Vervang `"YOUR_DIRECTORY"` door de daadwerkelijke map die `input.tiff` bevat. Als je niet zeker weet waar het script wordt uitgevoerd, geeft `Path.cwd()` de huidige werkmap weer—handig voor het debuggen van padproblemen.

## Stap 4 – Voer het OCR‑proces uit (extract text from image)

Nu gebeurt de magie. Het aanroepen van `process()` stuurt de afbeelding door de OCR‑pipeline en retourneert een resultaatobject.

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

Achter de schermen kan de engine de afbeelding naar grijstinten converteren, drempelwaarden toepassen en deze aan een neuraal netwerk voeren. Je hoeft die stappen niet te beheren; de bibliotheek abstraheert ze.

## Stap 5 – Print de herkende tekst (convert scanned image text)

Tot slot, geef de tekst weer. In echte projecten zou je deze waarschijnlijk naar een bestand of een database schrijven, maar afdrukken houdt het voorbeeld overzichtelijk.

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

Wanneer je het script uitvoert, zou je iets moeten zien als:

```
Hello, world!
This is a sample scanned document.
```

Als de output er rommelig uitziet, controleer dan of de bronafbeelding duidelijk is en of de OCR‑taal overeenkomt met de tekst.

## Volledig werkend script

Alles bij elkaar genomen, hier is het volledige, kant‑klaar script:

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Verwachte output

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

Als je **convert scanned image text** naar een doorzoekbare PDF wilt omzetten, kun je `ocr_result.text` doorsturen naar een PDF‑generator zoals `reportlab`—maar dat is een eigen tutorial.

## Veelvoorkomende valkuilen & Pro‑tips

- **Low‑resolution scans**: OCR heeft moeite onder 150 DPI. Als je TIFF wazig is, schaal deze eerst op met Pillow (`Image.open(...).resize(...)`).
- **Multiple pages**: Voor multi‑page TIFF‑bestanden, itereren over `Image.load_multi_page()` (als je bibliotheek dit ondersteunt) en de resultaten samenvoegen.
- **Language support**: Veel engines gebruiken standaard Engels. Stel `ocr_engine.language = "spa"` in voor Spaans, bijvoorbeeld.
- **Whitespace handling**: OCR voegt vaak losse regeleinden toe. Gebruik `str.splitlines()` of reguliere expressies om de output op te schonen.
- **Performance**: Voor bulkverwerking, hergebruik één `OcrEngine`‑instantie in plaats van voor elk bestand een nieuwe te maken.

## Het voorbeeld uitbreiden

Nu je **how to ocr python** voor een enkele afbeelding onder de knie hebt, overweeg je de volgende stappen:

1. **Batch processing** – Loop over een map met TIFF‑bestanden en schrijf elk resultaat naar een `.txt`‑bestand.
2. **Integration with Pandas** – Sla de geëxtraheerde tekst op naast metadata voor snelle analyse.
3. **Hybrid approach** – Combineer OCR met NLP‑bibliotheken zoals `spaCy` om entiteiten (namen, data, bedragen) uit gescande facturen te extraheren.
4. **Alternative file formats** – Vervang `Image.load` door `Image.from_bytes` om afbeeldingen te verwerken die uit een API of een database komen.

Al deze uitbreidingen bouwen voort op het kernidee van **extract text from image** en **convert scanned image text** naar iets dat machines kunnen begrijpen.

## Conclusie

We hebben een duidelijk, end‑to‑end **basic OCR example** doorlopen dat laat zien **how to ocr python**, hoe **read tiff file python** en hoe **extract text from image** bestanden met slechts een handvol regels. Het script is zelfstandig, bevat foutafhandeling en print het resultaat direct, waardoor het een solide basis vormt voor elk project dat gescande documenten naar bewerkbare tekst moet omzetten.

Voel je vrij om te experimenteren—verwissel de OCR‑backend, pas de preprocessing aan, of koppel de output aan een downstream‑workflow. De mogelijkheden zijn eindeloos wanneer je betrouwbaar **convert scanned image text** kunt omzetten naar doorzoekbare, doorzoekbare data.

Heb je vragen over randgevallen, taalpakketten of prestatie‑afstemming? Laat een reactie achter hieronder, en happy coding!

![how to ocr python example](/images/ocr-python-example.png "Screenshot of how to ocr python script output")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}