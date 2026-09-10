---
category: general
date: 2026-01-12
description: Hur man kör OCR och extraherar text från fakturabilder med Aspose OCR
  och en lättviktig Hugging Face-modell. Lär dig att ladda ner modellen, korrigera
  OCR‑fel och utföra OCR på bilden.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: sv
og_description: Hur du kör OCR på fakturabilder, extraherar text och rättar fel med
  en Hugging Face LLM. Följ den här kompletta guiden för felfria resultat.
og_title: Hur du kör OCR på fakturabilder – Fullständig handledning
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: Hur man kör OCR på fakturabilder – Komplett steg‑för‑steg‑guide
url: /sv/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kör OCR på fakturabilder – Komplett steg‑för‑steg‑guide

Har du någonsin undrat **how to run OCR** på en skannad faktura och få ren, sökbar text utan att spendera timmar på att städa upp den? Du är inte ensam. I många verkliga projekt är den råa OCR‑utdata full av felaktiga igenkänningar—tänk “O” för “0”, “l” för “1”, eller till och med hela ord som är förvrängda. De goda nyheterna? Med några rader Python kan du inte bara **perform OCR on image**‑filer utan också automatiskt **correct OCR errors** med en lättviktsmodell från Hugging Face.

I den här handledningen går vi igenom allt du behöver veta: från att ladda en fakturabild, extrahera råtext, ladda ner en kvantiserad modell, till att polera resultatet så att du får en perfekt transkription redo för efterföljande bearbetning. I slutet kommer du kunna **extract text from invoice** PDF‑filer eller PNG‑filer i ett enda, repeterbart skript.

## Förutsättningar & Installation

Before diving in, make sure you have:

| Krav | Varför det är viktigt |
|------|------------------------|
| Python 3.9+ | Modern syntax och typindikeringar |
| `aspose-ocr` package | Tillhandahåller `ocr.OcrEngine` som används i exemplet |
| `aspose-ai` package | Levererar `AsposeAI`‑postprocessorn |
| Access to a GPU (optional) | Snabbar upp LLM‑lagren; annars fungerar CPU bra |
| Internet connection (first run) | Behövs för att automatiskt **download Hugging Face model** |

Du kan installera de nödvändiga biblioteken med:

```bash
pip install aspose-ocr aspose-ai
```

