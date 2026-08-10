---
category: general
date: 2026-06-16
description: Extrahera text från TIFF‑filer med Python OCR. Lär dig hur du konverterar
  TIFF till text steg för steg och hanterar flersidiga dokument med lätthet.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: sv
og_description: Extrahera text från TIFF‑filer med Python OCR. Följ den här guiden
  för att konvertera TIFF till text, hantera flersidiga skanningar och få rena resultat.
og_title: Extrahera text från TIFF – komplett Python‑guide
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: Extrahera text från TIFF – Komplett Python‑guide
url: /sv/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från TIFF – Komplett Python‑guide

Har du någonsin behövt **extrahera text från TIFF**‑bilder men varit osäker på var du ska börja? Du är inte ensam—många utvecklare stöter på detta problem när de hanterar skannade arkiv eller äldre dokument. Den goda nyheten? Med några rader Python kan du **konvertera TIFF till text** på ett ögonblick, även när filen innehåller dussintals sidor.

I den här handledningen går vi igenom ett verkligt exempel: att läsa in en flersidig TIFF, ställa in OCR‑språket till franska och hämta den igenkända texten från varje sida. I slutet har du ett färdigt skript, förstår varför varje steg är viktigt och vet hur du kan anpassa det för andra språk eller bildformat.

## Förutsättningar

- Python 3.8 eller nyare installerat.
- `ocr`‑paketet (eller något kompatibelt OCR‑bibliotek som erbjuder en `OcrEngine`‑klass). Du kan installera det med `pip install ocr-lib`—byt ut mot det faktiska paketnamnet du använder.
- En flersidig TIFF‑fil (t.ex. `french-scans.tif`) som du vill bearbeta.
- Grundläggande kunskap om Python‑skriptning.

Inga tunga beroenden, inga externa tjänster—bara ren Python och en OCR‑motor.

---

## Steg 1: Ställ in OCR‑motorn för att **extrahera text från TIFF**

Först och främst—vi behöver en OCR‑motorinstans och vi måste tala om för den vilket språk som ska användas. I vårt fall är källmaterialet franska, så vi ställer in språket därefter.

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**Varför detta är viktigt:**  
Språkinställningen förbättrar noggrannheten avsevärt. Franska tecken som “é” eller “ç” skulle läsas fel som generiska symboler om motorn använder engelska som standard. Genom att explicit välja franska ger vi motorn rätt teckenkarta.

> **Proffstips:** Om du bearbetar dokument på flera språk kan du ändra `engine.language` i farten innan varje `recognize()`‑anrop.

---

## Steg 2: Läs in den flersidiga TIFF‑filen du vill **konvertera TIFF till text**

En TIFF kan innehålla flera ramar—tänk på varje ram som en separat sida. OCR‑biblioteket abstraherar detta åt oss, så vi pekar helt enkelt på filen.

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**Varning för kantfall:**  
Om filvägen är felaktig eller TIFF‑filen är korrupt, kommer `load_from_file`‑metoden att kasta ett undantag. Omge den med ett `try/except`‑block för produktionskod:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## Steg 3: Kör OCR på hela dokumentet – Kärnan i **extrahera text från TIFF**

Nu låter vi motorn göra sin magi. `recognize()`‑anropet bearbetar varje sida på en gång och returnerar ett rikt resultatobjekt.

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**Vad händer under huven?**  
Motorn itererar över varje ram, tillämpar förbehandling (räta upp, binarisering), kör det neurala nätverket och samlar ihop resultatet. Eftersom vi anropade `recognize()` bara en gång kan biblioteket dela resurser mellan sidor, vilket är snabbare än att loopa manuellt.

---

## Steg 4: Hämta den igenkända texten från JSON‑resultatet – **konvertera TIFF till text** sida för sida

Resultatobjektet kan serialiseras till JSON. Inuti den JSON‑en hittar du en `pages`‑array, där varje element innehåller ett `text`‑fält.

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

