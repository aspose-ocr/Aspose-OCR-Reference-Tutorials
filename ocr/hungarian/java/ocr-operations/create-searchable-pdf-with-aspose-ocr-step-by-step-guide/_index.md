---
category: general
date: 2026-01-02
description: Készíts kereshető PDF-et egy beolvasott képes PDF-ből az Aspose OCR használatával.
  Tanulja meg beállítani az OCR nyelvet, beágyazni egy szövegréteges PDF-et, és alkalmazni
  a magas tömörítésű PDF-beállításokat.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: hu
og_description: Készítsen gyorsan kereshető PDF-et. Ez az útmutató bemutatja, hogyan
  konvertálja a beolvasott képes PDF-et, ágyazzon be szövegréteget, állítsa be az
  OCR‑nyelvet, és engedélyezze a magas tömörítésű PDF-et.
og_title: Kereshető PDF létrehozása Aspose OCR-rel – Teljes útmutató
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: Kereshető PDF létrehozása Aspose OCR-rel – Lépésről lépésre útmutató
url: /hu/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása – Teljes programozási útmutató

Szükséged volt már **create searchable PDF** fájlok létrehozására beolvasott képekből, de nem tudtad, hol kezdjed? Nem vagy egyedül. Sok dokumentum‑intenzív munkafolyamatban egy egyszerű, csak képet tartalmazó PDF halálpont a keresés és indexelés számára.  

A jó hír, hogy az Aspose OCR segítségével **convert scanned image PDF**-t teljesen kereshető dokumentummá alakíthatsz néhány Java sorral. Ez az útmutató minden lépésen végigvezet – az OCR motor inicializálásán, a magas tömörítésű PDF beállításainak konfigurálásán, egy rejtett szövegréteg beágyazásán, sőt a megfelelő OCR nyelv kiválasztásán.  

A útmutató végére egy futtatható programod lesz, amely kereshető PDF-et állít elő, egy olyan fájlt, amelyet gond nélkül be lehet helyezni bármely keresőmotorba vagy dokumentumkezelő rendszerbe.

---

## Kereshető PDF létrehozása – Áttekintés

Mielőtt belemerülnénk a kódba, tisztázzuk, mit jelent valójában a „create searchable PDF”. A kereshető PDF két párhuzamos réteget tartalmaz:

1. **Visual layer** – az eredeti beolvasott kép (vagy renderelt oldal).  
2. **Text layer** – láthatatlan, de gép‑olvasható karakterek, amelyeket az OCR nyert ki.  

Amikor ilyen PDF-et nyitsz meg az Adobe Readerben és szöveget jelölsz ki, valójában a rejtett szövegréteggel lépsz interakcióba, nem a képpel. Ez a kettős réteg megközelítés teszi lehetővé a **embed text layer PDF** funkciót.

## Beolvasott kép PDF konvertálása Aspose OCR használatával

Az első dolog, amire szükséged van, egy beolvasott kép (PNG, JPEG, TIFF), amelyet PDF‑vé szeretnél alakítani. Az Aspose OCR be tudja olvasni a képet, futtatja az OCR‑t, és átadja az eredményt egy PDF‑írónak.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**Miért működik:**  
- `setCreateSearchablePdf(true)` azt mondja az Aspose-nak, hogy generálja a rejtett szövegréteget, ezzel teljesítve a **embed text layer pdf** követelményt.  
- `setCompressionLevel(9)` a fájlt a **high compression pdf** tartományba helyezi, csökkentve a végső méretet anélkül, hogy az OCR pontosságát feláldozná.  
- A `RecognitionLanguage.ENGLISH` argumentum azt mutatja, hogyan **set OCR language**; cserélheted francia, német stb. nyelvre a forrásanyag függvényében.

## Magas tömörítésű PDF beállítások

Nagy beolvasott PDF-ek gyorsan több száz megabájtra nőhetnek. Az Aspose egyszerű tömörítési API-t kínál, amely a PDF szinten működik. A `setCompressionLevel` metódus 0‑tól 9‑ig terjedő értékeket fogad el (0 = nincs tömörítés, 9 = maximális tömörítés).  

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

