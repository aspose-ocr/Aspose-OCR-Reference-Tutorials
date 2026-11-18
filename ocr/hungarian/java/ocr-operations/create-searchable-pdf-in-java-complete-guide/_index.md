---
category: general
date: 2026-07-05
description: Készíts kereshető PDF-et Java-ban az Aspose OCR segítségével. Tanulja
  meg, hogyan tömörítheti a képeket a PDF-ben, hogyan konvertálhat beolvasott képet
  PDF-be, és hogyan tilthatja le a betűkészlet beágyazását a PDF-ben a kisebb fájlok
  érdekében.
draft: false
keywords:
- create searchable pdf
- compress images in pdf
- convert scanned image to pdf
- disable font embedding pdf
language: hu
og_description: Keressenelhető PDF létrehozása Java-ban az Aspose OCR-rel. Ez az útmutató
  bemutatja, hogyan lehet tömöríteni a képeket PDF-ben, hogyan lehet szkennelt képet
  PDF-be konvertálni, és hogyan lehet letiltani a betűtípus beágyazását a PDF-ben.
og_title: Kereshető PDF létrehozása Java-ban – Lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to compress
    images in PDF, convert scanned image to PDF, and disable font embedding PDF for
    smaller files.
  headline: Create Searchable PDF in Java – Complete Guide
  type: TechArticle
tags:
- Java
- OCR
- PDF
title: Kereshető PDF létrehozása Java-ban – Teljes útmutató
url: /hu/java/ocr-operations/create-searchable-pdf-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása Java-ban – Teljes útmutató

Valaha is szükséged volt **create searchable PDF** létrehozására egy beolvasott dokumentumból, de elakadtál a „hogyan‑csináljam‑meg” részben? Nem vagy egyedül. Sok projektben a TIFF vagy JPEG PDF‑vé alakítása, amelyet ténylegesen keresni is lehet, *elengedhetetlen* funkció, különösen ha **compress images in PDF**‑t is szeretnél, hogy a fájlméretek kezelhetőek maradjanak.  

Ebben a tutorialban egy gyakorlati példán keresztül mutatjuk be az Aspose OCR for Java használatát. A végére pontosan tudni fogod, hogyan **convert scanned image to PDF**, hogyan állítsd be a **compress images in PDF** opciót, és még a **disable font embedding PDF**‑t is kikapcsolhatod, hogy néhány extra kilobájtot spórolj meg. Nincs felesleges szó – csak egy teljes, futtatható megoldás, amelyet ma be tudsz illeszteni a kódbázisodba.

## Mit fogsz megtanulni

- Az Aspose OCR motor beállítása egy Java projektben.  
- OCR végrehajtása egy TIFF‑en (vagy bármely raszteres képen).  
- `PdfSaveOptions` konfigurálása a **compress images in PDF** és a **disable font embedding PDF** érdekében.  
- Az eredmény mentése **searchable PDF**‑ként, amelyet azonnal indexelhetsz vagy kereshetsz.  

**Előfeltételek**  
- Java 8 vagy újabb telepítve.  
- Maven vagy Gradle a függőségkezeléshez (a Maven példát mutatjuk).  
- Egy beolvasott kép fájl (TIFF, PNG vagy JPEG), amelyet feldolgozni szeretnél.  

Ha ezek megvannak, vágjunk bele.

![Kereshető PDF munkafolyamat – Java OCR PDF konverzió](/images/create-searchable-pdf-workflow.png "Diagram showing the steps to create searchable PDF with Aspose OCR")

## 1. lépés: Aspose OCR függőség hozzáadása

Először húzd be az Aspose OCR könyvtárat a projektedbe. Maven‑nel add hozzá a `pom.xml`‑hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Ha Gradle‑t használsz, az ekvivalens:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tipp:** Figyeld az Aspose kiadási megjegyzéseket; az újabb verziók gyakran hoznak teljesítményjavulást az OCR pontosságában.

## 2. lépés: Az OCR motor inicializálása

