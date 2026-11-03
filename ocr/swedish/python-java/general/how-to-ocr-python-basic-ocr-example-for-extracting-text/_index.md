---
category: general
date: 2026-04-26
description: 'hur man OCR:ar i Python: Lär dig att extrahera text från bild och läsa
  TIFF-filer i Python med ett grundläggande OCR‑exempel. Snabb, körbar kod medföljer.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: sv
og_description: 'hur man OCR i Python: En steg‑för‑steg‑guide som visar hur man extraherar
  text från bild, läser TIFF‑fil i Python och konverterar skannad bildtext med ett
  enkelt, körbart skript.'
og_title: hur man OCR:a i Python – Grundläggande OCR-exempel för att extrahera text
tags:
- OCR
- Python
- Image Processing
title: hur man OCR:ar i Python – Grundläggande OCR-exempel för att extrahera text
url: /sv/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hur man OCR:ar i Python – Grundläggande OCR‑exempel för att extrahera text

Har du någonsin funderat **hur man OCR:ar i Python** när du har en skannad TIFF liggande på skrivbordet? Du är inte den enda som stirrar på en hög bildfiler och frågar: “Hur får jag orden ur detta?” Den goda nyheten är att förvandla en bild till ren text är en barnlek med rätt bibliotek och några tydliga steg.

I den här handledningen går vi igenom ett **grundläggande OCR‑exempel** som läser en TIFF‑fil, extraherar texten och skriver ut den i konsolen. I slutet vet du exakt hur du **extraherar text från bild**‑filer, hur du hanterar de små egenheterna i TIFF‑format och vad du kan justera om du behöver **konvertera skannad bildtext** till något mer användbart. Ingen gömd magi – bara rakt på sak Python‑kod som du kan kopiera‑klistra och köra idag.

## Vad du behöver

Innan vi dyker ner, se till att du har:

- Python 3.9+ installerat (den senaste stabila versionen är bäst).
- Ett pip‑installabelt OCR‑bibliotek. I den här guiden använder vi ett fiktivt paket `aocr` som efterliknar populära verktyg som Tesseract; du kan byta ut det mot `pytesseract` eller `easyocr` senare.
- En TIFF‑bild du vill bearbeta – döp den till `input.tiff` och lägg den i en mapp som du refererar till i koden.
- Grundläggande kunskap om kommandoraden (endast för att installera paketet).

Det är allt. Inga tunga beroenden, inga Docker‑behållare, bara några rader kod.

## Steg 1 – Installera och importera beroenden (hur man OCR:ar i Python)

Först, hämta OCR‑paketet. Öppna en terminal och kör:

```bash
pip install aocr
```

Om du föredrar ett riktigt bibliotek, byt ut `aocr` mot `pytesseract` och installera Tesseract‑motorn separat.

