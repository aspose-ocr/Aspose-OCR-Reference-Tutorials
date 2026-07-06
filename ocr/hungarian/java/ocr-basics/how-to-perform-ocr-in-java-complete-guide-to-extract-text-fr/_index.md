---
category: general
date: 2026-06-06
description: Hogyan végezzünk OCR-t Java-ban – gyorsan szöveget nyerjünk ki képből,
  konvertáljuk a képet szöveggé, és olvassuk el a szöveget JPG-ből egy egyszerű kódrészlet
  segítségével.
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: hu
og_description: hogyan hajtsunk végre OCR-t Java-ban – tanulja meg, hogyan nyerjen
  ki szöveget képből, konvertálja a képet szöveggé, és olvassa el a szöveget jpg-ből
  egy kész példával.
og_title: Hogyan végezzünk OCR-t Java-ban – Lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  headline: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  type: TechArticle
- description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  name: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  steps:
  - name: What You’ll Learn
    text: '- Install an OCR library (yes, **ocr in java** is easier than you think).
      - Create and configure an OCR engine instance. - Load a JPG (or any image) and
      set the language. - Process the image and **extract text from image** files.
      - Print the recognized string to the console.'
  - name: Expected Output
    text: 'If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console
      will show:'
  - name: 'Pro Tip: Batch Processing'
    text: 'If you need to **extract text from image** files in bulk, wrap the core
      logic in a loop:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Hogyan végezzünk OCR-t Java-ban – Teljes útmutató a képekből szöveg kinyeréséhez
url: /hu/java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk OCR-t Java-ban – Teljes útmutató a képekből történő szöveg kinyeréséhez

Gondolkodtál már azon, **how to perform OCR** a telefonoddal készített képen? Nem vagy egyedül. Akár egy nyugták beolvasását végző alkalmazást építesz, akár csak szöveget kell kinyerned egy beolvasott PDF-ből, a **how to perform OCR** Java-ban egy olyan készség, amely gyorsan megtérül. Ebben a tutorialban egy gyakorlati példán keresztül vezetünk, amely **extracts text from image** fájlokból, **converts image to text**, és még azt is megmutatja, hogyan **read text from jpg** csak néhány kódsorral.

> *Pro tipp:* Ugyanez a megközelítés működik PNG, BMP vagy bármely, az OCR motor által támogatott formátummal – csak cseréld ki a fájlnevet.

## Hogyan végezzünk OCR-t Java-ban – Áttekintés

Az Optikai Karakterfelismerés (OCR) egy olyan technológia, amely a betűket ábrázoló képeket valós, kereshető szöveggé alakítja. A Java ökoszisztémában több könyvtár is létezik – Tesseract, Asprise és kereskedelmi SDK-k – amelyek hasonló munkafolyamatot kínálnak: betölt egy képet, megadja a motor számára a várt nyelvet, futtatja a felismerést, és lekéri az eredményt. Az alábbiakban egy általános `OcrEngine` osztályt használunk, hogy a példát tisztán tartsuk, de bármely konkrét megvalósítással helyettesítheted, amely követi ugyanazt a mintát.

### Mit fogsz megtanulni

- Telepíts egy OCR könyvtárat (igen, **ocr in java** könnyebb, mint gondolnád).
- Hozz létre és konfigurálj egy OCR motor példányt.
- Tölts be egy JPG-t (vagy bármilyen képet), és állítsd be a nyelvet.
- Feldolgozd a képet és **extract text from image** fájlokból.
- Írd ki a felismert karakterláncot a konzolra.

A végére egy önálló Java programod lesz, amelyet bármely projektbe beilleszthetsz és azonnal futtathatsz.

![how to perform OCR example](ocr-example.png "how to perform OCR in Java illustration")

## 1. lépés – OCR könyvtár telepítése és importálása (ocr in java)

Mielőtt egyetlen Java sort is írnál, szükséged van egy könyvtárra, amely ténylegesen elvégzi a nehéz munkát. Ha Maven-t használsz, adj hozzá egy függőséget így (cseréld le a `com.example.ocr`-t a választott SDK valódi csoportazonosítójára):

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

Ha inkább Gradle-t használsz:

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

Miután a JAR a classpath-on van, importáld a szükséges osztályokat:

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

> **Miért fontos:** A megfelelő osztályok importálása megakadályozza a „cannot find symbol” hibákat, és boldoggá teszi az IDE-det – semmi sem frusztrálóbb, mint egy hiányzó import, amikor **convert image to text** próbálsz.

## 2. lépés – OCR motor példány létrehozása (how to perform OCR)

Most, hogy a könyvtár készen áll, indítsd el a motort. Tekintsd a motort az agynak, amely a pixeleket nézve kitalálja a betűket.

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

A motor létrehozása általában olcsó; a legtöbb SDK belső puffereket lusta módon allokál, így biztonságosan újra felhasználhatod ugyanazt a példányt sok kép esetén, ha kötegelt feldolgozást végzel.

## 3. lépés – Kép betöltése és nyelv beállítása (extract text from image)

A következő lépés, hogy adjunk a motorhoz valamit, amit olvashat. Itt egy JPEG-et töltünk be a lemezről, és megmondjuk az OCR motornak, hogy a szöveg mongol (ISO 639‑2 kód: “mon”). A útvonalat vagy a nyelvkódot módosíthatod a saját felhasználási esetedhez.

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

