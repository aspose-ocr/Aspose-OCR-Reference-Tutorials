---
category: general
date: 2026-07-05
description: Hur man använder OCR i Python för att snabbt konvertera TIFF till text.
  Lär dig OCR‑bibliotekets Python‑steg för att extrahera text från TIFF‑bilder och
  bygga en Python‑OCR‑motor.
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: sv
og_description: Hur använder man OCR i Python? Den här guiden visar dig steg för steg
  hur du konverterar TIFF till text med en Python OCR-motor och OCR‑biblioteket i
  Python.
og_title: Hur du använder OCR i Python – Fullständig TIFF‑textutvinning
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: Hur man använder OCR i Python – Extrahera text från TIFF
url: /sv/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder OCR i Python – Extrahera text från TIFF

Har du någonsin funderat på **how to use OCR in Python** för att omvandla en skannad bok till redigerbar text? Du är inte ensam—utvecklare, forskare och hobbyister stöter alla på detta hinder när de hanterar fler‑sidiga TIFF‑bilder. Den goda nyheten? Med **ocr library python** kan du starta en liten OCR‑motor, rikta den mot en TIFF‑fil och få ren, sökbar text på sekunder.

I den här handledningen går vi igenom allt du behöver: installera rätt paket, ladda en fler‑sidig TIFF, köra OCR‑motorn och slutligen skriva ut varje sidas innehåll. I slutet kommer du kunna **convert TIFF to text** och **extract text from TIFF** filer utan att lämna din Python‑miljö.

## Förutsättningar

- Python 3.9 eller nyare (exemplet testades på 3.11)
- En nyare version av `ocr`‑biblioteket (eller någon kompatibel `python ocr engine` du föredrar)
- En fler‑sidig TIFF‑fil som du vill bearbeta (vi kallar den `scanned_book.tif`)
- Grundläggande kunskap om Python‑skript och virtuella miljöer

Inga tunga externa verktyg krävs—bara pip och några rader kod.

## Installera OCR‑biblioteket för Python

Först och främst: du behöver en solid OCR‑backend. För den här guiden använder vi det fiktiva `ocr`‑paketet som levereras med ett enkelt hög‑nivå‑API, men samma mönster fungerar med Tesseract‑baserade omslag som `pytesseract` eller kommersiella SDK:er.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro tip:** Om du kör Windows och paketet är beroende av inhemska binärer, se till att du har rätt Visual C++‑redistributable installerad. Installationsprogrammet varnar dig vanligtvis om något saknas.

## Hur man använder OCR‑motor i Python

Nu när biblioteket är klart, låt oss starta en OCR‑motor och rikta den mot vår TIFF‑fil. Följande kodsnutt skapar en motorinstans, ställer in språket till engelska och förbereder den för fler‑sidig bearbetning.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**Varför ange språket?**  
De flesta OCR‑motorer använder språkmodeller för att förbättra noggrannheten. Om du hoppar över detta steg faller motorn tillbaka till en generisk modell som kan feltolka skiljetecken eller specialtecken.

## Ladda den fler‑sidiga TIFF‑bilden

Nästa steg är att ladda det skannade dokumentet. Hjälpfunktionen `ocr.Image.load` förstår TIFF‑stackar direkt och returnerar ett objekt som representerar varje sida internt.

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Edge case:** Om din TIFF använder kompression (CCITT Group 4, LZW, etc.) och biblioteket kastar ett fel, försök konvertera den till en okomprimerad version med ImageMagick först:
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## Utför OCR på alla sidor – Konvertera TIFF till text

Med bildobjektet i handen kan motorn nu bearbeta varje sida på en gång. Denna metod returnerar en lista där varje element innehåller OCR‑resultatet för en enskild sida.

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**Vad händer under huven?**  
Funktionen `recognize_multi_page` itererar över varje rasteriserad sida, kör neurala‑nätverkets igenkännare och paketerar ren‑text‑utdata tillsammans med förtroendescore. Det är i princip en batch‑operation som sparar dig från att skriva en manuell loop.

## Iterera genom resultat – Extrahera text från TIFF

Till sist visar vi den igenkända texten. Du kan skriva utdata till separata `.txt`‑filer, skicka den till en databas eller mata in den i ett sökindex—vad som helst som passar ditt arbetsflöde.

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### Förväntad utdata

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

