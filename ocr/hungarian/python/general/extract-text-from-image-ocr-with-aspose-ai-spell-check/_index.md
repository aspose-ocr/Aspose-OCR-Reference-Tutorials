---
category: general
date: 2026-05-03
description: Képről szöveg kinyerése Aspose OCR és AI helyesírás-ellenőrzés használatával.
  Tanulja meg, hogyan kell OCR-t végezni képen, betölteni a képet OCR-hez, felismerni
  a számla szövegét, és felszabadítani a GPU erőforrásokat.
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: hu
og_description: Szöveg kinyerése képből az Aspose OCR és AI helyesírás-ellenőrző segítségével.
  Lépésről lépésre útmutató, amely bemutatja, hogyan kell OCR-t végezni a képen, hogyan
  töltsük be a képet OCR-hez, és hogyan szabadítsuk fel a GPU erőforrásokat.
og_title: Képből szöveg kinyerése – Teljes OCR és helyesírás-ellenőrző útmutató
tags:
- OCR
- Aspose
- AI
- Python
title: Szöveg kinyerése képből – OCR az Aspose AI helyesírás-ellenőrzővel
url: /hu/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# szöveg kinyerése képből – Teljes OCR és helyesírás-ellenőrző útmutató

Valaha szükséged volt **szöveg kinyerésére képből**, de nem tudtad, melyik könyvtár biztosítja a sebességet és a pontosságot? Nem vagy egyedül. Sok valós projektben – gondolj számlafeldolgozásra, nyugták digitalizálására vagy szerződések beolvasására – a tiszta, kereshető szöveg kinyerése a képből az első akadály.

A jó hír, hogy az Aspose OCR egy könnyű Aspose AI modellel párosítva néhány Python sorral el tudja végezni ezt a feladatot. Ebben az útmutatóban végigvezetünk a **képek OCR‑elésének** lépésein, a kép helyes betöltésén, a beépített helyesírás-ellenőrző utófeldolgozó futtatásán, és végül a **GPU erőforrások felszabadításán**, hogy az alkalmazásod memória‑kímélő maradjon.

A útmutató végére képes leszel **számlaképek szövegének felismerésére**, a gyakori OCR‑hibákat automatikusan javítani, és a GPU‑t tisztán tartani a következő köteghez.

---

## Amire szükséged lesz

- Python 3.9 vagy újabb (a kód típusjelöléseket használ, de korábbi 3.x verziókon is működik)
- `aspose-ocr` és `aspose-ai` csomagok (telepítés: `pip install aspose-ocr aspose-ai`)
- A CUDA‑t támogató GPU opcionális; ha nincs, a szkript CPU‑ra vált.
- Egy példakép, pl. `sample_invoice.png`, egy olyan mappában, amelyre hivatkozhatsz.

Nincs nehéz ML keretrendszer, nincs hatalmas modell letöltés – csak egy kis Q4‑K‑M kvantált modell, amely kényelmesen elfér a legtöbb GPU‑n.

## 1. lépés: OCR motor inicializálása – szöveg kinyerése képből

Az első lépés egy `OcrEngine` példány létrehozása, és a várt nyelv megadása. Itt az angolt választjuk, és egyszerű szöveg (plain‑text) kimenetet kérünk, ami ideális a további feldolgozáshoz.

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**Miért fontos:** A nyelv beállítása szűkíti a karakterkészletet, ezáltal javítva a pontosságot. Az egyszerű szöveg mód eltávolítja a formázási információkat, amelyeket általában nem használsz, ha csak szöveget akarsz kinyerni a képből.

## 2. lépés: Kép betöltése OCR‑hez – hogyan OCR‑eljük a képet

Most egy tényleges képet adunk a motorhoz. A `Image.load` segédfüggvény ismeri a gyakori formátumokat (PNG, JPEG, TIFF), és elrejti a fájl‑IO sajátosságait.

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**Tipp:** Ha a forrásképek nagyok, fontold meg azok átméretezését, mielőtt a motorhoz küldenéd; a kisebb méretek csökkenthetik a GPU memóriahasználatot anélkül, hogy rontanák a felismerés minőségét.

## 3. lépés: Aspose AI modell konfigurálása – szöveg felismerése számláról

