---
category: general
date: 2026-03-26
description: Leer hoe je OCR kunt uitvoeren op Arabische PNG‑afbeeldingen en Arabische
  tekst snel kunt extraheren. Deze gids toont het omzetten van afbeelding naar tekst
  met stap‑voor‑stap Python‑code.
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: nl
og_description: Hoe voer je OCR uit op Arabische PNG‑afbeeldingen? Volg deze volledige
  gids om Arabische tekst te extraheren, Arabische tekst te herkennen en een afbeelding
  naar tekst te converteren met Python.
og_title: Hoe OCR uit te voeren op een Arabische PNG – Tekst uit afbeelding halen
tags:
- OCR
- Python
- Arabic
title: Hoe OCR op een Arabische PNG uit te voeren – Tekst uit afbeelding extraheren
url: /nl/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren op Arabische PNG – Tekst uit afbeelding halen

Heb je je ooit afgevraagd **hoe je OCR** kunt uitvoeren op een afbeelding met Arabisch schrift? Misschien heb je een gescande bon, een historisch manuscript, of gewoon een screenshot van een social‑media‑post en heb je de tekst nodig in een doorzoekbaar formaat. Je bent niet de enige—ontwikkelaars wereldwijd lopen tegen dit probleem aan bij het werken met rechts‑naar‑links‑talen.

In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat laat zien **hoe je OCR** uitvoert op een PNG‑bestand, Arabische tekst extraheert, en het resultaat naar de console print. Geen vage “zie de docs”‑links; alleen de code die je kunt copy‑pasten, plus uitleg waarom elke regel belangrijk is. Aan het einde kun je **afbeelding naar tekst** betrouwbaar omzetten, zelfs wanneer de bron een lastige Arabische PNG is.

> **Wat je zult leren**
> - Een Python OCR‑engine voor Arabisch configureren  
> - Een PNG‑afbeelding laden en veelvoorkomende valkuilen behandelen  
> - Arabische tekst herkennen en de output verifiëren  
> - Tips voor **het extraheren van Arabische tekst** uit verschillende beeldkwaliteiten  

Voordat we beginnen, zorg ervoor dat je Python 3.8+ geïnstalleerd hebt en een recente versie van de `ocr`‑bibliotheek (dezelfde die in het fragment wordt gebruikt). Als je een virtuele omgeving gebruikt, activeer die nu—dit houdt afhankelijkheden netjes.

## Vereisten

- Python 3.8 of nieuwer  
- `ocr`‑package (`pip install ocr‑engine` – vervang door de daadwerkelijke pakketnaam)  
- Een Arabische PNG‑afbeelding (`arabic_doc.png`) ergens geplaatst die je kunt refereren  
- Basiskennis van Python‑functies en -klassen  

Dat is alles. Geen zware frameworks, geen Docker‑containers—gewoon pure Python.

## Stap 1: Installeer en importeer de OCR‑bibliotheek

Allereerst. We hebben de OCR‑engine zelf nodig. De bibliotheek die we gebruiken biedt een `OcrEngine`‑klasse met een eenvoudige API.

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*Waarom `Imaging` apart importeren?* De `Imaging`‑submodule geeft ons een handige `Image.load`‑methode die PNG, JPEG en TIFF direct begrijpt. Als je deze stap overslaat, moet je zelf ruwe bytes verwerken, wat onnodig is voor de meeste use‑cases.

## Stap 2: Maak een OCR‑engine‑instantie

Nu maken we een instantie van de engine. Beschouw dit object als het “brein” dat de afbeelding zal verwerken.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **Pro tip:** Als je van plan bent om veel afbeeldingen achter elkaar te verwerken, hergebruik dan dezelfde `ocr_engine`‑instantie. Deze cachet taalmodellen, waardoor latere herkenningen sneller gaan.

## Stap 3: Stel de taal in op Arabisch

Arabisch is geen Latijn; het heeft een eigen karakterset, rechts‑naar‑links‑richting en contextuele vormgeving. Daarom moeten we expliciet aangeven welk taalmodel de engine moet laden.

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

Als je deze regel vergeet, valt de engine terug op Engels en krijg je rommelige output—iets wat ik veel te vaak heb gezien.

## Stap 4: Laad je PNG‑afbeelding

Hier begint het **afbeelding naar tekst**‑gedeelte echt. We laden het PNG‑bestand dat het Arabische schrift bevat.

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### Veelvoorkomende randgevallen

