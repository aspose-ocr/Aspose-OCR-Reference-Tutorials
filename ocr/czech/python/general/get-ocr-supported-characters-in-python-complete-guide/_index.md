---
category: general
date: 2026-06-25
description: Získejte rychle podporované znaky OCR pomocí knihovny aocr. Naučte se,
  jak vypsat znaky OCR, nastavit jazyky a ladit svůj OCR engine v Pythonu.
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: cs
og_description: Získejte podporované znaky OCR pomocí aocr. Tento průvodce vám ukáže,
  jak vypsat znaky OCR, vybrat jazyky a řešit okrajové případy v Pythonu.
og_title: Získání podporovaných znaků OCR v Pythonu – kompletní tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Získání podporovaných znaků OCR v Pythonu – Kompletní průvodce
url: /cs/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Získání podporovaných znaků OCR v Pythonu – Kompletní průvodce

Už jste se někdy zamýšleli, jak **získat podporované znaky OCR** pro konkrétní jazyk, když si pohráváte s OCR enginem? Nejste sami. Ať už stavíte skener účtenek nebo vícejazyčný parser dokumentů, vědět přesně, které glyfy váš engine dokáže rozpoznat, je záchrana. V tomto tutoriálu projdeme celý proces – instalaci knihovny, nastavení jazyka a nakonec výpis těchto znaků – takže během několika minut můžete ladit a dolaďovat svůj OCR pipeline.

Použijeme knihovnu **aocr**, lehký Python OCR engine, který usnadňuje dotazování schopností jazyka. Na konci tohoto průvodce budete schopni **vypsat OCR znaky**, přepínat mezi **podporovanými OCR jazyky** a dokonce odhalit mezery v pokrytí dříve, než vás překvapí v produkci.

---

## Požadavky

Než se pustíme dál, ujistěte se, že máte:

* Python 3.8 nebo novější (balíček aocr už nepodporuje 3.7)
* Terminál nebo příkazový řádek s přístupem k internetu
* Základní znalost Python skriptování (pokud už jste někdy použili `print()`, jste v pohodě)

Žádné těžké externí závislosti – jen pip balíček `aocr`.

---

## Instalace knihovny aocr (OCR Engine Python)

První věc, kterou potřebujete, je funkční instalace **OCR engine Python**. Balíček aocr je dostupný na PyPI, takže stačí jediný pip příkaz:

```bash
pip install aocr
```

Pokud používáte virtuální prostředí (vřele doporučeno), aktivujte jej nejprve:

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **Pro tip:** Připněte verzi (`pip install aocr==1.2.4`), abyste se vyhnuli neočekávaným změnám API později.

---

## Výběr jazyka (Supported OCR Languages)

aocr přichází s několika vestavěnými jazykovými balíčky. Každý balíček definuje sadu Unicode kódových bodů, které engine dokáže rozpoznat. Pro dotazování těchto balíčků musíte nastavit atribut `language` na instanci engine.

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

Místo `aocr.Language.ENGLISH` můžete použít libovolnou jinou hodnotu enumu (`FRENCH`, `GERMAN` atd.). Pokud se pokusíte přiřadit jazyk, který není součástí balíčku, aocr vyvolá `ValueError`. Proto je dobré nejprve zkontrolovat seznam **supported OCR languages**:

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## Získání sady znaků (Get OCR Supported Characters)

Nyní přichází jádro tutoriálu: skutečně **získat podporované znaky OCR**. Engine poskytuje praktickou metodu `get_supported_characters()`, která vrací seznam jednopísmenných řetězců.

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

Na pozadí aocr načte JSON soubor součástí jazykového balíčku a převede každý Unicode kódový bod na Python řetězec. Výsledek je deterministický, což znamená, že pokaždé, když spustíte skript na stejné verzi jazyka, získáte stejný seznam.

---

## Zobrazení počtu podporovaných znaků

Znalost počtu vám rychle pomůže odhadnout šíři pokrytí. Pro angličtinu obvykle uvidíte několik tisíc znaků (včetně interpunkce a číslic).

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

Volání `len()` je O(1), protože Python interně ukládá délku seznamu, takže neexistuje žádný výkonový dopad ani u velkých abeced.

