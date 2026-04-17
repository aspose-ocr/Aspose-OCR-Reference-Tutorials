---
category: general
date: 2026-03-26
description: Lär dig hur du utför OCR i Python och känner igen text från bildfiler.
  Den här guiden visar hur du extraherar text från PNG och snabbt konverterar bild
  till text.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: sv
og_description: Hur utför man OCR i Python? Följ den här guiden för att känna igen
  text från en bild, extrahera text från PNG och konvertera bild till text med en
  provlicens.
og_title: Hur man utför OCR i Python – Komplett handledning
tags:
- OCR
- Python
- Image Processing
title: Hur man utför OCR i Python – Komplett steg‑för‑steg‑handledning
url: /sv/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man utför OCR i Python – Komplett steg‑för‑steg‑handledning  

Har du någonsin undrat **hur man utför OCR** på en bild du just tagit med din telefon? Du är inte ensam—utvecklare överallt behöver ett pålitligt sätt att känna igen text från bildfiler utan att kämpa med komplexa inhemska bibliotek.  

I den här handledningen går vi igenom ett praktiskt exempel som visar **hur man utför OCR**, **recognize text from image**, och **extract text from PNG** med en lättviktig Python‑wrapper. I slutet kommer du kunna **convert image to text** på bara några kodrader, och du behöver inte oroa dig för licensproblem eftersom vi använder det inbyggda provläget.

## Vad du kommer att lära dig  

* Hur man ställer in en provlicens för OCR‑motorn (ingen filsökväg behövs).  
* Den exakta sekvensen av anrop för **recognize text from image**‑objekt.  
* Sätt att **extract text from PNG**‑filer och hantera vanliga fallgropar som saknade typsnitt.  
* Tips för att skala lösningen när du går från en provlicens till en produktionslicens.  

**Förutsättningar** – du behöver Python 3.8+ och paketet `ocr` (installerbart via `pip install ocr`). Inga andra externa verktyg krävs.

---  

![exempel på hur man utför OCR](https://example.com/ocr-demo.png "hur man utför OCR i Python – erkänd text visas")  

*Bildtext: hur man utför OCR i Python – exempelutdata*  

## Steg 1 – Aktivera en provlicens (Ingen filsökväg behövs)  

Innan motorn kan läsa något behöver den en giltig licens. Provläget är perfekt för experiment och små projekt.

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Varför detta är viktigt:* Licensobjektet talar om för OCR‑biblioteket att du kör i en sandlåda. Om du hoppar över detta steg kommer motorn att kasta ett `LicenseError` så snart du anropar `recognize()`.

**Proffstips:** När du går över till en betald licens, ersätt de två raderna ovan med `ocr.License("path/to/your/license.key").apply()`.

## Steg 2 – Skapa OCR‑motorns instans  

Nu när provläget är aktivt skapar vi huvudmotorn. Tänk på den som “hjärnan” som tittar på bilden och bestämmer vilka tecken som finns var.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Varför detta är viktigt:* `OcrEngine` innehåller konfiguration som språkpaket och DPI‑inställningar. Du kan justera dem senare, men standardinställningarna fungerar för de flesta PNG‑filer som bara innehåller engelska.

## Steg 3 – Ladda PNG‑filen du vill bearbeta  

Här är där vi **recognize text from image**. Metoden `ocr.Imaging.Image.load()` stöder PNG, JPEG, BMP och några andra format.

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Edge case:* Om din PNG använder en indexerad palett (vanligt för skärmbilder) kommer laddaren automatiskt att konvertera den till en 24‑bit RGB‑buffer. Den konverteringen kan ge en liten prestandapåverkan, men den garanterar korrekta OCR‑resultat.

## Steg 4 – Kör OCR och hämta texten  

Till sist ber vi motorn göra sitt och sedan hämta resultatet som ren text.

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Förväntad output** (exempel för en enkel bild som innehåller “Hello World”):

```
Hello World
```

Om bilden innehåller flera rader kommer output att bevara radbrytningar, vilket gör det enkelt att skicka vidare till processer som CSV‑tolkare eller NLP‑pipelines.

## Valfritt: Finjustering för bättre noggrannhet  

* **Språkpaket:** `ocr_engine.set_language("eng")` (standard) eller `"fra"` för franska.  
* **DPI‑skalning:** `ocr_engine.set_dpi(300)` kan förbättra resultat på lågupplösta skanningar.  
* **Förbehandling:** Att applicera ett binärt tröskelvärde (`ocr.Imaging.Image.threshold()`) före `set_image` ger ofta renare text på brusiga bakgrunder.  

Dessa justeringar är användbara när du går från en snabb demo till en produktionsklar **ocr tutorial python** som bearbetar hundratals filer per dag.

## Fullt skript – Klart att kopiera & klistra in  

Nedan är det kompletta, körbara skriptet som kombinerar alla stegen ovan. Spara det som `run_ocr.py` och ersätt `YOUR_DIRECTORY/sample1.png` med sökvägen till din egen PNG.

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

Kör det från kommandoraden:

```bash
python run_ocr.py
```

Du bör se den extraherade texten skrivas ut i konsolen. Om du får en tom sträng, dubbelkolla att bilden faktiskt innehåller tydlig, högkontrasttext och att provlicensen applicerades utan fel.

## Vanliga frågor & fallgropar  

* **“Fungerar detta med JPEG?”** – Absolut. Metoden `load()` upptäcker format automatiskt, så du kan byta PNG mot JPEG utan kodändringar.  
* **“Vad händer om bilden är roterad?”** – Motorn kan automatiskt upptäcka orientering, men för bästa resultat kan du förrotera med `input_image.rotate(90)` innan `set_image`.  
* **“Kan jag bearbeta flera bilder i en loop?”** – Ja. Flytta bara laddnings- och `recognize()`‑anropen in i en `for`‑loop; samma `ocr_engine`‑instans kan återanvändas, vilket sparar en liten mängd overhead.  

## Nästa steg – Från demo till produktion  

Nu när du vet **how to perform OCR**, överväg dessa uppföljningsteman:

* **Batch‑bearbetning** – Kombinera detta skript med `os.listdir()` för att **extract text from PNG**‑filer i bulk.  
* **Integrera med PDF** – Använd `pdf2image` för att konvertera PDF‑sidor till PNG och mata in dem i samma pipeline.  
* **Efterbehandling** – Använd regex eller fuzzy‑matching för att rensa vanliga OCR‑feligenkänningar (t.ex. “0” vs “O”).  

Var och en av dessa bygger på kärnidén **convert image to text** och utökar nytta av ditt OCR‑arbetsflöde.

---  

### TL;DR  

Vi har gått igenom allt du behöver veta för **how to perform OCR** i Python: aktivera en provlicens, skapa en motor, ladda en PNG, kör igenkänning och skriv ut resultatet. Med bara ett fåtal rader kan du **recognize text from image**, **extract text from PNG**, och **convert image to text** för vilken efterföljande applikation som helst.  

Prova det, justera DPI‑ eller språkinställningarna, och låt motorn göra det tunga arbetet. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}