Az OCR motor létrehozása olyan egyszerű, mint a `OcrEngine` példányosítása. Ez az objektum kezeli a kép betöltésétől a szöveg kinyeréséig minden lépést.

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

Miért van szükség egy dedikált motorra? Az Aspose elválasztja a nehéz feladatokat (kép előfeldolgozás, nyelvi modellek) a többi alkalmazásodtól, így ugyanazt az `engine`‑t több fájlra is újra felhasználhatod anélkül, hogy a nehéz erőforrásokat újra inicializálnád.

## 3. lépés: OCR végrehajtása a beolvasott képen

Most betápláljuk a motort egy beolvasott fájlba. A `recognizeImage` metódus egy `RecognitionResult`‑et ad vissza, amely a kinyert szöveget és a layout információkat tartalmazza.

```java
import com.aspose.ocr.RecognitionResult;

// ...

// Step 3: Perform OCR on the source image
String sourcePath = "YOUR_DIRECTORY/document_scan.tif"; // could be .png or .jpg too
RecognitionResult result = engine.recognizeImage(sourcePath);
```

> **Mi van, ha a kép nem TIFF?**  
> Az Aspose OCR automatikusan felismeri a gyakori raszteres formátumokat, így JPEG‑et, PNG‑t vagy BMP‑t is megadhatsz anélkül, hogy a kódot módosítanád.

## 4. lépés: PDF mentési beállítások konfigurálása (Képek tömörítése és Betűkészlet beágyazásának letiltása)

Itt jönnek a másodlagos kulcsszavak. Azt mondjuk az Aspose‑nak, hogy **compress images in PDF** és **disable font embedding PDF** legyen. Mindkét beállítás csökkenti a végleges fájlméretet – hasznos, ha tucatnyi dokumentumot szállítasz.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

// ...

// Step 4: Set up PDF save options
PdfSaveOptions pdfOpts = new PdfSaveOptions();

// Reduce PDF size by compressing images
pdfOpts.setCompressImages(true);
pdfOpts.setImageQuality(80); // 0‑100, 80 is a good balance

// Prevent fonts from being embedded – saves a few KB per page
pdfOpts.setEmbedFonts(false);
```

**Miért tömörítsük a képeket?**  
A beolvasott oldalak gyakran nagy felbontásúak; a 80 % minőségre való tömörítés egy 10 oldalas PDF‑et 12 MB‑ről kevesebb, mint 3 MB‑re csökkentheti, anélkül, hogy a vizuális minőség észrevehetően romlana.

**Miért tiltsuk le a betűkészlet beágyazását?**  
Ha az OCR motor szabványos rendszerbetűket (például Arial vagy Times New Roman) használ, azok beágyazása redundáns. Kikapcsolva a fájlméret tovább csökken, különösen nagy mennyiségű fájl esetén.

## 5. lépés: OCR eredmény mentése kereshető PDF‑ként

Az utolsó lépés mindent összeállít: a nyers képet, a kinyert szövegréteget és a korábban beállított PDF‑opciókat.

```java
// Step 5: Save the OCR result as a searchable PDF
String outputPath = "YOUR_DIRECTORY/document.pdf";
engine.saveAsSearchablePdf(outputPath, pdfOpts);

