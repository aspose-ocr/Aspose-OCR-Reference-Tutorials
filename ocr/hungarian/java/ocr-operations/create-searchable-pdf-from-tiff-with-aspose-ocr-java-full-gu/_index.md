---
category: general
date: 2026-06-28
description: Készítsen kereshető PDF-et többoldalas TIFF-ből Java-ban az Aspose OCR
  használatával. Tanulja meg, hogyan konvertálja a TIFF-et PDF-be, és hogyan adjon
  hozzá OCR szövegréteget a PDF-hez az azonnali kereshetőség érdekében.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- add ocr text layer pdf
language: hu
og_description: Kereshető PDF létrehozása TIFF képből Java-ban az Aspose OCR segítségével.
  Ez az útmutató bemutatja, hogyan konvertálhatjuk a TIFF-et PDF-re, és hogyan adhatunk
  hozzá OCR szövegréteget a PDF-hez a kereshető dokumentumokhoz.
og_title: Kereshető PDF létrehozása TIFF-fájlból az Aspose OCR (Java) segítségével
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Create searchable PDF from a multi‑page TIFF in Java using Aspose OCR.
    Learn how to convert TIFF to PDF and add OCR text layer PDF for instant searchability.
  headline: Create Searchable PDF from TIFF with Aspose OCR (Java) – Full Guide
  type: TechArticle
- description: Create searchable PDF from a multi‑page TIFF in Java using Aspose OCR.
    Learn how to convert TIFF to PDF and add OCR text layer PDF for instant searchability.
  name: Create Searchable PDF from TIFF with Aspose OCR (Java) – Full Guide
  steps:
  - name: What if my TIFF is single‑page?
    text: The same code works—Aspose treats a single‑page TIFF as a one‑element collection,
      so no extra handling is required.
  - name: Can I control the OCR language?
    text: 'Yes. Before calling `recognizeAndExportPdf`, set the language on the engine:'
  - name: How do I skip embedding the original image to reduce file size?
    text: Just set `pdfOptions.setEmbedOriginalImage(false)`. The PDF will contain
      only the searchable text layer, which dramatically shrinks the file but loses
      the visual representation.
  - name: Is the generated PDF truly searchable on all platforms?
    text: Modern PDF readers (Adobe Acrobat, Foxit, even browsers) honor the text
      layer. Some older, lightweight viewers might ignore it—test on your target platform
      if you’re unsure.
  type: HowTo
tags:
- Aspose OCR
- Java
- PDF Generation
title: Kereshető PDF létrehozása TIFF-ből Aspose OCR (Java) segítségével – Teljes
  útmutató
url: /hu/java/ocr-operations/create-searchable-pdf-from-tiff-with-aspose-ocr-java-full-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása TIFF-ből Aspose OCR-rel (Java) – Teljes útmutató

Gondolkodtál már azon, hogyan **hozz létre kereshető PDF-et** egy beolvasott TIFF-ből anélkül, hogy órákat töltenél harmadik fél eszközeivel kísérletezve? Nem vagy egyedül – a fejlesztőknek folyamatosan szükségük van egy megbízható módra, hogy a nehézkes képfájlokat PDF‑ekké alakítsák, amelyeket ténylegesen keresni lehet.  

Ebben az útmutatóban egy gyakorlati, vég‑től‑végig megoldáson vezetünk végig, amely nem csak **konvertálja a TIFF-et PDF‑be**, hanem **automatikusan hozzáadja az OCR szövegréteget a PDF-hez** is, így néhány Java sorral egy valóban kereshető dokumentumot kapsz.

## Mit fogsz megtanulni

- Hogyan állítsd be az Aspose OCR for Java-t és alkalmazz licencet (opcionális, de ajánlott).  
- A pontos lépések a **TIFF PDF‑be konvertálásához** az `OcrEngine` használatával.  
- Hogyan konfiguráld a `PdfExportOptions`‑t, hogy a generált fájl egy láthatatlan, kereshető szövegréteget tartalmazzon – pontosan ez, amit a **add OCR text layer PDF** jelent a valóságban.  
- Várt kimenet és egy gyors ellenőrzés, hogy minden rendben működött-e.

Előzetes Aspose tapasztalat nem szükséges; egy alap Java fejlesztői környezet (JDK 8+ és bármely IDE) elegendő.