> **Megjegyzés:** Ha nem állítasz be nyelvet, a motor alapértelmezés szerint angolt használ, ami drámaian csökkentheti a pontosságot, ha a szöveg valójában cirill vagy más írásrendszer. Mindig add meg a helyes nyelvet, ha lehetséges.

## 4. lépés – Kép feldolgozása és az eredmény lekérése (convert image to text)

Miután a kép és a nyelv be van állítva, kérd meg a motort, hogy végezze el a varázslatot. A `process()` hívás lefuttatja az OCR algoritmust, és egy `OcrResult` objektumot ad vissza, amely a felismert karakterláncot és a megbízhatósági pontszámokat tartalmazza.

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

A háttérben a motor előfeldolgozást végezhet – kiegyenesítés, binarizálás, zajcsökkentés – így neked nem kell ezeket a lépéseket megírnod. Ezért a legtöbb modern OCR könyvtár öröm használni **convert image to text** feladatokhoz.

## 5. lépés – Kinyert szöveg kiírása (read text from jpg)

Végül vedd ki a nyers szöveget az eredményből, és használd fel valami hasznosra. Ebben a demóban egyszerűen a konzolra nyomtatjuk, de fájlba is írhatod, keresőindexbe betáplálhatod, vagy egy másik szolgáltatásnak átadhatod.

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

Ez a sor önmagában bizonyítja, hogy sikeresen **read text from jpg** (vagy bármely támogatott formátum). Ha a kimenet torznak tűnik, ellenőrizd újra a nyelvkódot és a kép minőségét.

## Teljes működő példa (Minden lépés egyben)

Az alábbiakban egy teljes, azonnal futtatható Java osztály található, amely minden részt összekapcsol. Másold be egy `OcrDemo.java` nevű fájlba, állítsd be a kép útvonalát és a nyelvet, majd futtasd a `javac OcrDemo.java && java OcrDemo` parancsot.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to perform OCR in Java using a generic OCR SDK.
 * This example loads a JPG, sets the language to Mongolian, and prints
 * the recognized text to the console.
 *
 * Replace the import package with the actual library you are using.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Validate command‑line arguments
        if (args.length < 2) {
            System.err.println("Usage: java OcrDemo <image-path> <language-code>");
            System.exit(1);
        }

        String imagePath = args[0];   // e.g., "input.jpg"
        String language = args[1];    // e.g., "mon" for Mongolian

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image
        ocrEngine.setImage(new OcrInputImage(imagePath));

        // Step 3: Set the language (ISO‑639‑2)
        ocrEngine.getSettings().setLanguage(language);

        // Step 4: Run the recognition
        OcrResult result = ocrEngine.process();

        // Step 5: Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Várható kimenet

Ha az `input.jpg` a mongol „Сайн байна уу?” kifejezést tartalmazza, a konzol a következőt fogja mutatni:

```
=== Recognized Text ===
Сайн байна уу?
```

Ha a kép elmosódott vagy a nyelvkód hibás, torz karaktereket vagy egy üres karakterláncot fogsz látni – gyakori hibák, amelyeket a következőkben tárgyalunk.

## Gyakori hibák és megoldások

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Torz Cyrillic karakterek | Helytelen nyelvkód (alapértelmezett angol) | Állítsd be `ocrEngine.getSettings().setLanguage("mon")` vagy a megfelelő kódot. |
| Egyáltalán nem jelenik meg kimenet | A kép útvonala hibás vagy a fájl nem olvasható | Ellenőrizd az útvonalat, győződj meg róla, hogy a fájl létezik, és a folyamatnak olvasási jogosultsága van. |
| Alacsony pontosság (<70 %) | A kép alacsony kontrasztú vagy elfordított | Előfeldolgozd a képet: növeld a kontrasztot, kiegyenesítsd, vagy konvertáld szürkeárnyalatossá, mielőtt a motorhoz adnád. |
| `OutOfMemoryError` nagy PDF-eken | Sok nagy felbontású oldal betöltése egyszerre | Dolgozd fel az oldalakat egyenként, vagy méretezd le a képeket OCR előtt. |

### Pro tipp: Kötetes feldolgozás

Ha nagy mennyiségben kell **extract text from image** fájlokat feldolgozni, csomagold a fő logikát egy ciklusba:

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

Ez a kódrészlet bemutatja, milyen egyszerű skálázni egyetlen JPG-ról egy teljes mappa beolvasására.

## Továbbfejlesztés – Mit érdemes még felfedezni?

- **Language Packs:** A legtöbb OCR SDK lehetővé teszi további nyelvi adatfájlok letöltését. Új csomag hozzáadásával **convert image to text** olyan nyelvekhez, amelyek túlmutatnak az angolon és a mongolon.
- **PDF OCR:** Kombináld ezt a kódot az Apache PDFBox-szal, hogy

## Mit érdemes legközelebb megtanulni?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes működő kódpéldákat lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Képek szövegének kinyerése – OCR alapok Aspose.OCR Java-hoz](/ocr/english/java/ocr-basics/)
- [Kép konvertálása szöveggé Java-ban az Aspose.OCR BufferedImage használatával](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Hogyan OCR-eljünk képszöveget nyelvvel az Aspose.OCR használatával](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}