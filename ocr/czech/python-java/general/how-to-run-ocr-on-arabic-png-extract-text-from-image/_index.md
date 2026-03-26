---
category: general
date: 2026-03-26
description: Naučte se, jak spustit OCR na arabských PNG obrázcích a rychle extrahovat
  arabský text. Tento průvodce ukazuje převod obrázku na text pomocí krok‑za‑krokem
  Python kódu.
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: cs
og_description: Jak spustit OCR na arabských PNG obrázcích? Postupujte podle tohoto
  kompletního návodu k extrakci arabského textu, rozpoznání arabského textu a převodu
  obrázku na text pomocí Pythonu.
og_title: Jak spustit OCR na arabském PNG – Extrahovat text z obrázku
tags:
- OCR
- Python
- Arabic
title: Jak spustit OCR na arabském PNG – Extrahovat text z obrázku
url: /cs/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak spustit OCR na arabském PNG – Extrahovat text z obrázku

Už jste se někdy zamýšleli **jak spustit OCR** na obrázku obsahujícím arabské písmo? Možná máte naskenovaný účet, historický rukopis nebo jen snímek obrazovky z sociální sítě a potřebujete text v prohledávatelném formátu. Nejste v tom sami – vývojáři po celém světě narazí na tento problém při práci s pravoto‑levými jazyky.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který ukazuje **jak spustit OCR** na souboru PNG, extrahovat arabský text a vytisknout výsledek do konzole. Žádné vágní odkazy typu „viz dokumentace“; jen kód, který můžete zkopírovat‑vložit, a vysvětlení, proč je každá řádka důležitá. Na konci budete schopni **převést obrázek na text** spolehlivě, i když zdrojový soubor je obtížný arabský PNG.

> **Co se naučíte**
> - Nastavit OCR engine v Pythonu pro arabštinu  
> - Načíst PNG obrázek a vyřešit běžné úskalí  
> - Rozpoznat arabský text a ověřit výstup  
> - Tipy pro **extrahování arabského textu** z různých kvalit obrázků  

Než se pustíme dál, ujistěte se, že máte nainstalovaný Python 3.8+ a aktuální verzi knihovny `ocr` (ta, která je použita v ukázce). Pokud používáte virtuální prostředí, aktivujte jej nyní – pomůže vám udržet závislosti přehledné.

## Požadavky

- Python 3.8 nebo novější  
- balíček `ocr` (`pip install ocr‑engine` – nahraďte skutečným názvem balíčku)  
- arabský PNG obrázek (`arabic_doc.png`) umístěný na místě, na které můžete odkazovat  
- Základní znalost funkcí a tříd v Pythonu  

To je vše. Žádné těžké frameworky, žádné Docker kontejnery – jen čistý Python.

## Krok 1: Instalace a import OCR knihovny

Nejprve potřebujeme samotný OCR engine. Knihovna, kterou použijeme, poskytuje třídu `OcrEngine` s přehledným API.

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*Proč importovat `Imaging` zvlášť?* Podmodul `Imaging` nám poskytuje pohodlnou metodu `Image.load`, která rozumí PNG, JPEG i TIFF přímo. Vynechání tohoto kroku by vás přinutilo pracovat s surovými bajty, což není pro většinu případů potřeba.

## Krok 2: Vytvoření instance OCR engine

Nyní vytvoříme instanci engine. Představte si tento objekt jako „mozek“, který bude obrázek zpracovávat.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **Pro tip:** Pokud plánujete zpracovávat mnoho obrázků po sobě, znovu použijte stejnou instanci `ocr_engine`. Tím se uloží jazykové modely do cache a urychlí následná rozpoznávání.

## Krok 3: Nastavení jazyka na arabštinu

Arabština není latinka; má vlastní znakovou sadu, směr zprava doleva a kontextové tvarování. Proto musíme engine explicitně říct, který jazykový model má načíst.

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

Pokud tuto řádku zapomenete, engine výchozí nastavení použije angličtinu a výstup bude zkomolený – něco, co jsem viděl příliš často.

## Krok 4: Načtení vašeho PNG obrázku

Zde skutečně začíná část **převést obrázek na text**. Načteme PNG soubor, který obsahuje arabské písmo.

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### Běžné okrajové případy

