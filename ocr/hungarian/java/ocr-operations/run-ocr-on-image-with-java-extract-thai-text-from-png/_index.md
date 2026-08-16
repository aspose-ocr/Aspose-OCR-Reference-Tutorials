---
category: general
date: 2026-03-28
description: Futtass OCR-t képen Java-ban az Aspose OCR használatával, hogy a képet
  szöveggé alakítsa, és gyorsan, megbízhatóan kivonja a thai szöveget a PNG-ből.
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: hu
og_description: Futtass OCR-t képen Java és az Aspose OCR segítségével. Tanuld meg,
  hogyan konvertálj képet szöveggé, hogyan nyerj ki thai szöveget PNG-ből, és hogyan
  kezeld a gyakori buktatókat.
og_title: Futtass OCR-t képen Java-val – Gyors thai szöveg kinyerése
tags:
- OCR
- Java
- Aspose
- Image Processing
title: OCR futtatása képen Java-val – Thai szöveg kinyerése PNG-ből
url: /hu/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR futtatása képen Java‑val – Teljes körű útmutató

Gondolkodtál már azon, hogyan **futtathatsz OCR‑t képfájlokon** közvetlenül Java‑kódból? Lehet, hogy thai nyugta, beolvasott dokumentum vagy képernyőmentés gyűjteményed van, és a szöveget szeretnéd a gép által beolvasni anélkül, hogy kézzel gépelnéd be. Ez gyakori probléma, különösen, ha a forrás PNG, és a nyelv nem latin.

Ebben az útmutatóban pontosan megmutatjuk, hogyan **futtathatsz OCR‑t képen** az Aspose OCR könyvtárral, hogyan alakíthatod a képet egyszerű szöveggé, és hogyan nyerheted ki megbízhatóan a thai karaktereket. A végére képes leszel **képet szöveggé konvertálni**, **szöveget kinyerni PNG‑ból**, sőt **thai szöveget felismerni** néhány kódsorral.

## Mit fed le ez az útmutató

* Az Aspose OCR függőség beállítása Maven/Gradle projektben.  
* Az `OcrEngine` inicializálása és thai nyelvre konfigurálása.  
* OCR futtatása PNG‑fájlon és esetleges hibák kezelése.  
* Az eredmény kiírása a konzolra és a kimenet ellenőrzése.  

Előzetes Aspose tapasztalat nem szükséges – csak egy alap Java IDE és egy képfájl, amelyet feldolgozni szeretnél.

## Előfeltételek

* Java 8 vagy újabb telepítve (a könyvtár Java 11+‑tel is működik).  
* Build eszköz – Maven vagy Gradle (a Maven példát mutatjuk).  
* Aspose OCR licenc (az ingyenes próba verzió teszteléshez elegendő, de a licenc eltávolítja a kiértékelési korlátokat).  
* Egy PNG, amely thai szöveget tartalmaz, pl. `input.png` a projekted resources mappájában.

---

## 1. lépés: Aspose OCR hozzáadása a projekthez

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **Pro tipp:** Tartsd a könyvtár verzióját szinkronban a hivatalos Aspose kiadási jegyzékekkel; az újabb verziók nyelvi csomagokat és teljesítményjavításokat hoznak.

Miután a függőség feloldódott, az IDE‑nek automatikusan importálnia kell a szükséges osztályokat.

## 2. lépés: Az OCR motor inicializálása

A motor a folyamat szíve – gondolj rá úgy, mint a „agyra”, amely a pixelmintákat elemzi. Megmondjuk neki, hogy csak a thai karakterek érdekelnek.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

Miért állítjuk be explicit módon a nyelvet? Mert a `"th"` megadása szűkíti a karakterkészletet, ami felgyorsítja a felismerést és csökkenti a hasonló kinézetű glifek félreolvasását.

## 3. lépés: OCR futtatása a PNG fájlon

Most betápláljuk a motorba a dekódolni kívánt képet. A `recognizeImage` metódus egy `OcrResult` objektumot ad vissza, amely a kinyert szöveget és a biztonsági pontszámokat tartalmazza.

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

