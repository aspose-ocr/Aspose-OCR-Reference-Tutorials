---
category: general
date: 2026-09-10
description: Végezzen OCR-t a képen az Aspose OCR Java használatával. Tanulja meg
  a szöveg felismerését JPEG-fájlból, a szöveg kinyerését a képről, és a kép hatékony
  szöveggé konvertálását.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- recognize text from JPEG
- extract text from image
- convert image to text
- load image for OCR
language: hu
lastmod: 2026-09-10
og_description: Képen OCR végrehajtása az Aspose OCR Java-val. Ez az útmutató bemutatja,
  hogyan ismerhet fel szöveget JPEG-ből, hogyan nyerhet ki szöveget a képből, és hogyan
  konvertálhatja a képet szöveggé néhány kódsorral.
og_image_alt: Screenshot of Java code that performs OCR on an image using Aspose OCR
og_title: Kép OCR-olása az Aspose OCR segítségével – Java útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  headline: How to perform OCR on image with Aspose OCR in Java
  type: TechArticle
- description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  name: How to perform OCR on image with Aspose OCR in Java
  steps:
  - name: Prerequisites
    text: '* Java Development Kit (JDK) 8 or later. * Maven or Gradle to manage dependencies
      (the example uses Maven). * A valid Aspose OCR for Java license (or a temporary
      evaluation key). * An image file named `sample.jpg` placed in a known directory.'
  - name: Load image for OCR
    text: '```java // Step 1: Load the image you want to process String imagePath
      = "YOUR_DIRECTORY/sample.jpg"; ImageStream imageStream = ImageStream.fromFile(imagePath);
      ```'
  - name: Create and configure the OCR engine
    text: '```java // Step 2: Create an OCR engine instance OcrEngine engine = new
      OcrEngine();'
  - name: Recognize text from JPEG
    text: '```java // Step 3: Attach the image to the engine engine.setImage(imageStream);'
  - name: Extract text from image and output
    text: '```java // Step 5: Output the recognized text System.out.println("=== Recognized
      Text ==="); System.out.println(result.getText()); ```'
  - name: Expected output
    text: 'Assuming `sample.jpg` contains the text “Hello World”, the console will
      display:'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: Hogyan hajtsunk végre OCR-t egy képen az Aspose OCR segítségével Java-ban
url: /hu/java/ocr-operations/how-to-perform-ocr-on-image-with-aspose-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk OCR-t képen az Aspose OCR-rel Java-ban

Ha **OCR-t szeretne végrehajtani képeken** Java alkalmazásban, ez az útmutató egy teljes, azonnal futtatható megoldást nyújt. Megmutatjuk, hogyan **ismerjen fel szöveget JPEG** fájlokból, **vonjon ki szöveget a képből**, és **alakítsa át a képet szöveggé** az Aspose OCR modern API-jának használatával.

Az oktatóanyag minden szükséges lépést végigvezet – a kép betöltésétől a felismert szöveg kiírásáig – így OCR-funkciót integrálhat anélkül, hogy további forrásokat kellene keresnie. Nincs szükség külső eszközökre az Aspose OCR for Java könyvtáron kívül.

## Mit fog elérni

* **Kép betöltése OCR-hez** közvetlenül a fájlrendszerből.  
* Az Aspose OCR előfeldolgozásának (pl. zajcsökkentés) engedélyezése a pontosság javítása érdekében.  
* **Szöveg felismerése JPEG**-ből és más raszteres formátumokból.  
* **Szöveg kinyerése a képből** és kiírása a konzolra.  
* Megérteni, hogyan **alakítsa át a képet szöveggé** egy termelésre kész kódmintában.

### Előfeltételek

* Java Development Kit (JDK) 8 vagy újabb.  
* Maven vagy Gradle a függőségek kezeléséhez (a példában Maven-t használunk).  
* Érvényes Aspose OCR for Java licenc (vagy ideiglenes értékelő kulcs).  
* Egy `sample.jpg` nevű képfájl, amely egy ismert könyvtárban található.

> **Pro tip:** Használjon nagy felbontású JPEG-eket (300 dpi vagy nagyobb) a legjobb felismerési arányokért.  

## 1. lépés: Aspose OCR hozzáadása a projekthez

Ha Maven-nel kezeli a függőségeket, illessze be a következő kódrészletet a `pom.xml` fájljába:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version>
</dependency>
```

Gradle esetén adja hozzá:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Ezek a koordináták a legújabb stabil Aspose OCR könyvtárat töltik le, amely tartalmazza a később használt előfeldolgozási funkciókat.

## OCR végrehajtása képen – lépésről‑lépésre

Az alábbi szakaszok bontják le a teljes programot. Minden blokk egy önálló egység, amelyet másolhat, beilleszthet és futtathat.

### Kép betöltése OCR-hez

```java
// Step 1: Load the image you want to process
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ImageStream imageStream = ImageStream.fromFile(imagePath);
```

*Miért fontos:*  
`ImageStream.fromFile` beolvassa a JPEG nyers bájtjait, és előkészíti őket az OCR motor számára. A metódus bármely, az Aspose OCR által támogatott raszteres formátummal működik, így a JPEG-et PNG-re vagy BMP-re cserélheti kómmódosítás nélkül.

### OCR motor létrehozása és konfigurálása

```java
// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();

