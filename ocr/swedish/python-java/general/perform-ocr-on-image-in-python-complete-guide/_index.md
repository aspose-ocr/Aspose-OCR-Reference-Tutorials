---
category: general
date: 2026-06-22
description: Utför OCR på bild med Python på bara några rader. Lär dig hur du laddar
  en bild för OCR, känner igen text från PNG och använder OCR-motorn effektivt.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: sv
og_description: Utför OCR på bild snabbt med Python. Denna handledning visar hur man
  laddar en bild för OCR, känner igen text från PNG och använder OCR-motorn med förtroende.
og_title: Utför OCR på bild i Python – Steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Utför OCR på bild i Python – Komplett guide
url: /sv/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utför OCR på bild i Python – Komplett guide

Har du någonsin behövt **utföra OCR på bild**-filer men känt dig fast redan på den första kodraden? Du är inte ensam. I den här genomgången visar vi exakt hur du **laddar bild för OCR**, sätter upp en lättviktig **OCR-motor**, och slutligen **läser text från PNG** med bara några få kommandon.

Vi täcker allt från att installera biblioteket till att justera vitlistan så att endast siffror och versala bokstäver klarar skanningen. I slutet har du ett färdigt skript som du kan släppa in i vilket projekt som helst—ingen gåta, ingen extra fluff.

## Vad du kommer att lära dig

- Hur du **använder OCR-motor** programmässigt i Python.  
- De exakta stegen för att **ladda bild för OCR** från en lokal mapp.  
- Varför och hur du begränsar igenkänning till en anpassad teckenuppsättning.  
- Hur du **läser text från PNG** och hanterar resultatet på ett säkert sätt.  

**Förutsättningar:** Python 3.7+ installerat, en terminal du är bekväm med, och en bild (t.ex. `serial-number.png`) som du vill läsa. Ingen tidigare OCR‑erfarenhet krävs.

---

## Utför OCR på bild – Initiera OCR-motorn

Det första du måste göra är att skapa en instans av OCR-motorn. Tänk på motorn som hjärnan som analyserar pixlarna och omvandlar dem till tecken.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Varför detta är viktigt:* Utan en motor finns inget att bearbeta bilden med. Klassen `OcrEngine` samlar all tungt arbete—förbehandling, segmentering och teckenklassificering—i ett enda objekt som du kan återanvända.

---

## Ladda bild för OCR – Tillhandahåll PNG-filen

Nu när motorn finns, måste du mata den med bilden du vill läsa. Biblioteket förväntar sig ett `ImageStream`‑objekt, som du kan skapa direkt från en filsökväg.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Proffstips:* Håll bilden i ett högkontrastformat (svart text på vit bakgrund) och undvik komprimeringsartefakter; de kan störa OCR‑algoritmen.

---

## Begränsa tecken – Vitlista siffror och versala bokstäver

Ofta bryr du dig bara om en delmängd av tecken—t.ex. ett serienummer som bara innehåller A‑Z och 0‑9. Genom att sätta en vitlista säger du åt motorn att ignorera allt annat, vilket dramatiskt förbättrar noggrannheten.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*Vad händer under huven?* Motorn bygger ett filter som kastar bort alla glyfer som inte finns i vitlistan innan det sista klassificeringssteget. Detta är särskilt praktiskt när bilden innehåller brus eller dekorativ text du inte behöver.

---

## Läs text från PNG – Kör OCR‑processen

Med motorn förberedd och bilden laddad kan du äntligen **utföra OCR på bild**. Anropet `recognize()` kör hela kedjan och returnerar ett resultatobjekt.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

Om du är nyfiken på prestanda så avslutas metoden vanligtvis inom några hundra millisekunder för en 300 × 200 px PNG på en modern laptop.

---

## Utdata och verifiering – Hämta den igenkända texten

Det sista steget är att extrahera ren text från resultatobjektet. Allt som inte matchade vitlistan tas automatiskt bort, så du får en ren sträng redo för vidare bearbetning.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Typisk utdata:* `AB12C3D4E5` (förutsatt att bilden innehöll exakt det serienumret).  

Om utdata är tom eller förvrängd, dubbelkolla bildkvaliteten och vitlistan; ett vanligt fallgropp är att av misstag utelämna nödvändiga tecken.

---

## Edge Cases & Vanliga fallgropar

| Situation | Vad att kontrollera | Föreslagen åtgärd |
|-----------|---------------------|-------------------|
| **Fil ej hittad** | Sökvägsfel eller saknad fil | Använd `os.path.abspath` för att verifiera den fullständiga sökvägen innan du anropar `set_image`. |
| **Låg kontrast på bilden** | Texten smälter samman med bakgrunden | Applicera ett enkelt tröskelvärde (`Pillow` eller `OpenCV`) innan du matar bilden till motorn. |
| **Oväntade tecken** | Vitlistan för restriktiv | Lägg till de saknade tecknen i vitlistesträngen. |
| **Stora bilder** | Långsam igenkänning | Ändra storlek på bilden till max 1024 px bredd; OCR‑kvaliteten förblir vanligtvis hög. |

---

## Fullt skript – Klart att köra

Nedan är det kompletta, fristående skriptet som binder ihop alla delar. Spara det som `ocr_demo.py`, ersätt `YOUR_DIRECTORY` med den faktiska mappen, och kör `python ocr_demo.py`.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Förväntad konsolutdata* (när PNG‑filen innehåller `SN12345`):

```
Recognized text: SN12345
```

---

## Slutsats

Du vet nu exakt hur du **utför OCR på bild**‑filer i Python, från **laddning av bild för OCR** till **läsa text från PNG** och slutligen extrahera ett rent resultat med en anpassningsbar **OCR-motor**. Metoden är enkel, utbyggbar och fungerar direkt för de flesta serienummer‑liknande skanningar.

Vad blir nästa steg? Prova att byta vitlistan till gemena bokstäver, experimentera med olika bildformat (JPEG, BMP), eller integrera skriptet i en batch‑bearbetningspipeline. Samma mönster—motor → bild → inställningar → läsa → utdata—gäller för i princip alla OCR‑uppgifter du stöter på.

Har du frågor eller en märklig bild som vägrar samarbeta? Lägg en kommentar nedan, och lycka till med kodandet! 

![Diagram som illustrerar stegen för att utföra OCR på bild med Python](https://example.com/ocr-flow.png "Diagram som visar hur man utför OCR på bild med en Python OCR-motor")


## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Konvertera bild till text – Utför OCR på bild från URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Hur man använder AspOCR: Förprocessa bild‑OCR‑filter för .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Hur man extraherar text från bild genom att förbereda rektanglar i OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}