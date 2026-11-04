---
category: general
date: 2026-01-07
description: Hogyan futtassuk az OCR-t és nyerjünk ki szöveget a képből a számlafeldolgozáshoz.
  Tanulja meg, hogyan javíthatja az OCR pontosságát, hogyan tölthet be képet az OCR-hez,
  és hogyan dolgozhatja fel hatékonyan a számlák OCR-ét.
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: hu
og_description: Hogyan hajtsunk végre OCR-t számlákon lépésről lépésre. Szöveg kinyerése
  képből, az OCR pontosságának javítása, és kép betöltése OCR-hez az Aspose AI használatával.
og_title: Hogyan hajtsunk végre OCR-t számlákon – Teljes Python útmutató
tags:
- OCR
- Python
- Image Processing
title: Hogyan végezzünk OCR-t számlákon – Szöveg kinyerése képből Python segítségével
url: /hu/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan futtassunk OCR-t számlákon – Szöveg kinyerése képből Python segítségével

Gondolkodtál már azon, **hogyan futtassunk OCR-t** egy beolvasott számlán, és kapjunk tiszta, kereshető szöveget? Nem vagy egyedül. Sok fejlesztő akad el, amikor a nyers OCR kimenet tele van helyesírási hibákkal, törött sortörésekkel és hiányzó írásjelekkel. Ebben az útmutatóban egy teljes körű megoldáson keresztül vezetünk, amely nem csak **kivonja a szöveget a képből**, hanem **javítja az OCR pontosságát** egy Aspose AI modell utófeldolgozásával.

Megmutatjuk, hogyan **töltsünk be képet OCR-hez**, futtassuk a beépített motort, majd alkalmazzunk egy könnyű helyesírás-ellenőrzést, amely a végeredményt készen állóvá teszi a további elemzésekhez. A végére egy újrahasználható szkriptet kapsz, amely bármely számlafeldolgozó csővezetékbe beilleszthető.

> **Amire szükséged lesz**  
> * Python 3.9 vagy újabb  
> * `aspose-ocr` és `aspose-ai` csomagok (pip‑el telepítve)  
> * Egy számla kép (PNG, JPEG vagy TIFF) – példaként a `sample_invoice.png`‑t használjuk  
> * Opcionális: GPU legalább 4 GB VRAM‑mal a gyorsabb modellinferencia érdekében (a szkript CPU‑n is működik)

---

## 1. lépés: Szükséges csomagok telepítése és a környezet előkészítése

