---
category: general
date: 2026-04-26
description: Hur man skapar OCR snabbt och pålitligt. Lär dig att extrahera text från
  bild, ladda bild för OCR och köra OCR på PNG med en anpassad ordlista.
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: sv
og_description: Hur man skapar OCR i Python och extraherar text från en bild. Denna
  guide visar hur man laddar en bild för OCR, kör OCR på PNG och använder en anpassad
  ordlista.
og_title: Hur man skapar OCR i Python – Snabb textutvinning
tags:
- OCR
- Python
- Image Processing
title: Hur man skapar OCR i Python – Extrahera text från bild
url: /sv/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar OCR i Python – Steg‑för‑steg‑guide

Har du någonsin undrat **hur man skapar OCR** som kan läsa dina skannade PDF‑filer, skärmbilder eller handskrivna anteckningar? Du är inte ensam. I många verkliga projekt behöver vi *extrahera text från bild*‑filer, men de färdiga motorerna har ofta problem med domänspecifika ord.

I den här handledningen kommer du att se ett komplett, körbart exempel som laddar en bild för OCR, använder en anpassad ordlista och slutligen **kör OCR på PNG**‑filer. I slutet kommer du att kunna extrahera text från vilken bild som helst och anpassa motorn till din egen terminologi.

## Vad den här handledningen täcker

* Installera det lilla men kraftfulla `aocr`‑paketet (eller något kompatibelt bibliotek).  
* Konfigurera en **anpassad ordlista** så att termer som `aspocorp` eller `licensekey` känns igen.  
* **Ladda en bild för OCR**, oavsett om det är en PNG, JPEG eller en skannad PDF‑sida.  
* Köra OCR‑processen och skriva ut resultatet.

Inga externa dokumentationslänkar, bara en självständig lösning som du kan kopiera‑klistra in och köra idag.

### Förutsättningar

* Python 3.8 eller nyare (koden använder f‑strängar).  
* Grundläggande kunskap om kommandoraden – du kommer att skriva några `pip install`‑kommandon.  
* En bildfil (`technical_doc.png` i exemplet) placerad någonstans du kan referera till.

Om du uppfyller dessa tre punkter är du redo att köra.

---

## Steg 1: Installera OCR‑biblioteket

Först behöver vi en OCR‑motor som stöder ett programmerbart konfigurationsobjekt. `aocr`‑paketet är ett lättvikts‑wrapper runt en inbyggd OCR‑motor och fungerar bra för demonstrationer.

```bash
# Install the library (run once)
pip install aocr
```

> **Proffstips:** Om du är på Windows och får ett kompileringsfel, prova `pip install aocr‑binary` som levereras med förbyggda wheels.

### Varför installera detta bibliotek?

`aocr` ger oss direkt åtkomst till ett `config`‑objekt där vi kan injicera en **anpassad ordlista**. Det är den hemliga ingrediensen för att förbättra noggrannheten på nischade vokabulärer.

---

## Steg 2: Skapa OCR‑motorinstansen och lägg till en anpassad ordlista

Nu startar vi motorn och talar om vilka ord den ska behandla som kända.

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### Varför en anpassad ordlista är viktig

Standard‑OCR‑modeller är tränade på generiska korpusar. När modellen ser “aspocorp” kan den dela upp det till “aspo corp” eller helt enkelt släppa bokstäver. Genom att mata in en anpassad lista, biasar vi igenkänningaren mot den exakta stavningen vi behöver, vilket dramatiskt minskar efterbearbetningsarbetet.

---

## Steg 3: Ladda bilden du vill bearbeta

Här är där vi **laddar bild för OCR**. Metoden `Image.load` accepterar en sökvägssträng och bestämmer automatiskt filtypen.

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **Edge case:** Om din källa är en flersidig PDF, konvertera varje sida till PNG först (t.ex. med `pdf2image`) och mata in dem en‑och‑en till motorn.

### Tips för bättre bildkvalitet

