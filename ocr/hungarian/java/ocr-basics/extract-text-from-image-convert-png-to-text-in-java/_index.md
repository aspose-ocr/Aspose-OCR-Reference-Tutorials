---
category: general
date: 2026-02-19
description: Képről szöveg kinyerése Aspose OCR Java használatával – tanulja meg,
  hogyan konvertáljon PNG-t szöveggé, hogyan töltse be a képet OCR-hez, és kövesse
  a Java OCR útmutatót.
draft: false
keywords:
- extract text from image
- convert png to text
- load image for ocr
- java ocr tutorial
- Aspose OCR Java
- OCR language support
language: hu
og_description: Szöveg kinyerése képből az Aspose OCR Java-val. Kövesd ezt a lépésről‑lépésre
  Java OCR útmutatót a PNG szöveggé konvertálásához és a kép betöltéséhez az OCR-hez.
og_title: szöveg kinyerése képből – Java OCR útmutató
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Képből szöveg kinyerése – PNG konvertálása szöveggé Java-ban
url: /hu/java/ocr-basics/extract-text-from-image-convert-png-to-text-in-java/
---

vonalat; használd a `Paths.get(...).toAbsolutePath()`-t. |

Make sure alignment with dashes.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# szöveg kinyerése képből – Java OCR útmutató

Valaha is szükséged volt **szöveg kinyerése képből**, de nem tudtad, melyik könyvtár teszi ezt meg egyszerűen? Nem vagy egyedül – a fejlesztők gyakran kérdezik: „Hogyan konvertálhatok PNG-t szöveggé Java-ban?” A jó hír, hogy az Aspose OCR a teljes folyamatot olyan egyszerűvé teszi, mint egy séta a parkban. Ebben az útmutatóban végigvezetünk egy teljes **java ocr tutorial**-on, megmutatjuk, hogyan **load image for OCR**, és végül tiszta, kereshető szöveget kapunk.

Mindent lefedünk a motor beállításától a többnyelvű tartalom kezeléséig, így a végére képes leszel **szöveg kinyerése képből** fájlokból bármilyen méretben, formátumban vagy nyelven. Nincsenek külső szolgáltatások, nincs API kulcs – csak egyetlen JAR és néhány kódsor.

## Amire szükséged lesz

- JDK 8 vagy újabb telepítve (a kód JDK 11+‑on is működik).  
- Maven vagy Gradle az Aspose OCR könyvtár letöltéséhez, vagy manuálisan letöltheted a JAR‑t az Aspose weboldaláról.  
- Egy PNG kép, amely olvasható szöveget tartalmaz (példánkhoz a `khmer-sign.png` fájlt használjuk).  
- Egy IDE vagy szövegszerkesztő, amiben kényelmesen dolgozol – IntelliJ IDEA, Eclipse, VS Code, bármelyik megfelel.

Ennyi. Nincsenek nehéz keretrendszerek, nincs felhő hitelesítő adat. Készen állsz? Kezdjünk el **szöveg kinyerése képből** fájlokból.

## 1. lépés: Aspose OCR hozzáadása a projekthez

Először is – szükséged van az OCR motorra a classpath‑on. Ha Maven‑t használsz, add ezt a függőséget a `pom.xml`-hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check the latest version on Maven Central -->
</dependency>
```

Vagy Gradle‑lel:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

Ha a manuális megoldást részesíted előnyben, töltsd le a JAR‑t az Aspose letöltési oldaláról, helyezd a projekt `libs` mappájába, majd add hozzá a build útvonalhoz.

> **Pro tip:** Mindig a legújabb stabil verziót válaszd; a régebbi kiadások hiányozhatnak nyelvi csomagok vagy hibajavítások.

## 2. lépés: OCR motor példány létrehozása

Most, hogy a könyvtár elérhető, elindíthatunk egy `OcrEngine` példányt. Tekintsd a motort az agynak, amely a pixeleket karakterekké alakítja.

```java
import com.aspose.ocr.*;

