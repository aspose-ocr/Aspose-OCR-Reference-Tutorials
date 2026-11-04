---
category: general
date: 2026-06-25
description: Läs in bild för OCR och utför OCR på PNG med en steg‑för‑steg Python‑handledning
  som använder aocr. Lär dig felsökning, loggning och bästa praxis.
draft: false
keywords:
- load image for OCR
- perform OCR on PNG
- aocr logging setup
- OCR debugging Python
- image preprocessing OCR
language: sv
og_description: Ladda bild för OCR och utför OCR på PNG med aocr. Denna guide går
  igenom loggning, bildladdning och igenkänning med fullständig kod.
og_title: Ladda bild för OCR – Steg‑för‑steg Python‑handledning
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Load image for OCR and perform OCR on PNG with a step‑by‑step Python
    tutorial using aocr. Learn debugging, logging, and best practices.
  headline: Load Image for OCR – Complete Guide to Perform OCR on PNG Files
  type: TechArticle
- questions:
  - answer: Usually not. `aocr` handles PNG natively, but if the image is huge (>10
      MP) you might want to downscale first to speed up processing.
    question: Do I need to convert the PNG to another format?
  - answer: Rotate the log after each run or limit the level to `INFO` once you’re
      confident the pipeline works.
    question: What if the logger file grows too large?
  - answer: Absolutely. Just call `ocr_png` for each file; the function creates a
      fresh logger each time, keeping logs isolated.
    question: Can I process multiple images in a loop?
  - answer: Yes – `engine.result` also contains `boxes` and `confidences`. Explore
      the `aocr` docs for `result.boxes` if you need layout information.
    question: Is there a way to get bounding boxes instead of plain text?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Ladda bild för OCR – Komplett guide för att utföra OCR på PNG-filer
url: /sv/python/general/load-image-for-ocr-complete-guide-to-perform-ocr-on-png-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ladda bild för OCR – Komplett guide för att utföra OCR på PNG‑filer

Har du någonsin behövt **ladda bild för OCR** men varit osäker på hur du ska sätta upp korrekt felsökning? Du är inte ensam. I många projekt är det första hindret att få in PNG‑filen i motorn samtidigt som du kan se vad som händer under huven.  

I den här handledningen går vi igenom allt du behöver för att **utföra OCR på PNG**‑filer med `aocr`‑biblioteket – från att konfigurera en logger för detaljerad output till själva textigenkänningen. I slutet har du ett återanvändbart skript som du kan slänga in i vilket Python‑projekt som helst, och du förstår varför varje del är viktig.

## Vad du kommer att lära dig

- Hur du initierar `aocr`‑loggaren så att du kan spåra varje steg.
- Den exakta koden för att **ladda bild för OCR** med `aocr.OcrEngine`.
- Hur du konfigurerar loggnivån för att få granular debug‑information.
- Att köra motorn för att **utföra OCR på PNG** och hämta resultaten.
- Tips för att hantera vanliga fallgropar som saknade filer eller ej stödda format.

Ingen förkunskap om `aocr` krävs; bara en fungerande Python 3‑installation och en bild du vill läsa. Låt oss sätta igång.

![exempel på att ladda bild för OCR](assets/load-image-ocr.png "Illustration av att ladda en bild för OCR i Python")

## Förutsättningar

| Krav | Varför det är viktigt |
|------|-----------------------|
| Python 3.8+ | `aocr` riktar sig mot moderna tolkar och använder typ‑hints. |
| `aocr`‑biblioteket installerat (`pip install aocr`) | Utan paketet finns inte de klasser vi använder. |
| En PNG‑bild du vill läsa | Handledningen fokuserar på **utföra OCR på PNG**, så en PNG är nödvändig. |
| Skrivrättigheter till en loggmapp | Loggaren behöver skapa `ocr_debug.log`. |

Om du saknar något av detta, installera det nu – det tar bara en minut.

```bash
pip install aocr
```

## Steg 1: Ladda bild för OCR – Initiera loggning

Innan du ens rör bilden, sätt upp en logger. Att debugga OCR kan vara en mardröm om du är blind för vad motorn gör. Klassen `aocr.Logging` skriver allt till en fil, och genom att sätta nivån till `DEBUG` ser du varje internt anrop.

```python
import aocr

# Create a logger instance
ocr_logger = aocr.Logging()
# Choose where the log file will live – adjust the path to suit your project
ocr_logger.set_output_file("logs/ocr_debug.log")

# DEBUG gives you the most detail; you can switch to INFO for less noise
ocr_logger.set_level(aocr.LoggingLevel.DEBUG)
```

**Varför detta är viktigt:**  
Om OCR‑motorn inte kan hitta filen eller bildformatet inte stöds, fångar loggaren undantags‑stack‑tracen. Det sparar dig från oändligt gissande senare.

## Steg 2: Utföra OCR på PNG – Konfigurera motorn

Nu när loggaren är klar, koppla den till OCR‑motorn. Detta steg binder ihop de två så varje motoråtgärd registreras.

```python
# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
# Plug the logger into the engine
ocr_engine.logging = ocr_logger
```

**Pro‑tips:**  
Du kan återanvända samma `ocr_engine`‑instans för flera bilder. Kom bara ihåg att rensa tidigare tillstånd om du bearbetar en batch.

## Steg 3: Ladda bild för OCR – Mata in PNG‑filen