Néhány tipp:

- **Használj veszteségmentes képformátumokat** (PNG) szöveggazdag beolvasásokhoz; a JPEG jobb fényképekhez.  
- **Engedélyezd a betűkészlet részhalmazolását**, ha egyedi betűket ágyazol be – az Aspose ezt automatikusan megteszi, amikor kereshető PDF-et hozol létre.  
- **Teszteld a kimeneti méretet** minden módosítás után; néha a 8‑as szintű tömörítés 10 % méretcsökkenést eredményez elhanyagolható minőségveszteséggel a 9‑eshez képest.

## Szövegréteg beágyazása PDF-be a kereshetőséghez

Ha kihagyod a `setCreateSearchablePdf(true)` hívást, a kapott fájl rendben néz ki, de nem lesz kereshető a tartalma. A rejtett szövegréteget úgy hozza létre, hogy minden felismert karaktert a lap megfelelő helyéhez rendel.

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**Mire figyelj:**  

- **Vegyes nyelvű dokumentumok** – előfordulhat, hogy kétszer kell futtatni az OCR‑t, nyelvenként egyszer, majd össze kell vonni a szövegrétegeket.  
- **Komplex elrendezések** (táblázatok, többoszlopos) – az Aspose elég jó munkát végez, de ellenőrizd a kimenetet egy olyan PDF‑megjelenítővel, amely a rejtett szöveget is mutatja (pl. az Adobe Acrobat „Edit PDF” módja).

## OCR nyelv beállítása a pontos felismeréshez

Az OCR motor pontossága attól függ, milyen nyelvet adsz meg neki. Az Aspose beépített nyelvcsomagokkal érkezik, és egyedi nyelvcsomagokat is hozzáadhatsz.

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**Mikor változtasd a nyelvet:**  

- A dokumentumok **nem latin írásrendszert** tartalmaznak (cirill, arab) – válts a megfelelő `RecognitionLanguage`-ra.  
- Vegyes nyelvű oldalak – meghívhatod a `recognizeImageAndSave`-t kétszer, minden alkalommal más nyelvvel, majd összevonhatod a PDF‑eket.

## A teljes példa futtatása

Alább a teljes, futtatható program. Cseréld ki a helyőrző útvonalakat a valós fájlhelyekre, győződj meg róla, hogy az Aspose OCR JAR a classpath‑on van, és futtasd.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**Várható kimenet:** Amikor futtatod a programot, a konzol kiírja:

```
Searchable PDF created.
```

Nyisd meg a `searchable.pdf`-et bármely PDF‑nézőben, próbáld ki a szöveg kijelölését, és láthatod a láthatatlan réteg működését. Sikeresen **create searchable pdf**-t hoztál létre egy beolvasott képből.

![create searchable pdf example](image-placeholder.png "create searchable pdf example")

*A fenti képernyőkép (helyőrző) általában egy PDF‑nézőt mutat, ahol a beolvasott oldal fölött kiválasztható szöveg látható.*

## Összegzés

Mindezt lefedtük, ami szükséges a **create searchable PDF** fájlok létrehozásához az Aspose OCR használatával:

- Inicializáld az OCR motort.  
- **Convert scanned image PDF** úgy, hogy egy PNG/JPEG‑t adsz a `recognizeImageAndSave`‑nek.  
- Használd a `setCreateSearchablePdf(true)`‑t a **embed text layer PDF**-hez.  
- Alkalmazd a `setCompressionLevel(9)`‑et egy **high compression PDF** létrehozásához, amely könnyű marad.  
- Válaszd ki a megfelelő `RecognitionLanguage`‑t a **set OCR language** beállításához a maximális pontosság érdekében.

Innen tovább kísérletezhetsz kötegelt feldolgozással, különböző nyelvekkel, vagy akár több beolvasott oldalt egyetlen kereshető PDF‑be egyesíthetsz. Ugyanez a minta működik más nyelveknél is, például spanyol vagy japán – csak cseréld ki a `RecognitionLanguage` enumot.

Nyugodtan hagyj megjegyzést, ha elakadsz, és jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}