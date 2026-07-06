---
category: general
date: 2026-02-22
description: Naučte se, jak vypsat uložené modely v mezipaměti a rychle zobrazit adresář
  mezipaměti ve vašem počítači. Obsahuje kroky k prohlížení složky mezipaměti a správě
  místního úložiště AI modelů.
draft: false
keywords:
- list cached models
- show cache directory
- how to view cache folder
- AI model cache
- local model storage
language: cs
og_description: Zjistěte, jak vypsat uložené modely, zobrazit adresář cache a prohlédnout
  složku cache v několika jednoduchých krocích. Kompletní příklad v Pythonu je zahrnut.
og_title: seznam cachovaných modelů – rychlý průvodce pro zobrazení adresáře mezipaměti
tags:
- AI
- caching
- Python
- development
title: seznam modelů v mezipaměti – jak zobrazit složku mezipaměti a ukázat adresář
  mezipaměti
url: /cs/python/general/list-cached-models-how-to-view-cache-folder-and-show-cache-d/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# seznam uložených modelů – rychlý průvodce pro zobrazení adresáře cache

Už jste se někdy zamysleli, jak **list cached models** na svém pracovním stanici bez prohrabávání se v nejasných složkách? Nejste v tom sami. Mnoho vývojářů narazí na problém, když potřebují ověřit, které AI modely jsou již uloženy lokálně, zejména když je místo na disku omezené. Dobrá zpráva? V několika řádcích můžete jak **list cached models**, tak **show cache directory**, což vám poskytne úplný přehled o vaší cache složce.

V tomto tutoriálu projdeme samostatný Python skript, který přesně to dělá. Na konci budete vědět, jak zobrazit složku cache, kde se cache nachází na různých OS, a dokonce uvidíte přehledně vytištěný seznam všech stažených modelů. Žádná externí dokumentace, žádné hádání – jen čistý kód a vysvětlení, která můžete okamžitě zkopírovat a vložit.

## Co se naučíte

- Jak inicializovat AI klienta (nebo stub), který poskytuje nástroje pro cache.  
- Přesné příkazy pro **list cached models** a **show cache directory**.  
- Kde se cache nachází ve Windows, macOS a Linuxu, abyste se k ní mohli ručně dostat, pokud budete chtít.  
- Tipy, jak zacházet s okrajovými případy, jako je prázdná cache nebo vlastní cesta k cache.  

**Prerequisites** – potřebujete Python 3.8+ a pip‑instalovatelný AI klient, který implementuje `list_local()`, `get_local_path()` a volitelně `clear_local()`. Pokud ještě žádný nemáte, příklad používá mock třídu `YourAIClient`, kterou můžete nahradit skutečným SDK (např. `openai`, `huggingface_hub` atd.).  

Připravení? Pojďme na to.

## Step 1: Set Up the AI Client (or a Mock)

Pokud už máte objekt klienta, tento blok přeskočte. Jinak vytvořte malý stand‑in, který napodobuje rozhraní cache. To umožní spustit skript i bez skutečného SDK.

```python
# step_1_client_setup.py
import os
from pathlib import Path

class YourAIClient:
    """
    Minimal mock of an AI client that stores downloaded models in a
    directory called `.ai_cache` inside the user's home folder.
    """
    def __init__(self, cache_dir: Path | None = None):
        # Use a custom path if supplied, otherwise default to ~/.ai_cache
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        """Return a list of model folder names that exist in the cache."""
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        """Absolute path to the cache directory."""
        return str(self.cache_dir.resolve())

    # Optional helper for demonstration purposes
    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# Initialize the client (replace with real client if you have one)
ai = YourAIClient()
# Populate with dummy data the first time you run the script
if not ai.list_local():
    ai._populate_dummy_models()
```

> **Pro tip:** Pokud už máte skutečného klienta (např. `from huggingface_hub import HfApi`), stačí nahradit volání `YourAIClient()` za `HfApi()` a ujistit se, že metody `list_local` a `get_local_path` existují nebo jsou podle toho obaleny.

## Step 2: **list cached models** – načtení a zobrazení

Nyní, když je klient připraven, můžeme ho požádat, aby vyjmenoval vše, co zná lokálně. To je jádro naší operace **list cached models**.

```python
# step_2_list_models.py
print("Cached models:")
for model_name in ai.list_local():
    print(" -", model_name)
```

**Expected output** (s dummy daty z kroku 1):

```
Cached models:
 - model_1
 - model_2
 - model_3
```

Pokud je cache prázdná, uvidíte jen:

