---
category: general
date: 2026-05-06
description: Vytvořte prohledávatelný PDF z obrázku pomocí Aspose OCR v Javě. Naučte
  se převést obrázek na PDF, povolit opravu pravopisu a použít OCR GPU pro rychlé
  výsledky.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- enable spell correction
- use ocr gpu
- process image ocr
language: cs
og_description: Vytvořte prohledávatelný PDF z obrázku pomocí Aspose OCR v Javě. Tento
  návod ukazuje, jak převést obrázek na PDF, povolit opravu pravopisu a použít OCR
  GPU.
og_title: Vytvořte prohledávatelný PDF z obrázku pomocí Java OCR
tags:
- OCR
- Java
- PDF
title: Vytvořte prohledávatelný PDF z obrázku pomocí Java OCR
url: /cs/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF z obrázku pomocí Java OCR

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** ze skenovaného obrázku, ale nevedeli jste, kde začít? Nejste v tom sami — většina vývojářů narazí na tuto překážku, když poprvé řeší PDF založené na obrázcích. Naštěstí s Aspose OCR pro Java můžete **převést obrázek na PDF**, proměnit text na vybraný obsah a dokonce přidat opravu pravopisu pro vylepšený výsledek.

V tomto tutoriálu projdeme kompletním, připraveným příkladem, který ukazuje, jak **použít OCR GPU**, když je k dispozici, jak **efektivně zpracovat OCR obrázku** a proč má povolení opravy pravopisu vliv na následné vyhledávání. Na konci budete mít jedním kliknutím způsob, jak vygenerovat prohledávatelné PDF, které můžete distribuovat uživatelům nebo archivovat pro soulad s předpisy.

> **Tip:** Pokud spouštíte kód na stroji bez GPU, přejde automaticky na CPU, takže nemusíte nic přepisovat.

---

## Co budete potřebovat

- **Java 8+** (kód se kompiluje s JDK 8 a novějším)
- **Aspose OCR for Java** knihovna (stáhněte nejnovější JAR z webu Aspose)
- **Vstupní obrázek** (JPEG, PNG, TIFF atd.), který chcete převést na prohledávatelné PDF
- (Volitelné) **GPU** s podporou CUDA, pokud chcete nejrychlejší rozpoznávání

Žádné další frameworky, žádné Maven/Gradle triky — pouze jeden JAR na classpath a můžete začít.

---

## Krok 1: Inicializace OCR enginu – Srdce procesu  

Nejprve vytvoříme instanci `OcrEngine` a nasměrujeme ji na zdrojový soubor. Tento objekt je „pracovní kůň“, který načte obrázek, spustí neuronovou síť a vrátí nám text.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to convert
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

*Proč je to důležité:* Inicializace enginu jednou a jeho opakované používání eliminuje zátěž spojenou s opakovaným načítáním nativních knihoven — malý výkonový zisk, který se projeví při hromadném zpracování desítek souborů.

---

## Krok 2: Výběr zařízení pro zpracování – Použít OCR GPU, pokud je k dispozici  

Pokud má vaše pracovní stanice kompatibilní GPU, můžete Aspose říct, aby těžkou část prováděl na ní. Jinak engine automaticky přepne na CPU.

```java
        // Prefer GPU; fall back to CPU if no compatible device is found
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
```

*Jaký je přínos?* Akcelerace pomocí GPU může ušetřit sekundy u každé stránky, zejména u vysoce rozlišených skenů. Návrat na CPU zajišťuje, že stejný kód funguje všude, což je důvod, proč doporučujeme **use OCR GPU** jako výchozí nastavení.

---

## Krok 3: Zrychlete sken — využijte všechny CPU jádra  

I když je GPU zaneprázdněná, okolní předzpracování lze paralelizovat. Nastavení počtu vláken na počet dostupných procesorů dává enginu šanci zpracovávat více částí najednou.

```java
        // Use all logical cores for preprocessing and language detection
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());
```

*Poznámka:* Na 4‑jádrovém notebooku se spustí čtyři vlákna; na 16‑jádrové pracovní stanici získáte plný přínos. Jen mějte na paměti, že více vláken znamená vyšší spotřebu paměti.

---

## Krok 4: Vyčištění obrázku — filtry předzpracování  

Rozmazaný nebo šumivý sken vytvoří nečitelné texty. Přidání několika vestavěných filtrů dramaticky zvyšuje přesnost.

```java
        // Deskew the image so text lines are horizontal
        ocrEngine.getPreprocessing().add(new DeskewFilter());

        // Remove speckles and background noise
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());
```

*Proč tyto filtry?* `DeskewFilter` opravuje rotaci, která často vzniká, když je dokument nasunut do skeneru pod úhlem. `NoiseRemovalFilter` odstraňuje osamělé pixely, které by jinak byly mylně interpretovány jako znaky. Představte si to jako podání čistého listu papíru OCR enginu.

