---
category: general
date: 2026-01-12
description: Képből szöveg kinyerése Aspose OCR használatával Java-ban. Tanulja meg,
  hogyan nyerhet ki szöveget egy számla képből Java OCR példával, és hogyan szerezheti
  meg a kimeneti OCR szöveget.
draft: false
keywords:
- extract text from image
- how to extract text
- java ocr example
- process invoice image
- output ocr text
language: hu
og_description: Kép szövegének kinyerése Aspose OCR-rel Java-ban. Ez az útmutató bemutatja,
  hogyan nyerhetünk ki szöveget egy számla képből, tartalmaz egy Java OCR példát,
  és megjeleníti az OCR szöveget.
og_title: Szöveg kinyerése képből Java-ban – Teljes OCR példa
tags:
- OCR
- Java
- Aspose
title: Kép szövegének kinyerése Java-ban – Teljes OCR példa
url: /hu/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg kinyerése képből Java-ban – Teljes OCR példa

Gondolkodtál már azon, hogyan **szöveg kinyerése képből** fájlokból anélkül, hogy a hajadba nyúlnál? Lehet, hogy egy halom beolvasott számlád van, és gyorsan szükséged van a számokra. Tapasztalatom szerint a legegyszerűbb mód, ha egy dedikált OCR könyvtárra bízzuk a nehéz munkát. Ez a tutorial megmutatja, hogyan *hogyan nyerjünk ki szöveget* egy tipikus számla képből az Aspose OCR for Java használatával, és még egy **java ocr example**-t is bemutat, amely az OCR szöveget adja ki, amit továbbíthatsz a downstream rendszeredbe.

Át fogunk vezetni mindenen, amit tudnod kell: a projekt beállításától, a érdeklődési terület (ROI) meghatározásáig, amely a fejlécre és a teljes összegre fókuszál, egészen a kinyert szöveg kiírásáig. A végére képes leszel **process invoice image** fájlokat automatikusan feldolgozni és tiszta, kereshető szöveget visszanyerni.

> **What you’ll get:** egy azonnal futtatható Java programot, világos magyarázatokat minden lépéshez, és gyakorlati tippeket a valós számlák kezeléséhez.

## Előfeltételek

- Java Development Kit (JDK) 8 vagy újabb telepítve.
- Maven vagy Gradle a függőségkezeléshez (Maven példa látható).
- Aspose OCR for Java licenc (az ingyenes próba a teszteléshez működik).
- Egy számla kép (`invoice.png`) egy ismert könyvtárban elhelyezve.

Ha bármelyik ismeretlennek tűnik, ne aggódj—a legtöbb csak egy letöltésre van, és a kód továbbra is lefordul a community kiadással.

## 1. lépés: Maven projekt beállítása

Először hozz létre egy új Maven projektet (vagy adj hozzá egy meglévőhöz). A `pom.xml`-ben add hozzá az Aspose OCR függőséget:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest version available -->
    </dependency>
</dependencies>
```

> **Pro tip:** Tartsd naprakészen a verziószámot; az újabb kiadások gyakran javítják a pontosságot a számlákon előforduló nehéz betűtípusok esetén.

A fájl mentése után futtasd a `mvn clean install` parancsot, hogy a könyvtárat a helyi tárolóba töltse.

## 2. lépés: Számla kép betöltése

Most, hogy a könyvtár készen áll, írjunk egy kis Java osztályt. Az első dolog, amit csinálunk, egy `OcrEngine` példány létrehozása, és rámutatunk arra a képre, amelyet be szeretnénk olvasni.

```java
import com.aspose.ocr.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png"); // <-- replace with your path
```

Miért hozunk létre az engine-t **a kép betöltése előtt**? Az engine tartalmazza a konfigurációt, mint például a nyelv, DPI és ROI. A kép korai beállítása biztosítja, hogy ezek a beállítások az éppen feldolgozandó fájlra vonatkozzanak.

## 3. lépés: Érdeklődési területek (ROI) meghatározása

A számlák gyakran sok zajt tartalmaznak — táblázatok, logók és apró betűk. Az OCR-t csak a fejlécre és a teljes összegre korlátozva jelentősen növelheted a sebességet és a pontosságot. Az Aspose lehetővé teszi ezen zónák leírását téglalapokkal.

```java
        // Step 3: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Apply ROI to the engine
        engine.setRegion(region);
```

A koordináták pixelben vannak (`x`, `y`, `width`, `height`). Ha a számláid mérete változik, dinamikusan kiszámíthatod ezeket az értékeket — például először a kép méreteit ellenőrizve. Ez egy szép kiegészítés, ha **process invoice image** megoldásra van szükséged, amely kötegelt feldolgozást támogat.

## 4. lépés: OCR futtatása a megadott területeken

A ROI beállítása után az OCR engine a legfontosabb helyre tudja összpontosítani a figyelmet. A `recognize()` metódus egy `OcrResult`-ot ad vissza, amely a kinyert szöveget tartalmazza.

```java
        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();
