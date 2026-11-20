---
category: general
date: 2026-11-20
description: Utför OCR på bild med Aspose OCR och extrahera sedan text från bilden
  med den inbyggda AI‑postprocessorn. Lär dig ett komplett Python‑arbetsflöde på några
  minuter.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from image
language: sv
lastmod: 2026-11-20
og_description: Utför OCR på bilden med Aspose OCR, extrahera sedan text från bilden
  via AI‑efterbehandling. Följ den här steg‑för‑steg‑guiden i Python.
og_image_alt: Diagram showing how to perform OCR on image and extract text from image
  using Aspose
og_title: Utför OCR på bild och extrahera text från bilden med Aspose
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Perform OCR on image with Aspose OCR and then extract text from image
    using the built‑in AI post‑processor. Learn a complete Python workflow in minutes.
  headline: Perform OCR on image and extract text from image with Aspose
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI post‑processing
title: Utför OCR på bild och extrahera text från bild med Aspose
url: /sv/python/general/perform-ocr-on-image-and-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utför OCR på bild och extrahera text från bild med Aspose

Om du behöver **utföra OCR på bild**‑filer i Python visar den här guiden en komplett end‑to‑end‑lösning. Genom att använda Aspose OCR tillsammans med Aspose AI‑postprocessorn kan du på ett pålitligt sätt **extrahera text från bild**‑filer och förbättra rå OCR‑utdata med en lättviktig språkmodell.

I den här handledningen kommer du att:

* Ställa in Aspose OCR‑motorn.
* Köra OCR för att **extrahera text från bild**.
* Eventuellt konfigurera en AI‑modell för efterbehandling.
* Registrera en anpassad efterbehandlingsfunktion.
* Producera förbättrad text och rensa upp resurser.

Stegen fungerar med alla rasterbilder (PNG, JPEG, BMP) och kräver endast paketet `aspose-ocr`.

## Förutsättningar

Innan du börjar, se till att du har:

| Krav | Varför det är viktigt |
|------|-----------------------|
| Python 3.8+ | Krävs av Aspose SDK. |
| `aspose-ocr` pip‑paket | Tillhandahåller `AsposeOCR`, `AsposeAI` och modell‑konfigurationsklasser. |
| En bildfil (t.ex. `sample_image.png`) | Källan som du kommer att **utföra OCR på bild** för. |
| Valfritt: GPU‑stöd | Om du planerar att köra en större modell på en GPU, sätt `gpu_layers` därefter. |

Installera SDK:n med:

```bash
pip install aspose-ocr
```

## Steg 1: Utför OCR på bild

Den första operationen är att läsa in bilden och erhålla råtext. Detta är kärnsteget för **utföra OCR på bild**.

```python
from aspose.ocr import AsposeOCR

# Initialise the OCR engine
ocr_engine = AsposeOCR()

# Path to the image you want to process
image_path = "YOUR_DIRECTORY/sample_image.png"

# Execute OCR – this returns the plain text extracted from the image
raw_text = ocr_engine.recognize_image(image_path)

print("Raw OCR result:")
print(raw_text)
```

**Varför detta fungerar:** `AsposeOCR.recognize_image` kör en förtränad optisk teckenigenkänningsmodell som är optimerad för hastighet och noggrannhet på vanliga typsnitt. Metoden returnerar en vanlig Unicode‑sträng, vilket är baslinjen för all vidare bearbetning.

> **Proffstips:** Om bilden innehåller flera språk, sätt `ocr_engine.language = "eng+spa"` (eller någon annan stödjande ISO‑639‑2‑kod) innan du anropar `recognize_image`.

## Steg 2: Initiera AI‑postprocessorn

Aspose AI erbjuder ett lättviktigt efterbearbetningslager som kan rensa upp OCR‑fel, korrigera interpunktion eller tillämpa anpassad affärslogik.

```python
from aspose.ocr import AsposeAI

# Initialise the AI post‑processor with default logging
ai_processor = AsposeAI()
```

**Varför du behöver den:** Rå OCR missuppfattar ofta tecken (t.ex. “0” vs “O”). AI‑steget förfinar resultatet, vilket gör **extrahera text från bild**‑resultatet mer pålitligt för efterföljande uppgifter som indexering eller analys.

## Steg 3: (Valfritt) Konfigurera AI‑modellen

Du kan peka processorn mot en specifik Hugging Face‑modell, aktivera automatiska nedladdningar eller tvinga CPU‑körning. Detta steg är valfritt men användbart när du vill ha deterministiskt beteende.

```python
from aspose.ocr import AsposeAIModelConfig

# Create a configuration object
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"          # Download model if missing
model_config.hugging_face_repo_id = "openai/gpt2"   # Small, fast model
model_config.gpu_layers = 0                        # Use CPU; set >0 for GPU

# Apply the configuration to the AI processor
ai_processor.configure(model_config)
```

**Förklaring:**  
* `allow_auto_download` sparar dig manuellt modellhantering.  
* `hugging_face_repo_id` väljer en modell; `gpt2` är ett bra kompromiss mellan storlek och kvalitet för kort texts korrigering.  
* `gpu_layers` styr hur många transformer‑lager som körs på GPU:n; `0` tvingar ren CPU‑körning, vilket är säkert på alla maskiner.

## Steg 4: Registrera en anpassad efterbearbetningsfunktion

