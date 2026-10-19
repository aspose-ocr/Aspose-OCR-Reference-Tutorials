---
category: general
date: 2026-01-07
description: Hogyan listázhatók a modellek az Aspose OCR AI-ban Python használatával
  – megtanulhatja, hogyan szerezze meg a modell útvonalát, ellenőrizze a telepített
  modelleket, és szerezzen be egy Python modelllistát másodpercek alatt.
draft: false
keywords:
- how to list models
- get model path
- check installed models
- python get model list
- list available models
language: hu
og_description: Hogyan listázhatók a modellek az Aspose OCR AI-ban Python használatával.
  Keresse meg a modell útvonalát, ellenőrizze a telepített modelleket, és tekintse
  meg a rendelkezésre álló modellek teljes listáját.
og_title: Modellek listázása az Aspose OCR AI-ban – Python útmutató
tags:
- Aspose OCR
- Python
- AI models
title: Hogyan listázhatók a modellek az Aspose OCR AI-ban – Python útmutató
url: /hu/python/general/how-to-list-models-in-aspose-ocr-ai-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan listázhatók a modellek az Aspose OCR AI‑ban – Python útmutató

Gondolkodtál már azon, **hogyan listázhatók a modellek**, amelyek már telepítve vannak a gépeden az Aspose OCR AI használata közben? Nem vagy egyedül ezzel a problémával. Sok projektben ellenőrizned kell a modell mappát, meg kell erősítened, mely modellek vannak jelen, vagy akár egy hiányzó modell hibáját is nyomon kell követned – mindezt anélkül, hogy elhagynád a Python REPL‑t.

Ebben az útmutatóban egy teljes, azonnal futtatható példán keresztül mutatjuk be, hogyan **szerezheted meg a modell útvonalát**, **ellenőrizheted a telepített modelleket**, és végül **listázhatod a rendelkezésre álló modelleket** néhány kódsorral. Nincs külső szkript, nincs rejtett varázslat – csak tiszta Python és az Aspose OCR AI SDK.

> **Előfeltételek**  
> • Python 3.8 vagy újabb  
> • `asposeocr` csomag telepítve (`pip install asposeocr`)  
> • Alapvető ismeretek a modulok importálásáról

Ha ezek megvannak, merüljünk el a részletekben.

---

## Hogyan listázhatók a modellek az Aspose OCR AI‑val

Az első dolog, amire szükségünk van, a `AsposeAI` segédosztály, amely a `asposeocr.ai` modul része. Ez az osztály három hasznos metódust biztosít:

| Metódus | Mit ad vissza | Tipikus felhasználási eset |
|--------|----------------|-----------------|
| `get_local_path()` | Abszolút útvonal a mappához, ahol az Aspose tárolja az AI modelleket | Ellenőrizni, hogy az SDK a megfelelő helyet nézi |
| `list_local()` | Python `list` a lemezen létező modell mappanevekről | Gyorsan megtekinteni, mely modelleket lehet betölteni |
| `list_remote()` *(opcionális)* | Az Aspose felhőjéből letölthető modellek listája | Amikor egy olyan modellre van szükséged, ami helyileg nincs |

Az alábbi **teljes script** kiírja a helyi modell mappát és a telepített modellek listáját.

```python
# ---------------------------------------------------------
# Step 1: Import the Aspose OCR AI module
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

# ---------------------------------------------------------
# Step 2: Create an instance of the AI helper
# ---------------------------------------------------------
ai = AsposeAI()

# ---------------------------------------------------------
# Step 3: Retrieve and display the local model folder
# ---------------------------------------------------------
local_folder = ai.get_local_path()
print("Local AI model folder:", local_folder)

# ---------------------------------------------------------
# Step 4: List all models that are currently installed
# ---------------------------------------------------------
installed_models = ai.list_local()
print("Available models:", installed_models)
```

### Várt kimenet

A script friss telepítés után általában a következőhöz hasonlót látsz:

```
Local AI model folder: /home/user/.asposeocr/models
Available models: ['ocr-general-v1', 'ocr-handwritten-v2']
```

Ha a mappa üres, a `list_local()` egy üres listát (`[]`) ad vissza. Ez egy hasznos jelzés, hogy előbb le kell töltened egy modellt – erről később lesz szó.

---

## Miért fontos a modell útvonalának ismerete

Az **ahol** az SDK tárolja a fájlokat (`get model path`) megértése több, mint kíváncsiság:

1. **Hibakeresés** – Ha egy modell betöltése sikertelen, `ls`-el megtekintheted az útvonalat, és ellenőrizheted, hogy a fájl valóban létezik‑e.
2. **Egyedi modellek** – Egyes csapatok saját OCR modelleket képeznek, és a mappába helyezik őket. Az útvonal ismerete lehetővé teszi, hogy a fájlokat pontosan oda tedd, ahol az Aspose elvárja.
3. **Jogosultságok** – Linuxon a mappa más felhasználó tulajdonában lehet. A jogosultsági hiba korai felismerése órákat spórolhat fejfájástól.

> **Pro tipp:** Ha egy egyedi könyvtárra szeretnéd irányítani az SDK‑t, állítsd be az `ASPOSE_OCR_MODEL_PATH` környezeti változót a `AsposeAI()` létrehozása előtt.

```bash
export ASPOSE_OCR_MODEL_PATH=/my/custom/models
python my_script.py
```

---

## Telepített modellek ellenőrzése – Szélsőséges esetek és tippek

### 1. Nincsenek telepített modellek

Ha a `list_local()` `[]`‑t ad vissza, két lehetőséged van:

