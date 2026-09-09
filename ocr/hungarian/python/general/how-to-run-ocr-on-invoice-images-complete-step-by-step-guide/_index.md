---
category: general
date: 2026-01-12
description: Hogyan futtassunk OCR-t és nyerjünk ki szöveget számlaképekről az Aspose
  OCR és egy könnyű Hugging Face modell segítségével. Tanulja meg a modell letöltését,
  az OCR hibáinak javítását, és az OCR végrehajtását a képen.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: hu
og_description: Hogyan futtass OCR-t számla képeken, nyerd ki a szöveget, és javítsd
  ki a hibákat egy Hugging Face LLM-mel. Kövesd ezt a teljes útmutatót a hibátlan
  eredményekért.
og_title: Hogyan végezzünk OCR-t számla képeken – Teljes útmutató
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: Hogyan futtassunk OCR‑t számlaképeken – Teljes lépésről‑lépésre útmutató
url: /hu/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan futtassunk OCR-t számla képeken – Teljes lépésről‑lépésre útmutató

Gondolkodtál már azon, **hogyan futtassunk OCR-t** egy beolvasott számlán, és kapjunk tiszta, kereshető szöveget anélkül, hogy órákat töltenénk a tisztítással? Nem vagy egyedül. Sok valós projektben a nyers OCR‑kimenet tele van hibákkal – például “O” helyett “0”, “l” helyett “1”, vagy akár teljesen összekevert szavak. A jó hír? Néhány Python sorral nem csak **képfájlokon végezhetünk OCR‑t**, hanem automatikusan **javíthatjuk az OCR‑hibákat** egy könnyű modell segítségével a Hugging Face‑ről.

Ebben a tutorialban mindent végigvázolunk, amire szükséged van: egy számla kép betöltésétől, a nyers szöveg kinyeréséig, egy kvantált modell letöltéséig, egészen a végeredmény finomításáig, hogy egy tökéletes transzkripcióval zárhass, amely készen áll a további feldolgozásra. A végére képes leszel **szöveget kinyerni számla** PDF‑ekből vagy PNG‑kből egyetlen, újrahasználható szkript segítségével.

## Előfeltételek és beállítás

Mielőtt belevágnánk, győződj meg róla, hogy rendelkezel a következőkkel:

| Követelmény | Miért fontos |
|-------------|--------------|
| Python 3.9+ | Modern szintaxis és típusjelölések |
| `aspose-ocr` csomag | Biztosítja a példában használt `ocr.OcrEngine`‑t |
| `aspose-ai` csomag | Szolgáltatja az `AsposeAI` post‑processzort |
| GPU elérés (opcionális) | Gyorsítja az LLM rétegeket; CPU is működik |
| Internetkapcsolat (első futtatás) | Szükséges a **Hugging Face modell letöltéséhez** automatikusan |

A szükséges könyvtárak telepíthetők a következővel:

```bash
pip install aspose-ocr aspose-ai
```

