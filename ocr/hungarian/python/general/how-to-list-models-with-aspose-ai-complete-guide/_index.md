---
category: general
date: 2026-07-05
description: Hogyan listázhatók a modellek az Aspose AI-val, engedélyezhető az automatikus
  letöltés, és letölthető a Hugging Face modell Pythonban. Kövesse ezt a lépésről‑lépésre
  útmutatót a gyorsítótár beállításához, és kezdje el használni az Aspose AI-t még
  ma.
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: hu
og_description: Hogyan listázhatók a modellek az Aspose AI-val, engedélyezhető az
  automatikus letöltés, és letölthető egy Hugging Face modell. Tanulja meg beállítani
  a gyorsítótárat, és percek alatt használni az Aspose AI-t.
og_title: Hogyan listázhatunk modelleket az Aspose AI-val – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  headline: How to list models with Aspose AI – Complete Guide
  type: TechArticle
- description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  name: How to list models with Aspose AI – Complete Guide
  steps:
  - name: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
    text: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
  - name: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
    text: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
  - name: Initialise the AI, then call `list_local()` to see exactly what’s cached.
    text: Initialise the AI, then call `list_local()` to see exactly what’s cached.
  - name: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
    text: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
  type: HowTo
tags:
- Aspose
- Python
- LLM
- Model Management
title: Hogyan listázhat modelleket az Aspose AI-val – Teljes útmutató
url: /hu/python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan listázzuk a modelleket az Aspose AI-val – Teljes útmutató

Hogyan listázzuk a modelleket az Aspose AI-val egy kérdés, amely felmerül, amint elkezdesz kísérletezni nagy nyelvi modellekkel Pythonban. Ebben az útmutatóban végigvezetünk a **auto download** engedélyezésén, egy helyi gyorsítótár konfigurálásán, és egy modell közvetlen letöltésén a Hugging Face‑ről – így fájlok kézi keresése nélkül is gyorsan belevághatsz.

Ha valaha is azon töprengtél, *„hogyan használjam az Aspose‑t OCR‑vezérelt AI‑hoz?”* vagy *„mi a legegyszerűbb módja a gyorsítótár beállításának a modellfájlokhoz?”*, jó helyen vagy. A végére egy teljesen működő szkriptet kapsz, amely felsorolja a helyileg tárolt modelleket, automatikusan letölti a hiányzókat, és pontosan megmutatja, hol találhatók a fájlok a lemezen.

---

## Amire szükséged lesz

- Python 3.9 vagy újabb (a könyvtár típusjelzéseket használ, amelyekhez friss interpreter szükséges)
- `pip` hozzáférés a **Aspose OCR** csomag (`aocr`) telepítéséhez.  
  ```bash
  pip install aocr
  ```
- Internetkapcsolat az első letöltéshez a Hugging Face‑ről.
- Egy mappa, ahol a modell gyorsítótárat szeretnéd tárolni (pl. `./model_cache`).

Ennyi – nincs szükség extra Docker konténerekre, sem nehézkes virtuális környezetekre egy tiszta Python‑installáció mellett.

---

## ## Hogyan listázzuk a modelleket az Aspose AI-val

Ennek az útmutatónak a lényege, hogy **listázzuk a modelleket**, amelyeket az Aspose AI helyileg gyorsítótárazott. Miután a gyorsítótár be van állítva, a könyvtár felsorolhat mindent, amit ismer, így a hibakeresés és a verziókezelés egyszerűvé válik.

```python
import aocr

# 1️⃣ Create an Aspose AI instance
ai = aocr.AsposeAI()

# 2️⃣ Configure the model cache and auto‑download behavior
cfg = aocr.AsposeAIModelConfig()
cfg.allow_auto_download = "true"                     # ← enable auto download
cfg.directory_model_path = r"./model_cache"          # ← how to set cache
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# 3️⃣ Initialise the AI with the config we just built
ai.initialize(cfg)

# 4️⃣ List the models that are already cached locally
print("🗂️ Models cached at:", ai.get_local_path())
print("📦 Available models:", ai.list_local())
```

