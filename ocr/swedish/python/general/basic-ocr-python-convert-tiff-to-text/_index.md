---
category: general
date: 2026-03-18
description: Grundläggande OCR Python-handledning visar hur man konverterar TIFF till
  text, laddar bild‑OCR, ställer in GPU‑lager och fixar inledande nollor med Aspose
  AI.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: sv
og_description: Grundläggande OCR Python‑tutorial guidar dig genom att konvertera
  TIFF‑filer till ren text, ladda bilder, ställa in GPU‑lager och fixa ledande nollor.
og_title: Grundläggande OCR Python – konvertera TIFF till text
tags:
- OCR
- Python
- AI
- Aspose
title: grundläggande OCR Python – konvertera TIFF till text
url: /sv/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – Konvertera TIFF till Text med AI‑efterbehandling

Letar du efter ett sätt att göra **basic ocr python** på dina skannade dokument? I den här guiden går vi igenom hur du konverterar en TIFF‑fil till ren, sökbar text med hjälp av Aspose OCR och en AI‑efterprocessor.  

Om du någonsin har haft problem med att **convert TIFF to text** eftersom den råa utdata är full av stavfel eller konstiga symboler, är du inte ensam. Vi kommer också att visa hur du **load image OCR**, justerar motorn för att **set GPU layers**, och till och med **fix leading zeroes** som ofta förekommer i fakturanummer.

## Vad du kommer att lära dig

- Hur du initierar Aspose OCR‑motorn för tryckta dokument.  
- De exakta stegen för att **load image OCR** från en TIFF‑fil och få råtext.  
- Konfigurera en AI‑modell, ladda ner den automatiskt, och **setting GPU layers** för snabbare inferens.  
- Lägg till inbyggd stavningskontroll plus en anpassad funktion som **fixes leading zeroes**.  
- Rensa OCR‑resultatet och frigöra resurser på ett korrekt sätt.  

I slutet av den här handledningen har du ett enda, återanvändbart Python‑skript som omvandlar vilken TIFF som helst till en polerad, sökbar text—utan behov av manuell kopiering och inklistring.  

### Förutsättningar

- Python 3.8+ installerat på din maskin.  
- `aspose-ocr`‑paketet (`pip install aspose-ocr`).  
- Valfritt: ett GPU med minst 4 GB VRAM om du vill **set GPU layers**; annars faller koden tillbaka till CPU automatiskt.  

---

## basic ocr python – ladda bild och känna igen text

Det första vi behöver göra är att **load image OCR** så att motorn kan läsa pixlarna. Asposes `OcrEngine` hanterar många format, men här fokuserar vi på TIFF eftersom det är det vanligaste för skannade fakturor.

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Pro tip:** Om du hanterar multi‑page TIFF‑filer, bearbetar Aspose automatiskt varje sida i sekvens, så du behöver inga extra loopar.

Nu när bilden är laddad, låt oss köra ett grundläggande igenkänningspass.

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

Du kommer att se något liknande:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Lägg märke till *nollorna* före bokstäverna? Det är ett klassiskt OCR‑artefakt som vi kommer att rensa upp senare.

![basic ocr python workflow](/images/ocr-workflow.png "basic ocr python workflow diagram")

---

## Steg 2: Konvertera TIFF till text – förbered AI‑efterprocessorn

Rå OCR är användbart, men de flesta produktionspipelines behöver en polerad version. Aspose tillhandahåller en `AsposeAI`‑wrapper som kan ladda ner en modell från Hugging Face, köra den på GPU och automatiskt tillämpa stavningskontroll.

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### Varför `set GPU layers` är viktigt

`gpu_layers`‑parametern talar om för den underliggande GGUF‑modellen hur många transformer‑lager som ska hållas på GPU. Fler lager = snabbare inferens men högre VRAM‑användning. Om du har en modest laptop, sänk värdet till `10` eller utelämna det helt för att köra på CPU.

---

## Steg 3: Tillämpa stavningskontroll och **fix leading zeroes**

Aspose AI levereras med en inbyggd stavningskontroll som fångar de flesta engelska stavfel. Dock kräver domänspecifika korrigeringar—som att omvandla en inledande `0` till ett `O` för fakturakoder—en anpassad efterprocessor.

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **Why this works:** Det reguljära uttrycket söker efter en ordgräns (`\b`), en nolla, sedan exakt tre stora bokstäver. Det ersätter sedan nollan med bokstaven “O”. Du kan utöka mönstret för andra egenheter (t.ex. `0[0-9]{2}` för felavlästa siffror).

---

## Steg 4: Rensa OCR‑resultatet med AI‑efterprocessorn

Nu kombinerar vi allt: den rå strängen från **basic ocr python**, stavningskontrollen och vår noll‑korrigering. Metoden `run_postprocessor` returnerar en rensad version som är klar för efterföljande system.

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

Typisk utdata efter efterprocessorn:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Du kan se att den inledande nollan har förvandlats till ett `O`, och vanliga stavfel är korrigerade. Texten är nu lämplig för indexering i en sökmotor eller för att matas in i en data‑extraktionspipeline.

---

## Steg 5: Frigör AI‑resurser – håll ditt GPU nöjt

Om du kör flera OCR‑jobb i en långvarig tjänst är det god praxis att frigöra modellens GPU‑minne när du är klar.

```python
ocr_ai.free_resources()
```

Att hoppa över detta steg kan leda till “out‑of‑memory”-fel vid efterföljande anrop, särskilt när **set GPU layers** är satt till ett högt värde.

---

## Valfria variationer & kantfall

| Situation | Vad som ska ändras |
|-----------|--------------------|
| **Handwritten documents** | Använd `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` istället för `PRINTED`. |
| **No GPU available** | Sätt `gpu_layers=0` eller utelämna argumentet; modellen körs på CPU (långsammare men säkert). |
| **Different language** | Byt ut Hugging Face repo‑ID till en språk‑specifik modell, t.ex. `microsoft/Florence-2-base`. |
| **Batch processing** | Packa in stegen i en `for file in glob("*.tif"):`‑loop och samla resultat i en lista eller CSV. |
| **More complex zero patterns** | Utöka `invoice_fix` med ytterligare regex‑mönster, såsom `r"\b0+([A-Z]{2,})\b"` för flera inledande nollor. |

---

## Slutsats

Vi har just slutfört en **basic ocr python**‑pipeline som laddar en TIFF, extraherar råtext och sedan rensar den med en AI‑modell medan **setting GPU layers** används för prestanda. Den anpassade efterprocessorn visar hur man **fix leading zeroes**, en liten men ofta förbises detalj som kan bryta efterföljande analyser.

Känn dig fri att experimentera: prova en annan kvantisering (`float16` för högre noggrannhet), byt ut stavningskontrollen mot en domänspecifik ordlista, eller kedja flera anpassade korrigeringar tillsammans. Mönstret förblir detsamma—ladda, känna igen, konfigurera AI, efterprocessa och rensa upp.

**Nästa steg** du kan utforska inkluderar:

- Integrera den rensade utdata med en databas eller Elasticsearch‑index.  
- Använda samma metod för att **convert TIFF to text** för flerspråkiga PDF‑filer.  
- Lägg till ett UI med Flask eller FastAPI så icke‑tekniska användare kan ladda upp filer och få ren text omedelbart.  

Lycka till med kodningen, och må dina OCR‑resultat alltid vara skarpa och utan nollor!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}