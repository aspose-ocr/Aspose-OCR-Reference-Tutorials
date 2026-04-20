---
category: general
date: 2026-03-18
description: Alap OCR Python oktatóanyag bemutatja, hogyan konvertáljunk TIFF-et szöveggé,
  töltsünk be képet OCR-rel, állítsuk be a GPU rétegeket, és javítsuk a vezető nullákat
  az Aspose AI segítségével.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: hu
og_description: Az alap OCR Python oktatóanyag lépésről lépésre végigvezet a TIFF
  fájlok tiszta szöveggé konvertálásán, képek betöltésén, GPU rétegek beállításán
  és az előre álló nullák javításán.
og_title: Alap OCR Python – TIFF átalakítása szöveggé
tags:
- OCR
- Python
- AI
- Aspose
title: Alap OCR Python – TIFF konvertálása szöveggé
url: /hu/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – TIFF konvertálása szöveggé AI utófeldolgozással

Keresel egy módot, hogy **basic ocr python**‑t alkalmazz a beolvasott dokumentumaidon? Ebben az útmutatóban végigvezetünk a TIFF fájl tiszta, kereshető szöveggé alakításán az Aspose OCR és egy AI utófeldolgozó segítségével.  

Ha már valaha is nehezen tudtad **convert TIFF to text**, mert a nyers kimenet tele van hibákkal vagy furcsa szimbólumokkal, nem vagy egyedül. Megmutatjuk, hogyan **load image OCR**, hogyan állítsd be a **set GPU layers** paramétert, és még a számlaszámokban gyakran előforduló **fix leading zeroes**‑t is megoldjuk.

## What You’ll Learn

- Hogyan inicializáld az Aspose OCR motorját nyomtatott dokumentumokhoz.  
- A pontos lépések a **load image OCR** elvégzéséhez TIFF fájlból és a nyers szöveg lekéréséhez.  
- AI modell konfigurálása, automatikus letöltése, és **setting GPU layers** a gyorsabb inferenciáért.  
- Beépített helyesírás-ellenőrzés hozzáadása plusz egy egyedi függvény, amely **fixes leading zeroes**.  
- Az OCR eredmény tisztítása és a erőforrások megfelelő felszabadítása.  

A tutorial végére egyetlen, újrahasználható Python szkriptet kapsz, amely bármely TIFF‑et átalakít csiszolt, kereshető szöveggé – manuális másolás‑beillesztés nélkül.  

### Prerequisites

- Python 3.8+ telepítve a gépeden.  
- `aspose-ocr` csomag (`pip install aspose-ocr`).  
- Opcionális: GPU legalább 4 GB VRAM‑mal, ha **set GPU layers**‑t szeretnél használni; egyébként a kód automatikusan CPU‑ra vált.  

---

## basic ocr python – load image and recognize text

Az első dolog, amit tennünk kell, a **load image OCR**, hogy a motor olvasni tudja a pixeleket. Az Aspose `OcrEngine` sok formátumot kezel, de itt a TIFF‑re fókuszálunk, mivel ez a leggyakoribb a beolvasott számlák esetén.

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Pro tip:** Ha többoldalas TIFF‑ekkel dolgozol, az Aspose automatikusan sorban feldolgozza az egyes oldalakat, így nem kell extra ciklusokat írnod.

Miután a kép betöltődött, futtassunk egy alapvető felismerési lépést.

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

A kimenet valami ilyesmi lesz:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Észrevetted a *nullákat* a betűk előtt? Ez egy klasszikus OCR‑artefakt, amit később tisztítunk.

![basic ocr python workflow](/images/ocr-workflow.png "basic ocr python munkafolyamat diagramja")

---

## Step 2: Convert TIFF to text – prepare the AI post‑processor

A nyers OCR hasznos, de a legtöbb termelési folyamat egy csiszolt változatot igényel. Az Aspose egy `AsposeAI` wrapper‑t biztosít, amely letölthet egy modellt a Hugging Face‑ről, GPU‑n futtatja, és automatikusan alkalmaz helyesírás-ellenőrzést.

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

