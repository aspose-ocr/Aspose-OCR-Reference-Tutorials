---
category: general
date: 2026-04-26
description: Jak spustit OCR na naskenovaném formuláři, naučit se, jak předzpracovat
  obrázek ke snížení šumu, a rychle extrahovat text z obrázku.
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: cs
og_description: Jak spustit OCR na naskenovaných dokumentech, předzpracovat obrázky,
  snížit šum a efektivně extrahovat text.
og_title: Jak spustit OCR a předzpracovat obrázky – rychlý průvodce
tags:
- OCR
- image processing
- Python
title: Jak spustit OCR a předzpracovat obrázky – Extrahovat text ze skenovaných formulářů
url: /cs/python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak spustit OCR – Kompletní průvodce pro extrakci textu z obrázků

Už jste se někdy zamýšleli **jak spustit OCR** na nepořádném naskenovaném formuláři a získat čistý, prohledávatelný text? Nejste v tom sami. V mnoha reálných projektech je surový obrázek plný špiček, nerovnoměrného osvětlení a dalších zvláštností, které způsobují, že OCR fungující „out‑of‑the‑box“ selhává.  

Dobrá zpráva? Pouhých několik řádků Pythonu a chytrý předzpracovatelský pipeline vám umožní dramaticky zvýšit přesnost rozpoznávání, **snížit šum** a získat přesně ta slova, která potřebujete. V tomto tutoriálu projdeme každý krok – od načtení obrázku po vytištění finálního řetězce – takže si odnesete připravený úryvek kódu, který můžete přizpůsobit fakturám, účtenkám nebo jakémukoli naskenovanému dokumentu.

## Co si vytvoříte

- Instanci `OcrEngine`, která komunikuje s podkladovou OCR knihovnou.  
- Řetězec předzpracování, který **binarizuje** obrázek a aplikuje **median blur** pro vyhlazení špiček.  
- Jednoduché volání `process()`, které vrací objekt s atributem `text`, extrahovaný řetězec.  

Na konci budete mít samostatný skript, který můžete spustit na libovolném souboru obrázku a okamžitě uvidíte extrahovaný text v konzoli.

## Požadavky

- Python 3.9+ (syntaxe použitá zde odpovídá nejnovější stabilní verzi).  
- Fiktivní balíček `aocr` – představte si jej jako tenký obal kolem Tesseract nebo jakéhokoli moderního OCR enginu. Nainstalujte jej pomocí `pip install aocr`.  
- Naskenovaný obrázek (`scanned_form.jpg`) umístěný ve složce, na kterou můžete odkazovat.  

Pokud používáte skutečnou OCR knihovnu jako `pytesseract`, můžete zaměnit `OcrEngine` za odpovídající třídu – vše ostatní zůstane stejné.

![](how-to-run-ocr-example.png "příklad, jak spustit OCR, zobrazující naskenovaný formulář a extrahovaný text")

*Alt text: jak spustit OCR na naskenovaném dokumentu a zobrazit extrahovaný text.*

---

## Krok 1: Jak spustit OCR – Inicializace enginu

Než může engine něco číst, musíme vytvořit instanci. Představte si `OcrEngine` jako mozek, který později interpretuje vizuální data.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **Proč je to důležité:** Vytvoření instance enginu nastaví interní modely, načte jazykové balíčky a připraví běhové prostředí. Přeskočení tohoto kroku obvykle vede k chybě `NoneType`, když později zavoláte `process()`.

---

## Krok 2: Jak předzpracovat obrázek – Načtěte svůj naskenovaný formulář

Nyní, když je mozek připraven, nasytíme jej obrázkem. Obrázek může být v libovolném formátu podporovaném `aocr.Image`.

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **Tip:** Používejte absolutní cesty během vývoje, abyste se vyhnuli překvapením typu „soubor nenalezen“, když skript běží z jiného pracovního adresáře.

---

## Krok 3: Jak snížit šum – Aplikovat binarizaci a median blur

Surové skeny často obsahují rozptýlené tečky, nerovnoměrné pozadí nebo slabé stíny. Dva klasické triky – **binarizace** a **median blur** – vyčistí obrázek, aniž by poškozovaly hrany definující znaky.

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### Hlubší pohled