```
Cached models:
```

Ten malý prázdný řádek vám říká, že zatím nic není uloženo – užitečné při skriptování úklidových rutin.

## Step 3: **show cache directory** – kde se cache nachází?

Znalost cesty je často polovinou boje. Různé operační systémy ukládají cache na různá výchozí místa a některá SDK vám umožní přepsat ji pomocí environmentálních proměnných. Následující úryvek vytiskne absolutní cestu, abyste se do ní mohli `cd` nebo ji otevřít ve správci souborů.

```python
# step_3_show_path.py
print("\nCache directory:", ai.get_local_path())
```

**Typical output** na unixovém systému:

```
Cache directory: /home/youruser/.ai_cache
```

Na Windows můžete vidět něco jako:

```
Cache directory: C:\Users\YourUser\.ai_cache
```

Nyní přesně víte, **jak zobrazit složku cache** na jakékoli platformě.

## Step 4: Put It All Together – a single runnable script

Níže je kompletní, připravený ke spuštění program, který kombinuje všechny tři kroky. Uložte jej jako `view_ai_cache.py` a spusťte `python view_ai_cache.py`.

```python
# view_ai_cache.py
import os
from pathlib import Path

class YourAIClient:
    """Simple mock client exposing cache‑related utilities."""
    def __init__(self, cache_dir: Path | None = None):
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        return str(self.cache_dir.resolve())

    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    # Initialize (replace with real client if available)
    ai = YourAIClient()

    # Populate dummy data only on first run – remove this in production
    if not ai.list_local():
        ai._populate_dummy_models()

    # Step 1: list cached models
    print("Cached models:")
    for model_name in ai.list_local():
        print(" -", model_name)

    # Step 2: show cache directory
    print("\nCache directory:", ai.get_local_path())
```

Spusťte jej a okamžitě uvidíte jak seznam uložených modelů **a** umístění adresáře cache.

## Edge Cases & Variations

| Situace | Co dělat |
|-----------|------------|
| **Empty cache** | Skript vytiskne “Cached models:” bez položek. Můžete přidat podmíněné varování: `if not models: print("⚠️ No models cached yet.")` |
| **Custom cache path** | Při vytváření klienta předáte cestu: `YourAIClient(cache_dir=Path("/tmp/my_ai_cache"))`. Volání `get_local_path()` pak odráží tuto vlastní lokaci. |
| **Permission errors** | Na omezených strojích může klient vyvolat `PermissionError`. Zabalte inicializaci do `try/except` bloku a přejděte na adresář zapisovatelný uživatelem. |
| **Real SDK usage** | Nahraďte `YourAIClient` skutečnou třídou klienta a ujistěte se, že názvy metod odpovídají. Mnoho SDK poskytuje atribut `cache_dir`, který můžete číst přímo. |

## Pro Tips for Managing Your Cache

- **Periodic cleanup:** Pokud často stahujete velké modely, naplánujte cron job, který zavolá `shutil.rmtree(ai.get_local_path())` po potvrzení, že je již nepotřebujete.  
- **Disk usage monitoring:** Použijte `du -sh $(ai.get_local_path())` na Linux/macOS nebo `Get-ChildItem -Recurse | Measure-Object -Property Length -Sum` v PowerShellu, abyste sledovali velikost.  
- **Versioned folders:** Některé klienty vytvářejí podadresáře podle verze modelu. Když **list cached models**, uvidíte každou verzi jako samostatnou položku – použijte to k odstranění starších revizí.  

## Visual Overview

![snímek obrazovky list cached models](https://example.com/images/list-cached-models.png "list cached models – výstup v konzoli zobrazující modely a cestu ke cache")

*Alt text:* *list cached models – výstup v konzoli zobrazující názvy uložených modelů a cestu k adresáři cache.*

## Conclusion

Probrali jsme vše, co potřebujete k **list cached models**, **show cache directory** a obecně **jak zobrazit složku cache** na jakémkoli systému. Krátký skript demonstruje kompletní, spustitelné řešení, vysvětluje **proč** je každý krok důležitý a nabízí praktické tipy pro reálné použití.  

Dále můžete zkoumat **jak programově vymazat cache**, nebo integrovat tyto volání do většího nasazovacího pipeline, který ověří dostupnost modelu před spuštěním inference úloh. Každopádně nyní máte pevný základ pro správu lokálního úložiště AI modelů s jistotou.

Máte otázky ohledně konkrétního AI SDK? Zanechte komentář níže a šťastné cachování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}