### Why `set GPU layers` matters

A `gpu_layers` paraméter azt mondja meg az alatta lévő GGUF modellnek, hány transformer réteget tartson a GPU‑n. Több réteg = gyorsabb inferencia, de nagyobb VRAM‑használat. Ha egy szerény laptopod van, csökkentsd az értéket `10`‑re vagy hagyd el teljesen, hogy CPU‑n maradjon.

---

## Step 3: Apply spellcheck and **fix leading zeroes**

Az Aspose AI beépített helyesírás-ellenőrzővel érkezik, amely a legtöbb angol elírást elkapja. Azonban a domain‑specifikus javítások – például egy vezető `0` `O`‑ra cserélése számlakódoknál – egyedi utófeldolgozót igényelnek.

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

> **Why this works:** A reguláris kifejezés egy szóhatárt (`\b`), egy nullát, majd pontosan három nagybetűt keres. Ezután a nullát az “O” betűre cseréli. A mintát kiterjesztheted más sajátosságokra is (pl. `0[0-9]{2}` a félreolvasott számokhoz).

---

## Step 4: Clean the OCR result with the AI post‑processor

Most mindent összevonunk: a **basic ocr python**‑ből származó nyers stringet, a helyesírás-ellenőrzést és a nulla‑javítást. A `run_postprocessor` metódus egy megtisztított verziót ad vissza, amely készen áll a downstream rendszereknek.

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

Tipikus kimenet az utófeldolgozó után:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Láthatod, hogy a vezető nulla `O`‑ra változott, és a gyakori elírások javítva lettek. A szöveg most már alkalmas keresőmotor indexelésére vagy adatkinyerő pipeline‑ba való betáplálásra.

---

## Step 5: Release AI resources – keep your GPU happy

Ha több OCR feladatot futtatsz egy hosszú élettartamú szolgáltatásban, jó gyakorlat a modell GPU‑memóriájának felszabadítása a munka befejezése után.

```python
ocr_ai.free_resources()
```

Ennek kihagyása “out‑of‑memory” hibákat okozhat a későbbi hívásoknál, különösen ha **set GPU layers**‑t magas értékre állítottad.

---

## Optional Variations & Edge Cases

| Situation | What to change |
|-----------|----------------|
| **Handwritten documents** | Use `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` instead of `PRINTED`. |
| **No GPU available** | Set `gpu_layers=0` or omit the argument; the model will run on CPU (slower but safe). |
| **Different language** | Swap the Hugging Face repo ID to a language‑specific model, e.g., `microsoft/Florence-2-base`. |
| **Batch processing** | Wrap the steps in a `for file in glob("*.tif"):` loop and accumulate results in a list or CSV. |
| **More complex zero patterns** | Extend `invoice_fix` with additional regexes, such as `r"\b0+([A-Z]{2,})\b"` for multiple leading zeroes. |

---

## Conclusion

Épp most fejeztük be a **basic ocr python** pipeline‑t, amely betölti a TIFF‑et, nyers szöveget nyer ki, majd egy AI modell segítségével tisztítja, miközben **setting GPU layers**‑t használ a teljesítményért. Az egyedi utófeldolgozó bemutatja, hogyan **fix leading zeroes**, egy apró, de gyakran figyelmen kívül hagyott részlet, amely megzavarhatja a downstream elemzéseket.

Nyugodtan kísérletezz: próbálj ki más kvantálást (`float16` a magasabb pontosságért), cseréld le a helyesírás-ellenőrzőt egy domain‑specifikus szótárra, vagy láncolj több egyedi javítást egymás után. A minta ugyanaz marad – load, recognize, configure AI, post‑process, and clean up.

**Next steps** you might explore include:

- Integrating the cleaned output with a database or Elasticsearch index.  
- Using the same approach to **convert TIFF to text** for multi‑language PDFs.  
- Adding a UI with Flask or FastAPI so non‑technical users can upload files and receive cleaned text instantly.  

Happy coding, and may your OCR results always be crisp and zero‑free!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}