---
category: general
date: 2026-01-12
description: Python OCR-handledning som visar hur man extraherar tabelltext från en
  bild. Lär dig att läsa tabell från bild och extrahera vald text med Aspose OCR.
draft: false
keywords:
- python ocr tutorial
- extract table text
- read table from image
- extract selected text
- how to extract table
language: sv
og_description: Python OCR-handledning som lär dig hur du extraherar tabelltext från
  en bild, läser tabell från bild och extraherar vald text med Aspose OCR.
og_title: 'Python OCR-handledning: Extrahera tabelltext från bilder'
tags:
- OCR
- Python
- AsposeOCR
title: 'Python OCR-handledning: Extrahera tabelltext från bilder'
url: /sv/python-java/general/python-ocr-tutorial-extract-table-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR‑tutorial: Extrahera tabelltext från bilder

Har du någonsin behövt en **python ocr tutorial** som faktiskt visar hur du drar ut en tabell ur ett skannat formulär? Du är inte ensam. De flesta guider stannar vid generell textutvinning och lämnar dig att gissa hur du isolerar det snygga rutnätet av data du är intresserad av.  

I den här guiden går vi igenom ett verkligt scenario: läsa en tabell från en bild, extrahera endast den valda texten du behöver, och slutligen skriva ut resultaten. På vägen slänger vi in tips om **how to extract table** data på ett pålitligt sätt, så att du slipper uppfinna hjulet varje gång.

## Vad du kommer att lära dig

- Hur du sätter upp Aspose OCR för Python.  
- Hur du definierar ett rektangulärt område som innehåller en tabell.  
- De exakta stegen för att **extract table text** och **read table from image**.  
- Tips för att hantera flera språk eller oregelbundna tabelllayouter.  
- Ett komplett, körbart skript som du kan släppa in i ditt projekt idag.

**Förutsättningar**  
- Python 3.8 eller nyare.  
- Grundläggande förståelse för OCR‑koncept (ingen djup expertis krävs).  
- En PNG‑ eller JPEG‑bild som innehåller en tydlig tabell (vi kallar den `form_with_table.png`).  

Om du har detta, låt oss dyka in—utan onödig prat, bara handlingsbar kod.

![python ocr tutorial example of table region](table_region_example.png){alt="python ocr tutorial exempel som visar tabellområde"}

## Steg 1: Installera och importera Aspose OCR

Först och främst: du behöver Aspose OCR‑biblioteket. Paketet finns på PyPI, så ett enda `pip`‑kommando räcker.

```bash
pip install aspose-ocr
```

Importera sedan modulen och eventuella hjälpfunktioner du behöver.

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
```

*Pro tip:* Håll dina beroenden i en `requirements.txt`‑fil. Det gör det enkelt att reproducera miljön.

## Steg 2: Initiera OCR‑motorn (Python OCR Tutorial Core)

Att skapa motorn är hjärtat i varje **python ocr tutorial**. Här sätter vi också standardspråket till engelska—byt gärna ut det senare.

```python
# Step 2: Create an OCR engine and set the default language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

Varför ange språk? OCR‑noggrannheten kan öka dramatiskt när motorn vet vilka tecken som förväntas. Om du arbetar med flerspråkiga formulär kan du antingen ange en lista med språk eller åsidosätta per område (se nedan).

## Steg 3: Ladda din bild

Aspose OCR fungerar med de flesta vanliga bildformat. Peka bara på filvägen så får du ett `Image`‑objekt redo för bearbetning.

```python
# Step 3: Load the image that contains the form with the table
image_page = ocr.Image.load("YOUR_DIRECTORY/form_with_table.png")
```

*Edge case:* Stora bilder (över 5 MB) kan göra bearbetningen långsam. Överväg att ändra storlek eller komprimera dem innan OCR om prestanda blir ett problem.

## Steg 4: Definiera tabellområdet (Read Table from Image)

Nu blir det roligt: berätta för motorn *var* tabellen finns. Du anger ett `OcrRegion` med en `Rectangle` (x, y, width, height). Koordinaterna är pixelbaserade, så du kan behöva experimentera lite.

```python
# Step 4: Define the rectangular area where the table is located
# (x, y, width, height) – adjust these values for your image
table_region = ocr.OcrRegion(
    image_page,
    ocr.Rectangle(120, 340, 800, 450)
)

# Optional: override language for this specific region
table_region.language = ocr.Language.ENGLISH
```

Varför använda ett område? Genom att begränsa OCR till tabellområdet **extract selected text** snabbare och undviker brus från omgivande etiketter eller grafik. Det förbättrar också noggrannheten eftersom motorn kan fokusera på en enhetlig layout.

## Steg 5: Kör OCR på det definierade området

När området är satt anropar vi `process_region`. Metoden returnerar ett `OcrResult`‑objekt som innehåller råtext, förtroendescore och även begränsningsrutor om du behöver dem senare.

