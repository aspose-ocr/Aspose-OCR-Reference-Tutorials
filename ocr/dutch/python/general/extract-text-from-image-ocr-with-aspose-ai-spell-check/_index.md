---
category: general
date: 2026-05-03
description: tekst extraheren uit afbeelding met Aspose OCR en AI-spellingscontrole.
  Leer hoe je een afbeelding OCR't, afbeelding laadt voor OCR, tekst van factuur herkent
  en GPU‑resources vrijgeeft.
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: nl
og_description: tekst uit afbeelding extraheren met Aspose OCR en AI-spellingscontrole.
  Stapsgewijze handleiding die behandelt hoe je een afbeelding OCR't, afbeelding laadt
  voor OCR, en GPU‑resources vrijgeeft.
og_title: tekst uit afbeelding extraheren – Complete OCR‑ en spellingscontrolegids
tags:
- OCR
- Aspose
- AI
- Python
title: tekst uit afbeelding extraheren – OCR met Aspose AI Spell‑Check
url: /nl/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekst uit afbeelding extraheren – Complete OCR- en spell‑checkgids

Heb je ooit **tekst uit afbeelding** moeten extraheren maar wist je niet welke bibliotheek zowel snelheid als nauwkeurigheid biedt? Je bent niet de enige. In veel real‑world projecten—denk aan factuurverwerking, kassabon digitalisatie, of het scannen van contracten—het verkrijgen van schone, doorzoekbare tekst uit een foto is de eerste hindernis.

Het goede nieuws is dat Aspose OCR in combinatie met een lichtgewicht Aspose AI‑model die taak kan afhandelen in een paar regels Python. In deze tutorial lopen we door **hoe je een afbeelding OCR't**, de afbeelding correct laadt, een ingebouwde spell‑check‑post‑processor uitvoert, en uiteindelijk **GPU‑bronnen vrijgeeft** zodat je app geheugen‑vriendelijk blijft.

Aan het einde van deze gids kun je **tekst van facturen** herkennen, veelvoorkomende OCR‑fouten automatisch corrigeren, en je GPU schoon houden voor de volgende batch.

---

## Wat je nodig hebt

- Python 3.9 of nieuwer (de code gebruikt type‑hints maar werkt op eerdere 3.x‑versies)
- `aspose-ocr` en `aspose-ai` pakketten (installeren via `pip install aspose-ocr aspose-ai`)
- Een CUDA‑enabled GPU is optioneel; het script valt terug op CPU als er geen wordt gevonden.
- Een voorbeeldafbeelding, bijv. `sample_invoice.png`, geplaatst in een map die je kunt refereren.

Geen zware ML‑frameworks, geen enorme modeldownloads—alleen een klein Q4‑K‑M gekwantiseerd model dat comfortabel op de meeste GPU's past.

## Stap 1: Initialiseer de OCR‑engine – tekst uit afbeelding extraheren

Het eerste wat je doet is een `OcrEngine`‑instantie maken en aangeven welke taal je verwacht. Hier kiezen we Engels en vragen om plain‑text output, wat ideaal is voor downstream verwerking.

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**Waarom dit belangrijk is:** Het instellen van de taal beperkt de tekenset, waardoor de nauwkeurigheid verbetert. De plain‑text modus verwijdert lay‑outinformatie die je meestal niet nodig hebt wanneer je alleen tekst uit afbeelding wilt extraheren.

## Stap 2: Afbeelding laden voor OCR – hoe een afbeelding OCR't

Nu voeren we een echte afbeelding aan de engine. De `Image.load`‑helper begrijpt gangbare formaten (PNG, JPEG, TIFF) en abstraheert de eigenaardigheden van bestands‑IO.

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**Tip:** Als je bronafbeeldingen groot zijn, overweeg ze te verkleinen voordat je ze naar de engine stuurt; kleinere afmetingen kunnen GPU‑geheugengebruik verminderen zonder de herkenningskwaliteit te schaden.

## Stap 3: Configureer het Aspose AI‑model – tekst van factuur herkennen

