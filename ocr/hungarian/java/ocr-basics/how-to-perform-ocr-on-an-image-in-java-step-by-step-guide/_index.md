---
category: general
date: 2026-11-17
description: Tanulja meg, hogyan végezhet OCR-t egy képen Java-ban, és hogyan nyerhet
  ki szöveget a képekből egy egyszerű kódpélda segítségével. Tartalmazza a képek beolvasására
  vonatkozó Java tippeket.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: hu
lastmod: 2026-11-17
og_description: Hogyan hajtsunk végre OCR-t egy képen Java-ban, és gyorsan nyerjünk
  ki szöveget. Kövesd ezt az útmutatót, hogy Java-val olvass képet, és képet szöveggé
  alakíts egy azonnal futtatható példával.
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: Hogyan végezzünk OCR-t egy képen Java-ban – lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: Hogyan végezzünk OCR-t egy képen Java-ban – lépésről lépésre útmutató
url: /hu/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk OCR-t egy képen Java‑ban – lépésről‑lépésre útmutató

Ha **hogyan végezzünk OCR‑t** egy képen, ez a bemutató egy teljes, futtatható megoldást mutat be Java‑ban. Megmutatjuk, hogyan olvassunk be egy képfájlt, konfiguráljuk az OCR‑motort, és hogyan nyerjük ki a motor által felismert szöveget.

Beolvasott dokumentumokkal, nyugtákkal vagy képernyőképekkel gyakran szükség van a vizuális tartalom kereshető szöveggé alakítására. Ez az útmutató minden lépésen végigvezet, a kép betöltésétől a kinyert szöveg kiírásáig, és kitér a gyakori buktatókra, például a nem támogatott fájlformátumokra és a null eredményekre.

## Előfeltételek

Mielőtt elkezdené, győződjön meg róla, hogy rendelkezik:

* Java Development Kit (JDK) 8 vagy újabb verzióval.
* Egy build eszközzel (Maven vagy Gradle), amely letölti az OCR könyvtárat.
* Egy képfájllal (JPEG, PNG, BMP), amelyet feldolgozni szeretne.

A kód a **OCR library from the `com.asprise.ocr` package**‑t használja, mert csak egyetlen JAR‑ra van szüksége, és minden főbb platformon működik. Másik szolgáltatóval (Tesseract, Google Vision, stb.) helyettesíthető az importálási utasítások és a motor‑inicializációs kód cseréjével.

## 1. lépés: Az OCR függőség hozzáadása

Ha Maven‑t használ, adja hozzá a következő függőséget a `pom.xml`‑hez:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

Gradle‑hez helyezze ezt a sort a `build.gradle`‑ba:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

Ezek a sorok biztosítják, hogy a **read image Java** kód leforduljon, és az OCR motor elérhető legyen futás közben.

## 2. lépés: Kép beolvasása Java‑val

Egy képfájl beolvasása az első konkrét lépés minden **extract text image** munkafolyamatban. A Java beépített `ImageIO` osztálya a legtöbb általános formátumot kezeli.

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**Miért fontos:** Az `ImageIO.read` `null`‑t ad vissza nem támogatott formátumok vagy sérült fájlok esetén. A fenti metódus naplózza a problémát, és `null`‑t ad vissza, így a következő lépés megfelelően reagálhat.

## 3. lépés: OCR motor létrehozása és konfigurálása

Az OCR motornak tudnia kell, melyik nyelvet kell felismertie. A nyelv beállítása drámaian javítja a pontosságot, különösen nem‑angol dokumentumok esetén.

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**Miért fontos:** A motor elindítása viszonylag nehéz művelet, ezért érdemes egyszer létrehozni, és több kép esetén újrahasználni, ha az alkalmazás kötegelt feldolgozást végez.

## 4. lépés: OCR végrehajtása és a kép szöveggé konvertálása

Miután a kép betöltődött és a motor készen áll, futtathatja a felismerési lépést. Ez a **how to perform OCR** magja.

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**Szélsőséges esetek kezelése:** Ha a kép `null`, a metódus üres karakterláncot ad vissza ahelyett, hogy `NullPointerException`‑t dobna. Ez a környező kódot robusztusabbá teszi a felhasználó által biztosított fájlok kezelésekor.

## 5. lépés: A kinyert szöveg megjelenítése

Végül írja ki az eredményt a konzolra, vagy továbbítsa egy másik komponensnek (pl. adatbázis vagy UI widget).

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

Ha a programot a `java OcrDemo sample.jpg` paranccsal futtatja, a konzol a felismert karaktereket jeleníti meg. Ezzel befejeződik a **convert image to text** ciklus.

### Várt kimenet

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

Ha a képen nincs olvasható karakter, a program a `(no text detected)` üzenetet írja ki.

## Gyakori variációk és azok adaptálása

| Variáció | Mi változik | Mikor használjuk |
|-----------|--------------|-------------|
| **Másik nyelv** | Cserélje a `"eng"`‑t `"spa"`‑ra spanyol, `"fra"`‑ra francia stb. | Angolon kívül más nyelven írt dokumentumok |
| **Kötegelt feldolgozás** | Iteráljon egy fájlútvonal‑listán, használja újra ugyanazt az `Ocr` példányt. | Nagy mennyiségű beolvasott oldal |
| **Magasabb pontosság** | Használja az `Ocr.SPEED_SLOW`‑t vagy engedélyezze az `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")`‑t csak numerikus beolvasásokhoz. | Ha az OCR minősége kritikus (pl. számlaszámok) |
| **Tesseract alternatíva** | Cserélje az importot `net.sourceforge.tess4j.Tesseract`‑ra, és módosítsa az inicializációs kódot. | Olyan projektek, amelyek már Tesseract‑ra támaszkodnak |

## Profi tippek

* **Nagy képek átméretezése** a motorba való betáplálás előtt; az OCR sebessége a pixel számával arányosan nő.
* **Előfeldolgozás** a képen (szürkeárnyalatos, kontraszt növelés) OpenCV‑szerű könyvtárakkal, ha a forrás zajos.
* **Az OCR motor cache‑elése**, ha rövid időn belül sokszor hívja – a motor indítása és leállítása jelentős overhead‑et jelent.
* **Az eredmény validálása** reguláris kifejezésekkel, ha konkrét formátumot vár (pl. dátumok, telefonszámok).

## Összegzés

Most már tudja, **hogyan végezzünk OCR‑t** egy képen Java‑ban, a fájl beolvasásától a kinyert szöveg megjelenítéséig. A bemutató lefedte a **read image Java**, **extract text image**, **convert image to text**, és **image to text java** technikákat, valamint gyakorlati tippeket adott valós helyzetekhez.  

Innen tovább:

* Integrálja az OCR lépést egy webszolgáltatásba, amely feltöltéseket fogad.
* Kombinálja a kimenetet egy keresőindexszel a beolvasott dokumentumok teljes‑szöveges kereséséhez.
* Fedezze fel a fejlett OCR lehetőségeket, például a többnyelvű támogatást vagy egyedi karakterkészleteket.

Boldog kódolást, és élvezze a képek kereshető szöveggé alakítását!


## Mit érdemes még megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [How to Use OCR in Java – Extract Text from Image with Spell Correction](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Convert Image to Text in Java Using Aspose OCR – Full Guide](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [How to Enable GPU for OCR in Java – Extract Text from Image](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}