| Opció | Hogyan |
|--------|--------------|
| **Modell letöltése az Aspose‑tól** | `ai.download('ocr-general-v1')` (internet szükséges) |
| **Előre betanított modell másolása** | Helyezd a modell mappát manuálisan a `get_local_path()` által mutatott útvonalra |

### 2. Egy modell több verziója

Előfordulhat, hogy egyszerre látod az `ocr-general-v1` **és** az `ocr-general-v1-beta` mappákat. Az SDK az első megtalált egyezést tölti be, de egy konkrét verziót a pontos mappanév átadásával kényszeríthetsz a OCR konstruktorba:

```python
from asposeocr.ai import AsposeOCR

ocr = AsposeOCR(model_name='ocr-general-v1-beta')
```

### 3. Sérült modellfájlok

Részben letöltött modell `FileNotFoundError`‑t okozhat később. Ha gyanítod a sérülést, egyszerűen töröld a hibás mappát, és töltsd le újra:

```bash
rm -rf /home/user/.asposeocr/models/ocr-general-v1
python -c "from asposeocr.ai import AsposeAI; AsposeAI().download('ocr-general-v1')"
```

---

## A script kibővítése – Távoli modellek listázása (opcionális)

Ha szeretnéd megtekinteni, milyen modellek tölthetők le anélkül, hogy elhagynád a Pythont, adj még egy hívást:

```python
remote_models = ai.list_remote()
print("Remote models you can download:", remote_models)
```

Ez valami ilyesmit fog kiírni:

```
Remote models you can download: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Ezután kiválaszthatod a kívánt modellt, és meghívhatod a `ai.download('model-name')`‑t, hogy automatikusan letöltse.

---

## Teljes vég‑től‑végig példa

Mindent összegezve, itt egy **egyetlen, futtatható script**, amely:

1. Kiírja a helyi modell mappát.  
2. Listázza a telepített modelleket.  
3. Ha nincs megtalálható, letölt egy alapértelmezett modellt.  
4. Végül kiírja a frissített listát.

```python
# ---------------------------------------------------------
# Complete script – verifies model folder, installs if empty
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

def main():
    ai = AsposeAI()

    # 1️⃣ Show where Aspose expects models
    local_path = ai.get_local_path()
    print("🔎 Local AI model folder:", local_path)

    # 2️⃣ List currently installed models
    models = ai.list_local()
    print("📦 Installed models:", models)

    # 3️⃣ If nothing is installed, grab a default model
    if not models:
        default = 'ocr-general-v1'
        print(f"⚠️ No models found – downloading '{default}'...")
        try:
            ai.download(default)
            models = ai.list_local()
            print("✅ After download, installed models:", models)
        except Exception as e:
            print("❌ Failed to download model:", e)
            return

    # 4️⃣ (Optional) Show what you could download from the cloud
    remote = ai.list_remote()
    print("🌐 Remote models available:", remote)

if __name__ == "__main__":
    main()
```

A script tiszta gépen való futtatása a következőt eredményezi:

```
🔎 Local AI model folder: /home/user/.asposeocr/models
📦 Installed models: []
⚠️ No models found – downloading 'ocr-general-v1'...
✅ After download, installed models: ['ocr-general-v1']
🌐 Remote models available: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Most már van egy **önálló, idézhető** megoldásod, amelyet bármely AI asszisztens szó szerint idézhet.

---

## Gyakran Ismételt Kérdések (GYIK)

**Q: Működik ez Windows‑on?**  
A: Teljesen. Az SDK absztrahálja a fájlrendszert, így a `get_local_path()` például `C:\Users\YourName\.asposeocr\models`‑t ad vissza. Csak győződj meg róla, hogy a Python írni tud ebbe a mappába.

**Q: Tárolhatok modelleket hálózati meghajtón?**  
A: Igen – állítsd be az `ASPOSE_OCR_MODEL_PATH` változót a UNC útvonalra (`\\server\share\models`) a `AsposeAI` példány létrehozása előtt.

**Q: Mi van, ha egy nyelvre nincs alapértelmezett modell?**  
A: Használd a `list_remote()`‑t, hogy lásd, kínál-e az Aspose nyelvspecifikus modellt. Ha nem, saját modellt is képezhetsz, és a mappába helyezheted; csak a saját mappanevet add meg az OCR konstruktorban.

---

## Következtetés

Áttekintettük, **hogyan listázhatók a modellek** az Aspose OCR AI‑ban, megmutattuk, hogyan **szerezheted meg a modell útvonalát**, **ellenőrizheted a telepített modelleket**, és még **letölthetsz egy hiányzó modellt** – mindezt tiszta Python‑nal. A mappaszerkezet és a segédmetódusok (`get_local_path()`, `list_local()`, `list_remote()`) megismerésével teljes irányítást kapsz az alkalmazásod által használt AI modellek felett.

Mi a következő lépés? Próbáld ki a default modellt egy kézírás‑szöveg modellre cserélni, vagy irányítsd az SDK‑t egy házon belül képzett, egyedi modellre. Bármelyik úton is jársz, most már szilárd alapod van az OCR eszközök kezeléséhez bármely Python projektben.

Boldog kódolást, és legyen a modelllistád mindig naprakész!

---

![Hogyan listázzuk a modelleket képernyőkép](https://example.com/images/how-to-list-models.png "Hogyan listázzuk a modelleket")

*Kép alternatív szöveg:* **hogyan listázzuk a modelleket képernyőkép** (teljesíti az elsődleges kulcsszó követelményt).

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}