---
category: general
date: 2026-03-18
description: Basis OCR Python‑tutorial laat zien hoe je TIFF naar tekst converteert,
  afbeelding‑OCR laadt, GPU‑lagen instelt en voorloopnullen corrigeert met Aspose
  AI.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: nl
og_description: basis OCR Python-tutorial leidt je door het converteren van TIFF‑bestanden
  naar schone tekst, het laden van afbeeldingen, het instellen van GPU‑lagen en het
  corrigeren van leidende nullen.
og_title: basis OCR Python – converteer TIFF naar tekst
tags:
- OCR
- Python
- AI
- Aspose
title: basis OCR Python – converteer TIFF naar tekst
url: /nl/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – Converteer TIFF naar Tekst met AI‑Nabewerking

Op zoek naar een manier om **basic ocr python** toe te passen op je gescande documenten? In deze gids lopen we stap voor stap door het converteren van een TIFF‑bestand naar schone, doorzoekbare tekst met Aspose OCR en een AI‑nabewerker.  

Als je ooit hebt geworsteld met het **converteren van TIFF naar tekst** omdat de ruwe output vol staat met typefouten of vreemde symbolen, ben je niet de enige. We laten ook zien hoe je **image OCR** laadt, de engine aanpast om **GPU‑lagen in te stellen**, en zelfs **leidende nullen** corrigeert die vaak voorkomen in factuurnummers.

## Wat je zult leren

- Hoe je de Aspose OCR‑engine initialiseert voor gedrukte documenten.  
- De exacte stappen om **image OCR** te **laden** vanuit een TIFF‑bestand en ruwe tekst te verkrijgen.  
- Een AI‑model configureren, automatisch downloaden, en **GPU‑lagen instellen** voor snellere inferentie.  
- Ingebouwde spell‑check toevoegen plus een aangepaste functie die **leidende nullen corrigeert**.  
- Het OCR‑resultaat opschonen en bronnen correct vrijgeven.  

Aan het einde van deze tutorial heb je één herbruikbaar Python‑script dat elke TIFF omzet in gepolijste, doorzoekbare tekst—zonder handmatig knippen en plakken.

### Vereisten

- Python 3.8+ geïnstalleerd op je machine.  
- `aspose-ocr`‑package (`pip install aspose-ocr`).  
- Optioneel: een GPU met minstens 4 GB VRAM als je **GPU‑lagen wilt instellen**; anders valt de code automatisch terug op CPU.  

---

## basic ocr python – image laden en tekst herkennen

Het eerste wat we moeten doen is **image OCR** **laden** zodat de engine de pixels kan lezen. Aspose’s `OcrEngine` ondersteunt veel formaten, maar hier richten we ons op TIFF omdat dat het meest voorkomt bij gescande facturen.

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Pro tip:** Als je met multi‑page TIFF’s werkt, verwerkt Aspose automatisch elke pagina achter elkaar, zodat je geen extra loops nodig hebt.

Nu de afbeelding is geladen, voeren we een basis‑herkenningspassage uit.

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

Je ziet iets als:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Merk je de *nullen* vóór de letters op? Dat is een klassiek OCR‑artefact dat we later zullen opruimen.

![basis ocr python workflow](/images/ocr-workflow.png "basis ocr python workflow diagram")

---

## Stap 2: Converteer TIFF naar tekst – bereid de AI‑nabewerker voor

Ruwe OCR is nuttig, maar de meeste productiepijplijnen hebben een gepolijste versie nodig. Aspose biedt een `AsposeAI`‑wrapper die een model van Hugging Face kan downloaden, op de GPU kan draaien en automatisch spell‑check toepast.

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

### Waarom `set GPU layers` belangrijk is

De parameter `gpu_layers` vertelt het onderliggende GGUF‑model hoeveel transformer‑lagen op de GPU moeten blijven. Meer lagen = snellere inferentie maar hoger VRAM‑verbruik. Als je een bescheiden laptop hebt, verlaag de waarde naar `10` of laat het helemaal weg om op CPU te blijven.