Importera sedan det vi behöver. `Path`‑klassen från `pathlib` ger oss ett smidigt sätt att arbeta med filsökvägar på olika operativsystem.

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*Varför använda `Path`?* För att den abstraherar bort snedstreck (`/` vs `\`) och låter dig slå ihop kataloger utan att oroa dig för underliggande OS. Den lilla detaljen sparar ofta huvudvärk när du senare flyttar skriptet till en CI‑server.

## Steg 2 – Skapa OCR‑motorn (grundläggande OCR‑exempel)

Nästa steg är att starta OCR‑motorn. Tänk på `OcrEngine` som hjärnan som läser bilden och spottar ut tecken.

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

De flesta OCR‑bibliotek låter dig justera språk, DPI eller förtroendetrösklar här. För detta **grundläggande OCR‑exempel** håller vi oss till standardinställningarna, men du kan utforska `ocr_engine.config` senare om du behöver hantera flerspråkiga dokument.

## Steg 3 – Ladda din TIFF‑bild (läsa tiff‑fil i Python)

Här kommer delen **läsa tiff‑fil i Python** in. TIFF‑filer kan ha flera sidor, men `Image.load` hämtar som standard den första sidan – perfekt för en enkelsidig skanning.

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

Byt ut `"YOUR_DIRECTORY"` mot den faktiska mappen som innehåller `input.tiff`. Om du är osäker på var skriptet körs, skriver `Path.cwd()` ut den aktuella arbetskatalogen – praktiskt för felsökning av sökvägsproblem.

## Steg 4 – Kör OCR‑processen (extrahera text från bild)

Nu händer magin. Att anropa `process()` skickar bilden genom OCR‑pipeline:n och returnerar ett resultatobjekt.

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

Bakom kulisserna kan motorn konvertera bilden till gråskala, applicera tröskling och föra den in i ett neuralt nätverk. Du behöver inte hantera de stegen; biblioteket abstraherar dem åt dig.

## Steg 5 – Skriv ut den igenkända texten (konvertera skannad bildtext)

Till sist, skriv ut texten. I riktiga projekt skulle du troligen skriva den till en fil eller en databas, men utskrift håller exemplet enkelt.

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

När du kör skriptet bör du se något i stil med:

```
Hello, world!
This is a sample scanned document.
```

Om utskriften ser förvrängd ut, dubbelkolla att källbilden är tydlig och att OCR‑språket matchar texten.

## Fullt fungerande skript

Sätter vi ihop allt får vi det kompletta, körklara programmet:

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Förväntad utskrift

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

Om du behöver **konvertera skannad bildtext** till en sökbar PDF, kan du skicka `ocr_result.text` till en PDF‑generator som `reportlab` – men det är ett eget helt tutorial‑ämne.

## Vanliga fallgropar & Pro‑tips

- **Lågdpi‑skanningar**: OCR har svårt under 150 DPI. Om din TIFF är oskarp, skala upp den först med Pillow (`Image.open(...).resize(...)`).
- **Flera sidor**: För fler‑sidiga TIFF‑filer, iterera över `Image.load_multi_page()` (om ditt bibliotek stödjer det) och slå ihop resultaten.
- **Språkstöd**: Många motorer använder engelska som standard. Sätt `ocr_engine.language = "spa"` för spanska, till exempel.
- **Hantera blanksteg**: OCR lägger ofta till oönskade radbrytningar. Använd `str.splitlines()` eller reguljära uttryck för att rensa utskriften.
- **Prestanda**: Vid massbearbetning, återanvänd en enda `OcrEngine`‑instans istället för att skapa en ny för varje fil.

## Utöka exemplet

Nu när du behärskar **hur man OCR:ar i Python** för en enskild bild, överväg följande nästa steg:

1. **Batch‑bearbetning** – Loopa igenom en katalog med TIFF‑filer och skriv varje resultat till en `.txt`‑fil.
2. **Integration med Pandas** – Spara extraherad text tillsammans med metadata för snabb analys.
3. **Hybrid‑metod** – Kombinera OCR med NLP‑bibliotek som `spaCy` för att extrahera entiteter (namn, datum, belopp) från skannade fakturor.
4. **Alternativa filformat** – Byt `Image.load` mot `Image.from_bytes` för att hantera bilder som kommer från ett API eller en databas.

Alla dessa bygger på kärnidén att **extrahera text från bild** och **konvertera skannad bildtext** till något som maskiner kan förstå.

## Slutsats

Vi har gått igenom ett tydligt, end‑to‑end **grundläggande OCR‑exempel** som visar **hur man OCR:ar i Python**, hur man **läser tiff‑fil i Python**, och hur man **extraherar text från bild**‑filer med bara några få rader kod. Skriptet är självständigt, innehåller felhantering och skriver ut resultatet direkt, vilket gör det till en solid grund för alla projekt som behöver omvandla skannade dokument till redigerbar text.

Känn dig fri att experimentera – byt ut OCR‑bakänden, justera förbehandlingen, eller koppla utskriften till ett efterföljande arbetsflöde. Himlen är gränsen när du på ett pålitligt sätt kan **konvertera skannad bildtext** till sökbara, strukturerade data.

Har du frågor om kantfall, språkpaket eller prestandaoptimering? Lämna en kommentar nedan, och lycka till med kodandet! 

![hur man OCR:ar i Python‑exempel](/images/ocr-python-example.png "Skärmbild av hur man OCR:ar i Python‑skriptets utskrift")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}