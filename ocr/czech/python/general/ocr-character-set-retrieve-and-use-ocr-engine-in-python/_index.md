---
category: general
date: 2026-06-06
description: 'Průvodce znakovou sadou OCR: naučte se, jak použít OCR engine k výpisu
  podporovaných znaků pro latinské a cyrilské skripty s kompletními příklady v Pythonu.'
draft: false
keywords:
- ocr character set
- use OCR engine
- supported OCR characters
- script detection OCR
- OCR library Python
language: cs
og_description: 'Průvodce znakovou sadou OCR: objevte, jak v Pythonu použít OCR engine
  k výpisu podporovaných znaků pro různé skripty, včetně kódu a tipů.'
og_title: Sada znaků OCR – Získání a použití OCR enginu
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: 'OCR character set guide: learn how to use OCR engine to list supported
    characters for Latin and Cyrillic scripts with full Python examples.'
  headline: OCR Character Set – Retrieve and Use OCR Engine in Python
  type: TechArticle
tags:
- OCR
- Python
- Character Sets
title: Sada znaků OCR – Získání a použití OCR motoru v Pythonu
url: /cs/python/general/ocr-character-set-retrieve-and-use-ocr-engine-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR znaková sada – Získání a použití OCR enginu v Pythonu

Chcete vědět, jakou **ocr character set** vaše knihovna podporuje? V tomto tutoriálu vám ukážeme, jak **use OCR engine** k dotazu na podporované znaky pro různé skripty a proč je to důležité pro reálné projekty.

Pokud jste někdy zírali na prázdnou obrazovku a přemýšleli, proč se některá písmena po zpracování OCR nikdy neobjevila, nejste sami. Odpověď je často skryta v sadě znaků, kterou engine zná. Na konci tohoto průvodce budete schopni:

* Vypsat každý znak, který OCR engine dokáže rozpoznat pro daný skript.  
* Ošetřit případy, kdy skript není podporován.  
* Vložit informace o znakové sadě do následné validace nebo UI logiky.

Žádné magické triky v černé skříňce – jen čistý Python, pár řádků kódu a trochu vysvětlení.

---

## Požadavky

Než se pustíme dál, ujistěte se, že máte:

* Nainstalovaný Python 3.8+ (kód používá f‑stringy).  
* Knihovnu OCR, která poskytuje `ocr.OcrEngine` – pro tento příklad předpokládáme, že balíček nazvaný `ocr` je již nainstalován pomocí `pip install ocr-lib`.  
* Základní znalost import systému v Pythonu a výpisu (printing).

Pokud knihovnu postrádáte, spusťte:

```bash
pip install ocr-lib
```

A to je vše – žádné další binární soubory ani nativní závislosti nejsou potřeba pro základní dotazy na sadu znaků, které provedeme.

## Krok 1: Inicializace instance OCR enginu

Vytvoření objektu enginu je první věc, kterou uděláte, když **use OCR engine** funkčnost. Představte si to jako zapnutí skeneru; bez něj nemůžete klást žádné otázky.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Třída `OcrEngine` je lehký obal kolem podkladového rozpoznávacího enginu. Nespouští těžké zpracování, dokud o něco nepožádáte, takže náklady na spuštění jsou zanedbatelné.

> **Pro tip:** Pokud vaše aplikace vytváří mnoho instancí enginu, znovu použijte jedinou. Šetří paměť a snižuje latenci inicializace.

## Krok 2: Dotaz na OCR znakovou sadu pro konkrétní skript

Nyní, když máme engine, můžeme se ho zeptat, které znaky zná pro konkrétní psací systém. Metoda `get_supported_characters(script_name)` vrací Python `list` Unicode znaků.

```python
# Step 2: Get the list of characters the engine can recognize for the Latin script
latin_chars = engine.get_supported_characters("Latin")
print(f"Supported Latin chars ({len(latin_chars)}): {latin_chars}")
```

Spuštění výše uvedeného úryvku vytiskne něco jako:

```
Supported Latin chars (26): ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
```

Přesný výstup závisí na verzi OCR knihovny, ale vždy získáte plochý seznam znaků. Pokud potřebujete jak velká, tak malá písmena, jednoduše požádejte o skript `"Latin"` a poté na každý prvek aplikujte `.lower()`, nebo dotazujte samostatný skript `"Latin‑lower"`, pokud knihovna rozlišuje.

### Proč je to důležité?

Když předáte obrázek obsahující neobvyklé diakritické znaky (např. “ñ” nebo “ø”), OCR engine je může tiše nahradit zástupným znakem nebo je úplně zahodit. Znalost **ocr character set** předem vám umožní předvalidovat vstup, varovat uživatele nebo přejít na jiný engine.

## Krok 3: Získání znaků pro jiný skript – Příklad Cyrilice

Stejná metoda funguje pro jakýkoli skript, který engine tvrdí, že podporuje. Podívejme se, co se stane s Cyrilicí.

```python
# Step 3: Get the list of characters the engine can recognize for the Cyrillic script
cyrillic_chars = engine.get_supported_characters("Cyrillic")
print(f"Supported Cyrillic chars ({len(cyrillic_chars)}): {cyrillic_chars}")
```

Typický výstup:

```
Supported Cyrillic chars (33): ['А', 'Б', 'В', 'Г', 'Д', 'Е', 'Ё', 'Ж', 'З', 'И', 'Й', 'К', 'Л', 'М', 'Н', 'О', 'П', 'Р', 'С', 'Т', 'У', 'Ф', 'Х', 'Ц', 'Ч', 'Ш', 'Щ', 'Ъ', 'Ы', 'Ь', 'Э', 'Ю', 'Я']
```

Pokud engine **ne** podporuje požadovaný skript, obvykle vyvolá `ValueError` (nebo vrátí prázdný seznam v závislosti na implementaci). Ochráníme se proti tomu.

```python
def safe_get_characters(engine, script):
    try:
        chars = engine.get_supported_characters(script)
        if not chars:
            print(f"No characters returned for script '{script}'.")
        else:
            print(f"Supported {script} chars ({len(chars)}): {chars}")
        return chars
    except Exception as e:
        print(f"Error retrieving characters for script '{script}': {e}")
        return []

# Example usage:
safe_get_characters(engine, "Arabic")   # Might trigger the error branch
```

## Krok 4: Vizualizace OCR znakové sady (volitelné)

Někdy rychlá vizualizace pomůže, zejména když potřebujete ukázat zainteresovaným stranám, které znaky jsou pokryty. Níže je minimální příklad používající `matplotlib` k vykreslení mřížky znaků.

```python
import matplotlib.pyplot as plt

def plot_character_grid(chars, title="OCR Character Set"):
    cols = 10
    rows = (len(chars) + cols - 1) // cols
    fig, ax = plt.subplots(figsize=(cols, rows))
    ax.set_axis_off()
    for idx, ch in enumerate(chars):
        row = idx // cols
        col = idx % cols
        ax.text(col / cols, 1 - row / rows, ch, fontsize=14, ha='center', va='center')
    plt.title(title)
    plt.show()

# Visualize Latin characters
plot_character_grid(latin_chars, title="Latin OCR Character Set")
```

> **Image alt text:** ![Diagram sady znaků OCR](ocr_character_set.png){alt="Přehled sady znaků OCR"}

Diagram není vyžadován pro hlavní řešení, ale ukazuje, jak můžete **use OCR engine** metadata využít nad rámec prostého výpisu.

## Krok 5: Integrace znakové sady do reálných pracovních toků

Nyní, když můžeme získat **ocr character set**, podívejme se na praktický scénář: validace výstupu OCR před jeho uložením do databáze.

```python
def validate_ocr_output(text, allowed_chars):
    """Return True if every character in `text` exists in `allowed_chars`."""
    invalid = [c for c in text if c not in allowed_chars]
    if invalid:
        print(f"Invalid characters found: {invalid}")
        return False
    return True

# Suppose we ran OCR on an image and got this result:
ocr_result = "HELLO WORLD!"

# Use the previously fetched Latin set for validation:
if validate_ocr_output(ocr_result, set(latin_chars)):
    print("All characters are supported – safe to store.")
else:
    print("Result contains unsupported symbols – consider manual review.")
```

Tento vzor zabraňuje tomu, aby se špatná data dostala do následných pipeline, což je častý problém při práci s vícejazyčnými dokumenty.

## Časté úskalí a okrajové případy

| Pitfall | Why it Happens | How to Avoid |
|---------|----------------|--------------|
| **Chyba v názvu skriptu** (např. `"Cyrillic "` s koncovým mezerou) | Engine interpretuje řetězec doslovně a nemůže skript najít. | Odstraňte bílé znaky: `script.strip()` před voláním `get_supported_characters`. |
| **Prázdný seznam znaků** | Některé enginy zpřístupní skript, ale ještě nenačtou jazykový model. | Zavolejte `engine.load_language_model(script)`, pokud knihovna takovou metodu poskytuje, nebo zajistěte, aby soubory modelu byly přítomny. |
| **Problémy s normalizací Unicode** | Znaky jako “é” se mohou objevit jako složené (`\u00E9`) nebo rozložené (`e\u0301`). | Normalizujte řetězce pomocí `unicodedata.normalize('NFC', text)` před validací. |
| **Výkon u velkých skriptů** (např. čínština) | Získání tisíců znaků může být pomalé. | Uložte výsledek do cache po prvním volání; většina aplikací potřebuje seznam jen jednou. |

## Kompletní funkční příklad

Spojením všeho dohromady, zde je jeden skript, který můžete zkopírovat a spustit:

```python
import ocr
import matplotlib.pyplot as plt

def safe_get_characters(engine, script):
    try:
        chars = engine.get_supported_characters(script)
        if not chars:
            print(f"No characters returned for script '{script}'.")
        else:
            print(f"Supported {script} chars ({len(chars)}): {chars}")
        return chars
    except Exception as e:
        print(f"Error retrieving characters for script '{script}': {e}")
        return []

def plot_character_grid(chars, title="OCR Character Set"):
    cols = 10
    rows = (len(chars) + cols - 1) // cols
    fig, ax = plt.subplots(figsize=(cols, rows))
    ax.set_axis_off()
    for idx, ch in enumerate(chars):
        row = idx // cols
        col = idx % cols
        ax.text(col / cols, 1 - row / rows, ch, fontsize=14


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Aspose OCR tutoriál – Optické rozpoznávání znaků](/ocr/english/)
- [OCR post processing – Získání možností znaků](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Jak nastavit prahovou hodnotu v OCR rozpoznávání obrazu](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}