---
category: general
date: 2026-02-22
description: Jak používat OCR v Javě k extrakci textu z obrázku, zlepšení přesnosti
  OCR a načtení obrázku pro OCR s praktickými příklady kódu.
draft: false
keywords:
- how to use OCR
- extract text from image
- improve OCR accuracy
- load image for OCR
- OCR preprocessing
language: cs
og_description: Jak použít OCR v Javě k extrakci textu z obrázku a zlepšení přesnosti
  OCR. Postupujte podle tohoto návodu pro připravený spustitelný příklad.
og_title: Jak používat OCR v Javě – Kompletní průvodce krok za krokem
tags:
- OCR
- Java
- Image Processing
title: Jak používat OCR v Javě – Kompletní průvodce krok za krokem
url: /cs/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR v Javě – Kompletní krok‑za‑krokem průvodce

Už jste někdy potřebovali **jak používat OCR** na nakřivený snímek obrazovky a divili se, proč výstup vypadá jako nesmyslný text? Nejste v tom sami. V mnoha reálných aplikacích – skenování účtenek, digitalizace formulářů nebo získávání textu z memů – spolehlivé výsledky závisí na několika jednoduchých nastaveních.

V tomto tutoriálu projdeme **jak používat OCR** k *extrahování textu z obrazových* souborů, ukážeme vám, jak **zlepšit přesnost OCR**, a demonstrujeme správný způsob **načtení obrázku pro OCR** pomocí populární Java OCR knihovny. Na konci budete mít samostatný program, který můžete vložit do libovolného projektu.

## Co se naučíte

- Přesný kód, který potřebujete k **načtení obrázku pro OCR** (bez skrytých závislostí).
- Které předzpracovatelské příznaky zvyšují **zlepšení přesnosti OCR** a proč jsou důležité.
- Jak přečíst výsledek OCR a vytisknout jej do konzole.
- Časté úskalí – například zapomenutí nastavit oblast zájmu nebo ignorování redukce šumu – a jak se jim vyhnout.

### Předpoklady

- Java 17 nebo novější (kód se kompiluje s jakýmkoli aktuálním JDK).
- OCR knihovna, která poskytuje třídy `OcrEngine`, `ImagePreprocessingOptions`, `OcrInput` a `OcrResult` (například fiktivní balíček `com.example.ocr` použitý ve výřezu). Nahraďte ji skutečnou knihovnou, kterou používáte.
- Vzorek obrázku (`skewed_noisy.png`) umístěný ve složce, na kterou můžete odkazovat.

> **Tip:** Pokud používáte komerční SDK, ujistěte se, že licenční soubor je na classpath; jinak engine vyhodí chybu při inicializaci.

---

## Krok 1: Vytvoření instance OCR enginu – **jak používat OCR** efektivně

První, co potřebujete, je objekt `OcrEngine`. Představte si ho jako mozek, který bude interpretovat pixely.

```java
// Step 1: Initialize the OCR engine
import com.example.ocr.OcrEngine;

OcrEngine ocrEngine = new OcrEngine();
```

*Proč je to důležité:* Bez enginu nemáte kontext pro jazykové modely, znakové sady ani heuristiky obrazu. Vytvoření enginu hned na začátku vám také umožní později připojit předzpracovatelské možnosti.

---

## Krok 2: Nastavení předzpracování obrazu – **zlepšení přesnosti OCR**

Předzpracování je tajná omáčka, která promění špinavý sken na čistý, strojově čitelný text. Níže povolíme deskew, pokročilou redukci šumu, automatický kontrast a oblast zájmu (ROI), aby se zaměřila na relevantní část obrázku.

```java
import com.example.ocr.ImagePreprocessingOptions;
import java.awt.Rectangle;

// Step 2: Set up preprocessing to improve OCR accuracy
ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
preprocessing.setDeskewEnabled(true); // Correct image rotation
preprocessing.setNoiseReductionLevel(
        ImagePreprocessingOptions.NoiseReduction.HIGH); // Reduce speckles
preprocessing.setAutoContrastEnabled(true); // Boost contrast
preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600)); // Process a sub‑region only

ocrEngine.setPreprocessingOptions(preprocessing);
```

*Proč je to důležité:*  
- **Deskew** zarovná natočený text, což je nezbytné při skenování účtenek, které nejsou dokonale rovné.  
- **Redukce šumu** odstraňuje osamělé pixely, které by jinak byly interpretovány jako znaky.  
- **Automatický kontrast** rozšiřuje tonální rozsah, takže slabé písmo vystoupí do popředí.  
- **ROI** říká enginu, aby ignoroval irelevantní okraje, což šetří čas i paměť.

Pokud některý z těchto kroků vynecháte, pravděpodobně zaznamenáte pokles **zlepšení přesnosti OCR**.

---

## Krok 3: Načtení obrázku pro OCR – **načtení obrázku pro OCR** správně

