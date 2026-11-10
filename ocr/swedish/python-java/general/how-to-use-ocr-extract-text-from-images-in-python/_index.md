---
category: general
date: 2026-03-18
description: Hur man använder OCR för att extrahera text från bilder – en snabb guide
  för att känna igen text från PNG-filer och ladda bilder för OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: sv
og_description: Hur man använder OCR för att extrahera text från bilder – lär dig
  att känna igen text från PNG, ladda bild för OCR och extrahera text med ett enkelt
  Python‑skript.
og_title: 'Hur man använder OCR: Extrahera text från bilder i Python'
tags:
- OCR
- Python
- Image Processing
title: 'Hur man använder OCR: Extrahera text från bilder i Python'
url: /sv/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så använder du OCR: Extrahera text från bilder i Python

Har du någonsin undrat **hur man använder OCR** när du har en rörig skärmdump eller ett skannat kvitto? Du är inte ensam—utvecklare måste ständigt dra ut läsbar text från bilder, särskilt PNG-filer som kommer från mobilappar eller webbuppladdningar. I den här handledningen går vi igenom ett komplett, körbart exempel som visar hur du **extraherar text från bild**-filer, **läser text från PNG**-tillgångar, och till och med **läser in bild för OCR** med bara några rader Python.

Vi täcker allt från att installera rätt bibliotek till att hantera flerspråkiga dokument, så i slutet vet du exakt *hur du extraherar text* från vilken bild du än kastar på motorn. Inga vaga referenser, bara en klar, steg‑för‑steg‑lösning som du kan kopiera‑klistra och köra.

## Vad du kommer att lära dig

1. Ställ in en lättviktig OCR-motor (inga tunga beroenden krävs).  
2. Läs in en bildfil—specifikt en PNG—i motorn.  
3. Aktivera automatisk språkdetection så motorn kan hantera flerspråkigt innehåll.  
4. Kör igenkänningsprocessen och hämta resultatet som ren text.  
5. Justera arbetsflödet för kantfall som saknade filer eller format som inte stöds.

Om du är bekväm med grundläggande Python är du redo. Ingen tidigare OCR‑erfarenhet behövs, även om en snabb titt på bibliotekets dokumentation aldrig skadar.

![Hur man använder OCR på en PNG-bild](placeholder.png "Hur man använder OCR på en PNG-bild – steg‑för‑steg‑guide")

## Så använder du OCR – Läs in bild och läs av text {#how-to-use-ocr}

### Steg 1: Installera OCR‑biblioteket

Först och främst behöver du ett Python‑paket som tillhandahåller en `OcrEngine`‑klass. För den här handledningen använder vi det fiktiva men illustrativa **SimpleOCR**‑paketet, som du kan installera via pip:

```bash
pip install simple-ocr
```

**Proffstips:** Om du arbetar i en virtuell miljö (starkt rekommenderat), aktivera den innan du kör installationskommandot. Detta håller dina projektberoenden prydliga.

### Steg 2: Importera motorn och skapa en instans

Att skapa motorn är lika enkelt som att anropa dess konstruktor. Tänk på motorn som “hjärnan” som senare kommer att bearbeta bilden du matar in.

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

Varför skapar vi en ny instans varje gång? Isolering. En ny motor garanterar att ingen kvarvarande status från en tidigare körning förorenar den aktuella igenkänningen, vilket är avgörande när du bearbetar många filer i ett batch.

### Steg 3: Läs in bilden du vill bearbeta

Nu **läser vi faktiskt in bild för OCR**. Metoden `setImageFromFile` accepterar en sökväg till någon rasterbild; vi pekar den på en PNG som heter `mixed_doc.png`.

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

Om filen inte hittas kastar `SimpleOCR` ett tydligt `FileNotFoundError`. Du kan fånga det för att ge ett vänligt felmeddelande:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### Steg 4: Aktivera automatisk språkdetection

De flesta moderna OCR‑motorer levereras med språkpaket. Genom att skicka `"multilingual"` säger vi till motorn att sniffa texten och automatiskt välja rätt språkmodell. Detta är särskilt praktiskt när din PNG innehåller en blandning av engelska och spanska, till exempel.

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

Om du känner till språket i förväg kan du ersätta `"multilingual"` med en specifik lokalkod som `"eng"` eller `"spa"` för att snabba upp bearbetningen.

### Steg 5: Kör igenkänningsprocessen

Det tunga lyftet sker här. `recognize()` skannar bilden, tillämpar segmentering, kör det neurala nätverket och bygger internt en textbuffert.

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

Bakom kulisserna utför motorn:

- **Förbehandling** (räta upp, binarisering)  
- **Layoutanalys** (detektera kolumner, tabeller)  
- **Teckenklassificering** (med en djupinlärningsmodell)  

Allt detta är abstraherat bort, vilket är varför du bara behöver en rad.

### Steg 6: Hämta och skriv ut den igenkända texten

Till sist hämtar vi resultatobjektet och extraherar den rena strängen. Detta är delen där du faktiskt **extraherar text från bild**.

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**Förväntad output** (avkortad för korthet):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

Om bilden inte innehåller några igenkännbara tecken blir `text` en tom sträng. Du kan skydda mot det:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## Extrahera text från bild – Hantera vanliga kantfall

### Flera språk i en fil

När ett dokument blandar språk gör `"multilingual"`‑inställningen vanligtvis rätt. Men om du märker felaktiga igenkänningar kan du manuellt ange en reservlista:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### Icke‑PNG‑format

Även om vårt fokus är **läsa text från PNG**, accepterar `SimpleOCR` även JPEG, BMP och TIFF. Byt bara filändelsen i `setImageFromFile`. För TIFF‑stackar kan du behöva välja en specifik sida:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### Stora filer och minnesanvändning

Om du bearbetar gigapixel‑skanningar, överväg att ändra storlek innan OCR:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

Att ändra storlek minskar minnesbelastningen samtidigt som tillräcklig detalj bevaras för exakt igenkänning.

### Felsökning av misslyckade inläsningar

Ibland ser en bild bra ut för ögat men är korrupt internt. Aktivera utförlig loggning för att se vad motorn ser:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## Komplett, körklar skript

Nedan är det fullständiga programmet som sätter ihop alla delar. Kopiera det till en fil med namnet `ocr_demo.py`, justera platshållaren `YOUR_DIRECTORY`, och kör `python ocr_demo.py`.

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

Att köra detta skript bör skriva ut den rena textversionen av vad som än finns i `mixed_doc.png`. Känn dig fri att byta filen mot någon annan bild—**hur man extraherar text** fungerar på samma sätt.

---

## Slutsats

Vi har just gått igenom **hur man använder OCR** i Python för att **extrahera text från bild**‑filer, med särskilt fokus på **läsa text från PNG**‑tillgångar och de praktiska stegen för att **läsa in bild för OCR**. Kodsnutten ovan är en självständig lösning: installera paketet, mata in en fil, aktivera flerspråkig detection, kör motorn och hämta resultatet.

Härifrån kan du:

- Integrera skriptet i en webbtjänst som accepterar användaruppladdningar.  
- Batch‑processa en mapp med PDF‑filer konverterade till PNG.  
- Lägg till efterbehandling (t.ex. regex‑rengöring, stavningskontroll) för att förbättra noggrannheten.

Kom ihåg att OCR‑kvaliteten beror på bildens klarhet, rätt språkpaket och ibland lite förbehandling—så experimentera

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}