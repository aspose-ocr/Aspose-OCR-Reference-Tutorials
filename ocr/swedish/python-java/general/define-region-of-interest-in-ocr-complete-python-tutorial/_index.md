---
category: general
date: 2026-06-16
description: Definiera intresseområde i OCR för att extrahera spansk text från ID‑kort.
  Lär dig hur du laddar bild för OCR och specificerar ROI effektivt.
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: sv
og_description: Definiera intresseområde i OCR för att extrahera spansk text från
  ID‑kort. Steg‑för‑steg‑guide för att ladda bilder och specificera ROI.
og_title: Definiera intresseområde i OCR – Komplett Python‑handledning
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Definiera intresseområde i OCR – Komplett Python‑handledning
url: /sv/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definiera intresseområde i OCR – Komplett Python‑handledning

Har du någonsin undrat hur man **definierar intresseområde i OCR** så att du bara läser den del av en bild du faktiskt behöver? I den här handledningen går vi igenom exakt det, samt visar hur du **laddar bild för OCR** och extraherar spansk text från ett ID‑kort med bara några rader Python.  

Om du någonsin har stirrat på en brusig skanning och tänkt, “Det måste finnas ett renare sätt att hämta namn‑fältet,” så är du på rätt plats. Vid slutet kommer du kunna hämta ID‑kortstexten du bryr dig om utan att fastna i bakgrundsbrus.

## Vad du kommer att lära dig

- Varför du bör **definiera intresseområde** innan du kör OCR.  
- De exakta stegen för att **ladda bild för OCR** med en populär Python‑OCR‑wrapper.  
- Hur du **ange ROI** med pixelkoordinater.  
- Sätt att **extrahera ID‑kortstext** på ett pålitligt sätt, även när källspråket är spanska.  
- Tips för att hantera kantfall som roterade kort eller lågkontrast‑skanningar.  

Ingen tidigare OCR‑kunskap krävs—bara en fungerande Python 3‑miljö och en JPEG av ett ID‑kort du vill testa med.

---

![Illustration av intresseområde](placeholder.png){alt="Exempel på intresseområde som visar en markerad rektangel på en ID‑kortbild"}

## Steg 1: Installera och importera OCR‑biblioteket

Först och främst behöver du ett bibliotek som exponerar en `OcrEngine`‑klass liknande kodsnutten du såg. För den här guiden använder vi det fiktiva `ocr`‑paketet, men samma koncept gäller för `pytesseract`, `easyocr` eller någon wrapper som låter dig ange ett språk och en ROI.

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*Proffstips:* Om du använder `pytesseract` blir `Rectangle`‑klassen en enkel tupel `(left, top, width, height)`. Resten av flödet förblir identiskt.

## Steg 2: Ladda bild för OCR

Nu **laddar vi bild för OCR**. Motorn förväntar sig ett `ocr.Image`‑objekt, så vi pekar den på filen som innehåller ID‑kortet. Se till att sökvägen är absolut eller relativ till ditt skripts arbetskatalog.

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

Om bilden är stor, överväg att ändra storlek först; OCR‑motorer arbetar snabbare på bilder under 1500 px i bredd.

## Steg 3: Hur man anger ROI (Definiera intresseområde)

Här är kärnan i handledningen: **hur man anger ROI**. Ett intresseområde är helt enkelt en rektangel som talar om för OCR‑motorn, “Titta bara inom dessa pixelgränser.” Tänk på det som att rita en ruta runt namn‑fältet på ett ID‑kort.

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

Varför de siffrorna? I vårt exempel ligger namnet ungefär 120 px från vänster kant och 80 px från toppen. Justera dem för att matcha layouten på de kort du bearbetar.  

*Kantfall:* Om kortet är roterat 90°, byt `width` och `height` och justera `left`/`top` därefter, eller förrotera bilden med Pillow innan du matar den till motorn.

## Steg 4: Utför OCR inom ROI

Med ROI definierad kommer motorn att ignorera allt utanför rektangeln. Detta snabbar inte bara upp bearbetningen utan minskar också falska positiva resultat som orsakas av bakgrundsgrafik.

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

`recognize()`‑anropet returnerar ett objekt som innehåller den igenkända texten, förtroendescore och avgränsningsrutor för varje ord.

## Steg 5: Extrahera ID‑kortstext (och verifiera spansk output)

Till sist **extraherar vi ID‑kortstext** från ROI‑resultatet och skriver ut det. Eftersom vi tidigare satte språket till spanska kommer OCR‑motorn att använda språk‑specifika ordböcker, vilket förbättrar noggrannheten för tecken med diakritiska tecken som “ñ” eller “á”.

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### Förväntad output

```
ROI text: JUAN PÉREZ GARCÍA
```

Om du ser förvrängda tecken, dubbelkolla att bilden verkligen är på spanska och att OCR‑bibliotekets språkdatafiler är installerade.

## Vanliga fallgropar & hur man undviker dem

| Symptom | Trolig orsak | Lösning |
|---------|--------------|-----|
| Tom sträng returnerad | ROI skär inte någon text | Verifiera koordinater med en bildvisare; använd `engine.debug_draw_roi()` om tillgängligt. |
| Många skräptecken | Fel språkpaket | Installera om de spanska språkdata eller byt till `ocr.Language.AUTO`. |
| Låga förtroendescore | Bilden är suddig eller lågkontrast | Förbehandla med OpenCV – applicera `cv2.GaussianBlur` och `cv2.threshold`. |
| OCR körs på hela bilden trots ROI | Använder en äldre biblioteksversion | Uppgradera till den senaste `ocr`‑paketet; äldre versioner ignorerade ROI. |

## Utöka exemplet: Flera ROI:er

Ibland behöver du hämta mer än ett fält (t.ex. namn och ID‑nummer). Mönstret är detsamma: ändra `engine.region_of_interest` och anropa `recognize()` igen.

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

Du kan också batch‑processa en lista med rektanglar om biblioteket stödjer det, vilket sparar ett rundresor till OCR‑motorn.

## Fullt fungerande skript

När allt sätts ihop, här är ett färdigt skript som **definierar intresseområde**, **laddar bild för OCR**, och **extraherar spansk text** från ett ID‑kort.

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

Kör skriptet så bör du se namnet skrivet i konsolen. Byt rektangelvärdena för att rikta in dig på andra fält, och du får ett återanvändbart verktyg för alla ID‑kort‑liknande dokument.

## Nästa steg

- **Batch‑bearbetning:** Loopa igenom en mapp med ID‑kort och spara varje extraherat namn till en CSV‑fil.  
- **Språkdetection:** Låt användaren välja språk dynamiskt; `ocr.Language.AUTO` kan vara praktiskt.  
- **Post‑bearbetning:** Använd regex‑mönster för att rensa vanliga OCR‑fel (t.ex. ersätt “0” med “O” när det förekommer i namn).  

Genom att behärska hur man **definierar intresseområde** har du låst upp ett kraftfullt sätt att **extrahera ID‑kortstext** snabbt och exakt, särskilt när du hanterar spanska dokument.

---

### TL;DR

Vi visade dig hur man **definierar intresseområde i OCR**, **laddar bild för OCR**, och **hur man anger ROI** för att **extrahera spansk text från en bild** av ett ID‑kort. Det kompletta exemplet körs på under en minut och kan anpassas till vilken layout som helst med några koordinatjusteringar. Prova det, justera rektangeln, och se hur OCR fokuserar som en laser.

Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man extraherar text från bild genom att förbereda rektanglar i OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extrahera bildtext i C# med språkval med Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extrahera text från bild – OCR‑optimering med Aspose.OCR för .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}