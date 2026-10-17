---
category: general
date: 2026-06-25
description: Hur man använder OCR i Python – lär dig hur du laddar en bild för OCR,
  känner igen text i ett område och extraherar områdestext snabbt.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: sv
og_description: Hur man använder OCR i Python – steg‑för‑steg‑guide för att ladda
  en bild, känna igen text i ett specifikt område och extrahera fakturanumret.
og_title: 'Hur man använder OCR Python: Ladda bild och extrahera regiontext'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'Hur man använder OCR i Python: Ladda bild och extrahera regiontext'
url: /sv/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder OCR Python: Ladda bild och extrahera regiontext

**How to use OCR in Python** är enklare än du tror. Har du någonsin stirrat på en skannad faktura och undrat hur du kan hämta bara fakturanumret utan att parsra hela sidan? Du är inte ensam—många utvecklare stöter på det problemet när de först leker med optisk teckenigenkänning. I den här guiden går vi igenom att ladda en bild för OCR, definiera en rektangel, känna igen text i den regionen och slutligen extrahera regiontexten. I slutet har du ett färdigt skript som isolerar vilken textbit du än behöver.

> *Pro tip:* Om du arbetar med PDF‑filer, konvertera varje sida till en bild först—de flesta OCR‑bibliotek hanterar PNG/JPEG bäst.

## Vad du behöver

- Python 3.8+ (den senaste stabila versionen rekommenderas)  
- Ett OCR‑bibliotek som exponerar en `OcrEngine`‑klass (t.ex. **ocr** från `pip install ocr-lib`)  
- En exempelbild—här använder vi `invoice.png` placerad i en mapp du kontrollerar  
- Grundläggande kunskap om rektanglar (x, y, bredd, höjd)  

Inga tunga beroenden, inget GPU‑krav—bara vanlig CPU‑arbete, vilket gör det portabelt.

---

## Så här använder du OCR: Initiera motorn (Steg 1)

Innan någon text kan läsas behöver du en OCR‑motorinstans. Tänk på den som hjärnan som analyserar pixelmönster.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Varför detta är viktigt:* Initiering av motorn laddar språkmodeller och sätter standardkonfigurationer. Att hoppa över detta steg skulle kasta ett undantag så snart du anropar `recognize_region`.

## Ladda bild för OCR (Steg 2)

Nu när motorn är klar, matar vi den med en bild. Bibliotekets `Image.load`‑metod hanterar vanliga format och normaliserar bitmapen.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

Om filen inte hittas kommer Python att kasta ett `FileNotFoundError`. Se till att sökvägen är absolut eller relativ till ditt skripts arbetskatalog.  

*Edge case:* Vissa OCR‑motorer förväntar sig en gråskalebild. Om du märker låg noggrannhet, konvertera bilden först:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## Känn igen text i region (Steg 3)

Att definiera regionen är där du talar om för motorn *var* den ska titta. `Rectangle` tar flyttalsvärden för sub‑pixel‑precision, vilket kan vara praktiskt när du hanterar högupplösta skanningar.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – övre vänstra hörnet av rektangeln (i pixlar)  
- **width, height** – storleken på rutan  

Du kanske undrar hur du hittar dessa siffror. Ett snabbt sätt är att öppna bilden i någon redigerare (t.ex. GIMP eller Paint.NET) och använda markeringsverktyget för att läsa av koordinaterna.  

*Varför inte bara OCR:a hela sidan?* Att begränsa området minskar brus, snabbar upp bearbetningen och förbättrar avsevärt noggrannheten för små fält som fakturanummer.

---

## Så här extraherar du regiontext (Steg 4)

När regionen är satt, be motorn att känna igen bara den delen. Resultatobjektet innehåller råtexten och förtroendesiffrorna.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

Om OCR‑motorn stödjer flera språk kan du skicka en valfri språkkod:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*Vanligt fallgropp:* Vissa motorer returnerar en lista med ord istället för en enda sträng. I sådana fall, slå ihop dem:

```python
text = " ".join(region_result.words)
```

---

## Skriv ut det extraherade fakturanumret (Steg 5)

Till sist, skriv ut—eller spara—den extraherade texten. Du kan också efterbehandla strängen för att ta bort oönskade mellanslag eller icke‑numeriska tecken.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

Att köra skriptet med en korrekt justerad rektangel bör ge något i stil med:

```
Invoice number: 20231578
```

Om du får skräptecken, dubbelkolla rektangelkoordinaterna eller överväg att öka bildens upplösning.

---

## Fullt fungerande exempel

Sätter vi ihop allt, här är ett självständigt skript du kan kopiera‑klistra in och köra:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

Spara filen som `extract_invoice.py`, ersätt `YOUR_DIRECTORY` med den faktiska mappen, och kör:

```bash
python extract_invoice.py
```

Du bör se fakturanumret skrivet i konsolen.

---

## Vanliga frågor

**Q: Vad händer om fakturanumret är tryckt i ett fancy typsnitt?**  
A: De flesta moderna OCR‑motorer hanterar ett brett spektrum av typsnitt, men du kan öka noggrannheten genom att träna en anpassad språkmodell eller förbehandla bilden (t.ex. applicera ett tröskelfilter).

**Q: Kan jag extrahera flera fält samtidigt?**  
A: Absolut. Definiera en lista med `Rectangle`‑objekt—ett per fält—och loopa över dem, lagra varje resultat i en ordbok.

**Q: Fungerar detta på flersidiga PDF‑filer?**  
A: Konvertera varje sida till en bild först (med `pdf2image` eller liknande), och tillämpa sedan samma regionbaserade extraktion per sida.

---

## Avslutning

I den här handledningen gick vi igenom **hur man använder OCR** i Python för att ladda en bild, känna igen text i en specifik region och extrahera regionens text—perfekt för att hämta fakturanummer, order‑ID eller någon liten databit från skannade dokument. Genom att isolera intresseområdet får du snabbare, mer exakt och mindre efterbehandlingsarbete.

Redo för nästa steg? Prova att utöka skriptet för att hantera **load image for OCR** från en mapp med batch‑fakturor, eller experimentera med **recognize text in region** för olika fält som datum och totalsummor. Samma mönster gäller—byt bara rektangelkoordinaterna.

Om du stötte på problem eller har idéer för förbättringar, lämna en kommentar nedan. Lycka till med kodandet, och må dina OCR‑pipelines alltid vara korrekta!

## Vad du bör lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Extrahera text från bild med Aspose OCR – Steg‑för‑steg‑guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Hur man extraherar text från bild genom att förbereda rektanglar i OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Hur man använder AspOCR: Förbehandla bild‑OCR‑filter för .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}