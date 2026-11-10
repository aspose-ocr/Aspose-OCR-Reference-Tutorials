---
category: general
date: 2026-07-05
description: Haal tekst uit een afbeelding met Python OCR. Leer hoe je tekst uit een
  afbeelding herkent, een afbeelding laadt voor OCR, en de OCR-taal instelt in slechts
  een paar regels.
draft: false
keywords:
- extract text from image
- how to recognize text from image
- load image for ocr
- create ocr engine python
- set ocr language
language: nl
og_description: Tekst extraheren uit afbeelding met Python OCR. Deze gids laat zien
  hoe je tekst uit een afbeelding herkent, een afbeelding laadt voor OCR, een OCR‑engine
  maakt in Python‑stijl, en de OCR‑taal instelt.
og_title: Tekst extraheren uit afbeelding in Python – Tekst snel herkennen
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to recognize text
    from image, load image for OCR, and set OCR language in just a few lines.
  headline: Extract Text from Image in Python – Recognize Text Fast
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Tekst extraheren uit afbeelding in Python – Tekst snel herkennen
url: /nl/python-java/general/extract-text-from-image-in-python-recognize-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeelding halen in Python – Tekst snel herkennen

Heb je ooit **tekst uit een afbeelding** moeten halen, maar wist je niet welke bibliotheek je moest kiezen? Als je jezelf ooit afvroeg *hoe tekst uit een afbeelding te herkennen* zonder externe tools te gebruiken, ben je hier op de juiste plek. In deze tutorial zetten we een kleine OCR‑engine op, richten die op een afbeelding, en halen de tekst eruit—niet meer, niet minder.

We lopen elke stap door: **create OCR engine python**, **set OCR language**, **load image for OCR**, start de herkenning asynchroon, en lees tenslotte het resultaat. Aan het einde heb je een zelfstandige script die je in elk project kunt gebruiken, of het nu een document‑digitaliser of een chatbot is die memes leest.

## Wat je nodig hebt

- Python 3.8+ (de code werkt ook op 3.10 en nieuwer)  
- Het `ocr`‑pakket (een dunne wrapper rond Tesseract – installeer met `pip install ocr` of je favoriete fork)  
- Een afbeeldingsbestand (`.jpg`, `.png`, etc.) dat leesbare tekst bevat  
- Een klein beetje geduld voor het async‑gedeelte (het is snel, beloofd)

Dat is alles—geen zware afhankelijkheden, geen native builds. Als je Tesseract al op je systeem hebt, zal de `ocr`‑wrapper het automatisch vinden.

## Stap 1: Maak de OCR‑engine – het hart van extractie

Allereerst: je hebt een engine‑object nodig dat weet hoe het moet communiceren met de onderliggende OCR‑engine. Beschouw het als het “brein” dat later de afbeelding zal verwerken.

```python
import ocr

# Step 1: Instantiate the OCR engine
engine = ocr.OcrEngine()
```

*Waarom dit belangrijk is*: zonder een engine heb je geen context voor taalinstellingen of async‑mogelijkheden. De `OcrEngine`‑klasse abstraheert de low‑level command‑line‑aanroepen naar Tesseract, en biedt je een nette Python‑API.

## Stap 2: Stel OCR‑taal in – vertel de engine wat te verwachten

Als je document Engels is, kun je de standaard laten staan, maar het is goed om het expliciet in te stellen. Dit laat ook zien hoe je **set OCR language** voor andere locales kunt instellen.

```python
# Step 2: Explicitly set the language to English
engine.language = ocr.Language.ENGLISH
```

> **Pro tip**: Voor meertalige PDF‑bestanden kun je een lijst doorgeven zoals `[ocr.Language.ENGLISH, ocr.Language.FRENCH]`. De engine zal beide talen automatisch proberen.

## Stap 3: Laad afbeelding voor OCR – breng je afbeelding in het geheugen

Nu **load image for OCR** we echt. De wrapper ondersteunt lazy loading, zodat het bestand pas wordt gelezen wanneer de engine het nodig heeft.

```python
# Step 3: Load the image you want to process
image_path = "YOUR_DIRECTORY/large_document.jpg"
image = ocr.Image.load(image_path)
```

