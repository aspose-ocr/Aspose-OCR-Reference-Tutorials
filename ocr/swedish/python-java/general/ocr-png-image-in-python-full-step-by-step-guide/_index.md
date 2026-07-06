---
category: general
date: 2026-06-06
description: OCR PNG-bild med Python – lär dig hur du extraherar text från en bild,
  kör ett Python OCR‑exempel och läs även antik grekisk text enkelt.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: sv
og_description: OCR PNG-bild i Python förklarad. Den här guiden visar hur man extraherar
  text från en bild, kör ett Python‑OCR‑exempel och läser forngrekiska med lätthet.
og_title: OCR PNG-bild i Python – Komplett handledning
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR PNG‑bild i Python – Fullständig steg‑för‑steg‑guide
url: /sv/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR PNG-bild i Python – Fullständig steg‑för‑steg‑guide

Har du någonsin undrat hur man **OCR PNG image** filer direkt från ett Python‑script? Kanske har du en mapp full av skannade antika manuskript och du behöver **extract text from image** filer utan att manuellt skriva in allt. Den goda nyheten är att du inte behöver en doktorsexamen i datorseende—bara några rader kod och rätt bibliotek, så kommer du att läsa antik grekiska på sekunder.

I den här handledningen går vi igenom ett **python OCR example** som känner igen text från en PNG, sätter språket till grekisk polytonisk, och skriver ut resultatet. I slutet vet du exakt hur man **recognize image text**, hanterar vanliga fallgropar, och anpassar skriptet för andra språk eller bildformat.

## Vad du kommer att lära dig

- Installera och konfigurera ett Python OCR‑bibliotek (pytesseract + Tesseract OCR)
- Skapa en OCR‑motorinstans och ladda en PNG‑fil
- Ställ in igenkänningsspråket till grekisk polytonisk så att du kan **read ancient greek**
- Skriv ut den igenkända texten och felsök vanliga problem
- Utöka skriptet för att batch‑processa flera PNG‑filer eller byta till ett annat språk

### Förutsättningar

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | Modern syntax och typindikeringar |
| `pytesseract` package | Tunn omslag runt Tesseract‑motorn |
| Tesseract OCR binaries (≥ 5.0) | Den faktiska motorn som utför det tunga arbetet |
| Greek language data (`grc.traineddata`) | Behövs för att **read ancient greek** korrekt |
| A PNG image you want to analyse (e.g., `ancient_greek.png`) | Vårt mål för **ocr png image**‑demo |

Du kan installera Python‑delen med:

```bash
pip install pytesseract Pillow
```

Och på Ubuntu/macOS skulle du lägga till själva motorn:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

Glöm inte att ladda ner den grekiska polytoniska träningsdatan:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(Sökvägen kan skilja sig; justera `TESSDATA_PREFIX` om det behövs.)*

---

## OCR PNG-bild: Skapa motorinstansen

Det första vi behöver är ett objekt som kommunicerar med Tesseract. I `pytesseract` nås motorn via modul‑nivåfunktioner, men för tydlighetens skull kommer vi att omsluta den i en liten klass. Detta speglar “engine”-konceptet du såg i det ursprungliga kodsnutten.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**Varför omsluta den?**  
- Behåller det offentliga API:et identiskt med kodsnutten du började med, vilket gör migration smärtfri.  
- Gör det möjligt att lägga till loggning eller felhantering senare utan att röra huvudflödet.  
- Visar god OOP‑praxis—något som erfarna utvecklare uppskattar.

---

## Extrahera text från bild: Ställ in språket till grekisk polytonisk

Nu när vi har en motor måste vi tala om för den vilket språk som förväntas. Grekisk polytonisk använder diakritiska tecken som inte täcks av den standard “greek”-datan, så vi pekar Tesseract på den tränade filen `grc`.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

Om du någonsin vill **extract text from image** filer på ett annat språk, ersätt bara `"grc"` med `"eng"` för engelska, `"fra"` för franska osv. Samma rad fungerar för alla språk du har installerat.

