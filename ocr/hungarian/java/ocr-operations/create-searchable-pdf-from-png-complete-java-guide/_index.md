---
category: general
date: 2026-01-07
description: Készíts kereshető PDF-et egy képből Java-ban. Tanulja meg, hogyan konvertáljon
  képet PDF-be, hogyan vonjon ki szöveget a képből, és hogyan ismerje fel a szöveget
  PNG-ből az Aspose OCR használatával.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- image to searchable pdf
- recognize text from png
language: hu
og_description: Kereshető PDF létrehozása Java-ban az Aspose OCR-rel. Ez az útmutató
  bemutatja, hogyan lehet képet PDF-be konvertálni, szöveget kinyerni a képből, és
  szöveget felismerni PNG-ből.
og_title: Kereshető PDF létrehozása PNG-ből – Java útmutató
tags:
- OCR
- Java
- PDF
title: Kereshető PDF létrehozása PNG-ből – Teljes Java útmutató
url: /hu/java/ocr-operations/create-searchable-pdf-from-png-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása PNG‑ből – Teljes Java útmutató

Szükséged volt már **kereshető pdf** létrehozására egy beolvasott képből, de nem tudtad, hol kezdj? Nem vagy egyedül – a fejlesztők gyakran ütköznek ebbe a falba a dokumentumkezelő folyamatok építése során. A jó hír? Néhány Java‑sorral és az Aspose OCR‑rel **convert image to pdf**, beágyazhatod a rejtett szöveget, és egy tökéletesen kereshető dokumentumot kapsz.

Ebben az útmutatóban végigvezetünk a teljes folyamaton: PNG betöltése, OCR futtatása, és az eredmény mentése kereshető PDF‑ként. A végére képes leszel **extract text from image** fájlokból, **image to searchable pdf** eszközöket létrehozni, és még olyan szélsőséges eseteket is kezelni, mint a többoldalas TIFF‑ek. Nincs külső szolgáltatás, csak tiszta Java kód, amit ma már futtathatsz.

## Kereshető PDF létrehozása – Áttekintés

Mielőtt a kódba merülnénk, tisztázzuk, mit jelent a „searchable PDF”. Egy kereshető PDF két rétegből áll:

1. **Látható kép réteg** – az eredeti kép (a PNG, JPEG, stb.).
2. **Rejtett szövegréteg** – az OCR‑generált szöveg, amely a kép mögött helyezkedik el, és kereshetővé teszi a dokumentumot bármely PDF‑megjelenítőben.

Miért van szükség mindkettőre? A kép megőrzi az eredeti megjelenést, míg a szövegréteg lehetővé teszi a másolást, indexelést és a teljes szöveges keresést. Ez a tökéletes megoldás archiváláshoz, jogi megfeleléshez és kereshető archívumok építéséhez.

## 1. lépés: Aspose OCR beállítása a Java projektben

Először is – szükséged van az Aspose OCR könyvtárra. A legegyszerűbb módja, ha hozzáadod a Maven függőséget:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Ha nem Maven‑t használsz, töltsd le a JAR‑t az Aspose weboldaláról, és add hozzá a classpath‑hoz. **Pro tip:** tartsd a könyvtár verzióját összhangban a Java futtatókörnyezeteddel (Java 8+ tökéletesen működik).

### Miért fontos ez
Az Aspose OCR számos képformátumot és nyelvet támogat „out‑of‑the‑box”, így nem kell saját pixel‑feldolgozó kódot írnod. Emellett biztosítja a `OcrOutputFormat.PDF` enum‑t, amelyet később a kereshető PDF létrehozásához használunk.

## 2. lépés: Töltsd be a feldolgozni kívánt képet

Ezután meg kell mondanunk az OCR motornak, melyik fájlt olvassa be. Az API egy `ImageStream`‑et fogad, amely létrehozható fájlútvonalból, `java.io.InputStream`‑ből vagy akár byte‑tömbből.