public class ExtractTextExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        // ... further steps will follow
    }
}
```

Miért hozunk létre minden alkalommal egy új motort? A motor belső puffereket és nyelvi adatokat tárol; a tiszta indulás garantálja a determinisztikus eredményeket, különösen, ha később nyelveket váltasz.

## 3. lépés: A kívánt nyelv engedélyezése (opcionális, de ajánlott)

Az Aspose OCR több tucat nyelvi csomaggal érkezik. Ha ismered a forráskép nyelvét, engedélyezd azt kifejezetten; ez felgyorsítja a felismerést és javítja a pontosságot. A példánkban a Khmer (`khm`) nyelvet engedélyezzük, de helyettesítheted `ENG`-gel az angolhoz, `CHN`-nel a kínaihoz stb.

```java
// Enable Khmer language support (ISO 639‑2 code "khm")
ocrEngine.getLanguages().add(OcrLanguage.KHM);
```

> **Miért fontos:** Amikor **load image for OCR**, a motor csak a engedélyezett nyelvi szótárakban keres. Ha minden nyelvet bekapcsolod, az lelassíthatja a folyamatot és növelheti a hamis pozitív eredményeket.

## 4. lépés: Kép betöltése OCR‑hez – PNG konvertálása szöveggé

Itt történik a **load image for OCR** lépés. Az Aspose egy kényelmes `ImageStream.fromFile` segédfüggvényt biztosít, amely elrejti az alacsony szintű I/O‑t.

```java
// Load the PNG that contains the text you want to extract
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/khmer-sign.png"));
```

Ha a képed más formátumban van (JPEG, BMP, TIFF), ugyanaz a metódus működik – az Aspose automatikusan felismeri a formátumot. Csak győződj meg róla, hogy a fájl útvonala helyes; különben `FileNotFoundException`-t kapsz.

## 5. lépés: OCR folyamat futtatása és PNG konvertálása szöveggé

A motor készen áll és a kép betöltve, a tényleges felismerés egyetlen metódushívás. Az eredményobjektum a nyers karakterláncot és a megbízhatósági pontszámokat adja.

```java
// Run OCR and fetch the recognized text
String recognizedText = ocrEngine.recognize().getText();
```

Ennyi – most már **convert PNG to text**. A visszakapott karakterlánc tartalmazhat sortöréseket és szóközöket pontosan úgy, ahogy a motor látta. Utófeldolgozhatod `trim()`, `replaceAll("\\s+", " ")` vagy bármilyen más tisztítással.

## 6. lépés: Eredmény kiírása (vagy tárolása)

Gyors ellenőrzésként írd ki az eredményt a konzolra. Egy valódi alkalmazásban valószínűleg fájlba, adatbázisba írnád, vagy egy másik szolgáltatásnak adnád át.

```java
System.out.println("Recognized text:");
System.out.println(recognizedText);
```

**Várható kimenet** (a megadott Khmer jelhez) valahogy így nézhet ki:

```
សួស្តី
Welcome
```

Ha a kimenet összezavarodott, ellenőrizd újra, hogy a 3. lépésben a megfelelő nyelvet engedélyezted-e, és hogy a kép nem túl homályos. A kép felbontásának növelése (például 300 dpi-s beolvasás) gyakran segít.

## Teljes működő példa

Az összes részt összeállítva, itt egy önálló program, amelyet bemásolhatsz a `ExtractTextExample.java` fájlba és futtathatsz:

```java
import com.aspose.ocr.*;

public class ExtractTextExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable the language you need (Khmer in this case)
        ocrEngine.getLanguages().add(OcrLanguage.KHM);

        // 3️⃣ Load the PNG image you want to extract text from
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/khmer-sign.png"));

        // 4️⃣ Run OCR – this step actually converts PNG to text
        String recognizedText = ocrEngine.recognize().getText();

        // 5️⃣ Show the result
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

Futtasd a programot a következővel:

```bash
mvn compile exec:java -Dexec.mainClass=ExtractTextExample
```

vagy, ha Gradle‑t használsz:

```bash
./gradlew run --args='ExtractTextExample'
```

A konzolon meg kell jelennie a kinyert szövegnek, ami megerősíti, hogy sikeresen **extract text from image** használtad az Aspose OCR‑rel.

## Gyakori buktatók és megoldások

| Tünet | Valószínű ok | Megoldás |
|-------|--------------|----------|
| Üres karakterlánc visszakapva | Nincs engedélyezett nyelv vagy helytelen nyelvkód | Add hozzá a megfelelő `OcrLanguage`-t (pl. `ENG` az angolhoz). |
| Torzuló karakterek | A kép felbontása túl alacsony vagy zajos háttér | Használj magasabb felbontású forrást, vagy előfeldolgozd élesítő szűrővel. |
| `OutOfMemoryError` | Nagyon nagy kép betöltve teljes méretben | Méretezd le a képet, mielőtt a motorba adod (`ImageStream.fromFile(...).scale(0.5)`). |
| `FileNotFoundException` | Helytelen útvonal | Ellenőrizd a abszolút vagy relatív útvonalat; használd a `Paths.get(...).toAbsolutePath()`-t. |

> **Ne feledd:** Az OCR egy valószínűségi folyamat. Még tökéletes beállítások mellett is előfordulhat, hogy manuálisan kell korrigálni néhány karaktert, különösen a dőlt írásmódoknál.

## A tutorial bővítése – Következő lépések

- **Batch processing:** Ciklus egy PNG fájlok könyvtárán, minden képre ugyanazt a logikát alkalmazva.  
- **PDF output:** Használd az Aspose PDF-et, hogy a kinyert szöveget visszaágyazd egy kereshető PDF-be.  
- **Language detection:** Hívd meg a `ocrEngine.detectLanguage()`-t a nyelv beállítása előtt, hogy a motor automatikusan kitalálja.  
- **Cloud integration:** Ha skálázni kell, csomagold a kódot egy REST végpontra, és hagyd, hogy a mikro‑szolgáltatások hívják.

Mindezek a témák természetesen a most befejezett **java ocr tutorial**-ra épülnek, és bemutatják, mennyire sokoldalú az Aspose OCR API.

## Összegzés

Átmentünk egy teljes **java ocr tutorial**-on, amely lehetővé teszi, hogy **szöveg kinyerése képből** fájlokból, **convert PNG to text**, és helyesen **load image for OCR** az Aspose OCR segítségével. A lépések egyszerűek: add a könyvtárat, create an engine, enable a megfelelő nyelvet, load a PNG-t, futtasd a `recognize()`-t, és kezeld a kimenetet. Ezzel az alapokkal automatizálhatod az adatbevitelt, építhetsz kereshető archívumokat, vagy bármilyen alkalmazást, amelynek gép‑olvasható szövegre van szüksége képekből.

Próbáld ki a saját képeiddel – legyen az egy nyugta képernyőképe vagy egy beolvasott szerződés. Finomítsd a nyelvi beállításokat, kísérletezz a felbontással, és hamar rájössz, mennyire rugalmas a megoldás. Ha problémába ütközöl, nézd át újra a buktatók táblázatát vagy ellenőrizd az Aspose hivatalos dokumentációját; az alapos és naprakész.

Boldog kódolást, és legyen a következő projekted tele tiszta, kereshető szöveggel!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}