---

## 1. lépés: Projekt előkészítése és az Aspose OCR licenc alkalmazása  

Mielőtt bármilyen OCR API‑t meghívnál, a Aspose OCR JAR‑okat a classpath‑ba kell helyezned. Ha van kereskedelmi licenced, tedd a `.lic` fájlt egy elérhető helyre, és a `License` osztályt mutasd rá. Ez a lépés nem kötelező – az Aspose értékelő módban is fut –, de a licenc eltávolítja a vízjeleket és feloldja a teljes funkciókészletet.

```java
// Apply your Aspose OCR license (optional for full features)
License license = new License();
license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
```

> **Pro tipp:** Tartsd a licencfájlt a forráskód verziókezelésen kívül, hogy elkerüld a véletlen kiszivárgást.

---

## 2. lépés: OCR motor példányosítása  

Az `OcrEngine` objektum létrehozása az első valódi lépés a **create searchable pdf** felé. A motor tárolja az összes OCR beállítást, és később vezérli a konvertálást.

```java
// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Miért külön motor? Lehetővé teszi, hogy ugyanazt a konfigurációt több fájlra is újrahasználjuk, ami hasznos, ha tucatnyi TIFF‑et dolgozol fel egyszerre.

---

## 3. lépés: Többoldalas TIFF betöltése  

Az Aspose OCR egyszerűvé teszi a többoldalas TIFF betöltését. Csak add meg a fájl útvonalát egy `OcrInput` objektumnak; a könyvtár automatikusan felismeri és sorba rendezi az összes oldalt.

```java
// Load a multi‑page TIFF image as OCR input
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multipage.tif");   // all pages are added automatically
```

Ha egy oldalonként szeretnéd **konvertálni a TIFF-et PDF‑be**, akkor egy ciklusban meghívhatod az `ocrInput.add(pageStream)`‑t – az Aspose minden hívást külön oldalnak tekint.

---

## 4. lépés: PDF export beállítások konfigurálása – OCR szövegréteg hozzáadása  

Itt történik a varázslat a **add OCR text layer pdf** esetén. Néhány jelző beállításával azt mondod az Aspose‑nak, hogy ágyazza be az eredeti bitmapet (így a vizuális hűség megmarad) *és* generáljon egy rejtett szövegréteget, amelyet a keresőmotorok indexelhetnek.

```java
// Configure PDF export options
PdfExportOptions pdfOptions = new PdfExportOptions();
pdfOptions.setEmbedOriginalImage(true);      // keep the bitmap as background
pdfOptions.setCreateSearchablePdf(true);     // generate hidden text layer for search
pdfOptions.setAuthor("John Doe");
pdfOptions.setTitle("OCR Output");
```

- `setEmbedOriginalImage(true)`: biztosítja, hogy a PDF pontosan úgy nézzen ki, mint a beolvasott kép.  
- `setCreateSearchablePdf(true)`: létrehozza a láthatatlan szövegréteget – ez a **add OCR text layer pdf** lényege.  

Nyugodtan egészítsd ki a metaadatokat (author, title, subject) a példában látható módon; ez később segít a dokumentumkezelésben.

---

## 5. lépés: OCR futtatása és a kereshető PDF exportálása  

Most összekötjük a részeket. A `recognizeAndExportPdf` metódus végzi a nehéz munkát: OCR‑t futtat minden TIFF oldalra, kiírja a vizuális képet, és ráhelyezi a kereshető szöveget.

```java
// Perform OCR recognition and export the result as a searchable PDF
ocrEngine.recognizeAndExportPdf(
    ocrInput,
    "YOUR_DIRECTORY/searchable.pdf",
    pdfOptions
);