Ha a fájl nem található, az Aspose `FileNotFoundException`‑t dob. Jó ötlet a hívást `try‑catch` blokkba tenni a produkciós kódban, de ebben az útmutatóban egyszerűen maradunk.

## 4. lépés: A felismert szöveg kiírása

Végül kiírjuk az eredményt. A `getText()` metódus egy egyszerű Java `String`‑et ad vissza, amelyet tárolhatsz, hálózaton küldhetsz, vagy fájlba írhatod.

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

A program futtatásakor valami ilyesmit kell látnod:

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

Ha a kimenet összezavarodott, ellenőrizd, hogy a forrás PNG magas felbontású‑e (legalább 300 dpi), és hogy a nyelvkód `"th"` megfelel a célnyelvednek.

### Teljes kódlista

Az alábbiakban a teljes, azonnal futtatható Java fájl található. Másold be az IDE‑dbe, szükség szerint módosítsd a kép útvonalát, és nyomd meg a **Run** gombot.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![OCR futtatása képen példa](image.png "OCR futtatása képen példa – Java kód thai szöveg kinyerésére PNG‑ból")

## 5. lépés: Gyakori variációk és széljegyek

### Kép konvertálása szöveggé más formátumokban

Ha **képet szöveggé konvertálsz** JPEG‑re vagy BMP‑re, egyszerűen változtasd meg a fájlkiterjesztést az `imagePath`‑ban. Az Aspose OCR támogatja a PNG, JPEG, BMP, TIFF és még a PDF oldalakat is.

### Szöveg kinyerése PNG‑ból több nyelven

A motor egyszerre több nyelvet is felismerhet:

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

Az eredmény thai és angol karakterek keverékét tartalmazza, ami hasznos a kétnyelvű nyugták esetén.

### Alacsony minőségű képek kezelése

Homályos beolvasásoknál érdemes előfeldolgozást engedélyezni:

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

Ez beépített zajszűrő és kontraszt‑növelő algoritmusokat indít, javítva a **szöveg kinyerése PNG‑ból** lépést.

### Licenc aktiválása

Licenc nélkül az Aspose 100 oldal után egy vízjel sort helyez a kimenetbe. Aktiváld a licencet minél előbb:

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

Tedd a `.lic` fájlt a JAR mellé, vagy hivatkozz rá abszolút úton.

## Gyakran ismételt kérdések

**Q: Működik ez Linuxon?**  
A: Teljesen. Az Aspose OCR tisztán Java, így bármely JVM‑kompatibilis operációs rendszer megfelelő.

**Q: Mi van, ha a PNG kézzel írott thai szöveget tartalmaz?**  
A: A kézírás felismerése korlátozott; valószínűleg egy dedikált neurális háló modellre lesz szükség. Az Aspose OCR nyomtatott szövegnél kiemelkedő.

**Q: Képes vagyok egy mappában lévő képeket kötegelt feldolgozni?**  
A: Csomagold be a `recognizeImage` hívást egy ciklusba, például `Files.list(Paths.get("folder"))`. A teljesítmény érdekében használd ugyanazt az `OcrEngine` példányt.

## Összegzés

Lépésről‑lépésre végigvettük, hogyan **futtathatsz OCR‑t képen** Java‑ban, különösen hogyan **nyerhetsz ki thai szöveget** egy PNG‑ból. Az `OcrEngine` inicializálásával, a nyelv beállításával, a `recognizeImage` meghívásával és az eredmény kiírásával most már van egy megbízható módszered a **kép szöveggé konvertálására** külső szolgáltatások nélkül.

Innen tovább:

* **szöveg kinyerése PNG‑ból** tömegesen adatbányászati projektekhez.  
* Az OCR kimenet kombinálása egy fordító API‑val az angol megfelelőkhez.  
* Más, az Aspose által támogatott nyelvek felfedezése, például kínai vagy arab, a nyelvkód cseréjével.

Próbáld ki a saját képeiddel – állítsd be az előfeldolgozási opciókat, kísérletezz különböző fájlformátumokkal, és nézd meg, mennyire robusztus a megoldás a valós munkafolyamatodban.

Boldog kódolást, és legyen az OCR csővezetéked mindig pontos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}