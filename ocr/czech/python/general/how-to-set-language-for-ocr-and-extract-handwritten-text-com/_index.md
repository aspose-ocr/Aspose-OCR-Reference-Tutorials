---
category: general
date: 2026-03-26
description: Jak nastavit jazyk v OCR enginu a extrahovat ručně psaný text z obrázků
  – krok za krokem tutoriál pro převod obrázku na text.
draft: false
keywords:
- how to set language
- extract handwritten text
- convert image to text
- how to extract handwritten
- recognize handwritten notes
language: cs
og_description: Jak nastavit jazyk v OCR enginu a extrahovat ručně psané poznámky
  z obrázků. Naučte se převést obrázek na text během několika minut.
og_title: Jak nastavit jazyk pro OCR – Snadno extrahujte ručně psaný text
tags:
- OCR
- Python
- Image Processing
title: Jak nastavit jazyk pro OCR a extrahovat ručně psaný text – kompletní průvodce
url: /cs/python/general/how-to-set-language-for-ocr-and-extract-handwritten-text-com/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak nastavit jazyk pro OCR a extrahovat ručně psaný text – Kompletní průvodce

Už jste se někdy zamysleli **jak nastavit jazyk** ve vašem OCR enginu, aby skutečně rozuměl znakům, které potřebujete? Možná máte fotografii nákupního seznamu, poznámky ze schůzky nebo skicovaného diagramu a prostě se vám nedaří získat text. Dobrá zpráva? Nepotřebujete PhD z počítačového vidění – stačí pár řádků Pythonu a správné přepínače.

V tomto tutoriálu projdeme přesné kroky k **extrahování ručně psaného textu** z PNG, převodu tohoto obrázku na prostý text a vysvětlíme „proč“ za každým nastavením. Na konci budete schopni rozpoznávat ručně psané poznámky v jakémkoli projektu, ať už jde o aplikaci pro psaní poznámek nebo dávkový zpracovatelský pipeline.

> **Co budete potřebovat**  
> • Python 3.8+ (kód funguje také s 3.10)  
> • Knihovna `ocr` (nebo jakýkoli kompatibilní wrapper, který poskytuje `OcrEngine`)  
> • Ukázkový obrázek jako `note_handwritten.png` – jakýkoli obrázek s rozšířenými latinskými znaky bude stačit.

Pojďme začít.

---

## Jak nastavit jazyk a povolit rozpoznávání ručně psaného textu

První věc, kterou musíte udělat, je říct OCR enginu, jakou abecedu má očekávat. Pokud tento krok přeskočíte, engine se výchozí nastavení vrátí k obecné sadě, která často špatně rozpoznává diakritické znaky nebo speciální symboly.

```python
import ocr  # Assuming the library is named `ocr`

# Step 1: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Step 2: Choose the language that includes extended Latin characters
ocr_engine.language = ocr.Language.ExtendedLatin

# Step 3: Turn on the handwritten‑text flag
ocr_engine.recognize_handwritten = True
```

**Proč je to důležité:**  
- **ExtendedLatin** pokrývá znaky jako “ñ”, “ø” a “ç”, které jsou běžné v mnoha evropských poznámkách.  
- Přepínač `recognize_handwritten` přepíná podkladový model z OCR tištěného textu na neuronovou síť trénovanou na kurzívní tahy. Bez něj engine považuje vaše čmáranice za šum.

> **Tip:** Pokud zpracováváte dokumenty v několika jazycích, vytvořte samostatný engine pro každý jazyk nebo dynamicky přepínejte `ocr_engine.language` před každým voláním. Tím se vyhnete režii načítání nepoužívaných sad znaků.

![Snímek obrazovky konfigurace OCR enginu ukazující, jak nastavit jazyk](/images/ocr-set-language.png "Jak nastavit jazyk na OCR engine")

*Text obrázku: “Jak nastavit jazyk na konfigurační obrazovce OCR enginu.”*

## Extrahovat ručně psaný text z PNG obrázku

Nyní, když engine ví, co hledat, je čas mu předat obrázek. Metoda `recognize_image` vrací bohatý objekt výsledku; atribut `text` obsahuje prostý řetězec, který vás zajímá.

```python
# Step 4: Perform OCR on the input image
handwritten_result = ocr_engine.recognize_image("YOUR_DIRECTORY/note_handwritten.png")

# Step 5: Print the extracted text
print(handwritten_result.text)
```

When you run the script, you should see something like:

```
Buy milk
Call Dr. García at 5 pm
Pick up résumé
```

Tento výstup dokazuje, že jste úspěšně **převáděli obrázek na text** a že engine respektoval nastavení jazyka, které jste zadali.

**Časté úskalí**  
- **Nesprávná cesta** – Zkontrolujte umístění souboru; chybějící soubor vyvolá `FileNotFoundError`.  
- **Nízké rozlišení obrázku** – Ručně psané OCR má problémy pod 300 dpi. Zvětšete nebo přeškárujte, pokud výstup vypadá poškozeně.  
- **Inverze barev** – Pokud je pozadí tmavé a inkoust světlý, nejprve invertujte barvy (`Pillow` může pomoci).

## Převést obrázek na text pomocí pomocné funkce

Pokud plánujete spouštět OCR na desítky souborů, zabalte logiku do znovupoužitelné funkce. To také usnadní testování kódu a integraci s dalšími pipeline.