```

A háttérben az Aspose több előfeldolgozási lépést hajt végre: binarizálás, zajeltávolítás és karakter szegmentálás. Ezeket nem kell kézzel meghívnod — csak hagyd, hogy a `recognize()` elvégezze a dolgát.

## 5. lépés: Kinyert szöveg kiírása

Végül kiírjuk a szöveget a konzolra. Egy valódi alkalmazásban esetleg adatbázisba tárolhatod, egy downstream analitikai csővezetékbe továbbíthatod, vagy akár kereshető PDF-et is generálhatsz.

```java
        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

A program futtatásakor valami ilyesmit kell látnod:

```
ROI text:
Acme Corp.
Invoice #12345
Date: 2025-12-31
Total Amount: $1,250.00
```

Ha a kimenet összezavartnak tűnik, ellenőrizd újra a téglalap koordinátákat vagy növeld a kép felbontását. Az OCR engine-k a tiszta, magas DPI-s szkennelést kedvelik.

## Teljes működő példa

Az alábbiakban a teljes, önálló Java fájl látható, amelyet beilleszthetsz a `src/main/java/RoiExample.java`-ba. Nincs szükség külső kódrészletekre — minden, amire szükséged van, itt megtalálható.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.region.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png");

        // Step 2: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Step 3: Apply the ROI configuration to the engine
        engine.setRegion(region);

        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

> **Note:** Replace `YOUR_DIRECTORY` with the absolute path to your invoice image. If you’re using a relative path, make sure the working directory matches where you run the `java` command.

## Gyakori kérdések és speciális esetek

### Mi van, ha a számla mérete változik?

Dinamikusan kiszámíthatod a ROI-t:

```java
int imgWidth = engine.getImage().getWidth();
int imgHeight = engine.getImage().getHeight();

int headerHeight = imgHeight / 10;
int totalHeight = imgHeight / 8;

OcrRegion region = OcrRegion.builder()
        .addRectangle(0, 0, imgWidth, headerHeight)
        .addRectangle(0, imgHeight - totalHeight, imgWidth, totalHeight)
        .build();
```

### Hogyan kezeljem a több nyelvet?

Az Aspose OCR nyelvi csomagokat támogat. Csak állítsd be a nyelvet a `recognize()` hívása előtt:

```java
engine.setLanguage(OcrLanguage.Spanish); // or OcrLanguage.English, etc.
```

### Mi van, ha az OCR üres karakterláncokat ad vissza?

Tipikus okok:

- Alacsony kép felbontás (< 300 DPI). Növeld fel vagy kérj jobb minőségű szkennelést.
- Túl sötét vagy túl világos háttér. Alkalmazz egyszerű kontraszt‑növelő szűrőt az OCR előtt.
- Hibás ROI koordináták, amelyek teljesen kihagyják a szöveget.

## Tippek a termelésre kész OCR-hez

1. **Batch Processing:** Csomagfeldolgozás: Csomagold a logikát egy ciklusba, amely egy könyvtárban lévő számla fájlokon iterál. Naplózd minden eredményt az auditálhatóság érdekében.
2. **Error Handling:** Hibakezelés: Fogd el az `OcrException`-t, hogy elegánsan kihagyhasd a sérült képeket anélkül, hogy leállítanád a teljes feladatot.
3. **Performance:** Teljesítmény: Használj egyetlen `OcrEngine` példányt több képhez; új engine létrehozása fájlonként felesleges terhet jelent.
4. **Validation:** Érvényesítés: Kinyerés után futtass regex ellenőrzést a teljes összegre (`\$\d{1,3}(,\d{3})*(\.\d{2})?`), hogy a szám reálisnak tűnjön.

Ezeknek a javaslatoknak a megvalósítása egy egyszerű **java ocr example**-t robusztus, skálázható megoldássá alakít, amely bármely vállalkozás számára alkalmas, amelynek éjszakánként **process invoice image** fájlokat kell feldolgoznia.

## Következtetés

Most bemutattuk, hogyan **szöveg kinyerése képből** fájlokban Java használatával az Aspose OCR-rel, egy gyakorlati számlafeldolgozási szituációra fókuszálva. A ROI meghatározásával, az OCR engine futtatásával és a **kimeneti OCR szöveg** kiírásával most egy szilárd alapot kaptál az automatizált adatgyűjtő csővezetékek építéséhez.

Következő lépések? Próbáld meg kibővíteni a ROI-t, hogy tartalmazza a sor‑elemek táblázatait, kísérletezz különböző nyelvi beállításokkal, vagy add át a kinyert karakterláncokat egy PDF‑generáló könyvtárnak kereshető dokumentumokhoz. Nincs határ, ha az OCR-t modern Java eszközökkel kombinálod.

Van még kérdésed a **hogyan nyerjünk ki szöveget** más dokumentumtípusokból, vagy segítségre van szükséged a ROI finomhangolásához szokatlan elrendezésekhez? Írj egy megjegyzést alább — jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}