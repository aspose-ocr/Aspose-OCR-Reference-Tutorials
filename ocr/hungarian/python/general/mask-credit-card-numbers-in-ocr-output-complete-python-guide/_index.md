---
category: general
date: 2026-04-26
description: Maszkolja gyorsan a hitelkártya-számokat az AsposeAI OCR utófeldolgozással.
  Ismerje meg a PCI megfelelőséget, a reguláris kifejezéssel történő maszkolást és
  az adat tisztítását egy lépésről‑lépésre útmutatóban.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: hu
og_description: Maszkold a hitelkártyaszámokat az OCR-eredményekben az AsposeAI segítségével.
  Ez az útmutató a PCI-megfelelőséget, a reguláris kifejezésekkel történő maszkolást
  és az adattisztítást tárgyalja.
og_title: Hitelkártya számok maszkolása – Teljes Python OCR utófeldolgozási útmutató
tags:
- OCR
- Python
- security
title: Hitelkártya-számok maszkolása az OCR kimenetben – Teljes Python útmutató
url: /hu/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hitelkártya-számok maszkolása – Teljes Python útmutató

Volt már szükséged **hitelkártya-számok** maszkolására olyan szövegben, amely közvetlenül egy OCR motorból származik? Nem vagy egyedül. Szabályozott iparágakban a teljes PAN (Primary Account Number) felfedése komoly gondokat okozhat a PCI megfelelőségi auditoroknál. A jó hír? Néhány Python sorral és az AsposeAI post‑processing hook‑jával automatikusan elrejtheted a középső nyolc számjegyet, és biztonságban maradhatsz.

Ebben az útmutatóban egy valós példán keresztül vezetünk végig: OCR futtatása egy nyugta képen, majd egy egyedi **OCR post‑processing** függvény alkalmazása, amely megtisztítja a PCI adatokat. A végére egy újrahasználható kódrészletet kapsz, amelyet bármely AsposeAI munkafolyamatba beilleszthetsz, valamint néhány gyakorlati tippet a szélső esetek kezelésére és a megoldás skálázására.

## Mit fogsz megtanulni

- Hogyan regisztrálj egy egyedi post‑processzort az **AsposeAI**‑val.
- Miért gyors és megbízható a **regular expression masking** (reguláris kifejezéses maszkolás) megközelítés.
- A **PCI compliance** (PCI megfelelőség) alapjai az adattisztítás kapcsán.
- Módszerek a minta kiterjesztésére több kártyaformátum vagy nemzetközi számok esetén.
- Várható kimenet és hogyan ellenőrizheted, hogy a maszkolás működött.

> **Előfeltételek** – Rendelkezned kell egy működő Python 3 környezettel, az Aspose.AI for OCR csomaggal telepítve (`pip install aspose-ocr`), és egy mintaképpel (pl. `receipt.png`), amely tartalmaz egy hitelkártya-számot. Más külső szolgáltatás nem szükséges.

---

## 1. lépés: Definiáld a post‑processzort, amely a hitelkártya-számokat maszkolja

A megoldás lényege egy apró függvényben rejlik, amely megkapja az OCR eredményt, egy **regular expression masking** (reguláris kifejezéses maszkolás) rutint futtat, és visszaadja a megtisztított szöveget.

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**Miért működik ez:**  
- A regex `(\d{4})\d{8}(\d{4})` pontosan 16 egymást követő számjegyet egyeztet, ami a Visa, MasterCard és sok más kártya általános formátuma.  
- Az első és az utolsó négy számjegy (`\1` és `\2`) rögzítésével elegendő információt megőrzünk a hibakereséshez, miközben betartjuk a **PCI compliance** szabályait, amelyek tiltják a teljes PAN tárolását.  
- A `\1****\2` helyettesítés elrejti a középső nyolc érzékeny számjegyet, így a `1234567812345678` `1234****5678` lesz.

> **Pro tip:** Ha 15 számjegyű American Express számokat is támogatni szeretnél, adj hozzá egy második mintát, például `r'(\d{4})\d{6}(\d{5})'`, és futtasd egymás után mindkét helyettesítést.

---

## 2. lépés: Inicializáld az AsposeAI motorját

Mielőtt csatlakoztatnánk a post‑processzorunkat, szükségünk van az OCR motor egy példányára. Az AsposeAI tartalmazza az OCR modellt és egy egyszerű API-t az egyedi feldolgozáshoz.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**Miért inicializáljuk itt?**  
Az `AsposeAI` objektum egyszeri létrehozása és több kép között való újrahasználata csökkenti a terhelést. A motor emellett gyorsítótárazza a nyelvi modelleket, ami felgyorsítja a későbbi hívásokat – hasznos, ha nyugtákat szkennelsz kötegben.

---

## 3. lépés: Regisztráld az egyedi maszkoló függvényt