| Problém | Příznak | Řešení |
|---------|---------|--------|
| Obrázek je příliš tmavý | Výstup obsahuje spoustu prázdných míst | Předzpracujte pomocí Pillow (`ImageEnhance.Brightness`) |
| PNG má alfa kanál | Některé OCR enginy špatně čtou průhledné pixely | Před načtením převést na RGB (`image.convert("RGB")`) |
| Text je natočený | Rozpoznaný text je vzhůru nohama | Před předáním engine otočte obrázek (`image.rotate(90, expand=True)`) |

## Krok 5: Spuštění rozpoznávacího procesu

S všemi nastaveními na místě konečně požádáme engine, aby udělal svou práci.

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

Metoda `recognize` vrací objekt, který obsahuje surový Unicode řetězec, skóre důvěry a ohraničující rámečky. Pro většinu vývojářů stačí prostý text.

## Krok 6: Výpis rozpoznaného arabského textu

Nyní výsledek vytiskneme. V reálné aplikaci byste ho možná zapisovali do souboru, databáze nebo předávali překladatelskému API.

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

Po spuštění skriptu by se vám v konzoli měly zobrazit arabské znaky (ujistěte se, že váš terminál podporuje Unicode). Pokud vidíte otazníky nebo prázdné řetězce, zkontrolujte nastavení jazyka a kvalitu obrázku.

### Očekávaný výstup

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

Pokud výstup vypadá podobně jako řádek výše, gratulujeme – úspěšně jste **extrahovali arabský text** z PNG!

## Kompletní funkční příklad

Níže je celý skript připravený ke zkopírování. Nahraďte `YOUR_DIRECTORY/arabic_doc.png` cestou k vašemu souboru.

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

Spusťte ho pomocí `python run_ocr.py` (nebo jak jste soubor pojmenovali). Pokud je vše nainstalováno správně, uvidíte arabskou větu vytištěnou v konzoli.

## Jak spustit OCR na různých formátech obrázků

Stejný kód funguje pro JPEG, TIFF nebo BMP – stačí změnit příponu souboru. Metoda `Image.load` automaticky detekuje formát, takže můžete **převést obrázek na text** bez dalšího kódu.

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

Pamatujte, že kvalita vstupního obrázku výrazně ovlivňuje přesnost kroku **rozpoznat arabský text**. Vysoce rozlišené, málo komprimované obrázky dávají nejlepší výsledky.

## Extrahování textu z PNG: Tipy pro vyšší přesnost

1. **DPI má význam** – Cílem je alespoň 300 dpi. Nižší DPI často vede k vynechaným znakům.  
2. **Kontrast je král** – Použijte nástroje pro zpracování obrazu (např. OpenCV) ke zvýšení kontrastu před předáním obrázku OCR engine.  
3. **Odstranění šumu** – Malé skvrny mohou model zmást; pomůže medianové filtrování.  

Zde je rychlý úryvek používající Pillow pro vylepšení PNG před OCR:

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## Často kladené otázky

**Q: Funguje to i s pravoto‑levými jazyky jinými než arabštinou?**  
A: Ano. Stačí změnit kód jazyka (`"ar"` → `"he"` pro hebrejštinu, `"fa"` pro perštinu) a engine načte odpovídající model.

**Q: Co když potřebuji extrahovat text z více PNG souborů ve složce?**  
A: Projděte soubory ve smyčce, znovu použijte stejnou instanci `ocr_engine` a výsledky uložte do seznamu nebo do samostatných `.txt` souborů.

**Q: Můžu získat skóre důvěry pro každé slovo?**  
A: Ano. `ocr_result` často poskytuje metodu `get_confidences()`. Spojte každé skóre s odpovídajícím slovem pro kontrolu kvality.

## Další kroky

Nyní, když už víte **jak spustit OCR** na arabských PNG, zvažte následující rozšíření:

- **Dávkové zpracování:** Spojte skript s `os.listdir` a **extrahujte arabský text** z celého adresáře.  
- **Post‑processing:** Použijte knihovny `arabic_reshaper` a `python-bidi` pro správné zobrazení pravoto‑levého výstupu v PDF.  
- **Integrace:** Předejte extrahovaný text do vyhledávacího indexu (např. Elasticsearch), aby byly skenované dokumenty prohledávatelné.  

Každé z těchto témat staví na základech, které jsme zde probrali, a pomůže vám proměnit jednoduchý **převést obrázek na text** skript v produkční pipeline.

---

![how to run OCR on Arabic PNG](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}