---
category: general
date: 2026-04-26
description: Készíts kereshető PDF-et egy képből az Aspose OCR Java használatával.
  Tanulja meg, hogyan konvertáljon képet PDF-be, OCR-rel alakítsa a képet PDF-be,
  és gyorsan nyerjen ki szöveget a képből.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- extract text from image
- how to set language
language: hu
og_description: Készítsen kereshető PDF-et egy képből az Aspose OCR segítségével.
  Ez az útmutató bemutatja, hogyan konvertálhatja a képet PDF‑be, hogyan OCR‑zhatja
  a képet PDF‑be, és hogyan nyerhet ki szöveget a képből.
og_title: Kereshető PDF létrehozása képből Java OCR segítségével
tags:
- Java
- OCR
- PDF
title: Kereshető PDF létrehozása képből Java OCR-rel
url: /hu/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása képből Java OCR-rel

Valaha szükséged volt **kereshető PDF** létrehozására egy beolvasott számlából, de nem tudtad, hol kezdjed? Nem vagy egyedül – sok fejlesztő szembesül ezzel a problémával, amikor olyan PDF-et szeretne, amelyben tényleg keresni lehet. A jó hír? Az Aspose OCR for Java-val **képet PDF‑re konvertálhatsz**, futtathatsz OCR-t menet közben, és néhány kódsorral egy rendezett kereshető fájlt kapsz.

Ebben az útmutatóban végigvezetünk a teljes folyamaton: kép betöltése, a motor tájékoztatása a várt nyelvről, OCR végrehajtása, és végül egy **kereshető PDF** mentése. A végére megtanulod, hogyan **extract text from image** manuálisan, hogyan állíthatod be a nyelvet, és hogyan kezelhetsz néhány gyakori edge case‑et. Nincs külső szolgáltatás, nincs rejtélyes parancssori eszköz – csak tiszta Java.

## Amire szükséged lesz

- Java 17 vagy újabb (az API régebbi kiadásokkal is működik, de a 17 a legoptimálisabb).  
- Aspose OCR for Java könyvtár – a legújabb JAR‑t a Maven Central‑ból szerezheted be (`com.aspose:aspose-ocr:23.10`).  
- Egy képfájl, amely olvasható szöveget tartalmaz (PNG, JPG vagy TIFF megfelelő).  
- Egy kis adag IDE‑türelem – az IntelliJ IDEA vagy a VS Code megfelel.

Ha már megvannak ezek, nagyszerű! Ha nem, az alábbi Maven‑kódrészlet elindít:

```xml
<!-- Add to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Most, hogy az alapok megvannak, merüljünk el a kódban.

## 1. lépés: Az OCR motor inicializálása – a **create searchable pdf** szíve

Mielőtt bármilyen konverzió megtörténne, létre kell hoznod egy `OcrEngine` példányt. Gondolj rá úgy, mint egy agyra, amely a pixeleket karakterekké alakítja.

```java
import com.aspose.ocr.*;

public class PdfExportDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

*Why this matters:* A motor tárolja az összes felismerési beállítást (nyelv, pontossági mód stb.). Egyszeri példányosítása és többszöri újrahasználata több képnél hatékonyabb, mint minden fájlhoz új motor létrehozása.

## 2. lépés: **How to set language** – a pontosság javítása francia, német vagy bármely írásrendszer esetén

Ha ismered a forrásdokumentum nyelvét, add meg az OCR motor számára. Ez felgyorsítja a feldolgozást és csökkenti a hibás felismeréseket.

```java
        // Step 2: (Optional) Specify the language to improve text extraction
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

A `OcrLanguage.FRENCH` helyett használhatod az `ENGLISH`, `SPANISH`, `GERMAN` stb. értékeket. Ha nem vagy biztos, hagyd ki a sort, és hagyd, hogy az Aspose kitalálja – de számíts egy kis pontosságcsökkenésre.

## 3. lépés: Töltsd be a képet, amelyet **convert image to pdf** szeretnél

A `setImage` metódus elfogad fájlútvonalat, `InputStream`‑et vagy akár egy `java.awt.Image` objektumot is. Ha byte‑tömböd van (például egy webes feltöltésből), csomagold be egy `ByteArrayInputStream`‑be, és add át közvetlenül.

```java
        // Step 3: Load the image that contains the text to be recognized
        ocrEngine.setImage("YOUR_DIRECTORY/french_invoice.png");
```

## 4. lépés: OCR végrehajtása és **ocr image to pdf** egy hívásban

Az Aspose ezt a lépést könnyűvé teszi: a `recognizeToPdf` lefuttatja a felismerő motort és egy lépésben egy kereshető PDF‑et ír ki.

```java
        // Step 4: Recognize the text and save it as a searchable PDF
        ocrEngine.recognizeToPdf("YOUR_DIRECTORY/french_invoice_searchable.pdf");