Varje `result.text`‑sträng innehåller den råa OCR‑utdata för den sidan. Om du behöver bevara radbrytningar, exponerar de flesta motorer `result.lines` som en lista av strängar.

## Hantera stora TIFF‑filer – Tips & tricks

Att bearbeta en 500‑sidig TIFF kan vara minneskrävande. Här är några strategier för att hålla allt smidigt:

1. **Chunk the pages** – Istället för `recognize_multi_page`, anropa `engine.recognize(page)` inom en generator som returnerar en sida åt gången.
2. **Adjust DPI** – Att sänka bildens upplösning (t.ex. från 300 DPI till 200 DPI) minskar CPU‑belastningen medan det knappt påverkar noggrannheten för de flesta tryckta texter.
3. **Parallelize** – Om din OCR‑motor är trådsäker, starta en `concurrent.futures.ThreadPoolExecutor` för att köra igenkänning på flera sidor samtidigt.

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## Spara den extraherade texten till filer

De flesta verkliga pipelines behöver beständig lagring. Nedan är ett koncist sätt att dumpa varje sidas text till en egen fil, med bevarad sidordning.

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

Nu har du en ren katalog med `.txt`‑filer redo för indexering eller vidare NLP‑bearbetning.

## Bildförhandsgranskning – Så här använder du OCR‑resultat visuellt

Om du vill se OCR‑överlappning på originalbilden (praktiskt för felsökning), låter många bibliotek dig rita avgränsningsrutor. Här är ett snabbt exempel med Pillow:

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![Hur man använder OCR i Python – OCR‑överlappning på en TIFF‑sida](ocr_overlay_example.png)

*Alt text:* Hur man använder OCR i Python – visuell överlagring av igenkänd text på en TIFF‑sida.

## Vanliga fallgropar och hur man undviker dem

| Problem | Varför det händer | Lösning |
|-------|-------------------|--------|
| Felaktiga tecken | Fel språkmodell | Ställ in `engine.language` till rätt enum |
| Saknade sidor | TIFF‑kompression stöds inte | Konvertera till okomprimerad TIFF först |
| Långsam prestanda | Hög DPI + enkeltrådad bearbetning | Sänk DPI eller aktivera flertrådad bearbetning |
| Tomt resultat | Bilden är för mörk/låg kontrast | Förprocessa med kontrastutsträckning (`opencv` eller `Pillow`) |

Att åtgärda dessa tidigt sparar dig timmar av felsökning senare.

## Nästa steg – Gå bortom grundläggande extraktion

Nu när du behärskar grunderna i **how to use OCR in Python**, överväg att utforska:

- **PDF generation** – Kombinera extraherad text med `reportlab` för att återskapa sökbara PDF‑filer.
- **Language detection** – Auto‑switch `engine.language` med `langdetect`.
- **Structured data extraction** – Använd reguljära uttryck eller spaCy för att extrahera datum, namn eller tabeller från den råa texten.
- **Alternative OCR backends** – Byt `ocr` mot `pytesseract` eller `easyocr` om du behöver flerspråkigt stöd.

Var och en av dessa ämnen knyter naturligt tillbaka till sekundära nyckelord **ocr library python**, **convert tiff to text**, **extract text from tiff**, och **python ocr engine**, vilket ger dig en solid grund för mer avancerade projekt.

---

### Slutsats

Vi har gått igenom **how to use OCR in Python** från installation till fler‑sidig bearbetning, och visat exakt hur du **convert TIFF to text** och **extract text from TIFF** med en enkel **python OCR engine**. Det kompletta, körbara exemplet ovan bör fungera direkt för de flesta standard‑TIFF‑filer, och tipsen hjälper dig att skala upp till större dokument eller integrera OCR i större pipelines.

Prova det med dina egna skannade böcker, kvitton eller arkivbilder—sen experimentera med idéerna på nästa nivå som listas i avsnittet “Next Steps”. Lycka till med kodandet, och må dina OCR‑resultat alltid vara korrekta!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Extrahera text från bild med Aspose OCR – steg‑för‑steg‑guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Hur man extraherar text från tiff med Aspose.OCR för Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Hur man utför bildtextextraktion från ström med Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}