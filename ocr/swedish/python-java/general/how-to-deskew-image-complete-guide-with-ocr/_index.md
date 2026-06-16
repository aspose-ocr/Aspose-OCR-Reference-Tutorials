---
category: general
date: 2026-03-26
description: Lär dig hur du räta upp en bild, känner igen text från en bild och bygger
  en bildförbehandlingspipeline för att ta bort brus från skanningen och konvertera
  den skannade bilden till text.
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: sv
og_description: Hur man räta upp en bild och omvandlar en snedskannad bild till sökbar
  text. Följ den här guiden för att känna igen text från en bild, ta bort brus från
  skanningen och konvertera den skannade bilden till text.
og_title: Hur man räta upp en bild – Steg‑för‑steg OCR‑guide
tags:
- OCR
- image-processing
- Python
title: Hur man räta upp en bild – Fullständig guide med OCR
url: /sv/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man räta upp en bild – Komplett guide med OCR

Har du någonsin undrat **hur man räta upp en bild** som kom från en billig skanner? Du är inte ensam. En sned sida ser oprofessionell ut, och viktigare, lutningen kan störa vilken OCR-motor som helst som försöker **läsa text från bild**.  

I den här handledningen går vi igenom en fullständig **image preprocessing pipeline** som räta upp, binariserar och avlägsnar brus från en skanning, och sedan skickar den till en OCR-motor så att du kan **konvertera skannad bild till text** med minimal möda. Ingen magi, bara ren Python och ett litet bibliotek som gör det tunga jobbet.

## Vad du behöver

- Python 3.9+ (koden fungerar på 3.10 och nyare)
- `ocr`‑paketet (installera via `pip install ocr‑toolkit` – byt ut mot ditt faktiska biblioteksnamn)
- En skannad JPEG eller PNG som är tydligt sned (t.ex. `skewed_scan.jpg`)
- Lite nyfikenhet på varför varje förbehandlingssteg är viktigt

Det är allt. Inga tunga beroenden som OpenCV om du inte vill gå djupare senare.

## Steg 1: Ladda den skannade bilden

Det första är att läsa in filen i minnet. Detta steg är enkelt men avgörande – om sökvägen är fel kraschar allt annat.

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **Why?**  
> Att ladda bilden ger oss ett manipulerbart objekt som `ocr.ImagePreprocessor` kan arbeta med. Att hoppa över detta steg skulle göra pipeline blind för den faktiska pixeldata.

## Hur man räta upp bilden och förbereder den för OCR

Nu när vi har bilden, låt oss räta upp den. Metoden `deskew()` uppskattar lutningsvinkeln och roterar bilden tillbaka till horisontell.

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **Pro tip:** Om dina skanningar bara är lite sneda (≤ 3°) är standardalgoritmen vanligtvis prick‑fri. För extrema vinklar kan du behöva justera de interna parametrarna – kolla bibliotekets dokumentation för `max_angle`.

## Binarisera bilden – Gör den svart‑vit

OCR‑motorer älskar högkontrast‑inmatning. Att konvertera bilden till en binär (svart‑vit) representation tar bort subtila nyanser som kan förvirra teckenigenkänning.

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **What’s happening?**  
> Pixlar ljusare än 128 blir vita; allt annat blir svart. Justera tröskelvärdet om din skanning är ovanligt mörk eller ljus.

## Ta bort brus från skanningen före OCR

Även en perfekt räta bild kan innehålla prickar, damm eller komprimeringsartefakter. De där små fläckarna är en plåga för varje OCR‑motor.

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **Why remove noise?**  
> Brus skapar falska kanter som OCR‑motorn kan tolka som tecken. En liten radie fungerar för de flesta skanningar; öka den för kraftigt korniga dokument.

## Använd bildförbehandlingspipeline

All konfiguration är klar – nu kör vi pipeline på originalbilden.

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **Result:** `processed_image` är en rensad, rak, högkontrast‑bitmap redo för textutvinning.

## Läs text från bild med OCR-motor

Dags att faktiskt läsa texten. Vi initierar OCR‑motorn, matar den med vår polerade bild och begär den råa strängen.

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Expected output** (sample):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Om du ser förvrängda tecken, dubbelkolla steg för att räta upp bilden eller experimentera med ett annat `threshold`‑värde.

## Bygga en bildförbehandlingspipeline – Fullt skript

När vi sätter ihop allt, här är ett enda körbart skript som du kan klistra in i en `.py`‑fil och köra:

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

> **Tip:** Packa in hela processen i en funktion (`def ocr_from_file(path): …`) om du planerar att bearbeta många filer i ett batch‑jobb.

## Vanliga frågor & kantfall

- **What if the image is already upright?**  
  `deskew()`‑metoden upptäcker en nästan nollvinkel och lämnar bilden orörd, så du kan säkert köra den på varje fil.

- **My scan is in color—should I keep it?**  
  Färg tillför inget värde för de flesta OCR‑uppgifter. Binarisering tar bort den, vilket snabbar upp bearbetning och minskar minnesanvändning.

- **Can I chain multiple preprocessing steps?**  
  Absolut. `ImagePreprocessor`‑klassen är designad för pipelines; du kan lägga till `sharpen()`, `contrast_enhance()` eller egna filter innan du anropar `apply()`.

- **The OCR output has stray line breaks—how to fix?**  
  Efterbehandla strängen med `text.replace("\n", " ").strip()` eller använd ett mer avancerat layout‑analysbibliotek som Tesseracts `--psm`‑lägen.

## Nästa steg

Nu när du vet **hur man räta upp en bild** och har en solid **image preprocessing pipeline**, kan du utforska:

- Integrera **recognize text from image** i ett Flask‑API för dokumentuppladdningar i realtid.
- Använda pipeline för att **remove noise from scan** av historiska dokument där bevarande är viktigt.
- Skala upp till batch‑bearbetning av tusentals sidor och skapa en sökbar PDF med `pdfminer` eller `PyMuPDF`.

Känn dig fri att experimentera med olika tröskelvärden, brusreduceringsradier eller till och med byta OCR‑backend till Tesseract om du behöver flerspråkigt stöd. Grundprinciperna är desamma: räta upp, rensa, sedan läs.

---

*Happy coding! If you run into trouble, drop a comment below—I'll be glad to help you fine‑tune the pipeline.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}