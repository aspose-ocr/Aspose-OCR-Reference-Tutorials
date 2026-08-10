---
category: general
date: 2026-02-14
description: Képről szöveg kinyerése az Aspose OCR segítségével. Tanulja meg, hogyan
  töltsön be képet OCR-hez, hogyan olvassa el a szöveget egy téglalapból, és kövesse
  ezt az Aspose OCR oktatót percek alatt.
draft: false
keywords:
- extract text from image
- load image for ocr
- read text from rectangle
- aspose ocr tutorial
language: hu
og_description: Azonnal szöveget nyer ki a képből. Ez az útmutató bemutatja, hogyan
  töltsön be képet OCR-hez, hogyan olvassa ki a szöveget egy téglalapból, és hogyan
  fejezze be az Aspose OCR bemutatót.
og_title: Kép szövegének kinyerése az Aspose OCR-rel – Gyors útmutató
tags:
- Aspose
- OCR
- Java
title: Szöveg kinyerése képből az Aspose OCR-rel – Lépésről‑lépésre bemutató
url: /hu/java/ocr-operations/extract-text-from-image-with-aspose-ocr-step-by-step-demo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép szövegének kinyerése Aspose OCR-rel – Lépésről‑lépésre bemutató

Valaha szükséged volt **extract text from image**-re, de nem tudtad, hol kezdj? Nem vagy egyedül — sok fejlesztő szembesül ezzel, amikor először próbálja meg a nyugták beolvasását vagy a személyazonosító ellenőrzését. A jó hír? Az Aspose OCR-rel betölthetsz egy képet, meghatározhatod a pontos területet, ahol a szöveg található, és néhány sor kóddal kinyerheted a karaktereket.

Ebben a **aspose ocr tutorial**‑ban végigvezetünk minden szükséges lépésen: a kép betöltése OCR‑hez, egy olyan téglalap beállítása, amely megmondja a motornak, hol keressen, és végül a kinyert szöveg olvasása. A végére egy futtatható Java programod lesz, amely kiírja a ROI szöveget a konzolra — nincs rejtély, csak egy tiszta, működő megoldás.

## Amire szükséged lesz

| Előfeltétel | Miért fontos |
|--------------|----------------|
| **Java JDK 8+** | Az Aspose OCR Java könyvtárként érkezik; bármely modern JDK megfelel. |
| **Aspose.OCR for Java** (download from the Aspose website or add via Maven) | Biztosítja az `OcrEngine`, `ImageStream` és a kapcsolódó osztályokat. |
| **An image file** (e.g., `receipt.jpg`) that contains printable text | Egy képfájl (pl. `receipt.jpg`), amely nyomtatható szöveget tartalmaz |
| **IDE or editor** (IntelliJ, Eclipse, VS Code…) | Segít gyorsan lefordítani és futtatni a példát. |

Ha Maven‑t használsz, add hozzá ezt a függőséget a `pom.xml`‑hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Aspose for the latest version -->
</dependency>
```

> **Pro tipp:** A fenti verziószám 2026 februárjában aktuális. A legújabb kiadásra frissítve biztosítod a hibajavításokat és a teljesítményjavulásokat.

## 1. lépés – Az OCR motor inicializálása

Először is: szükséged van egy `OcrEngine` példányra. Gondolj rá úgy, mint az agyra, amely a pixeleket elemzi.

```java
// Step 1: Create the OCR engine object
OcrEngine ocrEngine = new OcrEngine();
```

Miért így hozod létre? Az Aspose szétválasztja a motort (amely a konfigurációt tartalmazza) a képadattól, így lehetőséged nyílik ugyanazt a motort több képnél is újrahasználni, ha szeretnéd.

## 2. lépés – Kép betöltése OCR‑hez

Most ténylegesen **load image for OCR**‑t hajtunk végre. Az `ImageStream.fromFile` segédfüggvény beolvassa a fájlt egy áramlásba, amelyet az Aspose értelmez.

```java
// Step 2: Load the target image (replace with your own path)
String imagePath = "YOUR_DIRECTORY/receipt.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

Ha a fájl nem található, a motor kivételt dob, ezért érdemes ezt try‑catch blokkba helyezni a termék kódban. Ebben a demóban hagyjuk, hogy a kivétel feljebb terjedjen — így a példa tiszta marad.

## 3. lépés – Téglalap meghatározása (Read Text from Rectangle)

Itt jön képbe a **read text from rectangle** rész. Megmondod a motornak, pontosan hol keressen, ami felgyorsítja a feldolgozást és csökkenti a hamis pozitív eredményeket.

```java
// Step 3: Create a rectangle that covers the area with the receipt total
// Parameters: x, y, width, height (all in pixels)
Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);
```

> **Miért téglalap?**  
> A legtöbb dokumentumnak előre meghatározott elrendezése van – gondolj egy nyugtára, ahol az összeg mindig az alja felé kerül. Ennek a szeletnek a fókuszálásával az OCR motor figyelmen kívül hagyja a lényegtelen grafikákat és növeli a pontosságot.

