---
category: general
date: 2026-01-12
description: Naučte se, jak zobrazit informace z AsposeAI výpisem lokálních modelů,
  zobrazením názvu modelu, velikosti a časového razítka posledního použití v přehledném
  příkladu v Pythonu.
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: cs
og_description: 'Jak zobrazit informace z AsposeAI: vypsat místní modely, zobrazit
  název modelu, velikost a čas posledního použití s kompletním průvodcem v Pythonu.'
og_title: Jak zobrazit informace – seznam místních modelů, název, velikost, naposledy
  použito
tags:
- AsposeAI
- Python
- Model Management
title: Jak zobrazit informace – seznam lokálních modelů, název, velikost, naposledy
  použito
url: /cs/python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zobrazit informace – Seznam lokálních modelů, název, velikost, naposledy použito

Už jste se někdy zamýšleli **jak zobrazit informace** z vaší instalace AsposeAI, aniž byste museli prohledávat logy nebo UI? Nejste v tom sami. V mnoha datových pipelinech je první věc, kterou potřebujete, rychlý přehled o tom, které modely jsou na vašem stroji, jak se jmenují, jak velké jsou a kdy jste s nimi naposledy pracovali.

Právě to si dnes ukážeme: stručný, end‑to‑end Python úryvek, který **vypíše lokální modely**, poté **zobrazí název modelu**, **ukáže velikost modelu** a **zobrazí čas posledního použití**. Žádné externí knihovny, žádná skrytá magie — pouze klient AsposeAI, který už máte.

Na konci tohoto tutoriálu budete schopni vložit kód do libovolného skriptu, spustit ho a okamžitě získat přehlednou tabulku vašich lokálně cachovaných modelů. Je to ideální pro kontrolu prostředí, tvorbu health dashboardů nebo prostě jen pro uspokojení zvědavosti, co se skrývá na disku.

## Požadavky

- Python 3.8 nebo novější (příklad používá f‑stringy, takže 3.6+ je nutností)
- Nainstalovaný balíček `asposeai` (`pip install asposeai`)
- Platná licence AsposeAI nebo trial klíč (klient načte přihlašovací údaje z proměnných prostředí nebo konfiguračního souboru)

Pokud už máte vše připravené, skvěle — ponořme se dál.

## Krok 1: Jak zobrazit informace – Inicializace klienta AsposeAI

Než budeme moci **vypisovat lokální modely**, potřebujeme objekt klienta, který komunikuje s runtime AsposeAI. Tento krok je základem; bez něj by zbytek kódu vyvolal `NameError`.

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*Proč je to důležité*: Inicializace klienta vytvoří relaci s lokálním inference enginem a načte potřebné nativní knihovny. Také ověří, že je licence aktivní, čímž zabrání nejasným chybám později při dotazování modelů.

> **Tip**: Pokud spouštíte tento kód na CI serveru, nastavte proměnnou `ASPOSEAI_LICENSE` v prostředí, aby klient mohl startovat bez interaktivních výzev.

## Krok 2: Seznam lokálních modelů – Získání dostupných modelů

Jakmile je klient připraven, můžeme **vypisovat lokální modely**. Metoda `list_local()` vrací kolekci objektů, z nichž každý má vlastnosti jako `name`, `size_mb` a `last_used`.

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*Co se děje pod kapotou*: `list_local()` prohledá adresář, kde AsposeAI cachuje soubory modelů (`~/.asposeai/models` ve výchozím nastavení) a vytvoří lehké metadata objekty. Je to rychlé, protože nenačítá váhy modelu — pouze čte malý JSON manifest.

Pokud se někdy chcete ujistit, že je konkrétní model již v cache, tento volání je nejrychlejší způsob, jak to potvrdit.

## Krok 3: Zobrazit název modelu, ukázat velikost modelu a čas posledního použití

S modely v ruce konečně **zobrazíme informace** iterací přes kolekci a výpisem každého atributu. Zde **zobrazíme název modelu**, **ukážeme velikost modelu** a **zobrazíme čas posledního použití** v jedné přehledné řádce.

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**Očekávaný výstup** (vaše časové značky se budou lišit):

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*Proč formátujeme takto*: Pomlčka (`–`) odděluje pole pro čitelnost a řádek s hlavičkou usnadňuje skenování výstupu v konzoli. Pokud budete později potřebovat strojově čitelný formát (CSV, JSON), můžete snadno nahradit volání `print` za `writer.writerow` nebo `json.dump`.

### Ošetření okrajových případů

- **Žádné modely v cache** — `list_local()` vrátí prázdný seznam. Smyčka prostě nic nevytiskne a zůstane jen hlavička. Můžete přidat ochranu:

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **Chybějící atributy** — V ojedinělých případech může být manifest poškozený. Přístup k `model_info.last_used` může vyvolat `AttributeError`. Zabalte výpis do `try/except`, pokud takové situace očekáváte.

- **Velké adresáře s modely** — Pokud máte stovky modelů, zvažte stránkování výstupu nebo zápis do souboru místo tisknutí do konzole.

## Vizuální souhrn (volitelné)

Pokud dáváte přednost rychlému vizuálnímu náhledu, diagram níže znázorňuje tok od inicializace klienta po finální výpis.  

![Diagram ukazující, jak zobrazit informace z AsposeAI klienta](/images/how-to-display-info.png "diagram jak zobrazit informace")

*Alt text*: **jak zobrazit informace** – schéma inicializace AsposeAI klienta, výpisu modelů a zobrazení informací.

## Kompletní funkční skript

Sestavením všech částí získáte kompletní, připravený ke spuštění skript:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
How to display info from AsposeAI:
List local models and show each model's name, size, and last‑used timestamp.
"""

from asposeai import AsposeAI

def main():
    # Initialize client
    aspose_ai = AsposeAI()

    # Retrieve local models
    local_models = aspose_ai.list_local()

    # Header
    print("Available local models:")
    print("-" * 50)

    if not local_models:
        print("No local models found. Use aspose_ai.download(...) to fetch one.")
        return

    # Display each model's details
    for model_info in local_models:
        try:
            print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
        except AttributeError:
            # Fallback if any attribute is missing
            print(f"{model_info.name} – info incomplete")

if __name__ == "__main__":
    main()
```

Uložte jej jako `list_models.py`, udělejte spustitelným (`chmod +x list_models.py`) a spusťte:

```bash
./list_models.py
```

Uvidíte přehlednou tabulku, kterou jsme demonstrovali výše.

## Závěr

Prošli jsme **jak zobrazit informace** z AsposeAI pomocí **výpisu lokálních modelů**, následně **zobrazením názvu modelu**, **ukázáním velikosti modelu** a **zobrazením času posledního použití**. Přístup je nenáročný, vyžaduje jen standardní balíček `asposeai` a může být vložen do libovolného automatizačního pipeline nebo ladící relace.

Dále můžete:

- Exportovat výstup do CSV pro analýzu v tabulkovém procesoru (modul `csv`).
- Posílat časové značky do monitorovacího dashboardu a upozorňovat na zastaralé modely.
- Kombinovat tento skript s `aspose_ai.download()` pro automatické obnovení modelů, které dlouho nebyly použity.

Pamatujte, že jasná viditelnost vašeho inventáře modelů šetří čas, snižuje nevyužité úložiště a udržuje vaše AI služby v chodu hladce. Vyzkoušejte skript, upravte formátování podle svých představ a nechte ho stát se nedílnou součástí vaší toolboxu.

Šťastné programování a ať jsou vaše modely vždy čerstvé!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}