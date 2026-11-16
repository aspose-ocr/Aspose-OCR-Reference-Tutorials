---
category: general
date: 2026-03-18
description: Proveďte OCR na obrázku a extrahujte ručně psaný text z fotografie. Naučte
  se, jak převést ručně psaný obrázek, extrahovat text z JPG a rozpoznat text z fotografie.
draft: false
keywords:
- perform OCR on image
- convert handwritten image
- extract text from jpg
- extract handwritten text
- recognize text from photo
language: cs
og_description: Proveďte OCR na obrázku a extrahujte ručně psaný text z fotografie.
  Tento tutoriál ukazuje, jak převést ručně psaný obrázek a rozpoznat text z jpg souborů.
og_title: Proveďte OCR na obrázku – Kompletní průvodce ručně psaným textem
tags:
- OCR
- Python
- Handwriting Recognition
title: Proveďte OCR na obrázku – Převod ručně psaného obrázku na text
url: /cs/python/general/perform-ocr-on-image-convert-handwritten-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Provést OCR na obrázku – Kompletní extrakce ručně psaného textu

Už jste někdy potřebovali **perform OCR on image** soubory, ale nebyli jste si jisti, zda engine dokáže číst nečisté rukopisy? Nejste v tom sami. V mnoha reálných aplikacích – například skenery účtenek nebo nástroje pro poznámky – narazíte na fotografie čmáraní, které je potřeba převést na prostý text.  

V tomto průvodci vám ukážeme, jak **convert handwritten image** soubory, **extract text from jpg**, a dokonce **recognize text from photo** proudy pomocí malé knihovny ve stylu Pythonu nazvané `ocr`. Na konci budete mít připravený skript, který vytáhne každé slovo z ručně psané poznámky, bez ohledu na to, jak nejistě bylo psáno perem.

## Co budete potřebovat

- Python 3.8+ (kód funguje na jakémkoli aktuálním interpreteru)
- Hypotetický balíček `ocr` – nainstalujte jej pomocí `pip install ocr-lib` (nahraďte skutečným názvem balíčku, který používáte)
- Jasná fotografie ručně psané poznámky uložená jako `note.jpg` (nebo jakýkoli jiný formát obrázku)
- Trochu zvědavosti – není potřeba pokročilé znalosti ML

To je vše. Žádné externí služby, žádné API klíče, jen lokální engine, který může **perform OCR on image** data.

![snímek obrazovky perform OCR on image ukazující editor kódu s OCR skriptem](example.png)

*Alt text: perform OCR on image screenshot showing code editor with OCR script.*

## Implementace krok za krokem

Níže rozdělujeme proces na malé části. Každý nadpis obsahuje klíčové slovo, abyste mohli rychle přeskakovat, a každý blok vysvětluje **why**, proč děláme to, co děláme – ne jen **what**.

### Krok 1: Instalace a ověření knihovny OCR

Než budete moci **perform OCR on image** soubory, musí být knihovna přítomna ve vašem prostředí. Otevřete terminál a spusťte:

```bash
pip install ocr-lib
```

> **Tip:** Pokud pracujete ve virtuálním prostředí (vysoce doporučeno), nejprve jej aktivujte. To udrží vaše závislosti v pořádku a zabrání konfliktům verzí.

Po instalaci si ověřme, že Python může balíček importovat:

```python
try:
    import ocr
    print("OCR library loaded successfully.")
except ImportError as e:
    raise SystemExit("Failed to import ocr library. Did you run pip install?") from e
```

Pokud uvidíte zprávu o úspěchu, jste připraveni na **convert handwritten image** data.

### Krok 2: Vytvoření instance engine a výběr režimu ručně psaného textu

Většina OCR engineů má ve výchozím nastavení rozpoznávání tištěného textu. Protože chceme **extract handwritten text**, musíme režim explicitně přepnout. Tento krok je zásadní, protože ručně psaný text často vyžaduje odlišné předzpracování (např. vyhlazování tahů).

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Tell the engine we’re dealing with handwriting
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

print("Engine configured for handwritten recognition.")
```

*Proč je to důležité:* Rukopisné znaky se mohou výrazně lišit ve velikosti a sklonu. Nastavením `RecognitionMode.HANDWRITTEN` engine použije model trénovaný na kurzívních vzorcích, což dramaticky zvyšuje přesnost.

### Krok 3: Načtení fotografie, kterou chcete analyzovat

Nyní skutečně **perform OCR on image** obsah. Metoda `load_image` přijímá cestu nebo objekt podobný souboru. Pro demonstraci načteme JPEG, ale stejný příkaz funguje i pro PNG, BMP nebo dokonce PDF stránky.

```python
# Step 3: Load the image file (replace the path with yours)
image_path = "YOUR_DIRECTORY/note.jpg"
engine.load_image(image_path)

print(f"Image '{image_path}' loaded into the OCR engine.")
```

Pokud je váš obrázek v cloudovém bucketu, nejprve jej stáhněte nebo předávejte `BytesIO` stream – `ocr` je dostatečně flexibilní, aby zvládl obojí.

### Krok 4: Spuštění procesu rozpoznávání

S připraveným engine a obrázkem v paměti konečně **perform OCR on image** a získáme surový text.

```python
# Step 4: Execute recognition
extracted_text = engine.recognize()

