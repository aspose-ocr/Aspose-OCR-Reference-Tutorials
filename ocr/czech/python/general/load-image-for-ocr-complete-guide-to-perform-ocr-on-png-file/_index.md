---
category: general
date: 2026-06-25
description: Načtěte obrázek pro OCR a proveďte OCR na PNG pomocí krok‑za‑krokem Python
  tutoriálu s aocr. Naučte se ladění, logování a osvědčené postupy.
draft: false
keywords:
- load image for OCR
- perform OCR on PNG
- aocr logging setup
- OCR debugging Python
- image preprocessing OCR
language: cs
og_description: Načtěte obrázek pro OCR a proveďte OCR na PNG pomocí aocr. Tento průvodce
  vás provede logováním, načítáním obrázku a rozpoznáváním s kompletním kódem.
og_title: Načtení obrázku pro OCR – krok za krokem Python tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Load image for OCR and perform OCR on PNG with a step‑by‑step Python
    tutorial using aocr. Learn debugging, logging, and best practices.
  headline: Load Image for OCR – Complete Guide to Perform OCR on PNG Files
  type: TechArticle
- questions:
  - answer: Usually not. `aocr` handles PNG natively, but if the image is huge (>10
      MP) you might want to downscale first to speed up processing.
    question: Do I need to convert the PNG to another format?
  - answer: Rotate the log after each run or limit the level to `INFO` once you’re
      confident the pipeline works.
    question: What if the logger file grows too large?
  - answer: Absolutely. Just call `ocr_png` for each file; the function creates a
      fresh logger each time, keeping logs isolated.
    question: Can I process multiple images in a loop?
  - answer: Yes – `engine.result` also contains `boxes` and `confidences`. Explore
      the `aocr` docs for `result.boxes` if you need layout information.
    question: Is there a way to get bounding boxes instead of plain text?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Načtení obrázku pro OCR – Kompletní průvodce prováděním OCR na PNG souborech
url: /cs/python/general/load-image-for-ocr-complete-guide-to-perform-ocr-on-png-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Načtení obrázku pro OCR – Kompletní průvodce prováděním OCR na PNG souborech

Už jste někdy potřebovali **načíst obrázek pro OCR**, ale nebyli jste si jisti, jak nastavit správné ladění? Nejste v tom sami. V mnoha projektech je první překážkou dostat ten PNG do enginu a zároveň mít přehled o tom, co se děje pod kapotou.  

V tomto tutoriálu vás provedeme vším, co potřebujete k **provádění OCR na PNG** souborech pomocí knihovny `aocr` – od nastavení loggeru pro podrobný výstup až po samotné rozpoznání textu. Na konci budete mít znovupoužitelný skript, který můžete vložit do libovolného Python projektu, a pochopíte, proč je každá část důležitá.

## Co se naučíte

- Jak inicializovat logger `aocr`, abyste mohli sledovat každý krok.
- Přesný kód pro **načtení obrázku pro OCR** pomocí `aocr.OcrEngine`.
- Jak nastavit úroveň logování pro získání detailních ladicích informací.
- Spuštění enginu pro **provádění OCR na PNG** a získání výsledků.
- Tipy pro řešení běžných problémů, jako chybějící soubory nebo nepodporované formáty.

Předchozí zkušenost s `aocr` není vyžadována; stačí funkční instalace Python 3 a obrázek, který chcete přečíst. Pojďme na to.

![load image for OCR example](assets/load-image-ocr.png "Illustration of loading an image for OCR in Python")

## Požadavky

| Požadavek | Proč je důležitý |
|-----------|-------------------|
| Python 3.8+ | `aocr` cílí na moderní interpretery a používá typové nápovědy. |
| knihovna `aocr` nainstalovaná (`pip install aocr`) | Bez balíčku nebudou existovat třídy, které používáme. |
| PNG obrázek, který chcete číst | Tutoriál se zaměřuje na **provádění OCR na PNG**, takže PNG je nezbytný. |
| Oprávnění zápisu do adresáře s logy | Logger potřebuje vytvořit soubor `ocr_debug.log`. |

Pokud vám něco chybí, nainstalujte to hned – zabere to jen minutu.

```bash
pip install aocr
```

## Krok 1: Načtení obrázku pro OCR – Inicializace logování

Než se vůbec dotknete obrázku, nastavte logger. Ladění OCR může být noční můra, pokud nevidíte, co engine dělá. Třída `aocr.Logging` zapisuje vše do souboru a nastavením úrovně na `DEBUG` uvidíte každý interní volání.

```python
import aocr

# Create a logger instance
ocr_logger = aocr.Logging()
# Choose where the log file will live – adjust the path to suit your project
ocr_logger.set_output_file("logs/ocr_debug.log")

# DEBUG gives you the most detail; you can switch to INFO for less noise
ocr_logger.set_level(aocr.LoggingLevel.DEBUG)
```

**Proč je to důležité:**  
Pokud OCR engine nenajde soubor nebo formát obrázku není podporován, logger zachytí výjimku a stack trace. To vás zachrání před nekonečným hádáním později.

## Krok 2: Provádění OCR na PNG – Konfigurace enginu

Nyní, když je logger připraven, připojte ho k OCR engine. Tento krok je spojuje, takže každá akce enginu je zaznamenána.

```python
# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
# Plug the logger into the engine
ocr_engine.logging = ocr_logger
```

**Pro tip:**  
Stejnou instanci `ocr_engine` můžete znovu použít pro více obrázků. Jen nezapomeňte vyčistit předchozí stav, pokud zpracováváte dávku.