```

A háttérben a könyvtár egy láthatatlan szövegréteget hoz létre, amely az eredeti képpel igazodik. Amikor megnyitod a kész fájlt az Adobe Readerben, beírhatsz egy szót a keresőmezőbe, és azonnal a megfelelő helyre ugrik.

## 5. lépés: Az eredmény ellenőrzése – hogyan néz ki a kimenet?

```java
        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF generated.");
    }
}
```

Futtasd a programot, majd nyisd meg a `french_invoice_searchable.pdf`‑t. Próbálj meg keresni egy olyan szót, amely biztosan szerepel a számlán (pl. „Total”). Ha a kiemelés a megfelelő helyen jelenik meg, sikeresen **create searchable pdf**‑t hoztál létre.  
![Create searchable PDF example](example.png)<!-- alt text includes primary keyword -->

### Várható kimenet

```
Searchable PDF generated.
```

És egy PDF‑fájl a `YOUR_DIRECTORY`‑ben, amelyet megoszthatsz, indexelhetsz vagy archiválhatsz.

## 6. lépés: Nyers szöveg kinyerése a képből (opcionális)

Néha a tiszta szövegre van szükség további feldolgozáshoz – például adatbázisba való betöltéshez vagy érzelemelemzéshez. Az Aspose lehetővé teszi a felismert szöveg közvetlen lekérését:

```java
        // Optional: Get the extracted text as a String
        String extractedText = ocrEngine.getText();
        System.out.println("Extracted text:");
        System.out.println(extractedText);
```

Ez a kódrészlet bemutatja a **extract text from image** műveletet PDF létrehozása nélkül. Hasznos, ha csak a tartalom érdekel, nem a vizuális elrendezés.

## Több oldal vagy kép kezelése

Mi van, ha a forrás egy többoldalas TIFF vagy JPEG‑ek mappája? Végig iterálhatsz a fájlokon, meghívhatod a `recognizeToPdf`‑et minden egyesre, majd összeolvashatod a PDF‑eket az Aspose PDF‑vel vagy bármely más könyvtárral. Íme egy gyors minta:

```java
import java.io.File;
import com.aspose.pdf.*;

public class MultiPageDemo {
    public static void main(String[] args) throws Exception {
        OcrEngine engine = new OcrEngine();
        File folder = new File("YOUR_DIRECTORY/images");
        Document finalDoc = new Document();

        for (File img : folder.listFiles((d, n) -> n.matches(".*\\.(png|jpg|tif)"))) {
            engine.setImage(img.getAbsolutePath());
            // Save each page as a temporary PDF
            String tempPdf = img.getName() + ".pdf";
            engine.recognizeToPdf(tempPdf);
            // Append to final document
            Document pageDoc = new Document(tempPdf);
            finalDoc.getPages().add(pageDoc.getPages().get_Item(1));
        }
        finalDoc.save("YOUR_DIRECTORY/combined_searchable.pdf");
        System.out.println("All pages merged into searchable PDF.");
    }
}
```

**Pro tip:** A merge után töröld a temporális PDF‑eket, hogy a munkaterület tiszta maradjon.

## Gyakori buktatók és hogyan kerüld el őket

- **Low‑resolution images:** Az OCR pontossága drámaian csökken 150 dpi alatt. Ha lehetséges, növeld a felbontást vagy kérj nagyobb felbontású beolvasást.  
- **Skewed pages:** Egy elforgatott kép összezavarhatja a motort. Használd a `ocrEngine.getImagePreprocessingSettings().setDeskew(true)`‑t a enyhe ferdeség automatikus korrigálásához.  
- **Unsupported language:** Győződj meg róla, hogy a beállított nyelv szerepel az Aspose OCR licencben; különben a motor visszaesik angolra.  
- **Large files:** Egy 30 MB-os TIFF feldolgozása memóriaigényes lehet. Fontold meg a fájl kisebb darabokra bontását vagy a JVM heap növelését (`-Xmx2g`).

## Következő lépések – merre tovább

Most, hogy elsajátítottad a **create searchable pdf** alapjait, érdemes lehet:

- **Batch conversion:** Kombináld a többoldalas mintát egy ütemezővel, hogy éjszakánként feldolgozza a bejövő beolvasásokat.  
- **Metadata injection:** Használd az Aspose PDF‑t cím, szerző vagy egyedi címkék hozzáadásához a kereshető PDF‑hez.  
- **Digital signatures:** Az OCR után tanúsítvánnyal biztosítsd a PDF‑et, ezzel megfelelve a jogi dokumentumok előírásainak.  

Mindezek a kiterjesztések továbbra is az általunk lefedett alapfogalmakra épülnek: az OCR motor inicializálása, opcionális nyelvbeállítás, kép betöltése és a `recognizeToPdf` meghívása.

---

### TL;DR

Egy teljes, futtatható példán keresztül bemutattuk, hogyan **create searchable PDF** készíthető egy képből az Aspose OCR for Java használatával. A lépések: motor inicializálása, opcionális nyelv beállítása (a “how to set language” kérdésre válaszolva), kép betöltése, OCR végrehajtása, kereshető PDF mentése, és opcionálisan a tiszta szöveg kinyerése. Kitértünk többoldalas kezelést, gyakori buktatókat és ötleteket a további automatizáláshoz.

Próbáld ki saját nyugtáiddal, szerződéseiddel vagy kézírásos jegyzeteiddel – alakítsd át ezeket a statikus képeket teljesen kereshető dokumentumokká néhány másodperc alatt. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}