---

## Känn igen bildtext: Kör OCR på en PNG

Med språket inställt matar vi PNG‑filen till motorn. Det ursprungliga exemplet använde en hårdkodad sökväg; vi gör det lite mer flexibelt genom att använda `Path`‑objekt.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**Tips & kantfall**  
- **File not found** – omslut anropet i ett `try/except FileNotFoundError` för att ge ett vänligt meddelande.  
- **Low‑resolution PNG** – överväg förbehandling (t.ex. storleksändring, binarisering) med Pillow före OCR.  
- **Non‑Greek text** – Tesseract kommer fortfarande att försöka avkoda, men noggrannheten sjunker kraftigt. Matcha alltid språket.

---

## Skriv ut den igenkända texten

Till sist skriver vi ut resultatet. I ett riktigt projekt kan du skriva till en databas, en CSV‑fil, eller till och med föra in det i en översättningspipeline.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

När du kör skriptet mot en klar skanning av en antik grekisk inskription bör du se något liknande:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

Om utskriften ser förvrängd ut, dubbelkolla att filen **greek.traineddata** finns i rätt mapp och att PNG‑filen inte är för brusig.

---

## Fullt fungerande exempel (alla steg i ett skript)

Nedan är det kompletta, färdiga programmet. Spara det som `ocr_greek.py` och kör `python ocr_greek.py`.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Förväntad utskrift** (avkortad för korthet):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

Om du ser de korrekta grekiska tecknen, grattis—du har framgångsrikt utfört en **ocr png image**‑operation i Python!

---

## Vanliga frågor & pro‑tips

### Hur förbättrar jag noggrannheten på en brusig PNG?

- Konvertera bilden till gråskala: `img = img.convert('L')`
- Applicera ett binärt tröskelvärde: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- Skala upp med `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

Dessa steg förvandlar ofta en **recognize image text**‑mardröm till ett rent resultat.

### Kan jag bearbeta en hel mapp med PNG‑filer?

Absolut. Omslut anropet `recognize_image` i en `for`‑loop över `Path.glob("*.png")`. Spara varje resultat i en dictionary eller skriv till en CSV för senare analys.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### Vad händer om jag bara behöver extrahera siffror?

Skicka en anpassad **config**‑sträng till `image_to_string`:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

På så sätt kan du **extract text from image** filer som innehåller tabeller, serienummer eller tidsstämplar.

### Finns det ett sätt att få förtroendesiffror?

Ja—använd `pytesseract.image_to_data` som returnerar en TSV med förtroende per ord. Du kan filtrera bort lågt förtroende‑token innan du sätter ihop den slutgiltiga strängen.

---

## Utöka handledningen

Nu när du har bemästrat grunderna, överväg att utforska dessa relaterade ämnen:

- **Batch OCR with multiprocessing** – snabba upp stora korpusar av PNG‑filer.  
- **Hybrid OCR + NLP pipelines** – översätt automatiskt den extraherade antika grekiskan till modern engelska.  
- **Alternative engines** – prova `easyocr` eller `opencv`‑baserade metoder för specifika användningsfall.  
- **Cloud OCR services** – Google Vision, Azure Computer Vision, eller AWS Textract för serverlös skalning.

Var och en av dessa bygger på det grundläggande **python ocr example** vi just gick igenom, så du kommer känna dig bekväm att dyka djupare.

## Slutsats

Vi har tagit ett enkelt kodsnutt och gjort om det till ett robust **ocr png image**‑arbetsflöde i Python. Genom att skapa en `OcrEngine`, sätta språket till grekisk polytonisk, mata in en PNG och skriva ut resultatet, vet du nu hur man **extract text from image** filer, **recognize image text**, och till och med **read ancient greek**.

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Extrahera text från bild med Aspose OCR – steg‑för‑steg‑guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Hur man ställer in tröskelvärde i OCR‑bildigenkänning](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Känna igen textbild med Aspose OCR för flera språk](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}