---
category: general
date: 2026-03-18
description: Kör OCR på bild snabbt med Python. Lär dig hur du känner igen text från
  PNG, laddar bilden för OCR och extraherar ord från bilden i en steg‑för‑steg‑guide.
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: sv
og_description: Kör OCR på bild med Python. Den här handledningen visar hur du känner
  igen text från PNG, laddar bilden för OCR och extraherar ord från bilden med ett
  komplett kodexempel.
og_title: Kör OCR på bild – Python‑guide
tags:
- OCR
- Python
- Image Processing
title: Kör OCR på bild – Komplett Python OCR‑exempel
url: /sv/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kör OCR på bild – Komplett Python OCR-exempel

Har du någonsin behövt **run OCR on image** filer men varit osäker på var du ska börja? Du är inte ensam; många utvecklare stöter på den muren när de första gången försöker extrahera text från skannade dokument. I den här handledningen går vi igenom ett **Python OCR example** som låter dig **recognize text from PNG** filer, **load image for OCR**, och **extract words from image** med förtroendesiffror – allt på bara några kodrader.

Vi kommer att gå igenom allt du behöver: det nödvändiga biblioteket, hur du sätter upp motorn, varför varje steg är viktigt, och hur utdata ser ut. När du är klar kan du enkelt klistra in detta kodsnutt i ditt eget projekt och börja hämta text från vilken bild som helst på ett ögonblick. Inga onödiga utsvävningar, bara en praktisk, körbar lösning.

## Vad du behöver

- Python 3.8 eller nyare installerat  
- `ocrengine`‑paketet (eller något bibliotek som tillhandahåller en `OcrEngine`‑klass). Du kan installera det via `pip install ocrengine` – justera namnet om du använder ett annat OCR‑bibliotek som `pytesseract`.  
- En bildfil (PNG, JPG, osv.) som du vill bearbeta – för den här guiden använder vi `invoice.png`.  

Det är allt. Inga tunga beroenden, inga externa tjänster, bara ren Python.

![run OCR on image example showing a scanned invoice](/images/run-ocr-on-image.png)

*Alt text: run OCR on image example – skannad faktura som bearbetas*

## Steg 1 – Installera och importera OCR-biblioteket

Först och främst, låt oss få OCR‑motorn in i vår miljö och importera den. Om du använder det hypotetiska `ocrengine`‑paketet ser importen ut så här:

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**Why this matters:** Att importera rätt klass ger dig tillgång till de metoder vi kommer att anropa senare, som `setImageFromFile` och `recognize`. Om du hoppar över detta steg kommer Python att kasta ett `ModuleNotFoundError`, och du fastnar innan du ens har laddat en bild.

## Steg 2 – Skapa en OCR Engine-instans

Nu när biblioteket är redo behöver vi ett motorobjekt som håller konfigurationen och tillståndet för igenkänningsprocessen.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*Pro tip:* Vissa OCR‑motorer låter dig justera språkmodeller eller DPI‑inställningar i detta skede. För ett grundläggande **python OCR example** fungerar standardinställningarna bra, men om du arbetar med lågupplösta skanningar kan du överväga att justera dem här.

## Steg 3 – Ladda bilden du vill bearbeta

Det nästa logiska steget är att **load image for OCR**. Du pekar motorn på filsökvägen till PNG‑filen (eller något annat stödd format) som du vill analysera.

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**What’s happening under the hood?** Motorn läser pixeldata, konverterar den till ett format som igenkänningsalgoritmen kan förstå, och lagrar den internt. Om filsökvägen är fel får du ett `FileNotFoundError`, så dubbelkolla att bilden faktiskt finns.

## Steg 4 – Kör igenkänningsalgoritmen

Med bilden laddad kör vi äntligen **run OCR on image** för att extrahera det textuella innehållet.

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

## Steg 5 – Iterera över igenkända ord och visa förtroende

Den mest användbara delen av någon OCR‑arbetsflöde är att se **the confidence** för varje extraherat token. Det visar hur säker motorn är på varje ord, så att du kan filtrera bort lågt förtroenderesultat om så behövs.

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**Förväntad output** (exempel):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

Du kan nu exakt se **what words were extracted from the image** och hur pålitlig varje detektion är. Detta är kärnan i någon **extract words from image**‑pipeline.

## Hantera vanliga kantfall

### Vad händer om bilden är gråskala?

Vissa OCR‑motorer presterar bättre med färgbilder. Om du märker lågt förtroende över hela bilden, försök konvertera PNG‑filen till en högkontrast svart‑vit version innan du matar in den i motorn. Pillow kan hjälpa:

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### Hantera flera språk

Om ditt dokument innehåller både engelska och spanska vill du **recognize text from PNG** med en flerspråkig modell. De flesta motorer låter dig ange språklistan under initieringen:

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### Filtrera lågt förtroendeord

Ibland behöver du bara ord med ett förtroende över exempelvis 90 %. Ett snabbt filter ser ut så här:

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## Fullt, körklart skript

Genom att sätta ihop allt får du ett enda skript som du kan kopiera‑klistra in och köra direkt (byt bara ut sökvägen till din PNG).

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

Kör det med:

```bash
python run_ocr_on_image.py
```

Du bör se listan med ord och förtroendeprocent utskrivna i konsolen, exakt som tidigare visat.

## Vanliga frågor

**Fungerar detta med JPG‑ eller TIFF‑filer?**  
Absolut. `setImageFromFile`‑metoden accepterar alla format som det underliggande biblioteket kan avkoda, så du kan **run OCR on image**‑filer av typen JPG, TIFF, BMP, osv.

**Kan jag bearbeta flera bilder i en loop?**  
Självklart. Lägg in laddnings‑ och igenkänningsstegen i en `for`‑loop över en lista med filsökvägar. Kom bara ihåg att återinitiera motorn om biblioteket kräver en ny instans per bild.

**Vad om jag behöver texten i en enda sträng istället för per ord?**  
De flesta OCR‑resultatobjekt exponerar en `getText()`‑metod som returnerar hela dokumentet. Exempel:

```python
full_text = ocr_result.getText()
print(full_text)
```

## Nästa steg och relaterade ämnen

Nu när du vet hur du **run OCR on image**, överväg att utforska:

- **Post‑processing**: Använd reguljära uttryck för att rensa upp datum, belopp eller ID:n som extraherats från fakturor.  
- **Batch processing**: Kombinera skriptet med `os.listdir()` för att hantera hela mappar med skannade dokument.  
- **Alternative libraries**: `pytesseract` är ett populärt open‑source‑alternativ; arbetsflödet är liknande – byt bara ut motor‑anropen.  
- **Exporting results**: Skriv de extraherade orden och förtroendesiffrorna till CSV för vidare analys.

Varje av dessa utökningar bygger direkt på grunden vi lagt här, så att du kan omvandla rå OCR‑data till handlingsbar information.

---

### TL;DR

Vi har visat ett koncist, **python OCR example** som demonstrerar hur man **load image for OCR**, **run OCR on image**, och **extract words from image** samtidigt som man rapporterar förtroende. Det fullständiga skriptet är redo att köras, och du har nu kunskapen att anpassa det till vilket projekt som helst som behöver **recognize text from PNG** (eller andra format). Prova det, justera förtroendetrösklarna, och se dina applikationer bli text‑medvetna på några minuter. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}