---
category: general
date: 2026-03-26
description: Lär dig hur du kör OCR på arabiska PNG‑bilder och extraherar arabisk
  text snabbt. Den här guiden visar hur du konverterar bild till text med steg‑för‑steg
  Python‑kod.
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: sv
og_description: Hur kör man OCR på arabiska PNG‑bilder? Följ den här kompletta guiden
  för att extrahera arabisk text, känna igen arabisk text och konvertera bilden till
  text med Python.
og_title: Hur man kör OCR på arabisk PNG – Extrahera text från bild
tags:
- OCR
- Python
- Arabic
title: Hur man kör OCR på en arabisk PNG – Extrahera text från bild
url: /sv/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så kör du OCR på en arabisk PNG – Extrahera text från bild

Har du någonsin funderat **hur man kör OCR** på en bild som innehåller arabisk skrift? Kanske har du en skannad kvitto, ett historiskt manuskript eller bara en skärmdump av ett inlägg på sociala medier och du behöver texten i ett sökbart format. Du är inte ensam—utvecklare över hela världen stöter på detta problem när de hanterar språk som skrivs från höger till vänster.

I den här handledningen går vi igenom ett komplett, körbart exempel som visar **hur man kör OCR** på en PNG‑fil, extraherar arabisk text och skriver ut resultatet i konsolen. Inga vaga “se dokumentationen”-länkar; bara koden du kan kopiera‑klistra in, plus förklaringar till varför varje rad är viktig. I slutet kommer du kunna **konvertera bild till text** på ett pålitligt sätt, även när källan är en knepig arabisk PNG.

> **Vad du kommer att lära dig**
> - Installera en Python OCR‑motor för arabiska  
> - Ladda en PNG‑bild och hantera vanliga fallgropar  
> - Känna igen arabisk text och verifiera resultatet  
> - Tips för **extrahering av arabisk text** från olika bildkvaliteter  

Innan vi dyker ner, se till att du har Python 3.8+ installerat och en aktuell version av `ocr`‑biblioteket (det som används i kodsnutten). Om du använder en virtuell miljö, aktivera den nu—det håller beroenden organiserade.

## Förutsättningar

- Python 3.8 eller nyare  
- `ocr`‑paketet (`pip install ocr‑engine` – ersätt med det faktiska paketnamnet)  
- En arabisk PNG‑bild (`arabic_doc.png`) placerad någonstans du kan referera till  
- Grundläggande kunskap om Python‑funktioner och -klasser  

Det är allt. Inga tunga ramverk, inga Docker‑behållare—bara ren Python.

## Steg 1: Installera och importera OCR‑biblioteket

Först och främst. Vi behöver själva OCR‑motorn. Biblioteket vi använder exponerar en `OcrEngine`‑klass med ett enkelt API.

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*Varför importera `Imaging` separat?* `Imaging`‑undermodulen ger oss en bekväm `Image.load`‑metod som förstår PNG, JPEG och TIFF direkt. Att hoppa över detta steg skulle tvinga dig att hantera råa bytes själv, vilket är onödigt för de flesta användningsfall.

## Steg 2: Skapa OCR‑motorinstansen

Nu skapar vi en instans av motorn. Tänk på detta objekt som “hjärnan” som kommer att bearbeta bilden.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **Proffstips:** Om du planerar att bearbeta många bilder i rad, återanvänd samma `ocr_engine`‑instans. Den cachar språkmodeller, vilket snabbar upp efterföljande igenkänningar.

## Steg 3: Ställ in språket till arabiska

Arabiska är inte latin; det har sin egen teckenuppsättning, skrivs från höger till vänster och har kontextuell formning. Därför måste vi uttryckligen tala om för motorn vilken språkmodell som ska laddas.

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

Om du glömmer den här raden, använder motorn som standard engelska och du får förvrängd output—något jag har sett hända alldeles för ofta.

## Steg 4: Ladda din PNG‑bild

Här börjar delen **konvertera bild till text** på riktigt. Vi laddar PNG‑filen som innehåller den arabiska skriften.

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### Vanliga kantfall