*Randgeval*: Als de afbeelding enorm is (meer dan 5 MB), overweeg dan eerst te verkleinen om de herkenning te versnellen. Je kunt dat doen met Pillow:

```python
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio, max 2000px
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")
```

## Stap 4: Start asynchrone herkenning – blokkeer je app niet

Het uitvoeren van OCR kan een seconde of twee duren, vooral bij grote scans. De `recognize_async`‑methode retourneert een future die je later kunt pollen, waardoor je **anders werk kunt uitvoeren terwijl OCR op de achtergrond draait**.

```python
# Step 4: Start the recognition asynchronously
future = engine.recognize_async(image)

# While OCR works, we can do something else
print("Processing other tasks while OCR runs...")
# Example placeholder work
for i in range(3):
    print(f"Task {i+1} done.")
```

Waarom async? In een webserver wil je niet dat één verzoek de hele worker‑pool blokkeert. Het future‑object geeft je controle: je kunt er `await` op gebruiken in async code of alleen blokkeren wanneer je het resultaat echt nodig hebt.

## Stap 5: Haal het resultaat op – blokkeer alleen wanneer nodig

Wanneer je uiteindelijk de tekst nodig hebt, roep je `future.get()` aan. Deze oproep **blokkeert alleen hier**, wat betekent dat de rest van je programma responsief blijft totdat de OCR klaar is.

```python
# Step 5: Get the recognized text (blocks here)
result = future.get()   # blocks only at this point
```

Als je binnen een `asyncio`‑lus zit, kun je in plaats daarvan `await future` gebruiken – de wrapper ondersteunt beide stijlen.

## Stap 6: Gebruik de herkende tekst – je data is klaar

Nu je een `result`‑object hebt, is het ophalen van de platte string triviaal. Laten we het afdrukken en ook laten zien hoe je het naar een bestand kunt schrijven.

```python
# Step 6: Output the OCR result
print("OCR completed:")
print(result.text)

# Optional: save to a .txt file
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Verwachte output** (afgekapt voor beknoptheid):

```
OCR completed:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Als de afbeelding geen tekst bevat, zal `result.text` een lege string zijn—handel dat geval netjes af.

## Volledig werkend voorbeeld – Alle stappen in één script

Hieronder staat het volledige, kant‑klaar script. Kopieer‑plak, pas `image_path` aan, en je bent klaar om te gaan.

```python
import ocr
from PIL import Image as PilImage

# -------------------------------------------------
# 1️⃣ Create OCR engine
engine = ocr.OcrEngine()

# 2️⃣ Set language (English)
engine.language = ocr.Language.ENGLISH

# 3️⃣ Load image (optional resize for large files)
original_path = "YOUR_DIRECTORY/large_document.jpg"
pil_img = PilImage.open(original_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")

# 4️⃣ Start async recognition
future = engine.recognize_async(image)
print("Processing other tasks while OCR runs...")
for i in range(3):
    print(f"Task {i+1} done.")

# 5️⃣ Wait for result
result = future.get()

# 6️⃣ Use the text
print("OCR completed:")
print(result.text)
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

> **Opmerking**: Vervang `"YOUR_DIRECTORY/large_document.jpg"` door het daadwerkelijke pad naar je afbeelding. Het script werkt op Windows, macOS en Linux zolang Tesseract geïnstalleerd is en bereikbaar in je `PATH`.

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Garbage characters** | Verkeerde taal of ontbrekende taal‑databestanden. | Zorg ervoor dat `engine.language` overeenkomt met de tekst en dat het bijbehorende `.traineddata`‑bestand bestaat in de `tessdata`‑map van Tesseract. |
| **Slow performance on big images** | OCR schaalt ongeveer met het aantal pixels. | Verklein of down‑sample voordat je het aan de engine geeft (zie de Pillow‑snippet). |
| **Future never resolves** | Afbeeldingsbestand corrupt of onleesbaar. | Plaats `future.get()` in een try/except‑blok en valideer `image.is_valid()` vóór herkenning. |
| **Unicode loss** |  |  |

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Tekst uit afbeelding halen met Aspose OCR – Stapsgewijze gids](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Afbeelding naar tekst converteren – OCR uitvoeren op afbeelding van URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Tekst uit afbeelding halen – OCR‑optimalisatie met Aspose OCR voor .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}