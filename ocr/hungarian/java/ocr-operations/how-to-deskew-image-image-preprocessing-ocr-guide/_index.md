---
category: general
date: 2026-06-22
description: 'Hogyan korrigáljuk a kép dőlését OCR-hez: tanulja meg a képelőfeldolgozás
  OCR lépéseit, távolítsa el a só és bors zajt, és növelje a pontosságot.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: hu
og_description: Hogyan korrigáljuk a kép dőlését OCR-hez, távolítsuk el a só‑és‑bors
  zajt, és alkalmazzuk az előfeldolgozó OCR technikákat egy teljes Java példában.
og_title: Hogyan kiegyenesítsük a képet – Képfeldolgozási OCR útmutató
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
title: Hogyan kiegyenesítsünk képet – Képelőfeldolgozási OCR útmutató
url: /hu/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan korrigáljuk a kép dőlését – Képelőfeldolgozás OCR útmutató

Valaha is elgondolkodtál már **hogyan korrigáljuk a kép dőlését**, hogy az OCR motorod tényleg elolvassa a szöveget? Nem vagy egyedül. Egy ferde szkennelés tökéletes dokumentumot is összekuszálttá tehet, és a legtöbb fejlesztő legalább egyszer szembesül ezzel a problémával.

Ebben az útmutatóban végigvezetünk egy teljes **image preprocessing OCR** csővezeten, amely nem csak a forgatást korrigálja, hanem **eltávolítja a só‑és‑bors** zajt és növeli a kontrasztot – lényegében mindazt, amire **preprocess images OCR**‑stílusban szükséged van, mielőtt a képet az motorhoz adnád. A végére egy azonnal futtatható Java kódrészletet és egy világos mentális modellt kapsz arról, hogy miért fontos minden egyes lépés.

## Hogyan korrigáljuk a kép dőlését – Az előfeldolgozó csővezeték felépítése

Bármely OCR‑barát munkafolyamat szíve egy **preprocess options** objektum, amely egy sor szűrőt láncol össze. Gondolj rá úgy, mint egy szállítószalagra: minden szűrő egy feladatot végez, majd átadja a képet a következőnek. Az alábbiakban egy minimális, de teljes példát láthatsz egy hipotetikus OCR könyvtár használatával, amely a `DeskewFilter`, `DenoiseFilter` és `ContrastBoostFilter` osztályokat tartalmazza.

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

### Miért működik ez

* **DeskewFilter** elemzi a kép domináns szövegsorait, becsli a szöget, és a bitmapet visszaforgatja vízszintes állásba. A legtöbb könyvtár a korrekciót ±15°-ra korlátozza, mivel a nagyobb szögek általában rosszul szkennelt oldalt jeleznek, amelyhez manuális beavatkozás szükséges.
* **DenoiseFilter** a klasszikus *só‑és‑bors* mintára céloz – azok az elszigetelt fekete vagy fehér pixelek, amelyek a TV-n látható statikusra emlékeztetnek. Ezek eltávolítása megakadályozza, hogy az OCR motor a zajt karakternek vegye.
* **ContrastBoostFilter** nyújtja a hisztogramot, így a halvány vonalak kiemelkednek. Az `1.5f` szorzó biztonságos alapértelmezett érték; növelheted, ha a szkenneléseid különösen kifakultak.

> **Pro tipp:** Ha tudod, hogy a dokumentumaid soha nem haladják meg a 10°-os dőlést, add meg ezt a kisebb határt a `DeskewFilter`-nek – az algoritmus gyorsabban fut, és kevésbé valószínű, hogy túlkorrekciót végez.

## Képelőfeldolgozás OCR: Szűrők helyes sorrendben való hozzáadása

A sorrend számít. Képzeld el, hogy a zajcsökkentést *előtt* végzed a dőléskorrekciónál; a zaj eltorzíthatja a szögdetektálást, ami rosszul igazított eredményt ad. Ezzel szemben a kontraszt növelés *után* a dőléskorrekciónak biztosítja, hogy a forgatás ne hozzon létre új artefaktusokat.

Az alábbiakban egy gyors ellenőrzőlista, amelyet bármely projektbe beilleszthetsz:

| Lépés | Szűrő | Indok |
|------|--------|--------|
| 1 | `DeskewFilter` | Igazítja a szöveg alapvonalát |
| 2 | `DenoiseFilter` | Eltávolítja az elszigetelt pixelzajt |
| 3 | `ContrastBoostFilter` | Javítja az OCR olvashatóságát |