Nu har vi en ren Python‑lista där varje element motsvarar en sidas OCR‑utdata.

---

## Steg 5: Skriv ut eller spara texten för varje sida – den sista delen av **extrahera text från TIFF**

Låt oss loopa igenom sidorna och visa den extraherade texten. Du kan också skriva varje sida till en separat `.txt`‑fil om du föredrar.

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### Förväntad utdata (exempel)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

Om OCR lyckas kommer du att se ett rent block med franska meningar för varje sida. Om du märker förvrängda tecken, dubbelkolla språkinställningen eller överväg att öka bildens upplösning innan OCR.

---

## Hantera vanliga fallgropar när du **konverterar TIFF till text**

| Problem | Varför det händer | Snabb lösning |
|-------|----------------|-----------|
| **Tom `pages`‑array** | TIFF‑filen laddades inte korrekt eller har noll ramar. | Verifiera filvägen och säkerställ att TIFF‑filen inte är en enkel‑sidig PNG som maskeras som TIFF. |
| **Skräptecken** | Språkfel eller låg bildkvalitet. | Ställ in rätt `engine.language` och förbehandla bilden (t.ex. öka DPI). |
| **Minnesökning på stora TIFF‑filer** | Att ladda alla sidor på en gång förbrukar RAM. | Bearbeta i delar: ladda en enskild ram, kör OCR, släpp sedan innan du går vidare till nästa. |
| **Unicode‑fel vid utskrift** | Konsolens kodning stödjer inte accentuerade tecken. | Använd `print(page["text"].encode('utf-8').decode('utf-8'))` eller konfigurera din terminal för UTF‑8. |

---

## Utöka skriptet: Från **extrahera text från TIFF** till batch‑bearbetning

Nu när du har en stabil grund, överväg följande nästa steg:

1. **Batch‑konvertering** – Packa in hela flödet i en funktion `def ocr_tiff(path):` och iterera över en katalog med TIFF‑filer.
2. **Skriv ut till filer** – Istället för att skriva ut, skriv varje sidas text till `page_{i}.txt` eller slå ihop allt till ett enda dokument.
3. **Alternativa OCR‑motorer** – Om du behöver högre noggrannhet, byt `ocr.OcrEngine()` mot Tesseract (`pytesseract`) eller Azure Cognitive Services—behåll bara samma “extrahera text från TIFF”‑logik.
4. **Efterbehandling** – Kör stavningskontroll, språkdetection eller regex‑rensning för att städa upp den råa OCR‑utdata.

## Fullt, körklart skript

Nedan är den kompletta koden, klar för kopiering och inklistring. Den inkluderar grundläggande felhantering och valfri sparning av varje sidas text till separata filer.

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

Kör detta skript, peka `tiff_file` på ditt dokument, och se hur konsolen fylls med rena franska meningar. Om du angav `out_folder` hittar du också en serie `page_#.txt`‑filer redo för vidare bearbetning.

## Slutsats

Vi har just **extraherat text från TIFF**‑filer med ett enkelt Python‑OCR‑arbetsflöde, och du vet nu hur du på ett pålitligt sätt **konverterar TIFF till text**. Från att initiera motorn med rätt språk till att loopa över varje sidas JSON‑resultat, har varje steg förklarats med “varför”, så att du kan anpassa mönstret till andra språk, bildformat eller större batch‑jobb.

Vad blir nästa steg? Prova att byta OCR‑backend till Tesseract, experimentera med olika språkpaket, eller integrera resultatet i en sökbar databas. Himlen är gränsen när du på ett pålitligt sätt kan omvandla skannade bilder till sökbar text.

Känn dig fri att lämna en kommentar om du stöter på problem eller har idéer för vidare förbättringar. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Extrahera text från bild med Aspose OCR – Steg‑för‑steg‑guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extrahera text från bilder med OCR‑operation på mappar](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Konvertera bild till text – Utför OCR på bild från URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}