System.out.println("Searchable PDF created at: " + outputPath);
```

Amikor megnyitod a `document.pdf`‑t az Adobe Reader‑ben vagy bármely modern nézőben, az eredeti beolvasott kép **plusz** egy láthatatlan szövegréteget fog mutatni. Ha beírsz egy szót a keresőmezőbe, a megfelelő helyek ki lesznek emelve – pontosan azt a funkciót nyújtja, amit a „create searchable pdf” ígér.

### Várható kimenet

A program egy érvényes TIFF‑kel futtatva valami ilyesmit ad:

```
Searchable PDF created at: YOUR_DIRECTORY/document.pdf
```

Nyisd meg a PDF‑et, nyomd meg a `Ctrl+F`‑et, gépeld be egy olyan szó, amely a beolvasott oldalon szerepel, és láthatod, hogy a megfelelő helyre ugrik. Ez a **create searchable pdf** munkafolyamat sikerének jele.

## Gyakori hibák és elkerülésük módja

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Blank PDF** | `PdfSaveOptions` nincs átadva a `saveAsSearchablePdf`‑nek. | Győződj meg róla, hogy a `PdfSaveOptions`‑t elfogadó overload‑t hívod. |
| **Garbage characters** | OCR nyelv nincs beállítva (alapértelmezett az angol). | Használd a `engine.getLanguage().setLanguage(OcrLanguage.FRENCH);`‑t a `recognizeImage` előtt. |
| **Huge file size** | `setCompressImages(false)` vagy `setEmbedFonts(true)`. | Tartsd meg mindkét flag‑et a fenti példában. |
| **Image distortion** | `setImageQuality` túl alacsonyra van állítva (<50). | Maradj a 70‑90 tartományban a jó kompromisszumért. |

## A példa kibővítése

Most, hogy tudod **convert scanned image to PDF** és a méretet is szabályozni, érdemes lehet:

- **Batch process** egy mappát a beolvasott fájlokkal egy egyszerű `for(File f : folder.listFiles())` ciklussal.  
- **Vízjelek** hozzáadása az Aspose PDF‑vel (`PdfDocument.addWatermarkText`).  
- Az OCR szöveg exportálása **plain .txt** fájlba indexelési rendszerekhez (`result.getText().writeToFile("doc.txt")`).  

Mindezek a kiegészítések ugyanazt az `OcrEngine` példányt használják, így alacsony marad a memóriahasználat.

## Teljes, készen‑álló kód

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Perform OCR on the source image
        String source = "YOUR_DIRECTORY/document_scan.tif";
        RecognitionResult result = engine.recognizeImage(source);

        // Step 3: Configure PDF save options (compress images & disable fonts)
        PdfSaveOptions pdfOpts = new PdfSaveOptions();
        pdfOpts.setCompressImages(true);      // Reduce PDF size by compressing images
        pdfOpts.setImageQuality(80);          // Image quality (0‑100)
        pdfOpts.setEmbedFonts(false);         // Do not embed fonts to keep file size small

        // Step 4: Save the OCR result as a searchable PDF
        String output = "YOUR_DIRECTORY/document.pdf";
        engine.saveAsSearchablePdf(output, pdfOpts);

        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF created at: " + output);
    }
}
```

Másold be ezt az IDE‑dbe, cseréld le a `YOUR_DIRECTORY`‑t egy valós útvonalra, és futtasd. Ha minden helyesen van beállítva, egy **searchable PDF**-et kapsz, amely a képtömörítésnek és a betűkészlet beágyazásának letiltásának köszönhetően könnyű is.

## Összegzés

Most már mindent tudsz, ami ahhoz kell, hogy **create searchable pdf** fájlokat készíts Java‑ban az Aspose OCR segítségével. Az engine inicializálásától, az OCR végrehajtásán, a **compress images in pdf** és a **disable font embedding pdf** beállításain, egészen a kereshető dokumentum mentéséig – minden lépést megmagyaráztunk a mögöttes okokkal együtt.  

Készen állsz a következő kihívásra? Próbáld ki az OCR nyelvi csomagok hozzáadását, a mappák kötegelt feldolgozását, vagy a PDF‑ek annotációkkal való rétegezését. Az alapok, amelyeket most elsajátítottál, megkönnyítik ezeket a bővítéseket.

Van kérdésed, vagy szeretnél saját trükköket megosztani? Írj egy megjegyzést alul, és jó kódolást!


## Mit tanulj meg legközelebb?


Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy könnyedén elsajátíthasd az API további funkcióit és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [PDF szöveg felismerése – OCR műveletek Aspose.OCR for Java‑val](/ocr/english/java/ocr-operations/)
- [PDF dokumentumok OCR‑os felismerése Aspose.OCR for Java‑ban](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Hogyan OCR‑ozz PDF‑et .NET‑ben az Aspose.OCR‑val](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}