Ha további lépéseket kell beillesztened – például egy **binarization** szűrőt a bináris OCR-hez – akkor azt a kontraszt növelés **után** helyeznéd el, mivel egy tiszta, nagy kontrasztú kép pontosabban binarizálódik.

## Só‑és‑bors zaj eltávolítása a DenoiseFilter-rel

A só‑és‑bors zaj hírhedt az alacsony minőségű szkenneléseknél, különösen a olcsó telefonkamerákból származóknál. A könyvtárunkban a `DenoiseFilter` egy medián‑szűrő kernelt valósít meg, amely minden pixelt a környező pixelek mediánjával helyettesít. Az eredmény? Ezek a foltok eltűnnek anélkül, hogy elmosnák a tényleges karaktereket.

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*Mikor növeld a kernel méretét?* Ha a forrásképek nagy foltokkal vannak tele, egy nagyobb kernel tisztább lesz, de légy óvatos: túl nagy esetén elkezdheted törölni a finom vonalakat a kis betűkben.

## Képek OCR előfeldolgozása – A csővezeték alkalmazása

Miután összeállítottad a szűrőláncot, a motorhoz való csatolása egyetlen soros hívás (`engine.setPreprocessOptions`). Ettől a pillanattól minden `recognizeText` hívás automatikusan a csővezetéken keresztül fut. Nem kell manuálisan meghívni minden szűrőt – a kódod rendezett marad, és a jövőbeni változtatások (új szűrő hozzáadása, paraméterek finomhangolása) egy helyen kezelhetők.

Íme, hogyan néz ki egy sikeres futtatás egy példascan-nel, amely eredetileg 12°-os dőléssel és észrevehető pepper zajjal rendelkezett:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Vedd észre, hogy a szöveg tiszta, helyesen orientált, és mentes a szabad karakterektől, amelyek egyébként „I n v o i c e” vagy „$‑‑‑” formában jelentek volna meg.

## Szélsőséges esetek és gyakori buktatók

| Helyzet | Mit figyelj | Javasolt megoldás |
|-----------|-------------------|---------------|
| Rotation > 15° | A DeskewFilter feladhat | Előre forgass manuálisan vagy használj nagyobb tartományú szűrőt |
| Extremely low resolution ( < 100 dpi ) | A kontraszt növelés nem tudja visszaállítani a részleteket | Először mintavételezd újra a képet (pl. `ResampleFilter`) |
| Mixed noise (Gaussian + salt‑pepper) | A DenoiseFilter önmagában nem elegendő | Helyezz egy `GaussianBlurFilter`-t a `DenoiseFilter` előtt |
| Color scans with colored text | Szürkeárnyalatos konverzió szükséges | Helyezz egy `GrayscaleFilter`-t a kontraszt növelés előtt |

Ezeknek a helyzeteknek az előre látásával órákat takaríthatsz meg a későbbi hibakeresésben.

## Teljes működő példa (minden egyben)

Az alábbiakban egy önálló Java osztályt találsz, amelyet bármely Maven vagy Gradle projektbe beilleszthetsz, amely tartalmazza a `com.example.ocr` függőséget. Bemutatja, hogyan **korrigáljuk a kép dőlését**, **eltávolítsuk a só‑és‑bors zajt**, és **preprocess images OCR**‑stílusban.

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

**Várható kimenet** (feltételezve, hogy a `scanned-document.png` egy tiszta számlát tartalmaz):

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

Ha a képet egy már tökéletesen igazított képre cseréled, észre fogod venni, hogy a csővezeték továbbra is fut – semmi nem romlik, és az OCR pontosság magas marad.

## Következtetés

Most már alaposan érted, **hogyan korrigáljuk a kép dőlését**, és miért fontos minden egyes előfeldolgozó lépés – **image preprocessing OCR**, **remove salt pepper**, és **preprocess images OCR** – a tiszta, kereshető szöveg előállításában. A fenti példa egy teljes...

## Mit érdemes következőként megtanulni?

Az alábbi útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan használjuk az AspOCR-t: Kép OCR szűrők előfeldolgozása .NET-hez](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Dőlés szögének kiszámítása OCR kép előfeldolgozáshoz](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [Hogyan állítsuk be a küszöbértéket OCR képfelismerésben](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}