* Håll upplösningen på minst 300 dpi.  
* Säkerställ att bilden är rätt orienterad; rotera med `Pillow` om nödvändigt.  
* Konvertera färgade skanningar till gråskala för att minska brus.

---

## Steg 4: Kör OCR‑processen på PNG‑filen

Med motorn konfigurerad och bilden laddad, kör vi slutligen **OCR på PNG**.

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

`process()`‑anropet returnerar ett objekt som innehåller den igenkända texten, förtroendescore och avgränsningsrutor för varje ord.

---

## Steg 5: Skriv ut den igenkända texten

Det enklaste sättet att se vad motorn hittade är att skriva ut `text`‑attributet.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Förväntad utskrift

Om `technical_doc.png` innehåller meningen *“The Aspocorp licensekey expires on 2025‑12‑31.”*, bör konsolen visa:

```
The Aspocorp licensekey expires on 2025-12-31.
```

Observera hur den anpassade ordlistan behöll varumärkesnamnet intakt – något som en vanlig OCR kan ha förvrängt.

---

## Fullt fungerande exempel (klart att kopiera‑klistra in)

Nedan är hela skriptet, redo att sparas som `run_ocr.py`. Byt bara ut platshållarens sökväg mot platsen för din bild.

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Kör det från terminalen:

```bash
python run_ocr.py
```

Du bör se den extraherade texten skriven till konsolen, exakt som i det tidigare exemplet.

---

## Vanliga frågor (FAQ)

| Question | Answer |
|----------|--------|
| **Kan jag extrahera text från en skannad PDF?** | Ja. Konvertera varje sida till PNG (eller TIFF) först, och mata sedan in bilderna till samma skript. |
| **Vad händer om min bild är en JPEG istället för PNG?** | Metoden `Image.load` stöder JPEG, BMP, TIFF och PNG direkt. Byt bara filändelsen. |
| **Hur förbättrar jag noggrannheten på lågkontrastskanningar?** | Förprocessa med `Pillow` – öka kontrasten, applicera binarisering, eller använd `opencv` för att räta upp bilden. |
| **Finns det ett sätt att få förtroendescore för varje ord?** | `ocr_result` innehåller `words` – varje ord har ett `confidence`‑attribut som du kan iterera över. |
| **Kan jag köra detta på en huvudlös server?** | Absolut. `aocr` har inga GUI‑beroenden, vilket gör det perfekt för CI‑pipelines. |

---

## Nästa steg & relaterade ämnen

Nu när du vet **hur man skapar OCR** och **extraherar text från bild**‑filer, överväg att utforska:

* **Förprocessningstekniker** – `load image for OCR` är bara första steget; använd `opencv` för att avbrusa eller skärpa.  
* **Batch‑bearbetning** – loopa över en katalog med PNG‑filer för att skapa ett sökbart arkiv.  
* **Flerspråkigt stöd** – lägg till språkpaket till motorn om du behöver läsa franska eller tyska dokument.  
* **Integrering med Elasticsearch** – indexera den extraherade texten för fulltextsökning över skannade tillgångar.

Var och en av dessa tillägg bygger på det grundmönster vi just gått igenom, så du kommer att finna övergången smidig.

---

## Sammanfattning

På några minuter har vi besvarat **hur man skapar OCR** som pålitligt **extraherar text från bild**‑filer, särskilt PNG‑filer, och vi har visat dig hur du **laddar bild för OCR**, använder en **anpassad ordlista**, och **kör OCR på PNG** utan några externa tjänster.

Kör skriptet, justera ordlistan för att matcha ditt eget fackspråk, så har du en solid grund för alla dokument‑digitaliseringsprojekt.

Om du stöter på problem, lämna en kommentar nedan—vi hjälper gärna till. Och glöm inte att dela dina framgångshistorier; gemenskapen lär sig bäst av verkliga exempel.

**Redo att automatisera ditt pappersarbete?** Hämta koden, anpassa den, och börja omvandla pixlar till sökbar text redan idag!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}