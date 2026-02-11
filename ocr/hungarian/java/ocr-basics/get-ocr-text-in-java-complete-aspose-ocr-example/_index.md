---
category: general
date: 2026-01-07
description: Szerezzen OCR‑szöveget egy képről az Aspose OCR Java használatával. Tanulja
  meg, hogyan lehet szöveget kinyerni a képből, betölteni a képet OCR‑hez, és percek
  alatt futtatni egy Java OCR példát.
draft: false
keywords:
- get OCR text
- extract text image
- java OCR example
- aspose OCR Java
- load image OCR
language: hu
og_description: Szerezzen OCR szöveget képekből az Aspose OCR Java segítségével. Ez
  az útmutató bemutat egy Java OCR példát, hogyan kell szöveget kinyerni a képből,
  és hogyan kell hatékonyan betölteni a képet OCR-hez.
og_title: OCR szöveg lekérése Java-ban – Teljes Aspose OCR útmutató
tags:
- OCR
- Java
- Aspose
- Image Processing
title: OCR szöveg lekérése Java-ban – Teljes Aspose OCR példa
url: /hu/java/ocr-basics/get-ocr-text-in-java-complete-aspose-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR szöveg lekérése Java-ban – Teljes Aspose OCR példa

Valaha szükséged volt **OCR szöveg lekérésére** egy beolvasott dokumentumból, de nem tudtad, melyik könyvtárat válaszd? Nem vagy egyedül. Sok valós projektben – gondolj számlázási automatizálásra, nyugta feldolgozásra vagy többnyelvű űrlap digitalizálásra – a képekből szöveg kinyerése az első lépés az automatizálás felé.

Ebben az útmutatóban végigvezetünk egy **java OCR példán** keresztül, amely az Aspose OCR for Java könyvtárat használja. A végére megtanulod, hogyan **tölts be képes OCR-t**, futtasd a motort, és **nyerd ki a szöveg képet** adatokat néhány kódsorral. Nincs felesleges részlet, csak egy gyakorlati megoldás, amelyet be tudsz másolni a saját projektedbe.

## Amit megtanulsz

- Hogyan állítsd be az Aspose OCR for Java-t (beleértve a Maven koordinátákat).  
- A pontos lépések a **képes OCR betöltéséhez** és egy nyelv megadásához.  
- Hogyan **kérj le OCR szöveget** egyszerű karakterláncként, és írd ki a konzolra.  
- Tippek többnyelvű képek kezeléséhez és a nyelvek automatikus felismeréséhez.  

*Előfeltételek*: Java 8 vagy újabb, Maven‑kompatibilis IDE (IntelliJ IDEA, Eclipse vagy VS Code), és egy érvényes Aspose OCR for Java licenc (az ingyenes próba a kiértékeléshez megfelelő).

---