```java
import com.aspose.ocr.*;

public class PdfOutputExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG (or any supported image) from disk
        String inputPath = "YOUR_DIRECTORY/input.png"; // replace with your actual path
        ocrEngine.setImage(ImageStream.fromFile(inputPath));
```

Figyeld meg, hogy `ImageStream.fromFile`‑t használunk. Ha valaha **convert image to pdf**-t kell végrehajtanod egy stream‑ből (például egy feltöltött fájlból), cseréld le ezt a hívást `ImageStream.fromInputStream(yourInputStream)`‑re.

### Edge case figyelmeztetés
Ha a képed nagyobb, mint 10 MB, először méretezd le. A nagy képek drámaian megnövelik az OCR időt, és memóriahiányhoz vezethetnek közepes szervereken.

## 3. lépés: OCR futtatása és az eredmény rögzítése

Most jön a varázslat. A `recognize()` hívás elindítja az OCR algoritmust, és egy `OcrResult` objektumot ad vissza, amely mind a felismert szöveget, mind a layout információkat tartalmazza.

```java
        // Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Optional: print extracted text to console (useful for debugging)
        System.out.println("Extracted Text:");
        System.out.println(ocrResult.getText());
```

Itt **extracting text from image**-t is végzünk, és kiírjuk a konzolra. Ez a lépés hasznos, ha csak a nyers szöveget szeretnéd PDF generálása nélkül. Ugyanezt az `ocrResult` objektumot később újra felhasználjuk a kereshető PDF létrehozásához.

### Miért kritikus ez a lépés
Az OCR motor nem csak karaktereket olvas, hanem megőrzi azok pozícióját is, ami lehetővé teszi a rejtett szövegréteg létrehozását a végső PDF‑ben. Ennek a lépésnek a kihagyása azt jelenti, hogy elveszítenéd a kereshetőséget.

## 4. lépés: Az eredmény mentése kereshető PDF‑ként

Végül elmondjuk az Aspose OCR‑nek, hogy PDF formátumban írja ki a kimenetet. A `save` metódus megkapja a célfájl nevét és egy `OcrOutputFormat` enum‑t.

```java
        // Save the OCR result as a searchable PDF (image + hidden text layer)
        String outputPath = "YOUR_DIRECTORY/output.pdf"; // replace with your desired output
        ocrResult.save(outputPath, OcrOutputFormat.PDF);

        System.out.println("Searchable PDF created at: " + outputPath);
    }
}
```

Amikor megnyitod az `output.pdf`‑et az Adobe Readerben vagy bármely modern PDF‑megjelenítőben, látni fogod az eredeti PNG‑t, de kereshetsz is bármely szó után, ami a képen megjelenik. Ez a **create searchable pdf** lényege.

### Lehetőségek, amikre szükséged lehet
- **Több oldal:** Ha többoldalas TIFF‑ed van, egyszerűen iterálj minden oldalon, hívd meg a `ocrEngine.setImage`‑t minden egyesre, és fűzd hozzá az eredményeket ugyanahhoz az `OcrResult`‑hez a mentés előtt.
- **Különböző nyelvek:** Használd a `ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);`‑t (vagy bármely támogatott nyelvet) a `recognize()` hívása előtt.
- **Egyedi DPI:** Homályos beolvasások esetén javíthatod a pontosságot a `ocrEngine.getImage().setResolution(300);` beállítással.

## 5. lépés: Az eredmény ellenőrzése (Mit várhatsz)

A program futása után ellenőrizd az `output.pdf` fájlt:

1. **Vizualizációs réteg:** A PDF pontosan azt a PNG‑t mutatja, amelyet megadtál.
2. **Szövegréteg:** Nyomd meg a `Ctrl+F`‑et (vagy Cmd+F‑et) és keress egy olyan szót, amely biztosan szerepel a képen. Azonnal megtalálja.
3. **Másolás‑beillesztés:** Jelölj ki egy bekezdést, másold be egy szövegszerkesztőbe – tiszta, kereshető szöveget kapsz.