Nyní skutečně nasměrujeme engine na soubor, který chceme přečíst. Třída `OcrInput` může přijímat více obrázků, ale pro tento příklad to zjednodušíme.

```java
import com.example.ocr.OcrInput;

// Step 3: Load the image you want to extract text from
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png"); // replace with your real path
```

*Proč je to důležité:* Cesta musí být absolutní nebo relativní k pracovnímu adresáři; jinak engine vyhodí `FileNotFoundException`. Také si všimněte, že metoda `add` naznačuje, že můžete zařadit několik obrázků – užitečné pro dávkové zpracování.

---

## Krok 4: Provedení OCR a výpis rozpoznaného textu – **jak používat OCR** od začátku do konce

Nakonec požádáme engine, aby rozpoznal text a vytiskl jej. Objekt `OcrResult` obsahuje surový řetězec, skóre důvěry a metadata řádek po řádku (pokud je budete potřebovat později).

```java
import com.example.ocr.OcrResult;

// Step 4: Run OCR and print the extracted text
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Očekávaný výstup** (předpokládáme, že vzorový obrázek obsahuje „Hello, OCR World!“):

```
=== OCR Output ===
Hello, OCR World!
```

Pokud výsledek vypadá poškrábaně, vraťte se ke Krok 2 a upravte předzpracovatelské možnosti – třeba snížit úroveň redukce šumu nebo upravit obdélník ROI.

---

## Kompletní spustitelný příklad

Níže je kompletní Java program, který můžete zkopírovat a vložit do souboru s názvem `OcrDemo.java`. Spojuje všechny kroky, o kterých jsme mluvili.

```java
// OcrDemo.java – A complete, runnable example showing how to use OCR in Java
import com.example.ocr.OcrEngine;
import com.example.ocr.ImagePreprocessingOptions;
import com.example.ocr.OcrInput;
import com.example.ocr.OcrResult;
import java.awt.Rectangle;

public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (this is the key to improve OCR accuracy)
        ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
        preprocessing.setDeskewEnabled(true);
        preprocessing.setNoiseReductionLevel(
                ImagePreprocessingOptions.NoiseReduction.HIGH);
        preprocessing.setAutoContrastEnabled(true);
        preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600));
        ocrEngine.setPreprocessingOptions(preprocessing);

        // 3️⃣ Load the image you want to extract text from
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace the path with your own image location
        ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run the OCR engine and print the result
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Uložte soubor, zkompilujte pomocí `javac OcrDemo.java` a spusťte `java OcrDemo`. Pokud je vše nastaveno správně, uvidíte extrahovaný text vytištěný v konzoli.

---

## Často kladené otázky a okrajové případy

| Otázka | Odpověď |
|----------|--------|
| **Co když je můj obrázek ve formátu JPEG?** | Metoda `OcrInput.add()` přijímá jakýkoli podporovaný rastrový formát – PNG, JPEG, BMP, TIFF. Stačí změnit příponu souboru v cestě. |
| **Mohu zpracovávat více stránek najednou?** | Rozhodně. Zavolejte `ocrInput.add()` pro každý soubor a pak předávejte stejný `ocrInput` do `recognize()`. Engine vrátí spojený `OcrResult`. |
| **Co když je výsledek OCR prázdný?** | Zkontrolujte, že ROI skutečně obsahuje text. Také se ujistěte, že je zapnuté `setDeskewEnabled(true)`; otočení o 90° může způsobit, že engine bude považovat obrázek za prázdný. |
| **Jak změním jazykový model?** | Většina knihoven nabízí metodu `setLanguage(String)` na `OcrEngine`. Zavolejte ji před `recognize()`, např. `ocrEngine.setLanguage("eng")`. |
| **Je možné získat skóre důvěry?** | Ano, `OcrResult` často poskytuje `getConfidence()` pro řádky nebo znaky. Použijte jej k filtrování výsledků s nízkou důvěrou. |

---

## Závěr

Probrali jsme **jak používat OCR** v Javě od začátku do konce: vytvoření enginu, nastavení předzpracování pro **zlepšení přesnosti OCR**, správné **načtení obrázku pro OCR** a nakonec výpis extrahovaného textu. Kompletní ukázkový kód je připraven k běhu a vysvětlení odpovídají na otázku „proč“ za každým řádkem.

Jste připraveni na další krok? Zkuste změnit obdélník ROI, zaměřit se na jiné části obrázku, pohrát si s `NoiseReduction.MEDIUM`, nebo integrovat výstup do prohledávatelného PDF. Můžete také prozkoumat související témata, jako je **extrahování textu z obrázku** pomocí cloudových služeb, nebo dávkové zpracování tisíců souborů pomocí vícevláknové fronty.

Máte další otázky ohledně OCR, předzpracování obrazu nebo integrace s Javou? Zanechte komentář a šťastné programování! 

![Jak používat OCR příklad](/images/ocr-demo.png "jak používat OCR – Java příklad ukazující předzpracování a výsledek")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}