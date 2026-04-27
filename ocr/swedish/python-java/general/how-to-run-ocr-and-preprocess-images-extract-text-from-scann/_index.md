---
category: general
date: 2026-04-26
description: Hur man kör OCR på ett inskannat formulär, lär dig hur du förbehandlar
  bilden för att minska brus och extraherar text från bilden snabbt.
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: sv
og_description: Hur man kör OCR på skannade dokument, förbehandlar bilder, minskar
  brus och extraherar text effektivt.
og_title: Hur man kör OCR och förbehandlar bilder – Snabbguide
tags:
- OCR
- image processing
- Python
title: Hur man kör OCR och förbehandlar bilder – Extrahera text från skannade formulär
url: /sv/python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så kör du OCR – En komplett guide för att extrahera text från bilder

Har du någonsin undrat **hur man kör OCR** på ett rörigt inskannat formulär och får ren, sökbar text? Du är inte ensam. I många verkliga projekt är den råa bilden full av fläckar, ojämn belysning och andra egenheter som får standard‑OCR att snubbla.  

Den goda nyheten? Med bara några rader Python och en smart förbehandlings‑pipeline kan du dramatiskt öka igenkänningsnoggrannheten, **reducera brus**, och hämta exakt de ord du behöver. I den här handledningen går vi igenom varje steg—från att ladda bilden till att skriva ut den slutgiltiga strängen—så att du får ett färdigt kodexempel som du kan anpassa till fakturor, kvitton eller vilket inskannat dokument som helst.

## Vad du kommer att bygga

- En `OcrEngine`‑instans som kommunicerar med det underliggande OCR‑biblioteket.  
- En förbehandlingskedja som **binariserar** bilden och applicerar en **median‑blur** för att jämna ut fläckar.  
- Ett enkelt anrop till `process()` som returnerar ett objekt med egenskapen `text`, den extraherade strängen.  

När du är klar har du ett självständigt skript som du kan köra på vilken bildfil som helst och omedelbart se den extraherade texten i konsolen.

## Förutsättningar

- Python 3.9+ (syntaxen som används här matchar den senaste stabila versionen).  
- Det fiktiva paketet `aocr` – tänk på det som ett tunt omslag runt Tesseract eller någon modern OCR‑motor. Installera det med `pip install aocr`.  
- En inskannad bild (`scanned_form.jpg`) placerad i en mapp du kan referera till.  

Om du använder ett riktigt OCR‑bibliotek som `pytesseract` kan du byta ut `OcrEngine` mot den lämpliga klassen—allt annat förblir detsamma.

![](how-to-run-ocr-example.png "exempel på hur man kör OCR som visar ett inskannat formulär och extraherad text")

*Alt text: hur man kör OCR på ett inskannat dokument och visar den extraherade texten.*

---

## Steg 1: Så kör du OCR – Initiera motorn

Innan motorn kan läsa något måste vi skapa en instans. Tänk på `OcrEngine` som hjärnan som senare kommer att tolka den visuella datan.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **Varför detta är viktigt:** Att instansiera motorn sätter upp interna modeller, laddar språkpaket och förbereder körmiljön. Att hoppa över detta steg resulterar ofta i ett `NoneType`‑fel när du senare anropar `process()`.

---

## Steg 2: Så förbehandlar du bilden – Ladda ditt inskannade formulär

Nu när hjärnan är redo matar vi den med en bild. Bilden kan vara i vilket format som helst som stöds av `aocr.Image`.

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **Proffstips:** Använd absoluta sökvägar under utveckling för att undvika “fil ej hittad”-överraskningar när skriptet körs från en annan arbetskatalog.

---

## Steg 3: Så minskar du brus – Applicera binarisering & median‑blur

Råa skanningar innehåller ofta lösa prickar, ojämn bakgrund eller svaga skuggor. Två klassiska knep—**binarisering** och **median‑blur**—rengör bilden utan att förlora kanterna som definierar tecken.

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### Djupdykning