print("=== Extracted Text ===")
print(extracted_text)
```

Volání `recognize()` vrací obyčejný Unicode řetězec. Pro většinu případů můžete jej přímo zapsat do souboru `.txt`, předat do pipeline pro zpracování přirozeného jazyka nebo zobrazit v GUI.

### Krok 5: Volitelné – Vyčištění nebo post‑zpracování výstupu

Ručně psané OCR není dokonalé; často uvidíte zbytečné zalomení řádků nebo špatně rozpoznané znaky. Rychlý krok čištění může zlepšit následné výsledky.

```python
# Step 5: Simple post‑processing (optional)
def tidy(text):
    # Collapse multiple spaces, strip leading/trailing whitespace
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(extracted_text)

print("\n=== Cleaned Text ===")
print(clean_text)
```

Neváhejte zapojit kontrolu pravopisu, jazykové modely nebo vlastní regulární výrazy podle vašeho doménového kontextu.

### Kompletní skript – připravený ke kopírování a vložení

Spojením všeho dohromady zde máte kompletní spustitelný program, který **extracts handwritten text** z JPEG a vytiskne úhledný výsledek.

```python
# -*- coding: utf-8 -*-
"""
Complete example: Perform OCR on image to extract handwritten text.
"""

# -------------------------------------------------
# Step 1: Import the OCR library and create an engine
# -------------------------------------------------
import ocr

engine = ocr.OcrEngine()

# -------------------------------------------------
# Step 2: Set the engine to recognize handwritten text
# -------------------------------------------------
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

# -------------------------------------------------
# Step 3: Load the image you want to analyze
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/note.jpg"   # <-- change this to your file
engine.load_image(image_path)

# -------------------------------------------------
# Step 4: Perform recognition and output the extracted text
# -------------------------------------------------
raw_text = engine.recognize()
print("=== Raw OCR Output ===")
print(raw_text)

# -------------------------------------------------
# Step 5: Optional cleanup for nicer display
# -------------------------------------------------
def tidy(text):
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(raw_text)
print("\n=== Cleaned OCR Output ===")
print(clean_text)
```

**Očekávaný výstup** (váš skutečný text se samozřejmě liší):

```
=== Raw OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3

=== Cleaned OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3
```

Pokud vidíte nesmysly, zkontrolujte kvalitu obrázku (dobré osvětlení, minimální rozmazání) a ujistěte se, že jste v režimu `HANDWRITTEN`. Tyto dva faktory jsou zodpovědné za většinu chyb rozpoznávání.

## Často kladené otázky (FAQ)

| Question | Answer |
|----------|--------|
| **Mohu to použít k extrakci textu z PNG?** | Ano. `engine.load_image("scan.png")` funguje stejným způsobem. |
| **Co když je můj obrázek PDF stránka?** | Nejprve stránku převeďte na obrázek (např. pomocí `pdf2image`) a pak ji předáte engine. |
| **Je knihovna thread‑safe?** | Ano, můžete vytvořit samostatné objekty `OcrEngine` pro každý vláken. |
| **Jak se to liší od `pytesseract`?** | `ocr` abstrahuje binární soubor Tesseract a obsahuje vestavěný model pro ručně psaný text, takže není potřeba instalovat externí spustitelné soubory. |
| **Co když potřebuji **extract text from JPG** soubory hromadně?** | Zabalte skript do smyčky, nebo použijte `engine.load_image` na každý soubor a shromážděte výsledky do seznamu nebo CSV. |

## Okrajové případy a osvědčené postupy

1. **Fotografie s nízkým kontrastem** – Zvýšte kontrast programově před načtením, nebo použijte `engine.apply_preprocessing('contrast', level=2)`.
2. **Smíšený tištěný a ručně psaný text** – Proveďte dva průchody: nejprve s `HANDWRITTEN`, poté s `PRINTED`, a sloučte výstupy.
3. **Velké obrázky** – Zmenšete na šířku ~1500 px; OCR enginy obvykle pracují rychleji s menšími buffery bez ztráty přesnosti.
4. **Unicode znaky** – Knihovna vrací řetězce UTF‑8, takže můžete okamžitě zpracovávat emoji, diakritické znaky nebo matematické symboly.

## Závěr

Právě jsme prošli konkrétním příkladem, jak **perform OCR on image** soubory, konkrétně zaměřenými na ručně psané poznámky. Instalací balíčku `ocr`, nastavením engine na režim `HANDWRITTEN`, načtením fotografie a voláním `recognize()` můžete **convert handwritten image** data na čistý, prohledávatelný text.  

Odtud můžete **extract text from jpg** soubory hromadně, předat výstup do aplikace pro poznámky, nebo jej zkombinovat se syntézou řeči pro zpřístupnění. Možnosti jsou neomezené a výše uvedený kód vám poskytuje pevný základ pro experimentování.

Máte nějaký tip, který byste chtěli sdílet – možná jiný formát souboru nebo netradiční trik předzpracování? Zanechte komentář a pojďme konverzaci udržet. Šťastné programování a užívejte si převod těch čmáraných poznámek na digitální zlato!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}