```python
def extract_handwritten_text(image_path: str) -> str:
    """
    Loads an image, sets the OCR engine to ExtendedLatin,
    enables handwritten recognition, and returns the plain text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()   # Remove leading/trailing whitespace


# Example usage
if __name__ == "__main__":
    txt = extract_handwritten_text("YOUR_DIRECTORY/note_handwritten.png")
    print("📝 Handwritten notes:\n", txt)
```

Pomocná funkce izoluje logiku **jak extrahovat ručně psaný** text, takže ji můžete volat z Flask endpointu, CLI nástroje nebo dávkové úlohy, aniž byste pokaždé přepisovali konfiguraci.

## Rozpoznávat ručně psané poznámky v reálných scénářích

Níže jsou uvedeny některé situace, kdy pravděpodobně budete potřebovat **rozpoznávat ručně psané poznámky** a jak se toto nastavení přizpůsobí:

| Scénář | Proč je jazyk důležitý | Navrhovaná úprava |
|----------|---------------------|-----------------|
| **Vícejazyčné nákupní seznamy** | Položky mohou obsahovat diakritiku (např. “crème”) | Přepněte `ocr_engine.language` podle seznamu nebo použijte `ocr.Language.AutoDetect`, pokud je podporováno |
| **Fotografie tabulí ve třídě** | Křída může vytvářet slabé tahy | Zvyšte kontrast obrázku před předáním enginu |
| **Lékařské předpisy** | Ručně psané je notoricky nečitelné | Spojte OCR se slovníkem pro opravu pravopisu názvů léků |

V každém případě jsou základní kroky—**jak nastavit jazyk**, povolit režim ručně psaného textu a zavolat `recognize_image`—identické. Tato konzistence je to, co dělá přístup robustním a snadno udržovatelným.

## Okrajové případy a pokročilé úpravy

1. **Dávkové zpracování** – Načtěte engine jednou, projděte soubory v cyklu a měňte atribut `language` jen podle potřeby. Tím se sníží režie inicializace.  
2. **Není‑latinské skripty** – Pokud potřebujete zpracovat cyrilici nebo arabštinu, nahraďte `ExtendedLatin` příslušným enumem (např. `ocr.Language.Cyrillic`). Platí stejný vzor.  
3. **Částečné rozpoznání** – Někdy engine vrátí prázdné řetězce pro velmi krátké tahy. Rychlá kontrola (`if not result.text.strip(): …`) vám umožní přejít na sekundární model nebo požádat uživatele o opětovné skenování.  
4. **Profilování výkonu** – Pro velké datové sady měřte dobu volání `recognize_image`. Pokud se stane úzkým hrdlem, zvažte paralelizaci pomocí `concurrent.futures.ThreadPoolExecutor`.

## Kompletní funkční příklad

Níže je kompletní skript, který můžete zkopírovat a vložit do souboru pojmenovaného `handwritten_ocr.py`. Obsahuje parsování argumentů, takže můžete nasměrovat na libovolný obrázek z příkazové řádky.

```python
#!/usr/bin/env python3
"""
handwritten_ocr.py – Convert an image containing handwritten notes
to plain text using the OCR library.

Usage:
    python handwritten_ocr.py path/to/image.png
"""

import sys
import argparse
import ocr  # Replace with the actual import if the library name differs


def extract_handwritten_text(image_path: str) -> str:
    """Extracts handwritten text from the given image."""
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()


def main():
    parser = argparse.ArgumentParser(
        description="Convert handwritten image to text (how to set language, extract handwritten text)."
    )
    parser.add_argument("image", help="Path to the PNG/JPG image containing handwritten notes")
    args = parser.parse_args()

    try:
        text = extract_handwritten_text(args.image)
        if text:
            print("✅ Extracted text:\n", text)
        else:
            print("⚠️ No text detected – try a higher‑resolution image.")
    except Exception as e:
        print(f"❌ Error processing {args.image}: {e}", file=sys.stderr)
        sys.exit(1)


if __name__ == "__main__":
    main()
```

Run it like:

```bash
python handwritten_ocr.py YOUR_DIRECTORY/note_handwritten.png
```

Měli byste vidět stejný výstup jako v předchozím úryvku, což potvrzuje, že jste úspěšně **převáděli obrázek na text** a **rozpoznali ručně psané poznámky**.

## Závěr

Probrali jsme **jak nastavit jazyk** na OCR engine, zapnuli přepínač pro ručně psaný text a vytvořili znovupoužitelnou funkci, která **extrahuje ručně psaný text** z libovolného obrázku. Dodržením výše uvedených kroků můžete spolehlivě **převádět obrázek na text**, ať už pracujete s jednou poznámkou nebo s obrovským archivem skenovaných dokumentů.

Dále zkuste experimentovat s různými jazykovými balíčky, dávkově zpracovat složku obrázků nebo integrovat tuto logiku do webové služby, která vrací JSON výsledky. Základy zůstávají stejné a flexibilita knihovny `ocr` znamená, že se můžete přizpůsobit téměř jakémukoli případu použití.

Máte otázky ohledně okrajových případů, výkonu nebo rozšíření skriptu na jiné jazyky? Zanechte komentář nebo mě kontaktujte na GitHubu – šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}