```python
# Step 5: Run OCR only on the defined region
region_result = ocr_engine.process_region(table_region)
```

Om du behöver extrahera flera tabeller, upprepa helt enkelt Steg 4‑5 med olika rektanglar.

## Steg 6: Skriv ut den extraherade tabelltexten

Till sist, skriv ut—eller spara—tabellens textrepresentation. Aspose OCR returnerar vanlig text med radbrytningar som vanligtvis matchar rader, vilket gör efterbearbetning enkel.

```python
# Step 6: Output the extracted table text
print("Table text:\n", region_result.text)
```

**Förväntad utskrift** (exempel):

```
Table text:
 Item        Qty   Price
 Apple       10    $1.20
 Banana      5     $0.80
 Orange      8     $1.00
```

Du kan nu föra in den här strängen i `csv`‑parsers, pandas DataFrames eller någon annan downstream‑analyspipeline.

## Fullt fungerande exempel

Sätter vi ihop allt får du det kompletta skriptet som du kan köra direkt. Byt ut `YOUR_DIRECTORY/form_with_table.png` mot den faktiska sökvägen till din bild.

```python
# -*- coding: utf-8 -*-
"""
Python OCR Tutorial: Extract Table Text from Images
---------------------------------------------------
A self‑contained example that demonstrates how to read a table from an image
using Aspose OCR for Python.
"""

# Install the library first:
# pip install aspose-ocr

import asposeocr as ocr

def extract_table(image_path, rect):
    """
    Extracts text from a rectangular region that contains a table.

    :param image_path: Path to the PNG/JPEG image.
    :param rect: Tuple (x, y, width, height) defining the table region.
    :return: Plain‑text representation of the table.
    """
    # Initialise OCR engine with English language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Load the image
    img = ocr.Image.load(image_path)

    # Define the region (override language if needed)
    region = ocr.OcrRegion(img, ocr.Rectangle(*rect))
    region.language = ocr.Language.ENGLISH  # optional per‑region override

    # Process only this region
    result = engine.process_region(region)

    return result.text

if __name__ == "__main__":
    # Adjust these coordinates to match your table location
    table_rect = (120, 340, 800, 450)   # x, y, width, height

    # Path to your image file
    img_file = "YOUR_DIRECTORY/form_with_table.png"

    extracted_text = extract_table(img_file, table_rect)
    print("=== Extracted Table Text ===")
    print(extracted_text)
```

Kör skriptet med `python extract_table.py`. Om allt stämmer ser du tabellen skriven i din konsol.

## Vanliga frågor & Edge‑Case‑hantering

**Vad händer om tabellen inte är perfekt rektangulär?**  
Du kan dela tabellen i flera överlappande områden eller använda en större rektangel som täcker hela området och sedan efterbearbeta texten (t.ex. dela på radbrytningar).

**Kan jag extrahera bara specifika kolumner?**  
Efter att du har hela tabelltexten, använd Python‑s `csv` eller `pandas` för att skiva ut de kolumner du är intresserad av. OCR‑steget returnerar allt inom rektangeln.

**Hur arbetar jag med icke‑engelska tabeller?**  
Sätt `ocr_engine.language` (eller `region.language`) till rätt enum, t.ex. `ocr.Language.FRENCH` eller kombinera flera språk med `ocr.Language.ENGLISH | ocr.Language.SPANISH`.

**Finns det ett sätt att få begränsningsrutor för varje cell?**  
Aspose OCR kan returnera `region_result.words` där varje ord innehåller en begränsningsruta. Du måste mappa dessa rutor tillbaka till ett rutnät—användbart för avancerad layoutanalys.

## Tips för bättre noggrannhet

- **Rensa bilden**: Binarisera eller öka kontrasten innan du skickar den till OCR. Bibliotek som Pillow kan hjälpa.  
- **Undvik komprimeringsartefakter**: Spara skanningar som PNG när det är möjligt.  
- **Tänk på DPI**: 300 dpi är en bra kompromiss; lägre värden kan leda till missade tecken.  
- **Testa olika rektangelstorlekar**: Lite större rektanglar fångar ofta löst placerade tecken som tillhör tabellen.

## Nästa steg

Nu när du har bemästrat **how to extract table** data med Aspose OCR kan du utforska:

- Konvertera den extraherade texten till en CSV‑fil med Python‑modulen `csv`.  
- Ladda in data i en **pandas** DataFrame för analys.  
- Använd OCR för att läsa handskrivna formulär (kräver en annan motor eller extra träning).  
- Automatisera batch‑bearbetning av dussintals skannade formulär med en enkel `for`‑loop.

Varje av dessa förlängningar bygger på kärnkoncepten i denna **python ocr tutorial**, så du är väl rustad för att skala upp.

---

*Lycka till med kodandet! Om du stöter på problem, lämna en kommentar nedan—jag hjälper gärna till att finjustera extraktionen.*

{{< /blocks/products/pf-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}