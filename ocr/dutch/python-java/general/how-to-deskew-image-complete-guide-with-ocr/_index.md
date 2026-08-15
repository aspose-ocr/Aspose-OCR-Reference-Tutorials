---
category: general
date: 2026-03-26
description: Leer hoe je een afbeelding kunt rechtzetten, tekst uit een afbeelding
  kunt herkennen en een beeldvoorverwerkingspipeline kunt bouwen om ruis uit een scan
  te verwijderen en een gescande afbeelding naar tekst te converteren.
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: nl
og_description: Hoe een afbeelding rechtzetten en een scheve scan omzetten in doorzoekbare
  tekst. Volg deze gids om tekst uit een afbeelding te herkennen, ruis uit een scan
  te verwijderen en een gescande afbeelding naar tekst te converteren.
og_title: Hoe een afbeelding rechtzetten – Stapsgewijze OCR‑gids
tags:
- OCR
- image-processing
- Python
title: Hoe een afbeelding rechtzetten – Complete gids met OCR
url: /nl/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een afbeelding rechtzetten – Complete gids met OCR

Heb je je ooit afgevraagd **hoe je een afbeelding rechtzet** die uit een goedkope scanner komt? Je bent niet de enige. Een scheve pagina ziet er onprofessioneel uit, en nog belangrijker, de helling kan elke OCR‑engine die probeert **tekst uit een afbeelding te herkennen** in de war brengen.  

In deze tutorial lopen we een volledige **image preprocessing pipeline** door die een scan rechtzet, binariseert en ruis verwijdert, en vervolgens doorgeeft aan een OCR‑engine zodat je **gescande afbeelding naar tekst kunt converteren** met minimale moeite. Geen magie, gewoon pure Python en een kleine bibliotheek die het zware werk doet.

## Wat je nodig hebt

- Python 3.9+ (de code werkt op 3.10 en nieuwer)
- Het `ocr`-pakket (installeer via `pip install ocr‑toolkit` – vervang door de naam van jouw bibliotheek)
- Een gescande JPEG of PNG die duidelijk scheef staat (bijv. `skewed_scan.jpg`)
- Een beetje nieuwsgierigheid naar waarom elke preprocessing‑stap belangrijk is

Dat is alles. Geen zware afhankelijkheden zoals OpenCV tenzij je later dieper wilt gaan.

## Stap 1: Laad de gescande afbeelding

Het eerste is om het bestand in het geheugen te laden. Deze stap is eenvoudig maar cruciaal—als het pad onjuist is, crasht alles.

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **Waarom?**  
> Het laden van de afbeelding geeft ons een bewerkbaar object waar de `ocr.ImagePreprocessor` mee kan werken. Het overslaan van deze stap zou de pipeline blind maken voor de daadwerkelijke pixelgegevens.

## Hoe een afbeelding rechtzetten en voorbereiden voor OCR

Nu we de afbeelding hebben, laten we deze rechtzetten. De `deskew()`‑methode schat de hellingshoek en draait de afbeelding terug naar horizontaal.

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **Pro tip:** Als je scans slechts licht scheef staan (≤ 3°), is het standaardalgoritme meestal perfect. Voor extreme hoeken moet je mogelijk de interne parameters aanpassen—raadpleeg de bibliotheek‑documentatie voor `max_angle`.

## Binariseer de afbeelding – Maak hem zwart‑wit

OCR‑engines houden van hoog‑contrast invoer. Het omzetten van de afbeelding naar een binaire (zwart‑wit) weergave verwijdert subtiele tinten die de tekenherkenning kunnen verwarren.

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **Wat gebeurt er?**  
> Pixels helderder dan 128 worden wit; alles anders wordt zwart. Pas de drempelwaarde aan als je scan ongewoon donker of licht is.

## Verwijder ruis van de scan vóór OCR

Zelfs een perfect rechtgezette afbeelding kan vlekjes, stof of compressie‑artefacten bevatten. Die kleine vlekjes zijn de plaag van elke OCR‑engine.

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **Waarom ruis verwijderen?**  
> Ruis creëert valse randen die de OCR‑engine kan interpreteren als tekens. Een kleine radius werkt voor de meeste scans; verhoog deze voor sterk korrelige documenten.

## Pas de image preprocessing pipeline toe

Alle configuratie is ingesteld—nu voeren we de pipeline uit op de originele afbeelding.

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **Resultaat:** `processed_image` is een opgeschoonde, rechte, hoog‑contrast bitmap klaar voor tekstextractie.

## Herken tekst uit afbeelding met OCR‑engine

Tijd om de tekst daadwerkelijk te lezen. We initialiseren de OCR‑engine, voeren onze gepolijste afbeelding in, en vragen om de ruwe string.

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Verwachte output** (voorbeeld):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Als je onduidelijke tekens ziet, controleer dan de deskew‑stap opnieuw of experimenteer met een andere `threshold`‑waarde.

## Een image preprocessing pipeline bouwen – Volledig script

Alles samenvoegend, hier is een enkel, uitvoerbaar script dat je in een `.py`‑bestand kunt plaatsen en uitvoeren:

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Tip:** Plaats het geheel in een functie (`def ocr_from_file(path): …`) als je van plan bent om veel bestanden in één batch te verwerken.

## Veelgestelde vragen & randgevallen

- **Wat als de afbeelding al rechtop staat?**  
  De `deskew()`‑methode detecteert een bijna‑nulhoek en laat de afbeelding onaangeroerd, zodat je hem veilig op elk bestand kunt toepassen.

- **Mijn scan is in kleur—moet ik die behouden?**  
  Kleur voegt geen waarde toe voor de meeste OCR‑taken. Binarisatie verwijdert het, waardoor de verwerking sneller gaat en het geheugenverbruik daalt.

- **Kan ik meerdere preprocessing‑stappen combineren?**  
  Zeker. De `ImagePreprocessor`‑klasse is ontworpen voor pipelines; je kunt `sharpen()`, `contrast_enhance()` of aangepaste filters toevoegen voordat je `apply()` aanroept.

- **De OCR‑output bevat vreemde regeleinden—hoe los ik dat op?**  
  Verwerk de string na afloop met `text.replace("\n", " ").strip()` of gebruik een geavanceerdere layout‑analyse bibliotheek zoals Tesseract’s `--psm`‑modi.

## Volgende stappen

Nu je weet **hoe je een afbeelding rechtzet** en een solide **image preprocessing pipeline** hebt, kun je het volgende verkennen:

- Het integreren van **recognize text from image** in een Flask‑API voor realtime documentuploads.
- Het gebruiken van de pipeline om **remove noise from scan** van historische documenten waar behoud cruciaal is.
- Opschalen om duizenden pagina's in batches te verwerken en een doorzoekbare PDF te genereren met `pdfminer` of `PyMuPDF`.

Voel je vrij om te experimenteren met verschillende drempelwaarden, denoise‑radii, of zelfs de OCR‑backend te vervangen door Tesseract als je meertalige ondersteuning nodig hebt. De basisprincipes blijven hetzelfde: rechtzetten, opschonen, dan lezen.

---

*Veel plezier met coderen! Als je tegen problemen aanloopt, laat dan een reactie achter—ik help je graag de pipeline fijn af te stemmen.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}