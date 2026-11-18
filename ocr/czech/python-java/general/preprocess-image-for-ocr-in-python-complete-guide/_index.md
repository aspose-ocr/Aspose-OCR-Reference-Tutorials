---
category: general
date: 2026-06-25
description: Předzpracování obrázku pro OCR a rozpoznání textu ze skenovaného dokumentu
  pomocí Pythonu. Krok‑za‑krokem tutoriál s kompletním kódem.
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: cs
og_description: Předzpracujte obrázek pro OCR a rozpoznávejte text ze skenovaného
  dokumentu pomocí Pythonu. Sledujte tento podrobný, spustitelný návod.
og_title: Předzpracování obrázku pro OCR v Pythonu – Kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Předzpracování obrázku pro OCR v Pythonu – Kompletní průvodce
url: /cs/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Předzpracování obrázku pro OCR v Pythonu – Kompletní průvodce

Už jste se někdy zamýšleli, jak **preprocess image for OCR** tak, aby text byl čistý a spolehlivý? Nejste sami — většina vývojářů narazí na stejný problém, když je naskenovaná stránka poškozená nebo kontrast je špatný. Dobrou zprávou je, že několik řádků Pythonu může ten nepořádek narovnat, binarizovat obrázek a vrátit vám ostrý, prohledávatelný text.

V tomto tutoriálu projdeme přesné kroky k **preprocess image for OCR** *a* **recognize text from scanned document** souborům pomocí populární OCR knihovny. Na konci budete mít připravený spustitelný skript, pochopíte, proč má každé nastavení význam, a budete vědět, jak jej upravit pro obtížné okrajové případy.

## Co budete potřebovat

- Python 3.8 nebo novější (kód funguje také na 3.10+)
- OCR balíček, který poskytuje třídy `OcrEngine`, `ImagePreProcessingOptions` a `Image` (např. fiktivní modul `ocr` použitý v příkladu)
- Naskenovaný nebo vyfocený dokument, který je mírně zkosený nebo má nízký kontrast
- Vaše oblíbené IDE nebo jednoduchý terminál — žádné těžké GUI není potřeba

To je vše. Žádné extra binární soubory, žádné Docker akrobacie. Ponořme se.

## Předzpracování obrázku pro OCR – Krok za krokem

Níže je hlavní workflow rozdělený do pěti jasných fází. Každá fáze obsahuje **proč** to děláme, přesný **kód** a krátké **vysvětlení**, co se děje pod kapotou.

### Krok 1: Vytvořte instanci OCR Engine

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Proč je to důležité:*  
`OcrEngine` objekt je mozkem operace. Uchovává konfiguraci jako jazykové balíčky, prahy důvěry a — co je pro nás nejdůležitější — příznaky pro předzpracování obrazu. Jeho vytvoření jako první nám dává čistý základ pro povolení následujících triků.

### Krok 2: Povolit automatické narovnání a binarizaci

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*Proč je to důležité:*  
- **Deskewing** otáčí obrázek tak, aby řádky textu byly vodorovné. OCR enginy mají potíže, když se základní linie nakloní o více než několik stupňů.  
- **Binarization** převádí obrázek na čistou černobílou, odstraňuje šum pozadí, který může zmást klasifikátory znaků.  
- Obě možnosti jsou v mnoha moderních knihovnách *automatické*, ale stále je musíte zapnout — proto je zde explicitní přiřazení.

> **Tip:** Pokud jsou vaše zdrojové obrázky již dokonale zarovnané, můžete nastavit `auto_deskew=False`, abyste ušetřili milisekundu času zpracování.

### Krok 3: Načtěte zkosený obrázek, který chcete zpracovat

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*Proč je to důležité:*  
Metoda `Image.load` načte soubor do paměti a zabalí jej do objektu, který OCR engine rozumí. Také extrahuje metadata jako DPI, což může ovlivnit výchozí faktor škálování pro narovnání.

> **Okrajový případ:** Pokud je obrázek multi‑page TIFF, budete muset iterovat přes každou stránku nebo použít pomocníka jako `ocr.MultiPageImage.load`. Stejné nastavení předzpracování se použije na každou stránku.