> **Proffstips:** Om du planerar att köra LLM på GPU, installera `torch` med CUDA‑stöd (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

Nu när miljön är klar, låt oss gå in i koden.

## Steg 1 – Initiera OCR‑motorn och ladda din fakturabild

Det första du behöver göra är att skapa en instans av Asposes OCR‑motor och peka den på filen du vill bearbeta. Detta steg är grunden för **how to run OCR** på vilken bild som helst.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Varför detta är viktigt:** `load_image` accepterar PNG, JPEG, TIFF och även PDF‑sidor, vilket låter dig **perform OCR on image**‑data oavsett format.

## Steg 2 – Kör grundläggande OCR för att fånga råtext

När bilden är laddad kan motorn producera en rå transkription. Denna utdata är ofta brusig, vilket är anledningen till att vi senare kör ett korrigeringssteg.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

Typisk råutdata kan se ut så här:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

Lägger du märke till nollorna (`0`) där siffran “O” borde vara? Det är exakt den typen av fel vi kommer att fixa senare.

## Steg 3 – Konfigurera AI‑postprocessorn med en lättvikts‑LLM

Nu tar vi in en **download Hugging Face model** som är tillräckligt liten för att köras på modest hårdvara men ändå kraftfull nog att förstå fakturaspråk. Exemplet använder Qwen 2.5 3B‑Instruct GGUF‑modellen, kvantiserad till `int8` för ett litet minnesavtryck.

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **Varför denna modell?** `int8`‑kvantiseringen krymper filen till ~1,2 GB, vilket gör den möjlig på de flesta bärbara datorer. GPU‑lager accelererar inferens, men koden faller elegant tillbaka till CPU när ingen GPU hittas.

## Steg 4 – Kör LLM‑baserad korrigering på den råa OCR‑resultatet

När modellen är klar matar vi in den råa texten i postprocessorn. LLM:n kommer att skriva om transkriptionen, fixa vanliga OCR‑fel och normalisera siffror.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

Förväntad rengjord utdata:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

Du kan se att nollorna har förvandlats tillbaka till bokstaven “O”, och “Am0unt” är nu “Amount”. Detta är kärnan i att automatiskt **correct OCR errors**.

## Steg 5 – Frigör resurser och städa upp

Stora språkmodeller kan hålla fast GPU‑minne, så det är god praxis att frigöra resurser när du är klar.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

Om du planerar att bearbeta många fakturor i en batch, kan du hålla modellen laddad och bara frigöra den i slutet av skriptet.

## Fullt fungerande exempel

När vi sätter ihop allt, här är ett enda skript du kan lägga i en `.py`‑fil och köra:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

Att köra skriptet bör ge en utdata liknande “AI‑corrected”-blocket som visades tidigare. Känn dig fri att byta bildvägen mot någon annan faktura eller kvitto för att **extract text from invoice**‑filer i bulk.

## Vanliga frågor & kantfall

### Vad händer om jag inte har en GPU?

`gpu_layers`‑parametern är valfri. Sätt den till `0` eller utelämna den, så körs modellen helt på CPU. Förvänta dig långsammare inferens—ungefär 2–3 sekunder per sida på en modern laptop.

### Mina fakturor är flersidiga PDF‑filer. Hur hanterar jag dem?

Konvertera varje sida till en separat bild (t.ex. med `pdf2image`) och loopa över sidorna med samma skript. OCR‑motorn kan bearbeta varje bild oberoende, och LLM:n kommer att korrigera varje textblock.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### Modellnedladdning misslyckas bakom en brandvägg?

Ladda ner modellen manuellt från Hugging Face‑modellhubben, packa upp den i en lokal mapp och peka `hugging_face_repo_id` på den lokala sökvägen:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### Hur exakt är korrigeringen?

För typiska fakturor på engelska rättar LLM:n >95 % av vanliga OCR‑fel. Komplexa handskrivna anteckningar kan fortfarande behöva manuell granskning.

## Tips & tricks för produktionsanvändning

- **Batch processing:** Packa in steg 2‑4 i en funktion och mata in en lista med filsökvägar. Återanvänd samma `AsposeAI`‑instans för att undvika att ladda om modellen.
- **Logging:** Ersätt `print` med Pythons `logging`‑modul för att fånga både råa och korrigerade utdata för revisionsspår.
- **Error handling:** Omslut OCR‑anropet med `try/except`‑block. Om en bild misslyckas, logga filnamnet och fortsätt.
- **Performance tuning:** Experimentera med `gpu_layers`. Fler lager på GPU snabbar upp inferensen men ökar VRAM‑användning.

## Slutsats

Vi har gått igenom **how to run OCR** på fakturabilder från början till slut, och visat hur du **perform OCR on image**, **download Hugging Face model**, och automatiskt **correct OCR errors**. Det kompletta skriptet demonstrerar ett praktiskt arbetsflöde som du kan lägga in i vilken Python‑baserad automatiseringspipeline som helst.

Nästa steg? Försök utöka pipelinen till att **extract key fields** (fakturanummer, datum, total) med reguljära uttryck på den korrigerade texten, eller mata in den rengjorda utdata i en databas för sökbara poster. Du kan också experimentera med andra lättvikts‑LLM:er från Hugging Face om du behöver ett annat språk eller domänspecifik kunskap.

Lycka till med kodningen, och må dina OCR‑resultat alltid vara kristallklara! 

![hur man kör OCR på en fakturabild](ocr_invoice_example.png "hur man kör OCR på faktura")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}