System.out.println("Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf");
```

Amikor a konzol kiírja a sikerüzenetet, akkor **create searchable pdf**-et hoztál létre egy TIFF fájlból. Nyisd meg a keletkezett `searchable.pdf`‑t bármely PDF‑olvasóban, nyomd meg a `Ctrl+F`‑et, és keress egy szót, amely az eredeti képen is szerepel – azonnal megtalálja.

---

## Az eredmény ellenőrzése – Gyors ellenőrzőlista  

1. **Vizuális hűség** – A PDF-nek pontosan úgy kell kinéznie, mint a forrás TIFF (köszönhetően a `setEmbedOriginalImage` beállításnak).  
2. **Kereshetőség** – Használd a nézőprogram keresőjét; a rejtett szövegrétegnek egyezéseket kell adnia.  
3. **Metaadatok** – Nyisd meg a PDF tulajdonságait, és ellenőrizd, hogy a korábban beállított szerző és cím megjelenik-e.  

Ha bármelyik ellenőrzés nem sikerül, ellenőrizd, hogy a `setCreateSearchablePdf(true)` be van‑e kapcsolva, és hogy a licenc (ha van) nem értékelő módban korlátozásokkal fut.

---

## Szélsőséges esetek és gyakori kérdések  

### Mi van, ha a TIFF egyoldalas?  

Ugyanaz a kód működik – az Aspose egy egyoldalas TIFF‑et egy elemű gyűjteményként kezeli, így nincs szükség extra kezelésre.

### Vezérelhetem az OCR nyelvét?  

Igen. Mielőtt meghívod a `recognizeAndExportPdf`‑t, állítsd be a nyelvet a motoron:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.English);
```

Cseréld le az `English`‑t bármely támogatott nyelvi enumra.

### Hogyan hagyjam ki az eredeti kép beágyazását a fájlméret csökkentése érdekében?  

Csak állítsd `pdfOptions.setEmbedOriginalImage(false)`‑ra. A PDF csak a kereshető szövegréteget tartalmazza, ami jelentősen csökkenti a méretet, de elveszíti a vizuális ábrázolást.

### A generált PDF valóban kereshető minden platformon?  

A modern PDF‑olvasók (Adobe Acrobat, Foxit, még a böngészők is) tiszteletben tartják a szövegréteget. Néhány régebbi, könnyű olvasó esetleg figyelmen kívül hagyja – teszteld a célplatformon, ha bizonytalan vagy.

---

## Teljes működő példa  

Az alábbiakban a komplett, azonnal futtatható Java osztály látható. Cseréld ki a helyőrző útvonalakat a sajátjaidra, add hozzá az Aspose OCR JAR‑okat a projekthez, és indítsd el.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.*;

public class PdfExportDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply your Aspose OCR license (optional for full features)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Load a multi‑page TIFF image as OCR input
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/multipage.tif");   // all pages are added automatically

        // Step 4: Configure PDF export options
        PdfExportOptions pdfOptions = new PdfExportOptions();
        pdfOptions.setEmbedOriginalImage(true);    // keep the bitmap as background
        pdfOptions.setCreateSearchablePdf(true);   // generate hidden text layer for search
        pdfOptions.setAuthor("John Doe");
        pdfOptions.setTitle("OCR Output");

        // Step 5: Perform OCR recognition and export the result as a searchable PDF
        ocrEngine.recognizeAndExportPdf(
            ocrInput,
            "YOUR_DIRECTORY/searchable.pdf",
            pdfOptions
        );

        System.out.println("Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**Várt kimenet (konzol):**

```
Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf
```

Nyisd meg a `searchable.pdf`‑t, és keress egy szót, amely az eredeti TIFF‑ben is szerepel – voilà, sikeresen **create searchable pdf**-et hoztál létre!

---

## Összegzés  

Most egy komplett, termelés‑kész módszert mutattunk be a **create searchable PDF** létrehozására TIFF‑ből az Aspose OCR for Java segítségével. A `PdfExportOptions` konfigurálásával automatikusan **add OCR text layer PDF**‑t kapsz, így a statikus képek azonnal kereshető dokumentumokká válnak.  

Ha tovább szeretnél menni, próbáld ki a következőket:

- **convert TIFF to PDF** egyedi oldalméretekkel vagy DPI beállításokkal.  
- Vízjelek vagy digitális aláírások hozzáadása OCR után.  
- Tömeges feldolgozás egy mappában lévő TIFF‑ekkel egy egyszerű `for` ciklussal.  

Ezek a kiterjesztések ugyanazokra az alapelvekre épülnek, amelyeket itt bemutattunk, így a átmenet zökkenőmentes lesz.  

Van kérdésed vagy elakadtál? Hagyj egy megjegyzést alább, és jó kódolást!

## Mit érdemes még megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutató technikáira épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy további API‑funkciókat saját projektjeidben is könnyedén felfedezhess.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}