Aspose AI låter dig ansluta vilken callable som helst som tar emot den råa OCR‑strängen och returnerar en transformerad version. Nedan är ett enkelt exempel som konverterar all text till versaler.

```python
def my_post_processor(text):
    """
    Custom post‑processor that transforms the OCR result.
    Replace this logic with your own business rules.
    """
    return text.upper()

# Register the function with the AI processor
ai_processor.set_post_processor(my_post_processor, custom_settings=None)
```

**När du bör anpassa:** Använd en egen funktion när du behöver domänspecifik rensning, såsom att ta bort konfidentiella identifierare, normalisera datum eller tillämpa regex‑baserade korrigeringar. AI‑modellen körs *efter* denna funktion, så du kan kombinera deterministiska regler med probabilistiska förbättringar.

## Steg 5: Förbättra OCR‑resultatet med AI‑postprocessorn

Kör nu hela pipeline:n: den råa OCR‑texten passerar först genom din anpassade funktion, därefter genom AI‑modellen, och slutligen får du det förfinade resultatet.

```python
# Run the AI post‑processor on the raw OCR text
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("\nOriginal OCR :")
print(raw_text)
print("\nAI‑enhanced   :")
print(enhanced_text)
```

**Vad du bör se:**  
Om den ursprungliga bilden innehöll “Hello world”, kan konsolen visa:

```
Original OCR :
Hello world

AI‑enhanced   :
HELLO WORLD
```

I ett riktigt scenario skulle AI‑modellen korrigera stavfel, lägga till saknad interpunktion eller omformatera radbrytningar, vilket ger dig ett renare **extrahera text från bild**‑resultat redo för lagring eller analys.

## Steg 6: Frigör resurser när du är klar

Både OCR‑motorn och AI‑postprocessorn allokerar inhemska resurser. Att explicit frigöra dem förhindrar minnesläckor, särskilt i långvariga tjänster.

```python
# Clean up native resources
ai_processor.free_resources()
```

Om du också har instansierat `ocr_engine` med en tung backend, kan du anropa `ocr_engine.dispose()` (om tillgängligt) på samma sätt.

## Vanliga variationer och kantfall

| Situation | Rekommenderad justering |
|-----------|--------------------------|
| **Stora PDF‑filer med många sidor** | Loopa över varje sida, anropa `recognize_image` för varje rasteriserad sida och samla resultaten. |
| **GPU‑aktiverad miljö** | Sätt `model_config.gpu_layers` till det antal lager du vill köra på GPU:n (t.ex. `4`). Säkerställ att CUDA‑drivrutiner är installerade. |
| **Icke‑engelsk text** | Ändra `ocr_engine.language` till rätt språk‑kod och, om nödvändigt, välj en språk‑specifik Hugging Face‑modell. |
| **Mycket brusiga skanningar** | Förbehandla bilden med OpenCV (avlägsna brus, tröskel) innan du anropar `recognize_image`. |
| **Behov av att behålla originalversaler** | Ersätt `my_post_processor`‑funktionen med en no‑op eller en mer nyanserad regel istället för `text.upper()`. |

## Fullt fungerande exempel

Sammanfogar allt, här är ett komplett skript du kan köra som det är (ersätt `YOUR_DIRECTORY/sample_image.png` med din faktiska filsökväg):

```python
from aspose.ocr import AsposeOCR, AsposeAI, AsposeAIModelConfig

# 1️⃣ Perform OCR on image
ocr_engine = AsposeOCR()
image_path = "YOUR_DIRECTORY/sample_image.png"
raw_text = ocr_engine.recognize_image(image_path)

# 2️⃣ Initialise the AI post‑processor
ai_processor = AsposeAI()

# 3️⃣ (Optional) Configure the AI model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "openai/gpt2"
model_config.gpu_layers = 0            # CPU execution
ai_processor.configure(model_config)

# 4️⃣ Register a custom post‑processor (example: uppercase)
def my_post_processor(text):
    return text.upper()

ai_processor.set_post_processor(my_post_processor, custom_settings=None)

# 5️⃣ Enhance the OCR result
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("Original OCR :", raw_text)
print("AI‑enhanced   :", enhanced_text)

# 6️⃣ Release resources
ai_processor.free_resources()
```

När du kör detta skript skrivs både den råa OCR‑utdata och den AI‑förbättrade versionen ut, vilket demonstrerar hur du kan **utföra OCR på bild**‑filer och på ett pålitligt sätt **extrahera text från bild** i ett enda, reproducerbart arbetsflöde.

## Slutsats

Du vet nu hur du **utför OCR på bild**‑filer med Aspose OCR och sedan **extraherar text från bild** med den inbyggda AI‑postprocessorn. Handledningen täckte:

* Initiering av OCR‑motorn.
* Körning av OCR för att erhålla råtext.
* (Valfritt) konfigurering av en lättviktig Hugging Face‑modell.
* Tillägg av en

## Vad bör du lära dig härnäst?

Följande handledningar behandlar närliggande ämnen som bygger på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Extrahera text från bild med Aspose OCR & AI – Full steg‑för‑steg‑guide](/ocr/english/python/general/extract-text-image-with-aspose-ocr-ai-full-step-by-step-guid/)
- [Hur man korrigerar OCR‑fel – Extrahera text från bild med Aspose OCR – Steg‑för‑steg‑guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extrahera text från bild Python – Komplett Aspose OCR‑guide](/ocr/english/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}