- **Binarizace**: Hodnota `threshold=180` říká algoritmu: „Všechno, co je jasnější než 180, se stane bílým; vše ostatní se změní na černé.“ Upravit toto číslo, pokud je váš sken příliš tmavý nebo světlý.  
- **Median Blur**: Poloměr `2` znamená, že filtr se dívá na okno 5×5 pixelů a nahradí středový pixel mediánovou hodnotou. Tím se vyhladí izolované špičky a zároveň se zachovají tahy písmen.

> **Okrajový případ:** Pokud má váš dokument barevné zvýraznění, jednoduchý binární práh jej může smazat. V takovém případě zvažte použití `aocr.ImageFilters.adaptive_threshold()` – tento přizpůsobí práh lokálně po celém obrázku.

---

## Krok 4: Jak extrahovat text – Spustit OCR proces

S čistým obrázkem v ruce konečně necháme engine udělat své kouzlo.

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **Co se děje pod kapotou?** Engine spustí neuronovou síť (nebo starší vzorový matcher) nad maticí pixelů, přeloží každý rozpoznaný glyf do znaků Unicode a sestaví je do řádků a odstavců.

---

## Krok 5: Jak extrahovat text – Vytisknout výsledek

Objekt `ocr_result` poskytuje pohodlný atribut `text`. Podívejme se, co jsme získali.

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### Očekávaný výstup

Pokud naskenovaný formulář obsahuje:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Měli byste vidět něco jako:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Všimněte si, jak krok předzpracování odstranil rozptýlené tečky, které dříve změnily „Amount“ na „Am0unt“. To je síla **snížení šumu** před OCR.

---

## Časté problémy a jak je opravit

| Příznak | Pravděpodobná příčina | Rychlá oprava |
|---------|-----------------------|---------------|
| Zkreslené znaky (např. “@#%”) | Obrázek je příliš tmavý nebo příliš světlý | Upravte `threshold` v `binarize()`; zkuste `adaptive_threshold`. |
| Chybějící slova | Šum stále přítomen | Zvyšte `radius` pro `median_blur` nebo přidejte filtr `gaussian_blur`. |
| Špatný jazyk (např. anglická písmena se změní na čínská) | Načten nesprávný jazykový balíček | Při vytváření `OcrEngine()` předávejte `language="eng"`, pokud knihovna podporuje. |
| Pomalé zpracování velkých souborů | Vysoké rozlišení | Nejprve zmenšete obrázek: `aocr.ImageFilters.resize(width=1200)` před binarizací. |

---

## Dále – Další kroky a související témata

- **Dávkové zpracování**: Zabalte výše uvedenou logiku do smyčky, která automaticky zpracuje desítky souborů.  
- **Strukturovaný výstup**: Použijte regulární výrazy na `ocr_result.text` k získání polí jako datum nebo částka.  
- **Alternativní knihovny**: Zaměňte `aocr` za `pytesseract` – kód se mění jen v kroku inicializace enginu.  
- **Jak předzpracovat obrázek pro PDF**: Převěďte každou stránku PDF na obrázek a poté aplikujte stejný pipeline.  

Tyto rozšíření vám umožní škálovat řešení od jednoho formuláře po podnikovou úroveň pipeline pro ingestování dokumentů.

---

## Závěr

Probrali jsme **jak spustit OCR** od začátku do konce, ukázali **jak předzpracovat obrázek** k **snížení šumu** a demonstrovali **jak extrahovat text z obrázku** pomocí čistého, reprodukovatelného skriptu. Hlavní výsledek? Několik jednoduchých filtrů – binarizace a median blur – může proměnit špinavý sken na spolehlivý zdroj dat, čímž vám ušetří hodiny ručního čištění.

Vyzkoušejte skript na svých vlastních dokumentech, upravte prahy a sledujte, jak se přesnost zvyšuje. Až budete připraveni, prozkoumejte dávkové zpracování nebo integrujte výstup do databáze pro prohledávatelné archivy. Šťastné kódování a ať je vaše OCR vždy přesné!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}