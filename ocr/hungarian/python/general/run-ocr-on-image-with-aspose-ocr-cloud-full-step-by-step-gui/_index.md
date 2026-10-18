---
category: general
date: 2026-03-28
description: Tanulja meg, hogyan futtasson OCR-t képen, automatikusan töltse le a
  Hugging Face modellt, tisztítsa meg az OCR‑szöveget, és konfigurálja az LLM modellt
  Pythonban az Aspose OCR Cloud használatával.
draft: false
keywords:
- run OCR on image
- download hugging face model
- clean OCR text
- configure LLM model
language: hu
og_description: Futtass OCR-t a képen, és tisztítsd meg a kimenetet egy automatikusan
  letöltött Hugging Face modellel. Ez az útmutató bemutatja, hogyan konfigurálj LLM
  modellt Pythonban.
og_title: OCR futtatása képen – Teljes Aspose OCR Cloud útmutató
tags:
- OCR
- Python
- LLM
- HuggingFace
title: OCR futtatása képen az Aspose OCR Cloud használatával – Teljes lépésről‑lépésre
  útmutató
url: /hu/python/general/run-ocr-on-image-with-aspose-ocr-cloud-full-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép OCR futtatása – Teljes Aspose OCR Cloud bemutató

Volt már szükséged arra, hogy képfájlokon OCR-t futtass, de a nyers kimenet egy összegabalyodott kusza szövegnek tűnt? Tapasztalatom szerint a legnagyobb gond nem maga a felismerés – a tisztítás. Szerencsére az Aspose OCR Cloud lehetővé teszi, hogy egy LLM post‑processzort csatolj, amely automatikusan *tisztítja az OCR szöveget*. Ebben a bemutatóban végigvezetünk mindenen, amire szükséged van: a **Hugging Face modell letöltésétől** a LLM konfigurálásáig, az OCR motor futtatásáig, és végül az eredmény finomításáig.

A végére egy kész‑futtatható szkriptet kapsz, amely:

1. Letölti a kompakt Qwen 2.5 modellt a Hugging Face‑ről (automatikusan letöltve számodra).  
2. Beállítja a modellt úgy, hogy a hálózat egy részét GPU-n, a maradékot CPU-n futtassa.  
3. Végrehajtja az OCR motort egy kézzel írott jegyzet képen.  
4. Az LLM-et használja a felismert szöveg tisztítására, emberi olvasásra alkalmas kimenetet biztosítva.

> **Előfeltételek** – Python 3.8+, `asposeocrcloud` csomag, legalább 4 GB VRAM-mal rendelkező GPU (opcionális, de ajánlott), valamint internetkapcsolat az első modell letöltéséhez.

---

## Amire szükséged lesz

- **Aspose OCR Cloud SDK** – telepítés: `pip install asposeocrcloud`.  
- **Minta kép** – például `handwritten_note.jpg`, helyi mappában.  
- **GPU támogatás** – ha CUDA‑támogatott GPU-d van, a script 30 réteget áthelyez a GPU-ra; egyébként automatikusan CPU-ra vált.  
- **Írási jogosultság** – a script a modellt a `YOUR_DIRECTORY` könyvtárban tárolja; győződj meg róla, hogy a mappa létezik.

---

## 1. lépés – Az LLM modell konfigurálása (Hugging Face modell letöltése)

Az első dolog, amit teszünk, hogy megmondjuk az Aspose AI‑nek, honnan töltse le a modellt. A `AsposeAIModelConfig` osztály kezeli az automatikus letöltést, kvantálást és a GPU rétegek kiosztását.

```python
import asposeocrcloud as ocr
from asposeocrcloud.ai import AsposeAI, AsposeAIModelConfig

# ----------------------------------------------------------------------
# Step 1: Model configuration – this will download the model if it’s missing
# ----------------------------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                           # Enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF", # Repo on Hugging Face
    hugging_face_quantization="int8",                     # Small footprint, fast inference
    gpu_layers=30,                                        # 30 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY"               # Cache folder (optional)
)
```

**Miért fontos** – Az `int8` kvantálás jelentősen csökkenti a memóriahasználatot (≈ 4 GB vs 12 GB). A modell GPU és CPU közötti felosztása lehetővé teszi, hogy egy 3 milliárd paraméteres LLM-et futtass még egy közepes RTX 3060-on is. Ha nincs GPU-d, állítsd be a `gpu_layers=0` értéket, és az SDK mindent CPU-n tart.

> **Tipp:** Az első futtatás ~ 1,5 GB-ot tölt le, ezért adj neki néhány percet és stabil kapcsolatot.

---

## 2. lépés – Az AI motor inicializálása a modell konfigurációval

Most elindítjuk az Aspose AI motort, és átadjuk neki a frissen létrehozott konfigurációt.

```python
# ----------------------------------------------------------------------
# Step 2: Initialise the AI engine – pulls the model if needed
# ----------------------------------------------------------------------
ocr_ai = AsposeAI()
ocr_ai.initialize(model_config)  # This call blocks until the model is ready
```

**Mi történik a háttérben?** Az SDK ellenőrzi a `directory_model_path`-t, hogy van-e már meglévő modell. Ha megtalálja a megfelelő verziót, azonnal betölti; ellenkező esetben letölti a GGUF fájlt a Hugging Face‑ről, kicsomagolja, és előkészíti az inferencia csővezetéket.

---

## 3. lépés – OCR motor létrehozása és az AI post‑processzor csatolása

Az OCR motor végzi a karakterfelismerés nehéz munkáját. A `ocr_ai.run_postprocessor` csatolásával automatikusan engedélyezzük a **tisztított OCR szöveget** a felismerés után.