![Flowchart showing how to get OCR text from an image using Aspose OCR Java](https://example.com/ocr-flowchart.png "Get OCR text flow diagram")

## 1. lépés – Aspose OCR függőség hozzáadása (Képes OCR betöltése)

Először mondd meg a Mavennek, hogy töltse le az Aspose OCR könyvtárat. Nyisd meg a `pom.xml` fájlt, és illeszd be a következő `<dependency>` blokkot a `<dependencies>` elembe:

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version available -->
</dependency>
```

> **Pro tipp**: Ha Gradlet használsz, az ekvivalens `implementation 'com.aspose:aspose-ocr:23.9'`. A függőség hozzáadása a legolcsóbb módja a **képes OCR** képességek betöltésének a projektedbe.

## 2. lépés – OCR motor létrehozása és a kép betöltése

Most egy kis Java osztályt írunk, amely létrehozza az `OcrEngine` példányt, egy képfájlra mutat, és megmondja a motornak, melyik nyelvet ismerje fel. A nyelvet az ISO‑639‑2 kóddal azonosítjuk (pl. `"tam"` a tamilhez).

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {

    public static void main(String[] args) throws Exception {
        // 2️⃣ Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Load the image you want to process – this is the "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // 2️⃣ Choose the language (ISO‑639‑2). Change "tam" to any supported code.
        engine.getEngineOptions().setLanguage("tam");
        // If you prefer automatic detection, uncomment the next line:
        // engine.getEngineOptions().setAutoDetectLanguage(true);
```

### Miért állítsuk be a nyelvet explicit módon?

A nyelv megadása csökkenti a hamis pozitív eredményeket és felgyorsítja a felismerést. Többnyelvű PDF-ek esetén egy nyelvkódok tömbön iterálhatsz, vagy bekapcsolhatod az automatikus felismerést a kényelem érdekében.

## 3. lépés – OCR folyamat futtatása és **OCR szöveg lekérése**

A motor konfigurálása után a következő sor valójában végrehajtja a felismerést. Az eredményobjektum tartalmazza a kinyert karakterláncot és további metaadatokat.

```java
        // 3️⃣ Perform OCR – this is where we finally **get OCR text**
        OcrResult result = engine.recognize();

        // 3️⃣ Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Amikor futtatod a `LanguageExample`-t, valami ilyesmit kell látnod:

```
=== Extracted Text ===
தமிழ் உரை இங்கு வருகிறது...
```

Ha a `setAutoDetectLanguage(true)`-t használtad, a motor megpróbálja kitalálni a nyelvet, ami hasznos ismeretlen dokumentumok esetén.

## 4. lépés – Gyakori szélhelyzetek kezelése (Szöveg kép változatok kinyerése)

### Alacsony felbontású képek kezelése

Az OCR pontossága drasztikusan csökken 300 dpi alatti felbontásnál. Ha a forrásképed alacsony felbontású, fontold meg először a felbontás növelését:

```java
engine.getEngineOptions().setResolution(300); // forces 300 DPI
```

### Háttérzaj eltávolítása

Néha a beolvasott űrlapokon foltok vannak, amelyek összezavarják a motort. Engedélyezheted az előfeldolgozást:

```java
engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);
```

### Szöveg kinyerése meghatározott területekről

Ha csak egy adott téglalapból (pl. egy táblázatcellából) van szükséged szövegre, állíts be egy `Rectangle`-t a `recognize()` hívása előtt:

```java
engine.setRegion(new Rectangle(50, 100, 400, 200));
```

Ezek a finomhangolások a **java OCR példádat** elég robusztussá teszik a termelési feladatokhoz.

## 5. lépés – Az eredmény ellenőrzése (Mit várhatsz?)

Egy sikeres futtatás kiírja a kép egyszerű szöveges változatát. Többnyelvű képek esetén vegyes írásrendszereket láthatsz:

```
Hello World
こんにちは世界
مرحبا بالعالم
```

Ha a kimenet üres vagy torz, ellenőrizd:

1. A `setImage`-ben megadott fájlútvonal (helyes?).  
2. A nyelvkód megegyezik a képen látható írásrendszerrel.  
3. A kép minősége (kontraszt, DPI) elegendő.

## Teljes működő példa (Kész a másoláshoz és beillesztéshez)

Az alábbiakban az egész fájl látható, készen áll a fordításra és futtatásra. Cseréld ki a `YOUR_DIRECTORY/multilingual.png`-t a tesztképed tényleges útvonalára.

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {
        // Initialize OCR engine
        OcrEngine engine = new OcrEngine();

        // Load the image – this is the core "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // Set language (ISO‑639‑2). For Tamil use "tam". Change as needed.
        engine.getEngineOptions().setLanguage("tam");
        // Uncomment for auto‑detect:
        // engine.getEngineOptions().setAutoDetectLanguage(true);

        // Optional: improve accuracy on low‑res images
        // engine.getEngineOptions().setResolution(300);
        // engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);

        // Perform OCR and retrieve text
        OcrResult result = engine.recognize();

        // Print the extracted text – this is how we **get OCR text**
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Fordítás és futtatás:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.LanguageExample"
```

Most már a kinyert tartalomnak a konzolon kell megjelennie.

---

## Összegzés

Most megmutattuk, **hogyan lehet OCR szöveget lekérni** egy képről az Aspose OCR for Java segítségével. Ezt a **java OCR példát** követve **kivonhatod a szöveg képet** adatokat, **betöltheted a képes OCR-t**, és még finomhangolhatod a motort többnyelvű vagy zajos bemenetekhez.  

Innen tovább:

- Az OCR lépést integrálhatod egy nagyobb munkafolyamatba (pl. a szöveg tárolása adatbázisban).  
- Összekapcsolhatod egy fordítási API-val, hogy a többnyelvű beolvasásokat egyetlen nyelvre alakítsd.  
- Kísérletezhetsz más Aspose OCR funkciókkal, mint a PDF konverzió vagy a vonalkód felismerés.

Próbáld ki, törj el néhány dolgot, majd finomítsd a beállításokat, amíg a kimenet tökéletes lesz. Boldog kódolást, és legyen az OCR mindig kristálytiszta!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}