---

## Krok 5: Zapnutí chytrých funkcí — povolení opravy pravopisu a automatické detekce jazyka  

Pokud pracujete s vícejazyčnými dokumenty nebo jen chcete méně překlepů, zapněte vestavěný kontrolor pravopisu a nechte engine hádat jazyk.

```java
        // Activate spell correction to fix common OCR mistakes
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Let the engine automatically detect the language of the input
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

*Kdy je to užitečné?* Představte si sken obsahující jak anglické, tak španělské sekce. Funkce automatické detekce přepíná slovníky za běhu, zatímco oprava pravopisu vyčistí špatně rozpoznané znaky, např. “0” místo “O”. Tento krok je zásadní pro vytvoření **prohledávatelného PDF**, které skutečně vrací správné výsledky.

---

## Krok 6: Uložení výsledku — převod obrázku na PDF a jeho zpřístupnění pro vyhledávání  

Nakonec požádáme engine, aby zapsal PDF, kde původní obrázek leží za neviditelnou textovou vrstvou. Jedná se o klasický **convert image to PDF** workflow, ale PDF je nyní prohledávatelné.

```java
        // Generate a searchable PDF – the text layer sits behind the original image
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

Výstupní soubor (`output-searchable.pdf`) lze otevřít v libovolném PDF prohlížeči; budete moci text vybírat, kopírovat a vyhledávat stejně jako v nativním PDF. Žádné další nástroje nejsou potřeba.

---

## Kompletní funkční příklad — kopírujte a spusťte  

Níže je celý program připravený ke kompilaci. Nahraďte `YOUR_DIRECTORY` složkou, která obsahuje `input.jpg`.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine and load the source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 2: Select the processing device (GPU if available, otherwise CPU)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Step 3: Use all available CPU cores to speed up recognition
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 4: Add preprocessing filters to improve image quality
        ocrEngine.getPreprocessing().add(new DeskewFilter());
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());

        // Step 5: Enable spell correction and automatic language detection
        ocrEngine.getSettings().setEnableSpellCorrection(true);
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // Step 6: Perform OCR and save the result as a searchable PDF
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

**Očekávaný výstup:** Po spuštění programu uvidíte v konzoli řádek *„Searchable PDF generated successfully.“* Otevřením `output-searchable.pdf` v Adobe Readeru můžete zadat slovo z původního obrázku do vyhledávacího pole a okamžitě přejít na jeho místo.

---

## Často kladené otázky a okrajové případy  

- **Co když není detekováno GPU?**  
  Volání `setDeviceType(OcrDeviceType.GPU)` nevyvolá výjimku; pouze instruuje engine, aby nejprve zkusil GPU. Pokud selže, engine tiše přejde na CPU.

- **Mohu zpracovávat více obrázků v jednom běhu?**  
  Ano. Zabalte kód do smyčky, měňte název souboru v každé iteraci a znovu použijte stejnou instanci `OcrEngine`, čímž udržíte nízkou spotřebu paměti.

- **Moje PDF je obrovské — jak ho zmenšit?**  
  Po OCR můžete použít optimalizační API Aspose PDF, nebo jednoduše zmenšit vstupní obrázek před předáním enginu (`ImageStream.fromFile(...).setResolution(150)` pro 150 DPI).

- **Potřebuji zachovat původní rozlišení obrázku pro právní soulad.**  
  Formát `PDF_SEARCHABLE` zachovává bitmapu přesně tak, jak je; neviditelná textová vrstva je přidána navrchu, aniž by se změnila vizuální kvalita.

---

## Vizuální shrnutí  

![create searchable pdf example](placeholder-image.png "create searchable pdf example")

*Alt text:* *příklad vytvoření prohledávatelného PDF – Java OCR engine převádí naskenovaný JPG na prohledávatelné PDF.*

---

## Závěr  

Nyní máte **kompletní end‑to‑end řešení** pro převod libovolného obrázku na **prohledávatelné PDF** pomocí Aspose OCR pro Java. Díky **convert image to PDF**, **povolení opravy pravopisu** a **použití OCR GPU**, když je to možné, získáte rychlé, přesné a prohledávatelné výsledky, které fungují napříč platformami.

Co dál? Vyzkoušejte:

- **Různé výstupní formáty** (`PDF`, `DOCX`, `HTML`) a podívejte se, jak se chová textová vrstva.
- **Vlastní slovníky**, pokud zpracováváte oborový žargon.
- **Hromadné zpracování** pro automatické zpracování tisíců skenů.

Klidně upravte počet vláken, vyměňte filtry nebo zapojte vlastní pipeline předzpracování. Základní vzorec zůstává stejný: načíst → předzpracovat → nakonfigurovat → OCR → uložit.

Šťastné programování a ať jsou vaše PDF vždy prohledávatelná!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}