**Miért működik ez:**  
- `AsposeAI()` létrehozza a magas szintű belépési pontot, amely a háttérben lévő inferencia‑motorral kommunikál.  
- `AsposeAIModelConfig()` tartalmazza az összes beállítást; ha az `allow_auto_download` értéke `"true"`‑ra van állítva, a könyvtár automatikusan letölti a hiányzó fájlokat a megadott tárolóból.  
- `directory_model_path` a *cache directory* – az a hely, ahol az összes letöltött bináris fájl él.  
- `initialize()` alkalmazza a konfigurációt, és ha a gyorsítótár üres, elvégzi az első letöltést.  
- Végül a `list_local()` átvizsgálja a gyorsítótár mappát, és egy Python listát ad vissza a modellazonosítókról, amelyet kiírunk.

### Várható kimenet (első futtatás)

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

Ha újra futtatod a szkriptet, a könyvtár kihagyja a letöltést, és egyszerűen listázza a már létező modellt, bizonyítva, hogy a **hogyan állítsuk be a cache-t** valóban megtérül a későbbi futtatásoknál.

---

## ## Engedélyezze az automatikus letöltést hiányzó modellekhez

Gyakran több modellt is használsz különböző projektekben. Minden egyes modell kézi letöltése a Hugging Face‑ről fárasztó lehet. Az automatikus letöltés engedélyezésével az Aspose AI elvégzi a nehéz munkát.

```python
cfg.allow_auto_download = "true"
```

> **Pro tip:** Tartsd az `allow_auto_download` értékét `"true"` **csak** fejlesztési vagy CI környezetben. Éles környezetben érdemes lezárni a gyorsítótárat, hogy elkerüld a váratlan hálózati forgalmat.

Ha később úgy döntesz, hogy kikapcsolod, egyszerűen állítsd a flag-et `"false"`-ra, mielőtt újra meghívnád az `initialize()`‑t.

---

## ## Hugging Face modell letöltése menet közben

A sor

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

megmondja az Aspose AI‑nek, hogy melyik távoli tárolóból húzza le a modellt. A könyvtár bármely nyilvános Hugging Face modellt támogat, amely GGUF fájlt biztosít. Másik modellre van szükséged? Cseréld ki a repo ID‑t:

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

Amikor futtatod a szkriptet, az Aspose AI ellenőrzi a gyorsítótárat:

- **If the model exists**, it loads it instantly.  
- **If it doesn’t**, the auto‑download flag triggers a download, stores the file under `directory_model_path`, and then registers it for immediate use.

Ez a megközelítés megszünteti a „letöltés‑után‑futtatás” kétszakaszos folyamatot, amelyet sok oktatóanyag kényszerít.

---

## ## Hogyan használjuk az Aspose AI-t a modell listázása után

A modellek listázása csak a történet felét jelenti. Miután tudod, hogy egy modell jelen van, elkezdheted az inferenciát:

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**Miért fontos ez:**  
- `run_inference()` elrejti a tokenizálást, a batch‑kezelést és a GPU‑használatot.  
- A *model name* átadásával, amelyet a `list_local()`‑ból szereztél, garantálod, hogy az inferencia hívás pontosan a lemezen lévő fájlra mutat.

---

## ## Hogyan állítsuk be a cache helyét több projekthez

Ha több projektet kezelsz egyszerre, előfordulhat, hogy mindegyiknek saját gyorsítótár mappára van szüksége. A `directory_model_path` mező egyszerű karakterlánc, ezért dinamikusan építheted fel:

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

Most minden projekt egy izolált alkönyvtárat kap (`./model_cache/sentiment_analysis`), ami megakadályozza a verzióütközéseket és egyszerűvé teszi a takarítást.

---

## ## Gyakori buktatók és hogyan kerüljük el őket

