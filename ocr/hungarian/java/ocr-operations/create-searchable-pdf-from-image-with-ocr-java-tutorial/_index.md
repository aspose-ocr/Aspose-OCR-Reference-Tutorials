---
category: general
date: 2026-01-07
description: Készíts kereshető PDF-et egy képből az Aspose OCR Java használatával.
  Tanulja meg, hogyan konvertálhatja a képet PDF‑be, hogyan ismerheti fel a szöveget
  a képen, és hogyan generálhat PDF‑et JPG‑ből.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- how to use ocr
- generate pdf from jpg
language: hu
og_description: Kereshető PDF létrehozása képből Aspose OCR használatával Java-ban.
  Lépésről lépésre útmutató a kép PDF-re konvertálásához, a szöveg felismeréséhez
  a képen, és PDF generálásához JPG-ből.
og_title: Kereshető PDF létrehozása képből – Java OCR útmutató
tags:
- OCR
- Java
- PDF
- Aspose
title: Kereshető PDF létrehozása képből OCR-rel – Java útmutató
url: /hu/java/ocr-operations/create-searchable-pdf-from-image-with-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása képből OCR‑rel – Java oktatóanyag

Valaha is szükséged volt **kereshető PDF** létrehozására egy beolvasott képből, de nem tudtad, hol kezdjed? Nem vagy egyedül – sok fejlesztő ütközik ebben a problémában, amikor először próbálja meg egy JPEG‑et olyan PDF‑vé alakítani, amelyben tényleg kereshetsz.  

Ebben az útmutatóban egy teljes, futtatható példán keresztül mutatjuk be, hogyan **konvertálj képet PDF‑be**, **ismerd fel a szöveget a képről**, és végül **generálj PDF‑et JPG‑ből** az Aspose OCR for Java segítségével. Nincs homályos hivatkozás, csak olyan kód, amit ma be tudsz másolni, beilleszteni és futtatni.

## Amire szükséged lesz

Mielőtt belemerülnénk, győződj meg róla, hogy a következők telepítve vannak a gépeden:

* **Java 17** vagy újabb (az API bármely friss JDK‑val működik).  
* **Aspose.OCR for Java** könyvtár – a legújabb JAR‑t letöltheted a Maven Central‑ról vagy az Aspose weboldaláról.  
* Egy minta kép, például `sample.jpg`, egy olyan mappában, amelyre hivatkozhatsz.  
* Egy IDE vagy egyszerű szövegszerkesztő plusz egy terminál – bármi, amivel kényelmesen dolgozol.

Ennyi. Nincs nehéz keretrendszer, nincs extra natív függőség. Kezdjünk is bele.

## 1. lépés – Kereshető PDF létrehozása: OCR motor inicializálása

Az első dolog, amit teszünk, hogy létrehozzuk az `OcrEngine` példányt, és rámutatunk a forrásképre. Ez az objektum az Aspose OCR szíve; kezeli a bitmap betöltésétől a felismert szöveg kiadásáig minden lépést.

```java
import com.aspose.ocr.*;

public class HelloOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the image you want to turn into a searchable PDF
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

> **Miért fontos:** A motor helyes inicializálása biztosítja, hogy a könyvtár be tudja olvasni a megadott képformátumot. Ha az útvonal hibás, `FileNotFoundException` keletkezik, és a teljes folyamat leáll.

## 2. lépés – Teljesítmény növelése: GPU, többmagos CPU és helyesírás‑javítás engedélyezése

Az OCR CPU‑igényes lehet, különösen nagy dokumentumok esetén. Az Aspose néhány beállítást kínál, amellyel gyorsabbá és pontosabbá teheted a folyamatot.

```java
        // 2️⃣ Turn on performance helpers – GPU, multi‑core CPU, and spell correction
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)                 // uses GPU if one is available
                 .setUseMultiCore(true)           // spreads work across CPU cores
                 .setEnableSpellCorrection(true); // cleans up common OCR mistakes
```

> **Pro tipp:** Ha szerveren futtatsz GPU nélkül, a `setUseGpu(false)` nem árt – egyszerűen a többmagos CPU‑ra vált.

## 3. lépés – Képminőség javítása: Döntéskorrekció és zajszűrés (opcionális, de ajánlott)

A beolvasott anyag ritkán tökéletes. Egy kis dőlés vagy szemcsés zaj megzavarhatja a felismerőt. Az `ImageProcessingOptions` osztály lehetővé teszi a kép tisztítását, mielőtt a motor megpróbálja olvasni.

```java
        // 3️⃣ Pre‑process the image – straighten it and remove noise
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)   // automatically rotates tilted text
                 .setDespeckle(true); // reduces background speckles