### Krok 4: Proveďte OCR na předzpracovaném obrázku

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*Proč je to důležité:*  
V tomto okamžiku engine aplikuje kroky narovnání a binarizace, které jsme povolili dříve, a poté spustí svou neuronovou síť (nebo klasický pipeline ve stylu Tesseract) na vyčištěném bitmapu. Vrácený objekt `result` obvykle obsahuje prostý text, skóre důvěry a někdy i poziční data pro každé slovo.

> **Co když je text stále rozmazaný?**  
Zkontrolujte rozlišení obrázku: OCR funguje nejlépe při 300 dpi nebo vyšším. Pokud je váš zdroj nižší, zvažte zvětšení před načtením, nebo požádejte o originální sken od zdroje dokumentu.

### Krok 5: Výstup rozpoznaného textu

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*Proč je to důležité:*  
`result.text` je prostý řetězec představující vše, co engine dokázal přečíst. Vytištění je užitečné pro rychlé ladění; ve skutečné aplikaci byste jej pravděpodobně zapsali do souboru `.txt`, databáze nebo ho předali do následného NLP pipeline.

---

## Rozpoznání textu ze skenovaného dokumentu – Pokročilejší techniky

Nyní, když základní pipeline funguje, prozkoumejme několik běžných variant, na které můžete narazit, když se pokusíte **recognize text from scanned document** obrázky v reálném světě.

### 1. Zpracování více jazyků

Pokud váš dokument obsahuje jak angličtinu, tak francouzštinu, nakonfigurujte engine před krokem 1:

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

Většina OCR engineů přijímá kódy ISO‑639‑2; načtení extra jazykových balíčků přidá malou režii, ale dramaticky zlepší přesnost na vícejazykových stránkách.

### 2. Jemné ladění prahů binarizace

Automatická binarizace funguje pro většinu případů, ale některé staré fotokopie potřebují vlastní práh:

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

Experimentujte s hodnotami mezi 120 a 220, dokud pozadí nezmizí, aniž by se vymazaly slabé znaky.

### 3. Extrahování informací o rozložení

Někdy potřebujete víc než surový text — chcete vědět, kde se na stránce nachází každý odstavec. Mnoho engineů poskytuje kolekci `result.blocks`:

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

To je neocenitelné pro rekonstrukci tabulek nebo zachování pořadí sloupců.

### 4. Zpracování dávky souborů

Pokud máte složku plnou skenovaných PDF převedených na JPEG, zabalte celý tok do smyčky:

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

Smyčka znovu použije stejnou instanci `engine`, což je efektivnější než její opětovné vytvoření pro každý soubor.

### 5. Práce s nízkým rozlišením skenů

Nízké rozlišení obrázků (< 150 dpi) často produkuje rozmazané znaky. Rychlým řešením je zvětšit pomocí vysoce kvalitního algoritmu před předáním obrázku OCR engineu:

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

Zvětšení nevytvoří magicky detail, ale krok binarizace může pracovat s ostřejšími hranami, což poskytne mírné zlepšení.

## Očekávaný výstup

Spuštění původního pětikrokového skriptu na mírně zkoseném, 300 dpi skenu by mělo vypsat něco jako:

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

Pokud vidíte rozmazané znaky, dvojitě zkontrolujte příznaky předzpracování, rozlišení obrázku a konfiguraci jazyka.

## Závěr

Probrali jsme vše, co potřebujete k **preprocess image for OCR** a **recognize text from scanned document** souborům pomocí Pythonu. Začali jsme s čerstvou instancí engine, povolili automatické narovnání a binarizaci, načetli zkosený obrázek, spustili rozpoznání a vytiskli čistý text. Během toho jsme prozkoumali podporu více jazyků, ruční úpravy prahů, extrakci rozložení, dávkové zpracování a řešení pro nízké rozlišení.

Vyzkoušejte skript na vlastních skenech — možná hromadu účtenek, ručně psaný formulář nebo starý výstřižek z novin. Jakmile budete mít jistotu, zkuste přidat generování PDF nebo předat výstup do vyhledávacího indexu. Možnosti jsou neomezené.

**Jste připraveni na další výzvu?** Podívejte se na naše tutoriály o *„Extrahování tabulek ze skenovaných PDF pomocí Pythonu“* a *„Trénování vlastních OCR modelů s TensorFlow“*, abyste dále rozšiřovali svou sadu nástrojů pro automatizaci dokumentů.

Šťastné kódování a ať je vaše OCR vždy ostré!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}