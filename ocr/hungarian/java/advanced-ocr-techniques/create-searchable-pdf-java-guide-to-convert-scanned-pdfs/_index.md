---
category: general
date: 2026-02-22
description: Készíts kereshető PDF-et egy beolvasott PDF-ből az Aspose OCR Java használatával.
  Tanuld meg, hogyan konvertálj beolvasott PDF-et, tömörítsd a PDF képeket, és hatékonyan
  ismerd fel a PDF OCR-t.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- compress pdf images
- recognize pdf ocr
- image pdf to text
language: hu
og_description: Készítsen kereshető PDF-et egy beolvasott PDF-ből az Aspose OCR Java
  segítségével. Ez a lépésről‑lépésre útmutató bemutatja, hogyan konvertáljon beolvasott
  PDF-et, tömörítse a PDF képeket, és hajtsa végre a PDF OCR-t.
og_title: Kereshető PDF létrehozása – Java útmutató a beolvasott PDF-ek konvertálásához
tags:
- Java
- OCR
- PDF
- Aspose
title: Kereshető PDF létrehozása – Java útmutató a beolvasott PDF-ek konvertálásához
url: /hu/java/advanced-ocr-techniques/create-searchable-pdf-java-guide-to-convert-scanned-pdfs/
---

content.

Check that we didn't miss any markdown elements.

We need to ensure we kept the placeholder {{CODE_BLOCK_X}} unchanged.

Also ensure we kept the image alt and title translation; alt text changed, title changed.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása – Java útmutató a beolvasott PDF-ek konvertálásához

Volt már szükséged **create searchable PDF** létrehozására egy csomó beolvasott dokumentumból? Ez egy gyakori fejfájás—PDF-jeid jól néznek ki, de nem tudod használni a *Ctrl + F* keresést. A jó hír? Néhány Java sor és az Aspose OCR segítségével átalakíthatod ezeket a csak képet tartalmazó PDF-eket teljesen kereshető fájlokká, **convert scanned PDF** szöveggé, és még a **compressing PDF images** segítségével is lecsökkentheted az eredményt.

Ebben az útmutatóban végigvezetünk egy teljes, futtatható példán, elmagyarázzuk, miért fontos minden beállítás, és megmutatjuk, hogyan finomíthatod a folyamatot olyan szélsőséges esetekhez, mint a többoldalas beolvasások vagy az alacsony felbontású képek. A végére egy stabil, éles környezetben is használható kódrészletet kapsz, amely **recognize pdf ocr** megbízhatóan, és egy rendezett kereshető dokumentumot hoz létre.

---

## Amire szükséged lesz

- **Java 17** (vagy bármely friss JDK; az API JDK‑agnosztikus)  
- **Aspose.OCR for Java** könyvtár – letöltheted a Maven Centralból (`com.aspose:aspose-ocr`)  
- Egy beolvasott PDF (csak kép), amelyet kereshetővé szeretnél tenni  
- Egy IDE vagy szövegszerkesztő, amivel kényelmesen dolgozol (IntelliJ, VS Code, Eclipse…)

Nincs nehéz keretrendszer, nincs külső szolgáltatás—csak tiszta Java és egyetlen harmadik féltől származó JAR.

---

![kereshető pdf példa](placeholder-image.png "Illusztráció egy beolvasott dokumentumból létrehozott kereshető PDF-ről")

*Kép alternatív szöveg:* **create searchable pdf** illusztráció, amely a beolvasott PDF előtti és utáni állapotát mutatja, kereshető szöveggé alakítva.

---

## 1. lépés – Az OCR motor inicializálása  

Az első dolog, amit meg kell tenned, egy `OcrEngine` példány létrehozása. Gondolj rá úgy, mint egy agyra, amely a PDF-ben lévő minden bitmapet elemzi, és Unicode karaktereket ad ki.

```java
import com.aspose.ocr.*;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this object holds licensing info and global settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pro tip:** Ha sok PDF-et szeretnél egymás után feldolgozni, használd újra ugyanazt a `OcrEngine`-t, ahelyett, hogy minden alkalommal újat hoznál létre. Ez néhány ezredmásodpercet takarít meg, és csökkenti a memóriahasználat ingadozását.

---

## 2. lépés – PDF‑specifikus OCR beállítások konfigurálása  

Az Aspose lehetővé teszi, hogy finomhangold, hogyan épül fel a kimeneti PDF. Az alábbi három beállítás a legnagyobb hatással van a **compress pdf images** folyamatra, miközben megőrzi a kereshetőséget.

```java
        // Configure PDF‑specific options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // Higher DPI = better text recognition
        pdfOcrOptions.setCompressImages(true);           // Shrinks the final file size
        pdfOcrOptions.setEmbedOriginalImages(true);      // Keeps the visual look of the original scan
```

- **Output DPI** – 300 dpi egy jó kiindulási pont; alacsonyabb értékek gyorsabbak, de elmaradhatnak a kis betűk.  
- **CompressImages** – a háttérben veszteségmentes PNG tömörítést aktivál; a kereshető PDF éles marad, de könnyebb lesz.  
- **EmbedOriginalImages** – ez a jelző nélkül a motor eldobná az eredeti rasztert, csak láthatatlan szöveget hagyva. Az eredeti kép megtartása biztosítja, hogy a PDF pontosan úgy nézzen ki, mint a beolvasás, amit sok megfelelőségi csapat megkövetel.

---

## 3. lépés – A beolvasott PDF betöltése egy `OcrInput`‑ba  

Az Aspose a forrásfájlt egy `OcrInput` burkolóval olvassa be. Több fájlt is hozzáadhatsz, de ebben a demóban egyetlen **image PDF**-re koncentrálunk.

```java
        // Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");   // <- replace with the path to your file
