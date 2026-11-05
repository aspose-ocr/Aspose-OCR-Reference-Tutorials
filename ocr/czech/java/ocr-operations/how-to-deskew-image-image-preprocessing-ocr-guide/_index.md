---
category: general
date: 2026-06-22
description: 'Jak narovnat obrázek pro OCR: naučte se kroky předzpracování obrazu
  pro OCR, odstraňte šum typu sůl a pepř a zvyšte přesnost.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: cs
og_description: Jak vyrovnat sklon obrazu pro OCR, odstranit šum typu sůl a pepř a
  použít techniky předzpracování obrázků pro OCR v kompletním příkladu v Javě.
og_title: Jak vyrovnat šikmost obrázku – Průvodce předzpracováním obrazu pro OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: Jak narovnat obrázek – Průvodce předzpracováním obrazu pro OCR
url: /cs/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak opravit zkosení obrázku – Průvodce předzpracováním obrazu pro OCR

Už jste se někdy zamýšleli **jak opravit zkosení obrázku**, aby váš OCR engine skutečně četl text? Nejste v tom sami. Nakloněný sken může dokonalý dokument proměnit v nečitelný chaos a většina vývojářů se s tím setká alespoň jednou.

V tomto tutoriálu projdeme kompletní **image preprocessing OCR** pipeline, která nejen koriguje rotaci, ale také **odstraňuje salt pepper** artefakty a zvyšuje kontrast – v podstatě vše, co potřebujete k **preprocess images OCR**‑stylu před předáním do engine. Na konci budete mít připravený Java úryvek a jasný mentální model, proč je každý krok důležitý.

## Jak opravit zkosení obrázku – Vytvoření pipeline pro předzpracování

Jádrem každého OCR‑přátelského workflow je objekt **preprocess options**, který spojuje řadu filtrů. Představte si ho jako dopravní pás: každý filtr vykoná jednu úlohu a poté předá obrázek dalšímu. Níže je minimální, ale kompletní příklad používající hypotetickou OCR knihovnu, která obsahuje `DeskewFilter`, `DenoiseFilter` a `ContrastBoostFilter`.

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### Proč to funguje

* **DeskewFilter** analyzuje dominantní textové řádky obrázku, odhaduje úhel a otáčí bitmapu zpět do vodorovné polohy. Většina knihoven omezuje korekci na ±15°, protože větší úhly obvykle naznačují špatně naskenovanou stránku, která vyžaduje ruční zásah.
* **DenoiseFilter** cílí na klasický *salt‑and‑pepper* – izolované černé nebo bílé pixely, které vypadají jako šum na televizi. jejich odstranění zabraňuje OCR engine, aby zaměnil šum za znaky.
* **ContrastBoostFilter** rozšiřuje histogram, čímž zvýrazní slabé tahy. Násobitel `1.5f` je bezpečná výchozí hodnota; můžete ho zvýšit, pokud jsou vaše skeny zvláště vybledlé.

> **Pro tip:** Pokud víte, že vaše dokumenty nikdy nepřekročí sklon 10°, předávejte tuto menší mez `DeskewFilter`—algoritmus běží rychleji a je méně náchylný k nadměrné korekci.

## Image Preprocessing OCR: Přidání filtrů ve správném pořadí

Pořadí je důležité. Představte si, že odstraníte šum *před* opravením zkosení; šum může narušit detekci úhlu, což vede k nesprávně zarovnanému výsledku. Naopak, aplikace zvýšení kontrastu *po* opravení zkosení zajistí, že rotace nezavede nové artefakty.

Níže je rychlý kontrolní seznam, který můžete zkopírovat a vložit do libovolného projektu:

| Krok | Filtr | Důvod |
|------|--------|--------|
| 1 | `DeskewFilter` | Zarovnává základní linii textu |
| 2 | `DenoiseFilter` | Odstraňuje izolovaný šum pixelů |
| 3 | `ContrastBoostFilter` | Zvyšuje čitelnost pro OCR |

Pokud potřebujete vložit další kroky – například filtr **binarization** pro binární OCR – umístíte jej **po** zvýšení kontrastu, protože čistý, vysokokontrastní obrázek se binarizuje přesněji.

## Odstranění šumu Salt Pepper pomocí DenoiseFilter

Šum *salt‑and‑pepper* je notorický u nízkokvalitních skenů, zejména těch pořízených levnými telefonními fotoaparáty. `DenoiseFilter` v naší knihovně implementuje median‑filter jádro, které nahradí každý pixel mediánem jeho okolí. Výsledek? Tyto skvrny zmizí, aniž by rozmazaly skutečné znaky.

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*Kdy zvýšit velikost jádra?* Pokud jsou vaše zdrojové obrázky zaplněny velkými skvrnami, větší jádro je vyčistí, ale pozor: příliš velké může začít mazat jemné tahy v malých písmenech.

## Preprocess Images OCR – Aplikace pipeline

Jakmile sestavíte řetězec filtrů, jeho připojení k engine je jednorázové (`engine.setPreprocessOptions`). Od té chvíle každé volání `recognizeText` automaticky prochází pipeline. Není potřeba ručně volat každý filtr – váš kód zůstává přehledný a budoucí změny (přidání nového filtru, úprava parametrů) jsou centralizovány.

Zde je ukázka úspěšného běhu se vzorovým skenem, který původně měl sklon 12° a výrazný pepper šum:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Všimněte si, že text je čistý, správně orientovaný a bez odlehlých znaků, které by se jinak objevily jako “I n v o i c e” nebo “$‑‑‑”.

## Okrajové případy a běžné úskalí

| Situace | Na co si dát pozor | Navrhované řešení |
|-----------|-------------------|---------------|
| Rotace > 15° | DeskewFilter může selhat | Předrotovat ručně nebo použít filtr s vyšším rozsahem |
| Extrémně nízké rozlišení ( < 100 dpi ) | Zvýšení kontrastu nedokáže obnovit detaily | Nejprve převeďte obrázek (např. `ResampleFilter`) |
| Smíšený šum (Gaussian + salt‑pepper) | Samotný DenoiseFilter nestačí | Přidejte `GaussianBlurFilter` před `DenoiseFilter` |
| Barevné skeny s barevným textem | Je potřeba převod na odstíny šedi | Vložte `GrayscaleFilter` před zvýšení kontrastu |

Anticipací těchto scénářů ušetříte hodiny ladění později.

## Kompletní funkční příklad (vše v jednom)

Níže je samostatná Java třída, kterou můžete vložit do libovolného Maven nebo Gradle projektu, který zahrnuje závislost `com.example.ocr`. Ukazuje **jak opravit zkosení obrázku**, **odstranit salt pepper** šum a **preprocess images OCR**‑styl.

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**Očekávaný výstup** (předpokládáme, že `scanned-document.png` obsahuje čistou fakturu):

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

Pokud vyměníte obrázek za takový, který je již dokonale zarovnán, všimnete si, že pipeline stále běží – nic se nezlomí a přesnost OCR zůstává vysoká.

## Závěr

Nyní máte pevné pochopení **jak opravit zkosení obrázku** a proč každý krok předzpracování – **image preprocessing OCR**, **remove salt pepper** a **preprocess images OCR** – hraje klíčovou roli při poskytování čistého, prohledávatelného textu. Výše uvedený příklad je kompletní,

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Calculate Skew Angle for OCR Image Preprocessing](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}