```

> **Szélsőséges eset:** Ha a forrásképed már tiszta, kihagyhatod ezt a lépést. Nem árt, de néhány ezredmásodperces többletterhet jelent.

## 4. lépés – Szöveg felismerése a képről és PDF generálása

Most jön a varázslat. Meghívjuk a `recognize()` metódust, és a motor visszaad egy `OcrResult`‑ot. Innen különböző formátumokba menthetjük az eredményt – a PDF a leggyakoribb a kereshető dokumentumok esetén.

```java
        // 4️⃣ Perform OCR and get the result object
        OcrResult ocrResult = ocrEngine.recognize();

        // 5️⃣ Save the result as a searchable PDF (you could also choose TXT, DOCX, etc.)
        ocrResult.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);
    }
}
```

> **Mit látsz majd:** A `sample-output.pdf` az eredeti képet háttérrétegként tartalmazza, míg a felismert szöveg egy láthatatlan átfedésként helyezkedik el fölötte. Nyisd meg Adobe Readerben, és próbáld ki a szöveg kijelölését – meglepődni fogsz.

## 5. lépés – A kereshető PDF kimenet ellenőrzése

Miután a fájl kiírásra került, jó gyakorlat, ha leellenőrzöd, hogy a PDF valóban kereshető‑e.

```java
import java.awt.Desktop;
import java.io.File;

public class VerifyPdf {
    public static void main(String[] args) throws Exception {
        File pdf = new File("YOUR_DIRECTORY/sample-output.pdf");
        if (pdf.exists() && Desktop.isDesktopSupported()) {
            Desktop.getDesktop().open(pdf); // opens the PDF in the default viewer
        } else {
            System.out.println("PDF not found or cannot be opened on this platform.");
        }
    }
}
```

Nyisd meg a PDF‑et, nyomd meg a **Ctrl F**‑et, írj be egy szót, amely biztosan szerepel a képen – ha a keresés megtalálja, sikeresen **létrehoztad a kereshető PDF‑et**!

## OCR használata a valós életben (bónusz)

* **Kötegelt feldolgozás:** Csomagold a kódot egy ciklusba, amely egy mappában lévő JPG‑ket iterálja. Ne felejtsd el egyetlen `OcrEngine` példányt újra‑használni a memóriahasználat alacsonyan tartásához.  
* **Nyelvtámogatás:** Az Aspose OCR több mint 60 nyelvet támogat. Egyszerűen hívd meg: `ocrEngine.getEngineOptions().setLanguage(Language.English);` (vagy bármely más enum értéket).  
* **Hibakezelés:** Fogd el az `OcrException`‑t, hogy elegánsan kezeld a sérült fájlokat.  

Ezekkel a finomhangolásokkal a megoldás már alkalmas termelési környezetben is.

## Teljes Java példa – Kereshető PDF létrehozása JPG‑ből

Az alábbiakban a teljes, önálló programot találod, amelyet lefordíthatsz és futtathatsz változtatás nélkül. Cseréld le a `YOUR_DIRECTORY`‑t a saját géped tényleges elérési útjára.

```java
import com.aspose.ocr.*;

public class CreateSearchablePdf {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // -------------------------------------------------
        // 2️⃣ Performance helpers
        // -------------------------------------------------
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)
                 .setUseMultiCore(true)
                 .setEnableSpellCorrection(true);

        // -------------------------------------------------
        // 3️⃣ Image pre‑processing (optional but helpful)
        // -------------------------------------------------
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)
                 .setDespeckle(true);

        // -------------------------------------------------
        // 4️⃣ Run OCR and save as searchable PDF
        // -------------------------------------------------
        OcrResult result = ocrEngine.recognize();
        result.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);

        System.out.println("✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf");
    }
}
```

**Várt kimenet:**  

```
✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf
```

Nyisd meg a generált PDF‑et, és képesnek kell lenned keresni bármely szót, amely a `sample.jpg`‑ben megjelent. Ha nem látszik a szövegréteg, ellenőrizd a kép útvonalát, és győződj meg róla, hogy az OCR motor nem dob rejtett kivételeket.

## Összegzés

Most már tudod, hogyan **hozz létre kereshető PDF‑et** egy JPEG‑ből az Aspose OCR for Java segítségével. A kép betöltésétől, a teljesítménybeállítások finomhangolásán, a kép tisztításán, a szöveg felismerésén és a kereshető PDF mentésén át minden lépést megmutattunk a *miért* és *hogyan* magyarázatával.  

Most már **konvertálhatsz képet PDF‑be**, **felismerheted a szöveget a képről**, és **generálhatsz PDF‑et JPG‑ből** a saját alkalmazásaidban. Következő lépésként próbálj meg egy egész mappát feldolgozni, kísérletezz különböző nyelvekkel, vagy adj hozzá jelszóvédelmet a kimeneti PDF‑hez. A lehetőségek határtalanok.

Van kérdésed a szélsőséges esetekkel, licenceléssel vagy teljesítményhangolással kapcsolatban? Írj kommentet alább, és jó kódolást kívánunk! 

![OCR folyamatot ábrázoló diagram – kereshető pdf létrehozása](/images/ocr-pipeline.png "Kereshető PDF diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}