**Edge case:** Ha a téglalap meghaladja a kép határait, az Aspose csendben levágja, de adatveszteség keletkezik. Egy gyors ellenőrzés megakadályozhatja ezt:

```java
if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
    regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
    throw new IllegalArgumentException("ROI exceeds image dimensions.");
}
```

## 4. lépés – Kép feldolgozása

Miután minden be van állítva, megkérjük a motort, hogy végezze el a varázslatát.

```java
// Step 4: Run OCR on the defined ROI
OcrResult ocrResult = ocrEngine.process();
```

A `process()` hívás egy `OcrResult` objektumot ad vissza, amely tartalmazza a kinyert szöveget, a megbízhatósági pontszámokat, sőt az egyes szavak körülhatároló dobozait is, ha később szükséged van rájuk.

## 5. lépés – Kinyert szöveg kiírása

Végül, írd ki az eredményt. Egy valódi alkalmazásban adatbázisba mentheted vagy egy másik szolgáltatásnak továbbíthatod, de ehhez a tutorialhoz a konzolra írás elegendő.

```java
// Step 5: Display the recognized text
System.out.println("ROI text:");
System.out.println(ocrResult.getText());
```

**Várható kimenet** (feltételezve, hogy a téglalap a nyugta összegét fogta el):

```
ROI text:
$12.34
```

Ha a ROI üres vagy a kép elmosódott, üres karakterláncot vagy torz karaktereket látsz. Állítsd be a téglalapot, javítsd a kép minőségét, vagy engedélyezd az Aspose előfeldolgozási beállításait (pl. `setAutoSkewCorrection(true)`).

## Teljes működő példa

Az alábbiakban a teljes, futtatható program található. Másold be egy `RoiDemo.java` nevű fájlba, állítsd be a képfájlt, és futtasd a `javac RoiDemo.java && java RoiDemo` parancsot.

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

/**
 * Demo: Extract text from a specific rectangle (ROI) in an image using Aspose OCR.
 * Adjust the rectangle coordinates to match the area you want to read.
 */
public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.jpg"));

        // Step 3: Define the region of interest where text is expected
        // (x, y, width, height) in pixels
        Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
        ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);

        // Optional sanity check – ensures ROI fits inside the image
        if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
            regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
            throw new IllegalArgumentException("ROI exceeds image dimensions.");
        }

        // Step 4: Perform OCR on the defined ROI
        OcrResult ocrResult = ocrEngine.process();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **Eredmény ellenőrzése:** A futtatás után hasonlítsd össze a konzol kimenetét a téglalapban lévő tényleges szöveggel. Ha egyeznek, sikeresen **extract text from image**‑t hajtottál végre az Aspose OCR‑rel.

## Gyakori kérdések és tippek

### Mit tegyek, ha több ROI‑t kell feldolgozni ugyanabban a képen?

Hozz létre egy új `Rectangle`‑t minden területhez, hívd meg újra a `setRegionOfInterest`‑t, és futtasd újra a `process()`‑t. A motor újrahasználja ugyanazt a képadatot, így a teljesítmény gyors marad.

### Hogyan kezeli az Aspose a különböző nyelveket vagy betűtípusokat?

A nyelvi modellt a `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.English)` segítségével válthatod. Nem latin írásrendszerekhez töltsd be a megfelelő nyelvi csomagot (az Aspose letöltési oldalán elérhető).

### Támogatja a könyvtár a PDF bemenetet?

Igen — az Aspose OCR közvetlenül PDF áramlásokat is elfogad. Csak cseréld le az `ImageStream.fromFile`‑t `ImageStream.fromPdfFile("doc.pdf")`‑ra, és opcionálisan add meg az oldalszámot.

### Javítható a pontosság alacsony minőségű beolvasásoknál?

Engedélyezd az előfeldolgozást:

```java
ocrEngine.getEngineOptions().setAutoSkewCorrection(true);
ocrEngine.getEngineOptions().setBinarizationMethod(BinarizationMethod.Otsu);
```

## Összegzés

Most végigmentünk egy teljes **aspose ocr tutorial**‑on, amely bemutatja, hogyan **extract text from image**, **load image for OCR**, és **read text from rectangle** Java‑val. A kulcsfontosságú lépések a motor inicializálása, kép betáplálása, egy érdeklődési terület (ROI) meghatározása, feldolgozás, és végül az eredmény kiírása.

Innen tovább felfedezheted:

* **Batch processing** — egy mappában lévő nyugtákat ciklusba véve feldolgozni, és minden összeget adatbázisba menteni.  
* **Dynamic ROI detection** — képfeldolgozó könyvtárak (OpenCV) használata a szövegdobozok automatikus megtalálásához.  
* **Post‑processing** — regex vagy fuzzy matching alkalmazása az OCR hibák tisztításához.

Próbáld ki ezeket az ötleteket, állítsd be a téglalapot a saját dokumentumaidhoz, és hamarosan egy robusztus szövegkinyerő csővezetéked lesz. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}