Az AsposeAI egy `set_post_processor` metódust biztosít, amely lehetővé teszi bármilyen hívható objektum csatlakoztatását. Átadjuk a `mask_pci` függvényünket egy opcionális beállítási szótárral (most üres).

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**Mi történik a háttérben?**  
Amikor később meghívod a `run_postprocessor`-t, az AsposeAI a nyers OCR eredményt átadja a `mask_pci`-nek. A függvény egy könnyű objektumot (`data`) kap, amely a felismert szöveget tartalmazza, és egy új stringet ad vissza. Ez a tervezés érintetlenül hagyja az OCR magját, miközben egy helyen tudod érvényesíteni a **data sanitization** (adat-tisztítási) szabályokat.

---

## 4. lépés: Futtasd az OCR-t a nyugta képen

Most, hogy a motor tudja, hogyan tisztítsa meg a kimenetet, betáplálunk egy képet. Az útmutató kedvéért feltételezzük, hogy már rendelkezel egy `engine` objektummal, amely a megfelelő nyelvi és felbontási beállításokkal van konfigurálva.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**Tipp:** Ha nincs előre konfigurált objektumod, létrehozhatsz egyet a következővel:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

A `recognize_image` hívás egy olyan objektumot ad vissza, amelynek `text` attribútuma a nyers, nem maszkolt szöveget tartalmazza.

---

## 5. lépés: Alkalmazd a regisztrált post‑processzort

A nyers OCR adatok birtokában átadjuk őket az AI példánynak. A motor automatikusan futtatja a korábban regisztrált `mask_pci` függvényt.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**Miért használjuk a `run_postprocessor`-t a függvény kézi meghívása helyett?**  
Ez biztosítja a munkafolyamat konzisztenciáját, különösen ha több post‑processzort (pl. helyesírás-ellenőrzés, nyelvfelismerés) használsz. Az AsposeAI a regisztráció sorrendjében sorba helyezi őket, garantálva a determinisztikus kimenetet.

---

## 6. lépés: Ellenőrizd a megtisztított kimenetet

Végül nyomtassuk ki a megtisztított szöveget, és ellenőrizzük, hogy a hitelkártya-számok megfelelően vannak-e maszkolva.

```python
print(final_result.text)
```

**Várható kimenet** (részlet):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

Ha a nyugta nem tartalmazott kártyaszámot, a szöveg változatlan marad – nincs mit maszkolni, nincs miért aggódni.

---

## Szélső esetek és gyakori variációk kezelése

### Több kártya-szám egy dokumentumban
Ha egy nyugta több PAN-t (pl. egy hűségkártya és egy fizetési kártya) tartalmaz, a regex globálisan fut, és automatikusan minden egyezést maszkol. Nem szükséges extra kód.

### Nem szabványos formázás
Néha az OCR szóközöket vagy kötőjeleket szúr be (`1234 5678 1234 5678` vagy `1234-5678-1234-5678`). Bővítsd a mintát, hogy figyelmen kívül hagyja ezeket a karaktereket:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

A hozzáadott `[ -]?` opcionális szóközöket vagy kötőjeleket enged meg a számcsoportok között.

### Nemzetközi kártyák
Néhány régióban használt 19 számjegyű PAN-ok esetén kibővítheted a mintát:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

Csak ne feledd, hogy a **PCI compliance** továbbra is előírja a középső számjegyek maszkolását, függetlenül a hosszuktól.

### Maszkolt értékek naplózása (opcionális)
Ha audit nyomvonalra van szükséged, adj át egy jelzőt a `custom_settings`-en keresztül, és módosítsd a függvényt:

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

Ezután regisztráld a következővel:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## Teljes működő példa (másolásra kész)

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

A szkript futtatása egy `4111111111111111` számot tartalmazó nyugtán a következőt eredményezi:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

Ez a teljes folyamat – a nyers OCR-től a **data sanitization**-ig – néhány tiszta Python sorba csomagolva.

---

## Összegzés

Most bemutattuk, hogyan **maszkolhatod a hitelkártya-számokat** OCR eredményekben az AsposeAI post‑processing hook, egy tömör reguláris kifejezéses rutin és néhány bevált gyakorlat segítségével a **PCI compliance** érdekében. A megoldás teljesen önálló, bármely, az OCR motor által olvasható képen működik, és kiterjeszthető összetettebb kártyaformátumok vagy naplózási igények lefedésére.

Készen állsz a következő lépésre? Próbáld meg összekapcsolni ezt a maszkolást egy **adatbázis-beillesztési** rutinnal, amely csak az utolsó négy számjegyet tárolja hivatkozásként, vagy integrálj egy **kötegfeldolgozót**, amely egy egész nyugták mappáját szkennelje éjszaka. Felfedezheted továbbá más **OCR post‑processing** feladatokat is, mint például címstandardizálás vagy nyelvfelismerés – mindegyik ugyanazt a mintát követi, amit itt használtunk.

Van kérdésed a szélső esetekkel, a teljesítménnyel vagy azzal kapcsolatban, hogyan adaptáld a kódot egy másik OCR könyvtárhoz? Írj egy megjegyzést alább, és folytassuk a beszélgetést. Boldog kódolást, és maradj biztonságban!

![Diagram illustrating how mask credit card numbers works in an OCR pipeline](https://example.com/images/ocr-mask-flow.png "Diagram of OCR post‑processing masking flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}