---
category: general
date: 2026-07-05
description: Extrahera text från bild med Python OCR. Lär dig hur du laddar bild för
  OCR, läser text från ett område och extraherar text från en faktura med några få
  rader kod.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: sv
og_description: Extrahera text från en bild med Python OCR. Den här guiden visar hur
  du laddar en bild för OCR, läser text från ett område och snabbt extraherar text
  från en faktura.
og_title: Extrahera text från bild – Läs text från område med OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Extrahera text från bild – Läs text från område med OCR
url: /sv/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild – Läs text från region med OCR

Har du någonsin behövt **extrahera text från bild** men bara en specifik del är viktig—t.ex. totalbeloppet på en faktura? Du är inte ensam. I många verkliga projekt kommer du att behöva **läsa text från region** snarare än att analysera hela bilden. Lyckligtvis kan du med några rader Python ladda en bild för OCR, definiera ett intresseområde (ROI) och hämta exakt de tecken du behöver.

I den här handledningen går vi igenom ett komplett, körbart exempel som visar hur man **laddar bild för OCR**, sätter upp ett ROI och slutligen **extraherar text från faktura**. När du är klar har du ett färdigt kodsnutt som fungerar med vilket populärt OCR‑bibliotek som helst som stödjer region‑baserad igenkänning.

---

## Vad du behöver

- Python 3.8+ (koden fungerar även på 3.10)  
- Ett OCR‑paket som exponerar en `OcrEngine`‑klass (för demo använder vi ett fiktivt `ocr`‑modul; ersätt det med `pytesseract`, `easyocr` eller något annat bibliotek som erbjuder ROI‑stöd)  
- En exempelbild—t.ex. `invoice.png`—som innehåller tydlig, tryckt text  
- Grundläggande kunskap om Python‑funktioner och klasser (ingen djupinlärningsbakgrund krävs)

Om du redan har detta, toppen—låt oss dyka ner. Om inte, hämta den senaste Python‑versionen från python.org och installera OCR‑paketet via `pip install your-ocr-lib`.

---

![Exempel på att extrahera text från bild](extract-text-from-image.png "Extrahera text från bild – regionbaserad OCR‑demo")

*Bilden ovan illustrerar regionen (röd rektangel) som vi kommer att rikta in oss på för att **extrahera text från bild**.*

---

## Steg 1: Installera och importera OCR‑biblioteket

Först, se till att OCR‑biblioteket är tillgängligt i din miljö. Importmönstret nedan fungerar för de flesta paket som exponerar en hög‑nivå `OcrEngine`‑klass.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **Proffstips:** Om du använder `pytesseract` måste du installera Tesseract‑binären separat och sätta `pytesseract.pytesseract.tesseract_cmd` till dess sökväg.

---

## Steg 2: Skapa OCR‑motorn och ange språk

Att skapa motorn är enkelt, men att specificera språk förbättrar noggrannheten avsevärt, särskilt för fakturor som innehåller siffror och engelska ord.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

Varför gör vi så? OCR‑motorn använder språkmodeller för att förutsäga tecken; genom att tala om att den ska förvänta sig engelska minskar du falska positiva som att missta “0” för “O”.

---

## Steg 3: Ladda bild för OCR

Nu **laddar vi bild för OCR**. De flesta bibliotek accepterar en filsökväg eller ett Pillow‑bildobjekt. Här använder vi bibliotekets inbyggda laddare för enkelhetens skull.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

Se till att sökvägen pekar på rätt katalog; ett vanligt misstag är att glömma den relativa sökvägen när skriptet körs från en annan arbetskatalog.

---

## Steg 4: Definiera intresseområdet (ROI)

Att definiera ROI är kärnan i **läsa text från region**. Tänk på det som att rita en rektangel runt den del av fakturan som innehåller totalbeloppet.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` och `top` representerar X‑ respektive Y‑koordinaterna för rektangelns övre vänstra hörn.  
- `width` och `height` anger storleken på rutan.  
- Du kan experimentera med olika värden i en bildvisare som visar pixelkoordinater.

> **Varför ROI är viktigt:** Att köra OCR på hela sidan slösar CPU‑cykler och introducerar ofta brus från orelaterad text, tabeller eller grafik. Genom att fokusera på ett område får du renare resultat och snabbare bearbetning.

---

## Steg 5: Utför OCR på det specificerade området

Med allt på plats **extraherar vi text från bild**—men endast inom det ROI vi definierat.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

`recognize`‑metoden returnerar ett objekt som vanligtvis innehåller den råa strängen, förtroendescore och ibland begränsningsrutor för varje ord. För vårt ändamål behöver vi bara den rena texten.

---

## Steg 6: Skriv ut den extraherade texten

Låt oss skriva ut resultatet och se vad vi fick. Detta steg demonstrerar **extrahera text från faktura** i ett verkligt scenario.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### Förväntad utdata

```
Text inside ROI:
Total Amount: $1,245.67
```

Om din faktura har en annan layout kommer du att se den text som finns inom rektangeln—kanske ett fakturanummer, datum eller PO‑referens.

---

## Steg 7: Packa allt i en återanvändbar funktion (valfritt)

För att göra lösningen återanvändbar över flera fakturor, kapsla in logiken i en funktion. Detta illustrerar också **ocr på region** som ett generellt verktyg.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

Du kan nu anropa funktionen med vilken faktura som helst:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

---

## Vanliga fallgropar & hur du undviker dem

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| **Tomt resultat** | ROI täcker faktiskt ingen text (fel koordinater). | Dubbelkolla pixelvärden med en bildredigerare; lägg till en visuell debug‑överlappning. |
| **Skräptecken** | Låg bildupplösning eller dålig kontrast. | Förbehandla bilden: konvertera till gråskala, applicera tröskling (`cv2.threshold`). |
| **Fel språk** | Motorn använder som standard ett språk utan den nödvändiga teckenuppsättningen. | Ställ explicit in `ocr_engine.language` till `ENGLISH` eller lämplig lokalkod. |
| **Prestandaproblem** | OCR körs på stora bilder upprepade gånger. | Ändra storlek på bilden innan laddning, eller bearbeta endast ROI genom att beskära först. |

---

## Utöka exemplet: Flera ROI‑områden

Ibland innehåller en faktura flera fält du behöver—t.ex. **extrahera text från faktura** för både totalbelopp och fakturadatum. Du kan loopa över en lista med rektanglar:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

Detta mönster håller koden ren och gör det enkelt att lägga till fler områden senare.

---

## Slutsats

Vi har precis gått igenom ett komplett, end‑to‑end‑flöde för att **extrahera text från bild** med Python OCR, med fokus på ett specifikt område. Genom att **ladda bild för OCR**, definiera ett **intresseområde** och anropa motorn kan du på ett pålitligt sätt **läsa text från region**—perfekt för att hämta totaler från fakturor, datum från kvitton eller annan lokaliserad data.  

Känn dig fri att experimentera

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Extrahera text från bild med Aspose OCR – steg‑för‑steg‑guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extrahera text från bild – OCR‑optimering med Aspose.OCR för .NET](/ocr/english/net/ocr-optimization/)
- [Hur man extraherar text från bild genom att förbereda rektanglar i OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}