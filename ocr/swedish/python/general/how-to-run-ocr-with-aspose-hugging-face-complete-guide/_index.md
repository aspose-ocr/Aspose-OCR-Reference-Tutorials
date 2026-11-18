---
category: general
date: 2026-04-29
description: Lär dig hur du kör OCR på dina skanningar, använder Hugging Face-modellen
  automatiskt och känner igen text från skanningar med Aspose OCR på några minuter.
draft: false
keywords:
- how to run OCR
- use hugging face model
- recognize text from scans
- download model automatically
language: sv
og_description: Hur man kör OCR på skanningar med Aspose OCR, automatiskt laddar ner
  en Hugging Face-modell och får ren, punktuerad text.
og_title: Hur du kör OCR med Aspose och Hugging Face – Komplett guide
tags:
- OCR
- Aspose
- Hugging Face
- Python
title: Hur man kör OCR med Aspose och Hugging Face – Komplett guide
url: /sv/python/general/how-to-run-ocr-with-aspose-hugging-face-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kör OCR med Aspose & Hugging Face – Komplett guide

Har du någonsin undrat **hur man kör OCR** på en hög med skannade dokument utan att spendera timmar på att justera inställningarna? Du är inte ensam. I många projekt måste utvecklare **igenkänna text från skanningar** snabbt, men de stöter på problem med modellnedladdningar och efterbehandling.  

Good news: den här handledningen visar dig en färdig‑till‑körning‑lösning som **använder en Hugging Face-modell**, automatiskt hämtar den och lägger till interpunktion så att resultatet läses som om en människa skrivit det. I slutet har du ett skript som bearbetar varje bild i en mapp och skapar en ren `.txt`‑fil bredvid varje skanning.

## Vad du behöver

- Python 3.8+ (koden använder f‑strings, så äldre versioner räcker inte)
- `aspose-ocr`-paketet (installera via `pip install aspose-ocr`)
- Internetåtkomst för den första modellnedladdningen  
- En mapp med bildskanningar (`.png`, `.jpg` eller `.tif`)

Det är allt—inga extra binärer, ingen manuell modellhantering. Låt oss dyka in.