## Krok 3: Načtení obrázku pro OCR – Načtení PNG souboru

Zde je jádro tutoriálu: skutečně **načíst obrázek pro OCR**. Metoda `load_image` přijímá cestu k souboru; interně dekóduje PNG do bitmapy, kterou engine rozumí.

```python
# Path to the PNG you want to read
image_path = "samples/invoice.png"

# Load the image – this is where we “load image for OCR”
ocr_engine.load_image(image_path)
```

### Okrajové případy, na které si dát pozor

1. **Soubor nenalezen** – Pokud je cesta špatná, `aocr` vyhodí `FileNotFoundError`. Logger to zaznamená, ale můžete to také zachytit:

   ```python
   try:
       ocr_engine.load_image(image_path)
   except FileNotFoundError as e:
       print(f"❌ Could not locate {image_path}: {e}")
       raise
   ```

2. **Nepodporovaný formát** – Přestože PNG je široce podporováno, poškozený soubor může vyvolat `UnsupportedFormatError`. V takovém případě zvažte převod obrázku na čistý PNG pomocí Pillow před načtením.

## Krok 4: Provádění OCR na PNG – Spuštění rozpoznání

Jakmile je obrázek v paměti, můžete konečně **provést OCR na PNG**. Metoda `recognize` spustí pipeline enginu (předzpracování, segmentace, klasifikace) a naplní objekt výsledku.

```python
# Execute the OCR process
ocr_engine.recognize()
```

Po tomto volání engine drží rozpoznaný text. K němu můžete přistupovat přes atribut `result`:

```python
# Retrieve the plain text output
recognized_text = ocr_engine.result.text
print("📝 OCR Result:")
print(recognized_text)
```

**Proč byste měli výsledek zkontrolovat:**  
Některé OCR enginy vracejí prázdné řetězce u nízkokontrastních obrázků. Okamžité zobrazení výsledku vám umožní rozhodnout, zda je potřeba předzpracovat (např. zvýšit kontrast) před dalším spuštěním.

## Krok 5: Zabalit vše dohromady – Znovupoužitelná funkce

Složení všech částí do jedné funkce usnadní volání z jiných skriptů nebo webové služby. Tím také ukážete, jak **načíst obrázek pro OCR** a **provést OCR na PNG** v jednom přehledném balíčku.

```python
def ocr_png(image_path: str, log_dir: str = "logs") -> str:
    """
    Load a PNG image, run aocr OCR, and return the extracted text.
    
    Parameters
    ----------
    image_path : str
        Full path to the PNG file.
    log_dir : str, optional
        Directory where the debug log will be written.
    
    Returns
    -------
    str
        The plain‑text OCR result.
    """
    import os
    import aocr

    # Ensure the log directory exists
    os.makedirs(log_dir, exist_ok=True)

    # ---------- Logging ----------
    logger = aocr.Logging()
    logger.set_output_file(os.path.join(log_dir, "ocr_debug.log"))
    logger.set_level(aocr.LoggingLevel.DEBUG)

    # ---------- Engine ----------
    engine = aocr.OcrEngine()
    engine.logging = logger

    # ---------- Load Image ----------
    try:
        engine.load_image(image_path)
    except Exception as exc:
        logger.error(f"Failed to load image {image_path}: {exc}")
        raise

    # ---------- Recognize ----------
    engine.recognize()
    return engine.result.text

# Example usage
if __name__ == "__main__":
    txt = ocr_png("samples/invoice.png")
    print("\n--- Extracted Text ---\n")
    print(txt)
```

Spuštěním skriptu se vytvoří podrobný `ocr_debug.log` ve složce `logs` a poté se rozpoznaný text vypíše do konzole. Máte nyní **utility pro provádění OCR na PNG**, kterou můžete importovat kamkoli.

## Časté otázky a úskalí

- **Musím PNG převádět do jiného formátu?**  
  Obvykle ne. `aocr` zvládá PNG nativně, ale pokud je obrázek obrovský (>10 MP), můžete ho nejprve zmenšit, aby se zrychlilo zpracování.

- **Co když soubor s logy naroste příliš velký?**  
  Rotujte log po každém běhu nebo omezte úroveň na `INFO`, jakmile budete mít pipeline pod kontrolou.

- **Mohu zpracovávat více obrázků v cyklu?**  
  Rozhodně. Stačí zavolat `ocr_png` pro každý soubor; funkce vytvoří čerstvý logger při každém volání, takže logy zůstanou oddělené.

- **Existuje způsob, jak získat ohraničující rámečky místo prostého textu?**  
  Ano – `engine.result` také obsahuje `boxes` a `confidences`. Prozkoumejte dokumentaci `aocr` k `result.boxes`, pokud potřebujete informace o rozložení.

## Závěr

Nyní víte, jak **načíst obrázek pro OCR** a **provést OCR na PNG** pomocí knihovny `aocr`, včetně robustního nastavení logování, které usnadňuje ladění. Ukázková funkce zapouzdřuje celý workflow, takže ji můžete vložit do libovolného projektu a okamžitě začít extrahovat text.

Další kroky? Zkuste engine napájet různými typy obrázků (JPEG, TIFF) a podívejte se, jak se mění přesnost, nebo experimentujte s předzpracováním, jako je prahování, abyste zlepšili výsledky u špinavých skenů. A pokud vás zajímá extrakce strukturovaných dat (tabulky, formuláře), podívejte se na sekce `aocr` o analýze rozvržení – skvěle doplňují to, co jste právě vytvořili.

Šťastné kódování a ať jsou vaše OCR pipeline vždy bez chyb!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}