```python
# ----------------------------------------------------------------------
# Step 3: Build the OCR engine and bind the LLM post‑processor
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=None)
```

**Miért használjunk post‑processzort?** A nyers OCR gyakran tartalmaz rossz helyen lévő sortöréseket, hibásan felismert írásjeleket vagy felesleges szimbólumokat. Az LLM átírhatja a kimenetet helyes mondatokra, javíthatja a helyesírást, sőt hiányzó szavakat is kitalálhat – lényegében egy nyers dumpot átalakít szép szöveggé.

---

## 4. lépés – OCR futtatása képfájlon

Miután minden összekapcsoltuk, itt az ideje, hogy egy képet adjon a motorhoz.

```python
# ----------------------------------------------------------------------
# Step 4: Load the image and run OCR
# ----------------------------------------------------------------------
input_image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
raw_result = ocr_engine.recognize(input_image)   # Returns an OcrResult object
```

**Szélsőséges eset:** Ha a kép nagy (> 5 MP), érdemes előbb átméretezni a feldolgozás felgyorsítása érdekében. Az SDK elfogad egy Pillow `Image` objektumot, így szükség esetén előfeldolgozhatod a `PIL.Image.thumbnail()`‑val.

---

## 5. lépés – Engedjük, hogy az AI megtisztítsa a felismert szöveget és mutassa mindkét változatot

Végül meghívjuk a korábban csatolt post‑processzort. Ez a lépés bemutatja a *tisztítás előtti* és *utáni* különbséget.

```python
# ----------------------------------------------------------------------
# Step 5: Clean the OCR output using the LLM and display both results
# ----------------------------------------------------------------------
cleaned_result = ocr_engine.run_postprocessor(raw_result)

print("=== Before AI ===")
print(raw_result.text)

print("\n=== After AI ===")
print(cleaned_result.text)
```

### Várható kimenet

```
=== Before AI ===
Th1s 1s a h@ndwr1tt3n n0te.  It c0nta1ns m1st@k3s, l1n3 br3aks, & sp3c!@l ch@r@ct3rs.

=== After AI ===
This is a handwritten note. It contains mistakes, line breaks, and special characters.
```

Figyeld meg, hogy az LLM:

- Kijavította a gyakori OCR hibákat (`Th1s` → `This`).  
- Eltávolította a felesleges szimbólumokat (`&` → `and`).  
- Normalizálta a sortöréseket helyes mondatokká.

---

## 🎨 Vizuális áttekintés (OCR futtatása képen munkafolyamat)

![OCR futtatása képen munkafolyamat](run_ocr_on_image_workflow.png "Diagram, amely bemutatja az OCR futtatása képen csővezetékét a modell letöltésétől a tisztított kimenetig")

A fenti diagram összefoglalja a teljes csővezetéket: **Hugging Face modell letöltése → LLM konfigurálása → AI inicializálása → OCR motor → AI post‑processzor → tisztított OCR szöveg**.

---

## Gyakori kérdések és profi tippek

### Mi van, ha nincs GPU-m?

Állítsd be a `gpu_layers=0` értéket az `AsposeAIModelConfig`‑ban. A modell teljesen CPU-n fog futni, ami lassabb, de még mindig működőképes. Átválthatsz egy kisebb modellre is (pl. `Qwen/Qwen2.5-1.5B‑Instruct‑GGUF`), hogy az inferencia idő ésszerű maradjon.

### Hogyan változtathatom meg később a modellt?

Egyszerűen frissítsd a `hugging_face_repo_id`‑t, és futtasd újra az `ocr_ai.initialize(model_config)`‑t. Az SDK észleli a verzióváltozást, letölti az új modellt, és felülírja a gyorsítótárazott fájlokat.

### Testreszabhatom a post‑processzor promptját?

Igen. Adj át egy szótárat a `custom_settings`‑nek egy `prompt_template` kulccsal. Például:

```python
custom_prompt = {
    "prompt_template": "Correct the following OCR text and keep line breaks:\n{ocr_text}"
}
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=custom_prompt)
```

### Tároljam a tisztított szöveget fájlban?

Határozottan. A tisztítás után a eredményt `.txt` vagy `.json` fájlba írhatod a további feldolgozáshoz:

```python
with open("cleaned_note.txt", "w", encoding="utf-8") as f:
    f.write(cleaned_result.text)
```

---

## Összegzés

Most bemutattuk, hogyan **futtathatsz OCR-t képfájlokon** az Aspose OCR Cloud segítségével, automatikusan **letöltheted a Hugging Face modellt**, szakszerűen **konfigurálhatod az LLM modellt**, és végül **tisztíthatod az OCR szöveget** egy erőteljes LLM post‑processzorral. Az egész folyamat egyetlen, könnyen futtatható Python szkriptbe illeszkedik, és működik mind GPU‑val felszerelt, mind csak CPU‑t használó gépeken.

Ha már magabiztos vagy ebben a csővezetékben, gondolkodj el a következő kísérleteken:

- **Különböző LLM-ek** – próbáld ki a `meta-llama/Meta-Llama-3-8B‑Instruct‑GGUF`‑t egy nagyobb kontextusablakért.  
- **Kötegelt feldolgozás** – iterálj egy képmappán, és gyűjtsd össze a tisztított eredményeket egy CSV-be.  
- **Egyedi promptok** – szabja testre az AI-t a saját területére (jogi dokumentumok, orvosi jegyzetek stb.).

Nyugodtan módosítsd a `gpu_layers` értékét, cseréld le a modellt, vagy csatlakoztasd a saját promptodat. A lehetőségek határtalanok, és a jelenlegi kód a kiindulópont.

Boldog kódolást, és legyenek az OCR kimeneteid mindig tiszták! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}