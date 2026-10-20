---
category: general
date: 2026-05-03
description: Hogyan használjuk az OCR-t a PDF-fájlok szövegének kinyerésére Java-ban.
  Tanulja meg a PDF-ből történő szövegfelismerést, a PDF szöveggé konvertálását, és
  a többoldalas OCR PDF-ek hatékony kezelését.
draft: false
keywords:
- how to use ocr
- extract text from pdf
- recognize text from pdf
- convert pdf to text
- ocr multi page pdf
language: hu
og_description: Hogyan használjunk OCR-t a PDF-fájlok szövegének kinyerésére Java-ban.
  Ez az útmutató bemutatja, hogyan ismerhető fel a szöveg a PDF-ből, hogyan konvertálható
  a PDF szöveggé, és hogyan dolgozható fel az OCR többoldalas PDF.
og_title: Hogyan használjunk OCR-t Java-ban – Szöveg kinyerése többoldalas PDF‑ekből
tags:
- ocr
- java
- pdf
- aspose
title: Hogyan használjunk OCR-t Java-ban – Szöveg kinyerése többoldalas PDF-ekből
url: /hu/python-java/general/how-to-use-ocr-in-java-extract-text-from-multi-page-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjunk OCR-t Java-ban – Szöveg kinyerése többoldalas PDF-ekből

**Hogyan használjunk OCR-t** egy Java projektben? Ha valaha is szöveget kellett kinyerned PDF fájlokból anélkül, hogy a PDF belső szövegrétegére támaszkodnál, jó helyen vagy. Ez a tutorial egy teljes, futtatható megoldáson vezet végig, amely **felismeri a szöveget PDF-ből**, PDF-et szöveggé konvertál, és még egy **OCR többoldalas PDF**-et is kezel egyetlen hívással.

Képzeld el, hogy kapsz egy beolvasott szerződést — egy 12 oldalas TIFF-et egy PDF-ben. Szeretnéd a kereshető szöveget az indexeléshez, de a fájlban nincsenek beágyazott karakterek. Semmi gond; lépésről lépésre megmutatjuk, hogyan csináld.

> **Mit kapsz:** egy azonnal futtatható Java kódrészlet az Aspose.OCR használatával, magyarázatok arra, hogy miért fontos minden sor, tippek a gyakori buktatókhoz, és egy minta kimenet, amelyet azonnal ellenőrizhetsz.

---

## Amire szükséged lesz

* **Java 17** (vagy bármely friss JDK) – a kód régebbi verziókkal is működik, de a 17 a legoptimálisabb.
* **Aspose OCR for Java** könyvtár – letöltheted a JAR‑t az Aspose weboldaláról, vagy hozzáadhatod Maven/Gradle‑on keresztül.
* Egy **többoldalas PDF** (vagy TIFF), amelyet feldolgozni szeretnél. Példáinkban a `contract_multipage.pdf` fájlt használjuk, amely a `YOUR_DIRECTORY` mappában található.
* Egy érvényes **Aspose OCR licencfájl** (`Aspose.OCR.Java.lic`). Licenc nélkül a könyvtár értékelő módban fut, ami egy gyors teszthez megfelelő, de vízjelet ad a kimenethez.

Ennyi – nincs extra OCR motor, nincs natív bináris, csak egy JAR és egy licenc.

---