// Enable preprocessing to improve accuracy (e.g., denoising)
engine.getPreprocessing().setDenoise(true);
```

*Miért fontos:*  
Az `OcrEngine` példányosítása lefoglalja a magfelismerő motort. A **denoise** (zajcsökkentés) kapcsoló engedélyezése eltávolítja a vizuális zajt, amely gyakran zavarja a karakterek felismerését, különösen a beolvasott JPEG-ek esetén.

### Szöveg felismerése JPEG-ből

```java
// Step 3: Attach the image to the engine
engine.setImage(imageStream);

// Step 4: Perform OCR recognition
OcrResult result = engine.recognize();
```

*Miért fontos:*  
`engine.setImage` a képadatokat az OCR csővezetékhez köti. `engine.recognize()` lefuttatja a teljes felismerési folyamatot, és egy `OcrResult` objektumot ad vissza, amely a kinyert szöveget és a biztonsági metrikákat tartalmazza.

### Szöveg kinyerése a képből és kiírása

```java
// Step 5: Output the recognized text
System.out.println("=== Recognized Text ===");
System.out.println(result.getText());
```

*Miért fontos:*  
`result.getText()` a kép tartalmának egyszerű szöveges ábrázolását adja vissza. A konzolra való kiírás bemutatja, hogy a **kép átalakítása szöveggé** sikeres volt, és ezt a karakterláncot fájlokba, adatbázisokba vagy további szolgáltatásokba is átirányíthatja.

## Teljes, futtatható példa

Az alábbiakban a teljes Java osztály látható, amely magában foglalja az összes lépést. Cserélje le a `YOUR_DIRECTORY`-t a JPEG fájl abszolút útvonalára.

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the image for OCR
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ImageStream imageStream = ImageStream.fromFile(imagePath);

        // Create and configure the OCR engine
        OcrEngine engine = new OcrEngine();
        engine.getPreprocessing().setDenoise(true); // improve accuracy

        // Attach the image and run recognition
        engine.setImage(imageStream);
        OcrResult result = engine.recognize();

        // Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Várható kimenet

Feltételezve, hogy a `sample.jpg` a “Hello World” szöveget tartalmazza, a konzol a következőt jeleníti meg:

```
=== Recognized Text ===
Hello World
```

Ha a kép több sort tartalmaz, minden sor külön sorban jelenik meg a kimeneten.

## Gyakori változatok és szélsőséges esetek

| Helyzet                                   | Ajánlott módosítás |
|-------------------------------------------|-------------------|
| **Alacsony felbontású JPEG** (≤150 dpi)   | Növelje a `engine.getPreprocessing().setUpsample(true);` értékét, hogy az Aspose feljavítsa a felbontást a felismerés előtt. |
| **Színes háttér** (pl. beolvasott űrlapok) | Engedélyezze a `engine.getPreprocessing().setBinarize(true);` beállítást, hogy a képet fekete‑fehérre konvertálja. |
| **Nem latin írásrendszer** (pl. cirill)  | Állítsa be a nyelvet: `engine.getLanguage().setLanguage(OcrLanguage.RUSSIAN);`. |
| **Nagy kötegelt feldolgozás**             | Használjon egyetlen `OcrEngine` példányt több kép feldolgozásához, hogy csökkentse az indítási költséget. |
| **Bizalmi pontszámok szükségesek**        | Használja a `result.getConfidence()` metódust az egyes karakterek bizalmi értékeinek lekéréséhez. |

Ezek a módosítások azt mutatják, hogyan **betölthet képet OCR-hez** különböző feltételek mellett, miközben továbbra is megbízhatóan **OCR-t végez képen**.

## Teljesítménybeli megfontolások

* **Memory usage:** Minden `ImageStream` a teljes képet a memóriában tartja. Nagyon nagy fájlok (pl. >10 MB) esetén fontolja meg a kép darabokban történő streamelését a `ImageStream.fromByteArray` használatával.  
* **Thread safety:** Az `OcrEngine` *nem* szálbiztos. Hozzon létre külön példányt szálanként, ha párhuzamos OCR-feladatokat tervez.  
* **License mode:** Az értékelő mód korlátozza az egy munkamenetben feldolgozható oldalak számát. Telepítsen licencelt verziót a termelési terhelésekhez.

## Összegzés

Most már tudja, hogyan **OCR-t végezzen képen** Java-ban az Aspose OCR használatával. Az útmutató lefedte a kép betöltését, az előfeldolgozás engedélyezését, a szöveg felismerését JPEG-ből, a szöveg kinyerését és a kép szöveggé alakítását – mindezt egyetlen, tömör programban.

Innen tovább felfedezheti a kapcsolódó témákat, például a **szöveg felismerése JPEG**-ből tömegesen, a kimenet integrálását egy keresőindexbe, vagy az OCR kombinálását természetes nyelvfeldolgozással intelligensebb dokumentumfolyamatokhoz. Kísérletezzen az előfeldolgozási beállításokkal, hogy a legjobb pontosságot érje el a saját képforrásaiban.

--- 

*OCR végrehajtása képen Java példával*  
![OCR végrehajtása képen Java példával](image-placeholder.png){alt="OCR végrehajtása képen Aspose OCR Java használatával"}

## Mi legyen a következő tanulnivaló?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API-funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [szöveg felismerése képen az Aspose OCR-rel – Teljes Java OCR útmutató](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Hogyan OCR-eljünk képszöveget nyelvvel az Aspose.OCR használatával](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Kép előfeldolgozása OCR-rel Java-ban az Aspose OCR-rel – Pontosság növelése és szöveg kinyerése](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}