Ha a keresés nem működik, ellenőrizd, hogy a kép nem túl alacsony felbontású, illetve hogy a megfelelő nyelv lett beállítva. Gyakran egy egyszerű DPI‑növelés megoldja a problémát.

## Gyakori kérdések és profi tippek

- **Szükségem van licencre?**  
  Az Aspose OCR próbaverzióban vízjelet helyez el. Termeléshez vásárolj licencet, és állítsd be a `License license = new License(); license.setLicense("Aspose.OCR.lic");` kóddal.

- **Létrehozhatok **convert image to pdf**-t OCR nélkül?**  
  Igen – használd a `OcrOutputFormat.PDF`‑t a `ocrEngine.setRecognizeText(false);` beállítással a `recognize()` előtt. Így egy egyszerű, csak képet tartalmazó PDF-et kapsz.

- **Mi van, ha csak a kinyert szöveget szeretném?**  
  Hagyd ki a `save` hívást, és használd az `ocrResult.getText()`‑t; írhatod egy `.txt` fájlba, vagy betáplálhatod egy keresőindexbe.

- **Teljesítmény tippek:**  
  Használd ugyanazt az `OcrEngine` példányt több képhez; ez csökkenti a inicializálási költséget.

## Teljes működő példa (egyben)

Az alábbiakban a komplett, azonnal futtatható Java program látható. Cseréld ki a helyőrző útvonalakat a saját könyvtáraidra, add hozzá a Maven függőséget, és már indulhat a munka.

```java
import com.aspose.ocr.*;

public class PdfOutputExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the image (PNG, JPG, TIFF, etc.)
        String inputPath = "YOUR_DIRECTORY/input.png"; // <-- change this
        ocrEngine.setImage(ImageStream.fromFile(inputPath));

        // 3️⃣ Run OCR to get text and layout
        OcrResult ocrResult = ocrEngine.recognize();

        // Optional: display extracted text in console
        System.out.println("Extracted Text:");
        System.out.println(ocrResult.getText());

        // 4️⃣ Save as searchable PDF (image + hidden text layer)
        String outputPath = "YOUR_DIRECTORY/output.pdf"; // <-- change this
        ocrResult.save(outputPath, OcrOutputFormat.PDF);

        System.out.println("Searchable PDF created at: " + outputPath);
    }
}
```

**Várható kimenet:**  
```
Extracted Text:
[...the plain text that was recognized from the PNG...]
Searchable PDF created at: YOUR_DIRECTORY/output.pdf
```

Nyisd meg az `output.pdf`‑et bármely PDF‑megjelenítőben, és keress egy szót a kinyert szövegből – ki kell jelölnie, ami azt igazolja, hogy sikeresen **create searchable pdf**‑t hoztál létre.

## Összegzés

Most megmutattuk, hogyan **create searchable pdf**-t készíthetsz PNG‑ből Java és Aspose OCR segítségével. A lépések egyszerűek: állítsd be a könyvtárat, töltsd be a képet, futtasd az OCR‑t, és mentsd el PDF‑ként. Útközben megtanultad, hogyan **convert image to pdf**, **extract text from image**, és még **recognize text from png** is, haladóbb forgatókönyvekhez.

Mi a következő? Próbáld meg egy köteg beolvasott számlát egy ciklusba betáplálni, tárold a rejtett szöveget egy adatbázisban a teljes szöveges kereséshez, vagy kísérletezz különböző nyelvekkel és kép‑előfeldolgozási technikákkal. Ugyanez a minta más formátumokra is működik – csak cseréld ki a bemeneti fájlt, és máris **image to searchable pdf**-t tudsz készíteni.

Van kérdésed vagy elakadtál? Írj egy megjegyzést alább, és jó kódolást kívánunk!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}