---

## Náhled prvních 100 podporovaných znaků

Rychlá vizuální kontrola může odhalit, zda engine obsahuje symboly, které potřebujete (např. znak € nebo chytré uvozovky). Vytiskněme prvních sto znaků:

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

Operace `join` spojí výřez do jediného řetězce, což je čitelnější než tisknout celý Python seznam.

---

## Kompletní skript – všechny kroky na jednom místě

Níže je kompletní, spustitelný příklad, který spojuje vše dohromady. Uložte jej jako `list_supported_chars.py` a spusťte `python list_supported_chars.py` z terminálu.

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**Očekávaný výstup (zkrácený pro stručnost):**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

Přesný počet se může mírně lišit v závislosti na verzi aocr, ale vždy uvidíte dlouhou abecedu plus běžnou interpunkci.

---

## Ošetření okrajových případů

### Co když chybí jazykový balíček?

Pokud požádáte o jazyk, který není součástí balíčku, `aocr.Language` neobsahuje daný enum a narazíte na `AttributeError`. Ochráníte se tím jednoduchou kontrolou:

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### Prázdný seznam znaků

U některých méně běžných jazyků může dojít k prázdnému seznamu, pokud jsou tréninková data neúplná. V takovém scénáři můžete přejít na výchozí jazyk (např. angličtinu) nebo vyvolat varování:

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Normalizace Unicode

Seznam může obsahovat kombinované znaky (např. „é“ jako `e` + akut). Pokud vaše následné zpracování očekává předkomponované glyfy, proveďte krok normalizace:

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## Pro tipy pro reálné projekty

* **Cache seznam znaků** – Pokud zpracováváte tisíce obrázků, volání `get_supported_characters()` v každé iteraci přidává zbytečnou režii. Uložte seznam do proměnné na úrovni modulu nebo jej serializujte do JSON pro pozdější opětovné použití.
* **Validace napříč jazyky** – Když podporujete více jazyků v jedné aplikaci, najděte průnik znakových sad, abyste získali společný podmnožinu. Pomůže vám to navrhnout UI prvky, které zůstanou konzistentní napříč locale.
* **Ladění selhání OCR** – Pokud engine špatně klasifikuje glyf, porovnejte problematický znak s výstupem `list_supported_chars`. Pokud chybí, identifikovali jste mezeru v pokrytí, která může vyžadovat vlastní trénink.
* **Kombinace s vlastními fonty** – aocr respektuje Unicode rozsah, ale kvalita vykreslení se může lišit podle fontu. Otestujte podporované znaky s přesně tím fontem, který použijete v produkci, abyste předešli překvapením.

---

## Často kladené otázky

**Q: Funguje to s aocr verzí 2.x?**  
A: Ano, metoda `get_supported_characters()` je stabilní napříč 1.x a 2.x. Jediná změna je, že enumy jazyků byly přesunuty do `aocr.languages`.

**Q: Můžu získat Unicode kódový bod pro každý znak?**  
A: Rozhodně. Použijte `ord(ch)` uvnitř list comprehension:

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**Q: Co jazykům psaným zprava doleva, jako arabština?**  
A: aocr obsahuje enum `ARABIC`. Seznam znaků bude obsahovat arabské glyfy, ale možná budete muset povolit RTL vykreslování ve vašem downstream UI.

---

## Závěr

Nyní víte, **jak získat podporované znaky OCR** pomocí knihovny aocr v Pythonu, jak přepínat mezi **supported OCR languages**, a proč je **listing OCR characters** klíčový pro robustní text‑recognition pipeline. S kompletním skriptem a výše uvedenými tipy můžete rychle ověřit jazykové pokrytí, ladit chybějící glyfy a stavět chytřejší OCR‑řízené aplikace.

Připravený na další krok? Zkuste spojit tento seznam znaků s vlastním filtrem slovníku, nebo experimentujte s jiným OCR enginem (Tesseract, EasyOCR) a porovnejte výsledky. Čím více budete zkoumat, tím lepší budou vaše OCR řešení.

Šťastné kódování a ať jsou vaše sady znaků vždy kompletní!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Specify Allowed Characters OCR – Using Aspose.OCR for .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}