---

## Stap 3: Spell‑check toepassen en **leidende nullen corrigeren**

Aspose AI wordt geleverd met een ingebouwde spell‑checker, die de meeste Engelse spelfouten vangt. Domeinspecifieke correcties—zoals een leidende `0` omzetten naar een `O` voor factuurcodes—vereisen een aangepaste nabewerker.

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

> **Waarom dit werkt:** De reguliere expressie zoekt naar een woordgrens (`\b`), een nul, gevolgd door precies drie hoofdletters. Vervolgens vervangt hij de nul door de letter “O”. Je kunt het patroon uitbreiden voor andere eigenaardigheden (bijv. `0[0-9]{2}` voor verkeerd gelezen cijfers).

---

## Stap 4: OCR‑resultaat opschonen met de AI‑nabewerker

Nu combineren we alles: de ruwe string van **basic ocr python**, de spell‑check en onze nul‑correctie. De methode `run_postprocessor` retourneert een opgeschoonde versie die klaar is voor downstream‑systemen.

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

Typische output na de nabewerker:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Je ziet dat de leidende nul is omgezet naar een `O`, en veelvoorkomende spelfouten zijn gecorrigeerd. De tekst is nu geschikt voor indexering in een zoekmachine of voor invoer in een data‑extractiepijplijn.

---

## Stap 5: AI‑bronnen vrijgeven – houd je GPU tevreden

Als je meerdere OCR‑taken draait in een langdurige service, is het goed om het GPU‑geheugen van het model vrij te geven wanneer je klaar bent.

```python
ocr_ai.free_resources()
```

Het overslaan van deze stap kan leiden tot “out‑of‑memory”‑fouten bij volgende oproepen, vooral wanneer **GPU‑lagen** op een hoge waarde zijn ingesteld.

---

## Optionele variaties & randgevallen

| Situatie | Wat te wijzigen |
|-----------|----------------|
| **Handgeschreven documenten** | Gebruik `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` in plaats van `PRINTED`. |
| **Geen GPU beschikbaar** | Stel `gpu_layers=0` in of laat het argument weg; het model draait dan op CPU (trager maar veilig). |
| **Andere taal** | Vervang de Hugging Face repo‑ID door een taalspecifiek model, bijv. `microsoft/Florence-2-base`. |
| **Batchverwerking** | Plaats de stappen in een `for file in glob("*.tif"):`‑loop en verzamel resultaten in een lijst of CSV. |
| **Complexere nul‑patronen** | Breid `invoice_fix` uit met extra regexes, zoals `r"\b0+([A-Z]{2,})\b"` voor meerdere leidende nullen. |

---

## Conclusie

We hebben zojuist een **basic ocr python**‑pipeline voltooid die een TIFF laadt, ruwe tekst extraheert en vervolgens opschoont met een AI‑model terwijl **GPU‑lagen** worden ingesteld voor betere prestaties. De aangepaste nabewerker laat zien hoe je **leidende nullen** corrigeert, een klein maar vaak over het hoofd gezien detail dat downstream‑analyses kan breken.

Voel je vrij om te experimenteren: probeer een andere kwantisatie (`float16` voor hogere nauwkeurigheid), vervang de spell‑check door een domeinspecifiek woordenboek, of koppel meerdere aangepaste correcties aan elkaar. Het patroon blijft hetzelfde—laden, herkennen, AI configureren, nabewerken en opruimen.

**Volgende stappen** die je kunt verkennen:

- De opgeschoonde output integreren met een database of Elasticsearch‑index.  
- Dezelfde aanpak gebruiken om **TIFF naar tekst** te **converteren** voor meertalige PDF’s.  
- Een UI toevoegen met Flask of FastAPI zodat niet‑technische gebruikers bestanden kunnen uploaden en direct opgeschoonde tekst ontvangen.  

Happy coding, en moge je OCR‑resultaten altijd scherp en nul‑vrij zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}