Här är kärnan i handledningen: faktiskt **ladda bild för OCR**. Metoden `load_image` accepterar en filsökväg; den avkodar internt PNG‑filen till en bitmap som motorn kan förstå.

```python
# Path to the PNG you want to read
image_path = "samples/invoice.png"

# Load the image – this is where we “load image for OCR”
ocr_engine.load_image(image_path)
```

### Edge Cases att hålla koll på

1. **Fil ej hittad** – Om sökvägen är fel, kastar `aocr` ett `FileNotFoundError`. Loggaren noterar det, men du kan också fånga det:

   ```python
   try:
       ocr_engine.load_image(image_path)
   except FileNotFoundError as e:
       print(f"❌ Could not locate {image_path}: {e}")
       raise
   ```

2. **Ej stödd format** – Även om PNG är brett stödjat kan en korrupt fil trigga `UnsupportedFormatError`. I så fall, överväg att konvertera bilden till en ren PNG med Pillow innan du laddar den.

## Steg 4: Utföra OCR på PNG – Kör igenkänningen

Nu när bilden är i minnet kan du äntligen **utföra OCR på PNG**. Metoden `recognize` startar motorens pipelines (förbehandling, segmentering, klassificering) och fyller i resultatobjektet.

```python
# Execute the OCR process
ocr_engine.recognize()
```

Efter detta anrop innehåller motorn den igenkända texten. Du kan komma åt den via attributet `result`:

```python
# Retrieve the plain text output
recognized_text = ocr_engine.result.text
print("📝 OCR Result:")
print(recognized_text)
```

**Varför du bör kontrollera resultatet:**  
Vissa OCR‑motorer returnerar tomma strängar för lågkontrastbilder. Att se resultatet omedelbart låter dig avgöra om du behöver förbehandla (t.ex. öka kontrasten) innan du kör igen.

## Steg 5: Packa ihop allt – En återanvändbar funktion

Att samla bitarna i en enda funktion gör det enkelt att anropa från andra skript eller en webbtjänst. Detta visar också hur du **laddar bild för OCR** och **utför OCR på PNG** i ett snyggt paket.

```python
def ocr_png(image_path: str, log_dir: str = "logs") -> str:
    """
    Load a PNG image, run aocr OCR, and return the extracted text.
    
    Parameters
    ----------
    image_path : str
        Full path to the PNG file.
    log_dir : str, optional
        Directory where the debug log will be written.
    
    Returns
    -------
    str
        The plain‑text OCR result.
    """
    import os
    import aocr

    # Ensure the log directory exists
    os.makedirs(log_dir, exist_ok=True)

    # ---------- Logging ----------
    logger = aocr.Logging()
    logger.set_output_file(os.path.join(log_dir, "ocr_debug.log"))
    logger.set_level(aocr.LoggingLevel.DEBUG)

    # ---------- Engine ----------
    engine = aocr.OcrEngine()
    engine.logging = logger

    # ---------- Load Image ----------
    try:
        engine.load_image(image_path)
    except Exception as exc:
        logger.error(f"Failed to load image {image_path}: {exc}")
        raise

    # ---------- Recognize ----------
    engine.recognize()
    return engine.result.text

# Example usage
if __name__ == "__main__":
    txt = ocr_png("samples/invoice.png")
    print("\n--- Extracted Text ---\n")
    print(txt)
```

När du kör skriptet skapas en detaljerad `ocr_debug.log` i mappen `logs`, och den igenkända texten skrivs ut i konsolen. Du har nu ett **utföra OCR på PNG**‑verktyg som du kan importera någon annanstans.

## Vanliga frågor & fallgropar

- **Behöver jag konvertera PNG‑filen till ett annat format?**  
  Vanligtvis inte. `aocr` hanterar PNG nativt, men om bilden är enorm (>10 MP) kan du vilja skala ner först för att snabba upp bearbetningen.

- **Vad händer om loggfilen blir för stor?**  
  Roterar loggen efter varje körning eller begränsa nivån till `INFO` när du är säker på att pipeline fungerar.

- **Kan jag bearbeta flera bilder i en loop?**  
  Absolut. Anropa bara `ocr_png` för varje fil; funktionen skapar en ny logger varje gång, så loggarna hålls separata.

- **Finns det ett sätt att få bounding‑boxes istället för ren text?**  
  Ja – `engine.result` innehåller också `boxes` och `confidences`. Utforska `aocr`‑dokumentationen för `result.boxes` om du behöver layoutinformation.

## Slutsats

Du vet nu hur du **laddar bild för OCR** och **utför OCR på PNG** med `aocr`‑biblioteket, komplett med en robust loggningsuppsättning som gör felsökning smärtfri. Exempelfunktionen kapslar in hela arbetsflödet, så du kan slänga in den i vilket projekt som helst och börja extrahera text direkt.

Nästa steg? Prova att mata in olika bildtyper (JPEG, TIFF) för att se hur noggrannheten förändras, eller experimentera med förbehandlingstekniker som tröskling för att förbättra resultat på brusiga skanningar. Och om du är nyfiken på att extrahera strukturerad data (tabeller, formulär), kolla in `aocr`‑sektionerna om layout‑analys – de passar bra ihop med det du just byggt.

Lycka till med kodandet, och må dina OCR‑pipelines vara felfria!


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}