![exempel på hur man kör OCR](https://example.com/ocr-demo.png "exempel på hur man kör OCR")

## Steg 1: Importera Aspose OCR-klasser & konfigurera miljön

We start by pulling the necessary classes from the Aspose OCR library. Importing everything up front keeps the script tidy and makes it easy to spot missing dependencies.

```python
# Step 1: Import Aspose OCR classes
import os
from aspose.ocr import OcrEngine, AsposeAI, AsposeAIModelConfig
```

*Varför detta är viktigt*: `OcrEngine` gör det tunga arbetet, medan `AsposeAI` låter oss ansluta en stor språkmodell för smartare efterbehandling. Om du hoppar över importen kommer resten av koden inte ens att kunna kompileras—så glöm inte den.

## Steg 2: Konfigurera en GPU‑medveten Hugging Face-modell  

Now we tell Aspose where to fetch the model and how many layers should run on the GPU. The `allow_auto_download="true"` flag does the **download model automatically** part for you.

```python
# Step 2: Configure a GPU‑aware AI model (replace with your own model folder)
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=40,                     # use GPU for faster inference
    directory_model_path=r"YOUR_DIRECTORY/models"
)
```

> **Proffstips**: Om du inte har ett GPU, sätt `gpu_layers=0`. Modellen kommer då att falla tillbaka till CPU, vilket är långsammare men fortfarande fungerar.

### Varför välja en Hugging Face-modell?

Hugging Face har en enorm samling av färdiga LLM:er. Genom att peka på `Qwen/Qwen2.5-3B-Instruct-GGUF` får du en kompakt, instruktion‑optimerad modell som kan lägga till interpunktion, korrigera avstånd och till och med fixa mindre OCR‑fel. Detta är kärnan i **use hugging face model** i praktiken.

## Steg 3: Initiera AI-motorn och aktivera interpunktion efter‑behandling  

The AI engine isn’t just for fancy chat—here we attach a *punctuation adder* that cleans up raw OCR output.

```python
# Step 3: Initialise the AI engine and enable punctuation post‑processing
ai_engine = AsposeAI()
ai_engine.set_post_processor("punctuation_adder", {})
```

*Vad händer?* Anropet `set_post_processor` registrerar en inbyggd efterprocessor som körs efter att OCR‑motorn är klar. Den tar den råa strängen och sätter in kommatecken, punkter och stora bokstäver där de hör hemma, vilket gör den slutliga texten mycket mer läsbar.

## Steg 4: Skapa OCR-motorn och anslut AI-motorn  

Connecting the AI engine to the OCR engine gives us a single object that can both read characters and polish the result.

```python
# Step 4: Create the OCR engine and attach the AI engine
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_engine)
```

If you skip this step, the OCR will still work, but you’ll lose the punctuation boost—so the output will look like a stream of words.

## Steg 5: Bearbeta varje bild i en mapp  

Here’s the heart of the tutorial. We loop over each image, run OCR, apply the post‑processor, and write the cleaned text to a side‑by‑side `.txt` file.

```python
# Step 5: Run OCR on each image in a folder, post‑process the result, and save the text
scans_folder = r"YOUR_DIRECTORY/scans"
for image_file in os.listdir(scans_folder):
    # Filter only supported image types
    if not image_file.lower().endswith(('.png', '.jpg', '.tif')):
        continue

    image_path = os.path.join(scans_folder, image_file)

    # Recognise text from the image
    ocr_result = ocr_engine.recognize(image_path)

    # Apply the punctuation post‑processor
    ocr_result = ocr_engine.run_postprocessor(ocr_result)

    # Show a brief confidence summary
    print(f"{image_file} – confidence {ocr_result.confidence:.2%}")

    # Save the cleaned text next to the source image
    txt_path = image_path + ".txt"
    with open(txt_path, "w", encoding="utf-8") as txt_file:
        txt_file.write(ocr_result.text)
```

### Vad du kan förvänta dig

Running the script prints something like:

```
invoice_001.png – confidence 96.73%
receipt_2024.tif – confidence 94.12%
```

Each line tells you the confidence score (a quick health check) and creates `invoice_001.png.txt`, `receipt_2024.tif.txt`, etc., containing punctuated, human‑readable text.

### Kantfall & variationer

- **Icke‑engelska skanningar**: Byt `hugging_face_repo_id` till en flerspråkig modell (t.ex. `microsoft/Multilingual-LLM-GGUF`).
- **Stora batcher**: Inslå loopen i en `concurrent.futures.ThreadPoolExecutor` för parallell bearbetning, men var medveten om GPU‑minnesgränser.
- **Anpassad efterbehandling**: Ersätt `"punctuation_adder"` med ditt eget skript om du behöver domänspecifik rensning (t.ex. ta bort fakturanummer).

## Steg 6: Rensa upp resurser  

When the job finishes, freeing resources prevents memory leaks, especially important if you’re running this inside a long‑lived service.

```python
# Step 6: Release resources
ai_engine.free_resources()
ocr_engine.dispose()
```

Neglecting this step can leave GPU memory hanging, which would sabotage subsequent runs.

## Sammanfattning: Så kör du OCR från början till slut  

In just a handful of lines, we’ve shown **how to run OCR** on a folder of scans, **use a Hugging Face model** that downloads itself the first time, and **recognize text from scans** with punctuation added automatically. The complete script is ready to copy‑paste, adjust your paths, and execute.

## Nästa steg & relaterade ämnen  

- **Batch‑efterbehandling**: Utforska `ocr_engine.run_batch_postprocessor` för ännu snabbare massbearbetning.  
- **Alternativa modeller**: Prova `openai/whisper`‑familjen om du behöver tal‑till‑text tillsammans med OCR.  
- **Integration med databaser**: Spara den extraherade texten i SQLite eller Elasticsearch för sökbara arkiv.  

Feel free to experiment—swap the model, tweak `gpu_layers`, or add your own post‑processor. The flexibility of Aspose OCR combined with Hugging Face’s model hub makes this a versatile foundation for any document‑digitization project.

---

*Lycka till med kodandet! Om du stöter på problem, lämna en kommentar nedanför eller kolla Aspose OCR‑dokumentationen för djupare konfigurationsalternativ.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}