| Tünet | Valószínű ok | Megoldás |
|---------|--------------|-----|
| **`PermissionError` when accessing cache** | A gyorsítótár mappát más felhasználó birtokolja (gyakori megosztott szervereken) | Hozd létre a mappát manuálisan megfelelő jogosultságokkal: `mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **Model never appears in `list_local()`** | `allow_auto_download` `"false"`‑ra van állítva, és a modell még nincs gyorsítótárazva | Kapcsold be ideiglenesen a flag-et, futtasd egyszer, majd ha szeretnéd, kapcsold ki újra |
| **Unexpected model version** | Két különböző tároló ugyanazzal a névvel, de eltérő fájlokkal rendelkezik | Rögzítsd a pontos repo ID‑t (beleértve a tag/commit‑ot), vagy tiltsd le az automatikus letöltést az első sikeres húzás után |
| **Out‑of‑memory errors** | Nagy GGUF fájlok egy olyan gépen, amelynek nincs elegendő RAM/VRAM‑ja | Használj kisebb modellt (pl. `Qwen2.5-1.5B`), vagy állítsd be a `cfg.device = "cpu"`‑t a CPU‑inferencia kényszerítéséhez |

---

## ## Teljes script, amit másolhatsz‑beilleszthetsz

Az alábbiakban a teljes, azonnal futtatható példát találod, amely magában foglalja a fent bemutatott összes koncepciót. Mentsd el `list_models_demo.py` néven, és futtasd a `python list_models_demo.py` paranccsal.

```python
# list_models_demo.py
import os
import aocr

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Create the Aspose AI instance
    # ------------------------------------------------------------------
    ai = aocr.AsposeAI()

    # ------------------------------------------------------------------
    # 2️⃣ Build configuration: enable auto download, set cache path,
    #    and point at a Hugging Face repo
    # ------------------------------------------------------------------
    cfg = aocr.AsposeAIModelConfig()
    cfg.allow_auto_download = "true"                               # enable auto download
    cfg.directory_model_path = os.path.abspath("./model_cache")   # how to set cache
    cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

    # ------------------------------------------------------------------
    # 3️⃣ Initialise the AI with the configuration
    # ------------------------------------------------------------------
    ai.initialize(cfg)

    # ------------------------------------------------------------------
    # 4️⃣ Verify cache location and list all locally available models
    # ------------------------------------------------------------------
    print("🗂️ Models cached at:", ai.get_local_path())
    print("📦 Available models:", ai.list_local())

    # ------------------------------------------------------------------
    # 5️⃣ (Optional) Run a quick inference using the first listed model
    # ------------------------------------------------------------------
    if ai.list_local():
        model_name = ai.list_local()[0]
        prompt = "Give a short summary of the Python GIL."
        response = ai.run_inference(model_name, prompt)
        print("\n🤖 Model response:", response)

if __name__ == "__main__":
    main()
```

**Running it** will produce output similar to the earlier example, followed by a concise answer from the model. Feel free to replace the prompt with anything you like—this is the fastest way to test that the model is truly usable after you’ve **hogyan listázzuk a modelleket**.

---

## ## Összefoglalás

Áttekintettük mindent, ami szükséges a **hogyan listázzuk a modelleket** használatához az Aspose AI‑val, az **auto download** engedélyezésétől a tartós **cache** konfigurálásáig, valamint egy **Hugging Face model** igény szerinti letöltéséig. A legfontosabb tanulságok:

1. Hozz létre egy `AsposeAI` objektumot és egy `AsposeAIModelConfig`‑ot.  
2. Állítsd be az `allow_auto_download = "true"`‑t, és irányítsd a `directory_model_path`‑t egy általad kezelt mappára.  
3. Inicializáld az AI‑t, majd hívd meg a `list_local()`‑t, hogy pontosan lásd, mi van gyorsítótárazva.  
4. Használd a listázott modell nevét az inferenciához, és már készen is vagy a valós alkalmazások építésére.

---

## Mi a következő?

- **Experiment with different models** – swap `cfg.hugging_face_repo_id` for another repo and see how the list changes.  
- **Fine‑tune cache

## Mit kellene legközelebb megtanulnod?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [How to Set Aspose OCR License and Verify It in Java](/ocr/english/java/ocr-basics/set-license/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}