Aspose AI wordt geleverd met een klein GGUF‑model dat je automatisch kunt downloaden. Het voorbeeld gebruikt de `Qwen2.5‑3B‑Instruct‑GGUF`‑repository, gekwantiseerd naar `q4_k_m`. We geven de runtime ook de opdracht om 20 lagen op de GPU toe te wijzen, wat snelheid en VRAM‑gebruik in balans brengt.

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**Achter de schermen:** Het gekwantiseerde model is ongeveer 1,5 GB op schijf, een fractie van een full‑precision model, maar het vangt toch genoeg linguïstische nuances om typische OCR‑spelfouten te signaleren.

## Stap 4: Initialiseer AsposeAI en koppel de spell‑check post‑processor

Aspose AI bevat een kant‑en‑klare spell‑check post‑processor. Door deze te koppelen wordt elk OCR‑resultaat automatisch opgeschoond.

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**Waarom de post‑processor gebruiken?** OCR‑engines lezen vaak “Invoice” als “Invo1ce” of “Total” als “T0tal”. De spell‑check voert een lichtgewicht taalmodel uit over de ruwe string en corrigeert die fouten zonder dat je een aangepast woordenboek hoeft te schrijven.

## Stap 5: Voer de spell‑check post‑processor uit op het OCR‑resultaat

Met alles aangesloten levert één enkele aanroep de gecorrigeerde tekst op. We printen ook zowel de originele als de opgeschoonde versie zodat je de verbetering kunt zien.

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

Typische output voor een factuur kan er als volgt uitzien:

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

Let op hoe “Invo1ce” is omgezet naar het juiste woord “Invoice”. Dat is de kracht van de ingebouwde AI‑spell‑check.

## Stap 6: GPU‑bronnen vrijgeven – GPU‑bronnen veilig vrijgeven

Als je dit draait in een langdurige service (bijv. een web‑API die tientallen facturen per minuut verwerkt), moet je de GPU‑context na elke batch vrijgeven. Anders zie je geheugenlekken en krijg je uiteindelijk “CUDA out of memory” fouten.

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**Pro tip:** Roep `free_resources()` aan binnen een `finally`‑blok of een context‑manager zodat het altijd wordt uitgevoerd, zelfs als er een uitzondering optreedt.

## Volledig werkend voorbeeld

Alle onderdelen samenvoegen levert een zelfstandige script op die je in elk project kunt gebruiken.

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

Sla het bestand op, pas het pad naar je afbeelding aan, en voer `python extract_text_from_image.py` uit. Je zou de opgeschoonde factuurtekst in de console moeten zien.

## Veelgestelde vragen (FAQ)

**Q: Werkt dit op alleen‑CPU machines?**  
A: Absoluut. Als er geen GPU wordt gedetecteerd, valt Aspose AI terug op CPU‑executie, hoewel het langzamer zal zijn. Je kunt CPU forceren door `model_cfg.gpu_layers = 0` in te stellen.

**Q: Wat als mijn facturen in een andere taal dan Engels zijn?**  
A: Verander `ocr_engine.language` naar de juiste enum‑waarde (bijv. `aocr.Language.Spanish`). Het spell‑check model is meertalig, maar je krijgt mogelijk betere resultaten met een taalspecifiek model.

**Q: Kan ik meerdere afbeeldingen in een lus verwerken?**  
A: Ja. Plaats gewoon de laad‑, herkennings‑ en post‑processingstappen binnen een `for`‑lus. Vergeet niet `ocr_ai.free_resources()` aan te roepen na de lus of na elke batch als je dezelfde AI‑instantie hergebruikt.

**Q: Hoe groot is de model‑download?**  
A: Ongeveer 1,5 GB voor de gekwantiseerde `q4_k_m` versie. Het wordt gecached na de eerste uitvoering, zodat volgende runs direct zijn.

## Conclusie

In deze tutorial hebben we laten zien hoe je **tekst uit afbeelding** kunt extraheren met Aspose OCR, een klein AI‑model configureert, een spell‑check post‑processor toepast, en veilig **GPU‑bronnen vrijgeeft**. De workflow omvat alles van het laden van de afbeelding tot het opruimen, waardoor je een betrouwbare pijplijn krijgt voor **tekst van factuur herkennen** scenario's.

Volgende stappen? Probeer de spell‑check te vervangen door een aangepast entity‑extractie model

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}