| Probleem | Symptoom | Oplossing |
|----------|----------|-----------|
| Afbeelding is te donker | Output bevat veel lege plekken | Pre‑process met Pillow (`ImageEnhance.Brightness`) |
| PNG heeft een alfakanaal | Sommige OCR‑engines lezen transparante pixels verkeerd | Converteer naar RGB (`image.convert("RGB")`) vóór het laden |
| Tekst is gedraaid | Herkende tekst staat ondersteboven | Draai de afbeelding (`image.rotate(90, expand=True)`) vóór het doorgeven aan de engine |

## Stap 5: Voer het herkenningsproces uit

Met alles ingesteld vragen we nu de engine om zijn werk te doen.

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

De `recognize`‑methode retourneert een object dat de ruwe Unicode‑string, confidence‑scores en bounding boxes bevat. Voor de meeste ontwikkelaars is de platte tekst alles wat je nodig hebt.

## Stap 6: Geef de herkende Arabische tekst weer

Nu printen we het resultaat. In een echte applicatie zou je naar een bestand, een database of een vertaal‑API kunnen schrijven.

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

Wanneer je het script uitvoert, zou je de Arabische tekens in je console moeten zien (zorg dat je terminal Unicode ondersteunt). Als je vraagtekens of lege strings ziet, controleer dan de taalinstelling en de kwaliteit van de afbeelding.

### Verwachte output

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

Als de output er ongeveer zo uitziet als de regel hierboven, gefeliciteerd—je hebt succesvol **Arabische tekst geëxtraheerd** uit een PNG!

## Volledig werkend voorbeeld

Hieronder staat het volledige script, klaar om te copy‑pasten. Vervang `YOUR_DIRECTORY/arabic_doc.png` door het pad naar jouw eigen bestand.

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

Voer het uit met `python run_ocr.py` (of hoe je het bestand ook hebt genoemd). Als alles correct geïnstalleerd is, zie je de Arabische zin in de console verschijnen.

## Hoe OCR uit te voeren op verschillende afbeeldingsformaten

Dezelfde code werkt voor JPEG, TIFF of BMP—verander simpelweg de bestandsextensie. De `Image.load`‑methode detecteert automatisch het formaat, zodat je **afbeelding naar tekst** kunt omzetten zonder extra code.

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

Onthoud dat de kwaliteit van de bronafbeelding de nauwkeurigheid van de **herkenning van Arabische tekst** sterk beïnvloedt. Hoge resolutie, weinig compressie geeft de beste resultaten.

## Tekst uit PNG halen: Tips voor betere nauwkeurigheid

1. **DPI is belangrijk** – Streef naar minimaal 300 dpi. Lagere DPI leidt vaak tot gemiste tekens.  
2. **Contrast is koning** – Gebruik beeldbewerkings‑tools (bijv. OpenCV) om het contrast te verhogen vóór je de afbeelding aan de OCR‑engine geeft.  
3. **Ruisverwijdering** – Kleine vlekjes kunnen het model verwarren; median filtering helpt.  

Hier is een kort fragment met Pillow om een PNG te verbeteren vóór OCR:

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## Veelgestelde vragen

**V: Werkt dit ook met andere rechts‑naar‑links‑talen dan Arabisch?**  
A: Zeker. Verander gewoon de taalcodes (`"ar"` → `"he"` voor Hebreeuws, `"fa"` voor Perzisch) en de engine laadt het juiste model.

**V: Wat als ik tekst moet extraheren uit meerdere PNG’s in een map?**  
A: Loop over de bestanden, hergebruik dezelfde `ocr_engine`‑instantie, en verzamel de resultaten in een lijst of schrijf elk naar een apart `.txt`‑bestand.

**V: Kan ik confidence‑scores per woord krijgen?**  
A: Ja. `ocr_result` biedt vaak een `get_confidences()`‑methode. Koppel elke confidence aan het bijbehorende woord voor kwaliteitscontrole.

## Volgende stappen

Nu je weet **hoe je OCR** op Arabische PNG’s uitvoert, overweeg deze vervolgstappen:

- **Batchverwerking:** Combineer het script met `os.listdir` om **Arabische tekst te extraheren** uit een hele directory.  
- **Post‑processing:** Gebruik de `arabic_reshaper` en `python-bidi`‑bibliotheken om rechts‑naar‑links‑output correct weer te geven in PDF’s.  
- **Integratie:** Stuur de geëxtraheerde tekst naar een zoekindex (bijv. Elasticsearch) om gescande documenten doorzoekbaar te maken.  

Al deze onderwerpen bouwen voort op de hier behandelde basis, en ze helpen je om een eenvoudige **afbeelding naar tekst**‑script om te vormen tot een productie‑klare pipeline.

---

![how to run OCR on Arabic PNG](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}