- **Binarisering**: Värdet `threshold=180` säger till algoritmen: “Allt som är ljusare än 180 blir vitt; allt annat blir svart.” Justera detta tal om din skanning är för mörk eller för ljus.  
- **Median‑blur**: En radie på `2` betyder att filtret tittar på ett 5×5‑pixelfönster och ersätter centrumpixeln med medianvärdet. Detta jämnar ut isolerade fläckar samtidigt som bokstavsstreck behålls.

> **Edge case:** Om ditt dokument har färgade markeringar kan ett enkelt binärt tröskelvärde radera dem. I så fall överväg att använda `aocr.ImageFilters.adaptive_threshold()` istället—det anpassar avgränsningen lokalt över bilden.

---

## Steg 4: Så extraherar du text – Kör OCR‑processen

Med en ren bild i handen låter vi nu motorn göra sin magi.

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **Vad händer under huven?** Motorn kör ett neuralt nätverk (eller en äldre mönstermatchare) över pixelmatrisen, översätter varje igenkänd glyf till Unicode‑tecken och sätter ihop dem till rader och stycken.

---

## Steg 5: Så extraherar du text – Skriv ut resultatet

`ocr_result`‑objektet har en bekväm `text`‑attribut. Låt oss se vad vi fick.

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### Förväntad utskrift

Om det inskannade formuläret innehåller:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Du bör se något liknande:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Lägg märke till hur förbehandlingssteget eliminerade lösa prickar som tidigare gjorde att “Amount” blev “Am0unt”. Det är kraften i **hur man minskar brus** innan OCR.

## Vanliga fallgropar & hur du åtgärdar dem

| Symptom | Trolig orsak | Snabb åtgärd |
|---------|--------------|--------------|
| Otydliga tecken (t.ex. “@#%”) | Bilden är för mörk eller för ljus | Justera `threshold` i `binarize()`; prova `adaptive_threshold`. |
| Saknade ord | Bruset är fortfarande närvarande | Öka `radius` för `median_blur` eller lägg till ett `gaussian_blur`‑filter. |
| Fel språk (t.ex. engelska bokstäver blir kinesiska) | Fel språkpaket laddat | Skicka `language="eng"` när du skapar `OcrEngine()` om biblioteket stödjer det. |
| Långsam bearbetning på stora filer | Hög upplösning | Skala ner bilden först: `aocr.ImageFilters.resize(width=1200)` före binarisering. |

## Gå vidare – Nästa steg och relaterade ämnen

- **Batch‑behandling**: Packa in logiken i en loop för att automatiskt hantera dussintals filer.  
- **Strukturerad output**: Använd reguljära uttryck på `ocr_result.text` för att plocka ut fält som datum eller belopp.  
- **Alternativa bibliotek**: Byt ut `aocr` mot `pytesseract`—koden ändras bara i steget för motorinitialisering.  
- **Hur man förbehandlar bild för PDF‑filer**: Konvertera varje PDF‑sida till en bild och applicera sedan samma pipeline.  

Dessa tillägg låter dig skala lösningen från ett enstaka formulär till en företagsklassad dokument‑intagspipeline.

## Slutsats

Vi har gått igenom **hur man kör OCR** från början till slut, visat **hur man förbehandlar bild** för att **reducera brus**, och demonstrerat **hur man extraherar text från bild** med ett rent, reproducerbart skript. Huvudpoängen? Några enkla filter—binarisering och median‑blur—kan förvandla en brusig skanning till en pålitlig datakälla, vilket sparar dig timmar av manuellt arbete.

Kör skriptet med dina egna dokument, justera tröskelvärdena och se noggrannheten öka. När du är redo, utforska batch‑behandling eller integrera resultatet i en databas för sökbara arkiv. Lycka till med kodandet, och må din OCR alltid vara prickfri!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}