> **Pro tipp:** Ha GPU‑n szeretnéd futtatni az LLM‑et, telepítsd a `torch`‑ot CUDA‑támogatással (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

Most, hogy a környezet készen áll, vágjunk bele a kódba.

---

## 1. lépés – Az OCR motor inicializálása és a számla kép betöltése

Az első dolog, amit meg kell tenned, hogy létrehozz egy példányt az Aspose OCR motorjából, és rámutass a feldolgozni kívánt fájlra. Ez a lépés a **hogyan futtassunk OCR‑t** bármilyen képen alapja.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Miért fontos:** A `load_image` PNG, JPEG, TIFF és még PDF‑oldalakat is elfogad, így **képen végezhetünk OCR‑t** a formátumtól függetlenül.

---

## 2. lépés – Alap OCR futtatása a nyers szöveg rögzítéséhez

Miután a kép betöltődött, a motor képes nyers transzkripciót előállítani. Ez a kimenet gyakran zajos, ezért később egy javító lépést fogunk alkalmazni.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

A tipikus nyers kimenet így nézhet ki:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

Észrevetted a nullákat (`0`) ott, ahol a számjegy “O”-nak kellene lennie? Pont ezt a hibát fogjuk később kijavítani.

---

## 3. lépés – Az AI post‑processzor beállítása egy könnyű LLM‑mel

Most hozunk be egy **Hugging Face modell letöltését**, amely elég kicsi ahhoz, hogy szerény hardveren fusson, de elég erős ahhoz, hogy megértse a számlák nyelvezetét. A példában a Qwen 2.5 3B‑Instruct GGUF modellt használjuk, `int8` kvantálással a kis memóriaigény érdekében.

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

> **Miért ez a modell?** Az `int8` kvantálás a fájlt ~1,2 GB‑ra csökkenti, ami a legtöbb laptopon is megvalósítható. A GPU rétegek felgyorsítják az inferenciát, de a kód automatikusan visszaesik CPU‑ra, ha nincs GPU.

---

## 4. lépés – LLM‑alapú javítás futtatása a nyers OCR eredményen

A modell készen áll, most a nyers szöveget adjuk át a post‑processzornak. Az LLM átírja a transzkripciót, kijavítja a gyakori OCR‑hibákat és normalizálja a számokat.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

Várható tisztított kimenet:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

Láthatod, hogy a nullák visszaalakultak betűvé “O”, és az “Am0unt” most már “Amount”. Ez a **OCR‑hibák automatikus javításának** magja.

---

## 5. lépés – Erőforrások felszabadítása és takarítás

A nagy nyelvi modellek megtarthatják a GPU‑memóriát, ezért jó gyakorlat a források felszabadítása a munka befejezése után.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

Ha sok számlát szeretnél kötegelt módon feldolgozni, a modellt betöltve tarthatod, és csak a szkript végén szabadíthatod fel.

---

## Teljes működő példa

Mindent összerakva, itt egy egyetlen szkript, amelyet `.py` fájlba menthetsz és futtathatsz:

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

A szkript futtatása hasonló kimenetet kell, hogy eredményezzen, mint a korábban bemutatott „AI‑javított” blokk. Nyugodtan cseréld le a kép útvonalát bármely más számlára vagy nyugtára, hogy **szöveget nyerj ki számla** fájlokból tömegesen.

---

## Gyakran Ismételt Kérdések és Szélsőséges Esetek

### Mi van, ha nincs GPU‑m?

A `gpu_layers` paraméter opcionális. Állítsd `0`‑ra vagy hagyd el, és a modell teljesen CPU‑n fog futni. Lassabb lesz az inferencia – nagyjából 2–3 másodperc oldalanként egy modern laptopon.

### A számláim többoldalas PDF‑ek. Hogyan kezeljem őket?

Alakítsd át minden oldalt külön képpé (pl. a `pdf2image` használatával), majd a script ugyanazzal a ciklussal dolgozd fel az oldalakat. Az OCR motor minden képet önállóan képes feldolgozni, az LLM pedig minden szövegrészt javít.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### A modell letöltése tűzfal mögött sikertelen?

Töltsd le a modellt manuálisan a Hugging Face modellközpontból, csomagold ki egy helyi mappába, és állítsd be a `hugging_face_repo_id`‑t a helyi útvonalra:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### Mennyire pontos a javítás?

Tipikus angol nyelvű számlák esetén az LLM >95 %-ban javítja a gyakori OCR‑felismerési hibákat. A komplex kézírásos megjegyzések még mindig igényelhetnek manuális ellenőrzést.

---

## Tippek és trükkök a termeléshez

- **Kötegelt feldolgozás:** Csomagold a 2‑4. lépéseket egy függvénybe, és add át a fájlútvonalak listáját. Használd újra ugyanazt az `AsposeAI` példányt a modell újratöltésének elkerülése érdekében.
- **Naplózás:** Cseréld le a `print`‑et a Python `logging` moduljára, hogy a nyers és a javított kimeneteket is rögzítsd auditálási célokra.
- **Hibakezelés:** Tekerj `try/except` blokkokat az OCR hívás köré. Ha egy kép hibát jelez, naplózd a fájlnevet és folytasd.
- **Teljesítményhangolás:** Kísérletezz a `gpu_layers`‑számmal. Több GPU‑réteg gyorsítja az inferenciát, de több VRAM‑et igényel.

---

## Összegzés

Áttekintettük, **hogyan futtassunk OCR‑t** számla képeken a kezdetektől a befejezésig, bemutatva, hogyan **végezzünk OCR‑t képen**, **töltsünk le Hugging Face modellt**, és **javítsuk automatikusan az OCR‑hibákat**. A teljes szkript egy gyakorlati munkafolyamatot mutat be, amelyet bármely Python‑alapú automatizálási pipeline‑ba be lehet illeszteni.

Mi a következő lépés? Próbáld meg kiterjeszteni a folyamatot **kulcsmezők kinyerésére** (számlaszám, dátum, összeg) reguláris kifejezésekkel a javított szövegen, vagy a tisztított kimenetet egy adatbázisba táplálni kereshető rekordokként. Kísérletezhetsz más könnyű LLM‑ekkel a Hugging Face‑ről, ha más nyelvre vagy domain‑specifikus tudásra van szükséged.

Boldog kódolást, és legyen az OCR‑eredményed mindig kristálytiszta!

![hogyan futtassunk OCR-t egy számla képen](ocr_invoice_example.png "hogyan futtassunk OCR-t egy számla képen")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}