Az Aspose AI egy apró GGUF modellt tartalmaz, amelyet automatikusan letölthetsz. A példa a `Qwen2.5‑3B‑Instruct‑GGUF` tárolót használja, `q4_k_m` kvantálással. A futtatókörnyezetnek azt is megmondjuk, hogy a GPU‑ra 20 réteget foglaljon, ami egyensúlyt teremt a sebesség és a VRAM használat között.

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**A háttérben:** A kvantált modell körülbelül 1,5 GB helyet foglal a lemezen, ami csak töredéke egy teljes pontosságú modellnek, de még így is elegendő nyelvi finomságot tartalmaz ahhoz, hogy a tipikus OCR‑helyesírási hibákat felismerje.

## 4. lépés: AsposeAI inicializálása és a helyesírás-ellenőrző utófeldolgozó csatolása

Az Aspose AI tartalmaz egy kész helyesírás-ellenőrző utófeldolgozót. Ha csatolod, minden OCR eredmény automatikusan megtisztul.

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**Miért használjuk az utófeldolgozót?** Az OCR motorok gyakran félreolvassák az „Invoice” szót „Invo1ce”‑ként vagy a „Total” szót „T0tal”‑ként. A helyesírás-ellenőrző egy könnyű nyelvi modellt futtat a nyers szövegen, és kijavítja ezeket a hibákat anélkül, hogy saját szótárat kellene írnod.

## 5. lépés: Helyesírás-ellenőrző utófeldolgozó futtatása az OCR eredményen

Miután minden összekapcsolódott, egyetlen hívás adja vissza a javított szöveget. Ki is nyomtatjuk az eredeti és a tisztított változatot, hogy lásd a javulást.

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

Egy számla tipikus kimenete így nézhet ki:

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

Vedd észre, hogy a „Invo1ce” helyes szóra, az „Invoice”‑ra változott. Ez a beépített AI helyesírás-ellenőrző ereje.

## 6. lépés: GPU erőforrások felszabadítása – GPU erőforrások biztonságos felszabadítása

Ha ezt egy hosszú életű szolgáltatásban futtatod (pl. egy web‑API, amely percenként tucatnyi számlát dolgoz fel), minden köteg után fel kell szabadítanod a GPU kontextust. Ellenkező esetben memória‑szivárgásokat és végül a „CUDA out of memory” hibákat fogod tapasztalni.

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**Pro tipp:** Hívd meg a `free_resources()`‑t egy `finally` blokkban vagy egy kontextuskezelőben, hogy mindig végrehajtódjon, még akkor is, ha kivétel keletkezik.

## Teljes működő példa

Az összes részegység összerakásával egy önálló szkriptet kapsz, amelyet bármely projektbe beilleszthetsz.

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

Mentsd el a fájlt, állítsd be a képed elérési útját, és futtasd a `python extract_text_from_image.py` parancsot. A konzolon meg kell jelennie a tisztított számlaszövegnek.

## Gyakran Ismételt Kérdések (GYIK)

**K: Működik ez csak CPU‑s gépeken?**  
V: Teljesen. Ha nincs GPU észlelve, az Aspose AI CPU‑ra vált, bár lassabb lesz. A CPU kényszerítéséhez állítsd be a `model_cfg.gpu_layers = 0` értéket.

**K: Mi van, ha a számláim nem angol nyelvűek?**  
V: Állítsd a `ocr_engine.language`‑t a megfelelő enum értékre (pl. `aocr.Language.Spanish`). A helyesírás-ellenőrző modell többnyelvű, de nyelvspecifikus modellel jobb eredményeket érhetsz el.

**K: Feldolgozhatok több képet egy ciklusban?**  
V: Igen. Csak helyezd a betöltési, felismerési és utófeldolgozási lépéseket egy `for` ciklusba. Ne felejtsd el meghívni a `ocr_ai.free_resources()`‑t a ciklus után vagy minden köteg után, ha ugyanazt az AI példányt használod újra.

**K: Mekkora a modell letöltése?**  
V: Körülbelül 1,5 GB a kvantált `q4_k_m` verzióhoz. Az első futtatás után gyorsítótárazódik, így a későbbi indítások azonnaliak.

## Összegzés

Ebben az útmutatóban bemutattuk, hogyan **nyerjünk ki szöveget képből** az Aspose OCR használatával, hogyan konfiguráljunk egy apró AI modellt, alkalmazzunk egy helyesírás-ellenőrző utófeldolgozót, és biztonságosan **felszabadítsuk a GPU erőforrásokat**. A munkafolyamat mindent lefed a kép betöltésétől a saját takarításig, megbízható csővezetéket biztosítva a **számlák szövegének felismerése** esetekhez.

Következő lépések? Próbáld megcserélni a helyesírás-ellenőrzőt egy egyedi entitás‑kivonó modellre

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}