| Issue | Symptom | Fix |
|-------|---------|-----|
| Bild är för mörk | Utdata innehåller många tomrum | Förbehandla med Pillow (`ImageEnhance.Brightness`) |
| PNG har en alfakanal | Vissa OCR‑motorer läser felaktigt transparenta pixlar | Konvertera till RGB (`image.convert("RGB")`) innan laddning |
| Text är roterad | Känd text är upp och ner | Rotera bilden (`image.rotate(90, expand=True)`) innan du skickar den till motorn |

## Steg 5: Kör igenkänningsprocessen

Med allt på plats ber vi nu motorn att utföra sitt jobb.

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

`recognize`‑metoden returnerar ett objekt som innehåller den råa Unicode‑strängen, förtroendesiffror och avgränsningsrutor. För de flesta utvecklare är ren text allt du behöver.

## Steg 6: Skriv ut den igenkända arabiska texten

Nu skriver vi ut resultatet. I en riktig applikation kan du skriva till en fil, en databas eller skicka den till ett översättnings‑API.

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

När du kör skriptet bör du se de arabiska tecknen i din konsol (se till att din terminal stödjer Unicode). Om du ser frågetecken eller tomma strängar, dubbelkolla språkinställningen och bildkvaliteten.

### Förväntad output

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

Om outputen liknar raden ovan, grattis—du har framgångsrikt **extraherat arabisk text** från en PNG!

## Fullt fungerande exempel

Nedan är hela skriptet, redo att kopiera‑klistra in. Ersätt `YOUR_DIRECTORY/arabic_doc.png` med sökvägen till din egen fil.

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

Kör det med `python run_ocr.py` (eller vad du nu har döpt filen till). Om allt är installerat korrekt kommer du se den arabiska meningen skriven i konsolen.

## Så kör du OCR på olika bildformat

Samma kod fungerar för JPEG, TIFF eller BMP—byt bara filändelsen. `Image.load`‑metoden upptäcker automatiskt formatet, så du kan **konvertera bild till text** utan extra kod.

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

Kom ihåg att källbildens kvalitet starkt påverkar noggrannheten i steget **igenkänna arabisk text**. Högupplösta, lågt komprimerade bilder ger bästa resultat.

## Extrahera text från PNG: Tips för bättre noggrannhet

1. **DPI är viktigt** – Sikta på minst 300 dpi. Lägre DPI leder ofta till missade tecken.  
2. **Kontrast är kung** – Använd bildbehandlingsverktyg (t.ex. OpenCV) för att öka kontrasten innan du matar bilden till OCR‑motorn.  
3. **Brusborttagning** – Små fläckar kan förvirra modellen; medianfiltrering hjälper.  

Här är ett snabbt kodexempel med Pillow för att förbättra en PNG innan OCR:

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

## Vanliga frågor

**Q: Fungerar detta med andra språk som skrivs från höger till vänster än arabiska?**  
A: Absolut. Byt bara språkkoden (`"ar"` → `"he"` för hebreiska, `"fa"` för persiska) så laddar motorn rätt modell.

**Q: Vad händer om jag behöver extrahera text från flera PNG‑filer i en mapp?**  
A: Loopa igenom filerna, återanvänd samma `ocr_engine`‑instans och samla resultaten i en lista eller skriv varje till en separat `.txt`‑fil.

**Q: Kan jag få förtroendesiffror för varje ord?**  
A: Ja. `ocr_result` exponerar ofta en `get_confidences()`‑metod. Para varje förtroendesiffra med motsvarande ord för kvalitetskontroll.

## Nästa steg

Nu när du vet **hur man kör OCR** på arabiska PNG‑filer, överväg dessa fortsättningsidéer:

- **Batch‑bearbetning:** Kombinera skriptet med `os.listdir` för att **extrahera arabisk text** från en hel katalog.  
- **Efterbehandling:** Använd `arabic_reshaper`‑ och `python-bidi`‑biblioteken för att korrekt visa höger‑till‑vänster‑output i PDF‑filer.  
- **Integration:** Mata den extraherade texten i ett sökindex (t.ex. Elasticsearch) för att göra skannade dokument sökbara.  

Var och en av dessa ämnen bygger på grunderna som täcks här, och de hjälper dig att förvandla ett enkelt **konvertera bild till text**‑skript till en produktionsklar pipeline.

---

![how to run OCR on Arabic PNG](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}