```

> **Miért ne csak egy `File`-t adnál át?** Az `OcrInput` használata rugalmasságot biztosít, hogy több PDF-et összefűzz vagy akár képfájlokat (PNG, JPEG) keverj az OCR előtt. Ez a javasolt minta, amikor **convert scanned pdf** több forrásból származhat.

---

## 4. lépés – OCR végrehajtása és kereshető PDF lekérése bájt tömbként  

Most jön a varázslat. A motor minden oldalt elemez, futtatja az OCR motorját, és egy új PDF-et épít, amely tartalmazza az eredeti képet és egy rejtett szövegréteget.

```java
        // Perform OCR – the result is a byte array representing the searchable PDF
        byte[] searchablePdfBytes = ocrEngine.recognizePdf(ocrInput, pdfOcrOptions);
```

Ha a nyers szövegre más célokra (pl. indexelés) van szükséged, meghívhatod a `ocrEngine.recognize(ocrInput)` metódust, amely egy `String`-et ad vissza. De a **create searchable pdf** célhoz a bájt tömb az, amit a lemezre írsz.

---

## 5. lépés – A kereshető PDF mentése lemezre  

Végül írd a bájt tömböt egy fájlba. A Java NIO ezt egyetlen soros megoldássá teszi.

```java
        // Write the searchable PDF to disk
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/searchable_output.pdf"),
                searchablePdfBytes
        );

        System.out.println("Searchable PDF created.");
    }
}
```

Amikor megnyitod a `searchable_output.pdf`-et az Adobe Acrobatban vagy bármely modern megjelenítőben, észre fogod venni, hogy most már ki tudod jelölni, másolni és keresni a szöveget—pontosan azt ígéri a **image pdf to text** átalakítás.

---

## Beolvasott PDF szöveggé konvertálása OCR-rel (opcionális)

Néha csak a kinyert egyszerű szövegre van szükség, nem egy új PDF-re. Újra felhasználhatod ugyanazt a motort:

```java
        // Optional: extract plain text from the scanned PDF
        String extractedText = ocrEngine.recognize(ocrInput).getText();
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/extracted_text.txt"),
                extractedText.getBytes()
        );
```

Ez a kódrészlet bemutatja, milyen egyszerű a **recognize pdf ocr** használata az olyan további feldolgozásokhoz, mint egy kereső index feltöltése vagy természetes nyelv elemzés végrehajtása.

---

## PDF képek tömörítése kisebb fájlokért  

Ha a forrás beolvasások nagyok (pl. 600 dpi színes beolvasások), a keletkező kereshető PDF még mindig nagy lehet. A `setCompressImages(true)` jelző mellett manuálisan is lecsökkentheted a felbontást OCR előtt:

```java
        // Downscale each page image to 150 dpi before OCR (reduces size dramatically)
        pdfOcrOptions.setOutputDpi(150);
```

A DPI csökkentése nagyjából felére csökkenti a fájlméretet, de teszteld az olvashatóságot—néhány betűtípus 150 dpi alatti felbontásnál olvashatatlanná válik. A **compress pdf images** és az OCR pontosság közötti kompromisszumot a tárolási korlátaid alapján döntheted el.

---

## A PDF OCR beállítások magyarázata  

| Beállítás                | Hatás a kimenetre                         | Tipikus felhasználási eset                                   |
|--------------------------|-------------------------------------------|--------------------------------------------------------------|
| `setOutputDpi(int)`      | A OCR kimenet raszteres felbontását szabályozza | Magas minőségű archívumok (300 dpi) vs. könnyű web PDF-ek (150 dpi) |
| `setCompressImages`      | PNG tömörítést engedélyez                  | Amikor PDF-eket e-mailben kell küldeni vagy felhőben tárolni |
| `setEmbedOriginalImages` | Az eredeti beolvasást láthatóvá teszi       | Jogi vagy megfelelőségi dokumentumok, amelyeknek meg kell őrizniük az eredeti megjelenést |
| `setLanguage` (optional) | Kényszeríti a nyelvi modellt (pl. "eng")   | Többnyelvű korpuszok, ahol az alapértelmezett automatikus felismerés hibás lehet |

---

## Kép PDF szöveggé – Gyakori buktatók és elkerülésük módja  

1. **Low‑resolution scans** – OCR pontosság drámaian csökken 150 dpi alatt. Növeld fel a forrást, mielőtt az Aspose-nek adod, vagy kérj magasabb DPI-t a szkennertől.  
2. **Rotated pages** – Ha az oldalak oldalra vannak beolvasva, engedélyezd az automatikus forgatást: `pdfOcrOptions.setAutoRotate(true);`.  
3. **Encrypted PDFs** – A motor nem tudja olvasni a jelszóval védett fájlokat; előbb dekódold őket az Aspose.PDF `PdfDocument` használatával.  
4. **Mixed raster and text** – Néhány PDF már tartalmaz rejtett szövegréteget. Az OCR újbóli futtatása duplikálhatja a szöveget. Használd a `PdfOcrOptions.setSkipExistingText(true);` beállítást az eredeti réteg megőrzéséhez.

Ezeknek a problémáknak a kezelése biztosítja, hogy a **create searchable pdf** folyamatod robusztus legyen a valós dokumentumgyűjteményekben.

---

## Teljes működő példa (Minden lépés egy fájlban)

Az alábbiakban a teljes Java osztályt találod, amelyet beilleszthetsz az IDE-dbe. Cseréld ki a `YOUR_DIRECTORY`-t a tényleges mappára.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure PDF‑specific OCR options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // higher DPI improves accuracy
        pdfOcrOptions.setCompressImages(true);           // reduce output size
        pdfOcrOptions.setEmbedOriginalImages(true);      // keep original visual fidelity

        // 3️⃣ Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");        // <-- your source file

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}