![how to use ocr example](https://example.com/ocr-demo.png "Hogyan használjunk OCR-t Java-ban – a betöltés, felismerés és szöveg kimenet vizuális áttekintése")

*Image alt text: hogyan használjunk OCR-t Java-ban – a betöltés, felismerés és szöveg kimenet vizuális áttekintése.*

---

## 1. lépés: Az OCR motor beállítása – **Hogyan használjunk OCR-t** helyesen

Az első dolog, amit tenned kell, hogy létrehozod az OCR motor egy példányát, és alkalmazod a licencet. Licenc nélkül a motor még működik, de a kimenetben egy próbaverzió vízjelet látsz majd.

```java
// Import the Aspose OCR package
import com.aspose.ocr.*;

public class OcrPdfDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Apply your license – replace the path with your actual .lic file
        ocrEngine.setLicense(new License().setLicense("Aspose.OCR.Java.lic"));
```

**Miért fontos ez:**  
Az `OcrEngine` a központi objektum, amely az képelemzést, nyelvfelismerést és szövegkinyerést irányítja. A licenc korai beállítása megakadályozza, hogy a motor később próbaverzióra váltson, ami befolyásolhatja a pontosságot.

---

## 2. lépés: Dokumentum betöltése – **Szöveg kinyerése PDF-ből** hatékonyan

Az Aspose OCR közvetlenül olvashat PDF és TIFF konténereket is. Itt betöltünk egy többoldalas PDF-et, amely beolvasott képeket tartalmaz.

```java
        // 3️⃣ Load a multi‑page PDF (or TIFF) from disk
        PdfDocument pdfDoc = PdfDocument.fromFile("YOUR_DIRECTORY/contract_multipage.pdf");
```

**Miért fontos ez:**  
A `PdfDocument.fromFile` beolvassa a konténert, és minden oldalt képként elérhetővé tesz. Ez az absztrakció lehetővé teszi, hogy az OCR motor minden oldalt egységesen kezeljen, függetlenül az eredeti formátumtól.

**Tipp:** Ha a forrásfájl TIFF, ugyanaz a hívás működik – az Aspose automatikusan felismeri a formátumot. Nincs szükség extra kódra.

---

## 3. lépés: Az összes oldal egyszerre történő felismerése – **Szöveg felismerése PDF-ből** zökkenőmentesen

Ahelyett, hogy saját ciklust írnál az oldalakra, kérheted a motort, hogy egyetlen hívással dolgozza fel a teljes dokumentumot. Ez a leghatékonyabb módja a **PDF szöveggé konvertálásának**, amikor egy **OCR többoldalas PDF**-et kell kezelni.

```java
        // 4️⃣ Recognize text on all pages with a single method call
        List<OcrPageResult> recognizedPages = ocrEngine.recognizeDocument(pdfDoc);
```

**Miért fontos ez:**  
A `recognizeDocument` egyszeri meghívása csökkenti azt a terhelést, amelyet a motor többszöri újrainicializálása okozna. Emellett biztosítja a nyelvi beállítások konzisztenciáját az oldalak között, ami jogi dokumentumok esetén különösen fontos, mivel gyakran vegyes betűtípusokat tartalmaznak.

---

## 4. lépés: A felismert szöveg kiírása – **PDF konvertálása szöveggé** indexeléshez

Miután minden oldal feldolgozásra került, egyszerűen végigiterálunk az eredményeken és kiírjuk a kinyert karakterláncokat. Írhatsz is fájlba, adatbázisba, vagy betáplálhatod egy keresőindexbe.

```java
        // 5️⃣ Loop through each page's result and print the text
        for (int i = 0; i < recognizedPages.size(); i++) {
            OcrPageResult pageResult = recognizedPages.get(i);
            System.out.println("--- Page " + (i + 1) + " ---");
            System.out.println(pageResult.getText());
        }
    }
}
```

**Várható kimenet (rövidítve):**

```
--- Page 1 ---
THIS AGREEMENT is made on the 1st day of January 2024...
--- Page 2 ---
WHEREAS, the Parties desire to...
...
```

Ha a PDF 12 oldalt tartalmaz, tizenkét `--- Page X ---` szekciót látsz, mindegyik után az OCR‑kel kinyert szöveg következik.

---

## Haladó tippek egy **OCR többoldalas PDF**-hez

### 1. Nyelvi beállítások módosítása

Alapértelmezés szerint az Aspose megpróbálja automatikusan felismerni a nyelvet, de felgyorsíthatod a folyamatot, ha megadod:

```java
ocrEngine.getLanguage().setLanguage(Language.ENGLISH);
```

### 2. Képelőfeldolgozás vezérlése

A beolvasott szerződések gyakran zajosak. Engedélyezheted a kiegyenesítést és binarizálást:

```java
ocrEngine.getImageProcessingOptions()
        .setDeskew(true)
        .setBinarization(true);
```

### 3. Nagy fájlok kezelése elegánsan

Ha 100 MB-nál nagyobb PDF-eket dolgozol fel, fontold meg az oldalak streamelését a teljes dokumentum egyszerre történő betöltése helyett:

```java
for (int pageNum = 1; pageNum <= pdfDoc.getPageCount(); pageNum++) {
    OcrPageResult result = ocrEngine.recognizePage(pdfDoc.getPage(pageNum));
    // process result...
}
```

Ez a minta csökkenti a memóriaigényt, és kötegelt feladatoknál hasznos.

### 4. Exportálás strukturált formátumokba

A sima szöveg mellett exportálhatsz JSON‑ba vagy XML‑be a további feldolgozáshoz:

```java
String json = pageResult.toJson();
System.out.println(json);
```

---

## Gyakori hibák és hogyan kerüld el őket

| Hiba | Miért fordul elő | Megoldás |
|------|------------------|----------|
| **Üres kimenet** | Licenc nincs alkalmazva vagy a fájl útvonala hibás. | Ellenőrizd a `setLicense` útvonalat és erősítsd meg, hogy a fájl létezik. |
| **Hibás karakterek** | Helytelen nyelvi beállítás vagy alacsony felbontású forrás. | Állítsd be a megfelelő `Language` értéket és biztosítsd, hogy a forrás képek ≥300 dpi legyenek. |
| **Memóriahiányos hibák** | Egy hatalmas PDF egyszerre történő betöltése. | Használd a fent bemutatott streaming megközelítést. |
| **Részleges oldalfelismerés** | A PDF kevert raszter/vektor rétegeket tartalmaz. | Először lapítsd le a PDF-et: `pdfDoc.flatten();` OCR előtt. |

---

## Összefoglalás – Amit lefedtünk

* **Hogyan használjunk OCR-t** az Aspose-szal Java-ban.  
* **Szöveg kinyerése PDF-ből** (vagy TIFF) egyetlen hívással.  
* **Szöveg felismerése PDF-ből** minden oldalon manuális ciklusok nélkül.  
* **PDF konvertálása szöveggé** és tiszta kimenet.  
* Tippek egy **OCR többoldalas PDF** kezeléséhez, beleértve a nyelvi finomhangolást és a memóriahatékony streamelést.

Most már van egy komplett, production‑kész kódrészlet, amelyet bármely Java projektbe beilleszthetsz. Nyugodtan módosítsd a képelőfeldolgozási beállításokat, cseréld ki a kimeneti célhelyet, vagy integráld az eredményt egy keresőindexbe.

---

## Következő lépések

* **Fedezd fel az Aspose OCR fejlett funkcióit** – például kézírásfelismerés vagy PDF/A megfelelőség.  
* **Kombináld az OCR‑t PDF manipulációval** (pl. egy rejtett szövegréteg visszahelyezése a PDF-be kereshető PDF-ek létrehozásához).  
* **Automatizáld a kötegelt feldolgozást** úgy, hogy egy mappában lévő PDF-eket beolvasod, és minden eredményt egy megfelelő `.txt` fájlba írsz.

Ha bármilyen akadályba ütközöl, az Aspose fórumok remek helyek a segítségkérésre, és az API referencia kimerítő részleteket nyújt minden itt használt metódusról.

Boldog kódolást, és élvezd a makacs beolvasott dokumentumok kereshető szöveggé alakítását!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}