Mielőtt **betölthetnénk a képet OCR-hez**, biztosítanunk kell, hogy a szükséges könyvtárak elérhetők legyenek. Az Aspose OCR motor egy egyszerű Python wrapperrel érkezik, míg az AI utófeldolgozó egy Hugging Face kvantált modellen alapul.

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **Pro tipp:** Ha GPU gyorsítást tervezel, telepítsd a `torch`‑ot CUDA támogatással (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

---

## 2. lépés: A számla kép betöltése

A kép betöltése egyszerű, de érdemes megemlíteni, miért állítjuk be a fájlútvonalat explicit módon raw stringként (`r"..."`). Ez megakadályozza a véletlen escape‑karakter hibákat Windows útvonalaknál.

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*Miért fontos:* Az `ocr.Image.load` használata garantálja, hogy a kép előfeldolgozása (binarizálás, kiegyenesítés) az Aspose optimális alapértelmezései szerint történik, ami már **javítja az OCR pontosságát** mielőtt bármilyen AI varázslat bekövetkezne.

---

## 3. lépés: A beépített OCR motor futtatása

Most ténylegesen **futtatjuk az OCR-t**, és elkapjuk a nyers szöveget. Ez a lépés mutatja a tipikus kimenetet, amit egy alap OCR futtatás ad – gyakran egy sorok és időnként helyesírási hibákkal teli káosz.

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**Tipikus nyers kimenet** (rövidítve a tömörség kedvéért):

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Észreveheted, hogy az „Invoice” „Invo1ce”‑ként jelenik meg, vagy hogy hiányoznak az írásjelek. Itt lép be az AI utófeldolgozó.

---

## 4. lépés: Az Aspose AI modell konfigurálása

Az általunk használt AI modell **Qwen2.5‑3B‑Instruct‑GGUF**, egy könnyű, instrukcióra finomhangolt LLM, amely kényelmesen fut egy középkategóriás GPU‑n. Az alábbi konfiguráció megmondja az Aspose‑nak, hol töltse le a modellt, hány réteget tartson a GPU‑n, és mekkora legyen a kontextusméret a hosszú bekezdések kezelése érdekében.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **Miért ez a konfiguráció?**  
> * `gpu_layers=30` egyensúlyt teremt a sebesség és a memória között – a legtöbb inferencia a GPU‑n történik, míg a maradék rétegek a CPU‑n maradnak, hogy elkerüljük az OOM hibákat.  
> * `context_size=4096` biztosítja, hogy a modell egyszerre lássa az egész számlát, megakadályozva a fontos mezők levágását.

---

## 5. lépés: Egyszerű helyesírás-ellenőrző utófeldolgozó létrehozása

Egy kis függvénybe csomagoljuk az AI hívást, amelyet `simple_spell_check`‑nek nevezünk. A prompt szándékosan tömör: „Correct spelling and punctuation:” (Javítsd a helyesírást és az írásjeleket:) a nyers OCR szöveg után. A modell egy megtisztított változatot ad vissza.

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**Hogyan működik:** Az `ai.run_prompt` elküldi a promptot a helyben betöltött LLM‑nek, amely egyetlen stringet ad vissza javított helyesírással, megfelelő írásjelekkel és természetesebb sortöréssel.

---

## 6. lépés: Az utófeldolgozó alkalmazása a nyers OCR szövegre

Most jön a varázslat. A nyers OCR kimenetet betápláljuk az utófeldolgozóba, és kiírjuk a javított eredményt.

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**Minta javított kimenet**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Figyeld meg a javított „Invoice” helyesírást, a megfelelő kettőspont használatot és a konzisztens sortöréseket – pontosan ami a megbízható downstream elemzéshez szükséges.

---

## 7. lépés: Erőforrások felszabadítása

Mind az OCR motor, mind az AI modell natív erőforrásokat foglal le. Jó gyakorlat ezeket felszabadítani, amikor már nincs rájuk szükség, különösen hosszú‑távú szolgáltatások esetén.

```python
ai.free_resources()
engine.dispose()
```

---

## Teljes szkript – Kész a beillesztéshez

Az alábbiakban a komplett, futtatható szkriptet találod, amely minden lépést összekapcsol. Mentsd `invoice_ocr.py`‑ként, cseréld le a `YOUR_DIRECTORY`‑t a számla képedet tartalmazó mappára, és futtasd `python invoice_ocr.py`‑val.

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

Futtasd a szkriptet, és mind a zajos nyers OCR dumpot, mind a polírozott, **javított OCR pontosságú** verziót egyszerre láthatod.

---

## Gyakran ismételt kérdések és széljegyek

### 1. Mi van, ha a számla kép egy többoldalas PDF?

Az Aspose OCR közvetlenül be tudja tölteni a PDF oldalakat. Cseréld le a képbetöltő sort a következőre:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

Iterálj a `page_index`‑en, hogy minden oldalt sorban feldolgozz.

### 2. A GPU-m elfogy a memóriából – használhatok csak CPU‑t?

Természetesen. Állítsd `gpu_layers=0`‑ra az `AsposeAIModelConfig`‑ban. A modell teljesen a CPU‑n fut, ami lassabb, de biztonságos alacsony teljesítményű hardveren.

### 3. Hogyan kezelem a nem‑angol nyelvű számlákat?

Cseréld le a modell repository ID‑t egy nyelvspecifikus modellre, például `"mistralai/Mistral-7B-Instruct-v0.2"` a többnyelvű támogatáshoz. A pipeline többi része változatlan marad.

### 4. Láncolhatok több utófeldolgozót (pl. dátumformázás, összegek kinyerése)?

Igen. Az `ai.set_post_processor` elfogad egy listát a callable‑okból. Például:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

Az output először helyesírás‑ellenőrzésen, majd összeg‑kivonáson megy keresztül.

---

## Teljesítmény tippek és legjobb gyakorlatok

| Tipp | Miért segít |
|-----|---------------|
| **Több számla batch‑elése** – töltsd be őket listába, és dolgozd fel egy ciklusban. | Csökkenti a Python interpreter overhead‑et és melegen tartja az AI modellt a memóriában. |
| **Modell cache‑elése** – kerüld az `initialize` ismételt hívását egy webszolgáltatásban. | A modell betöltése ~30 másodpercet vehet igénybe; a cache‑elés azonnali válaszokat eredményez. |
| **Nagy képek átméretezése** 1500 px szélességre OCR előtt. | A kisebb képek felgyorsítják mind az OCR‑t, mind az AI inferenciát anélkül, hogy pontosságot veszítenének. |
| **Állítsd `allow_auto_download="false"`-ra production‑ben** – szállítsd a modellt a telepítéssel együtt. | Biztosítja a determinisztikus indítási időket és elkerüli a hálózati problémákat. |

---

## Összegzés

Áttekintettük, **hogyan futtassunk OCR-t** számlákon, a kép betöltésétől a AI‑vezérelt helyesírás‑ellenőrzővel való polírozásig. Ezeket a lépéseket követve megbízhatóan **kivonhatod a szöveget a képből**, **javíthatod az OCR pontosságát**, és zökkenőmentesen **feldolgozhatod a számla OCR‑t** bármely Python‑alapú munkafolyamatban.

Próbáld ki néhány különböző számla elrendezéssel – akár kézzel írt blokkot vagy beolvasott szerződést. Ugyanaz a pipeline minimális módosítással alkalmazkodik, bizonyítva, hogy egy jól felépített OCR + AI kombináció sokoldalú eszköz bármely dokumentum‑automatizálási projekthez.

Ha hasznosnak találtad ezt az útmutatót, oszd meg a csapatoddal, vagy csillagozd a repót, amely az Aspose csomagokat tartalmazza

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}