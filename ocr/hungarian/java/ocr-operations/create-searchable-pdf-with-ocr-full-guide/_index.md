---
category: general
date: 2026-06-22
description: Készíts kereshető PDF-et OCR-rel Java-ban. Tanuld meg, hogyan tiltsd
  le a tömörítést, és hogyan alakítsd gyorsan a beolvasott képes PDF-et kereshető
  PDF-é.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- ocr to searchable pdf
- how to disable compression
- pdf without compression
language: hu
og_description: Kereshető PDF létrehozása OCR-rel Java-ban. Ez az útmutató bemutatja,
  hogyan lehet letiltani a tömörítést, átalakítani a beolvasott képes PDF-et, és tömörítés
  nélküli PDF-et generálni.
og_title: Kereshető PDF létrehozása OCR-rel – Teljes Java oktatóanyag
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  headline: Create Searchable PDF with OCR – Full Guide
  type: TechArticle
- description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  name: Create Searchable PDF with OCR – Full Guide
  steps:
  - name: Set the output format to `PDF_SEARCHABLE`.
    text: Set the output format to `PDF_SEARCHABLE`.
  - name: Turn off PDF compression with `PdfCompression.NONE`.
    text: Turn off PDF compression with `PdfCompression.NONE`.
  - name: Run OCR and capture the `PdfDocument`.
    text: Run OCR and capture the `PdfDocument`.
  - name: Save the file to disk.
    text: Save the file to disk.
  type: HowTo
tags:
- OCR
- PDF
- Java
- Document Processing
title: Kereshető PDF létrehozása OCR-rel – Teljes útmutató
url: /hu/java/ocr-operations/create-searchable-pdf-with-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása OCR-rel – Teljes útmutató

Volt már szükséged **kereshető PDF** létrehozására egy sor beolvasott képből, de nem tudtad, mely beállításokat kell módosítani? Nem vagy egyedül – a legtöbb fejlesztő ugyanabba a helyzetbe ütközik, amikor a kimenet egy hatalmas, olvashatatlan tömb lesz.

Ebben az útmutatóban egy tiszta, vég‑től‑végig példán keresztül mutatjuk be, hogyan **hozzunk létre kereshető PDF-et** egy Java OCR motor használatával, **alakítsuk át a beolvasott képet PDF-é**, és, ami különösen fontos, **hogyan kapcsoljuk ki a tömörítést**, hogy a kapott fájl hű maradjon az eredeti méretekhez. A végére egy azonnal futtatható kódrészletet és alapos megértést kapsz arról, miért fontos minden beállítás.

## Mit fogsz megtanulni

* Hogyan konfiguráljuk az OCR motort **kereshető PDF-re ocr-oláshoz**.  
* A PDF tömörítés kikapcsolásának oka, és hogyan kapunk **PDF-t tömörítés nélkül**.  
* Egy komplett Java program, amely beolvasott képet vesz, OCR-t futtat, és **kereshető PDF-et** ment.  
* Tippek a szélhelyzetek kezeléséhez, például többoldalas beolvasások vagy alacsony felbontású források esetén.  

**Előfeltételek** – Java 8+ telepítve, egy kompatibilis OCR SDK (a kód az ABBYY FineReader Engine API-t használja, de a koncepciók bármely olyan könyvtárra alkalmazhatók, amely támogatja a `setOutputFormat` és `setPdfCompression` metódusokat). Egy IDE, mint az IntelliJ IDEA vagy az Eclipse megkönnyíti a munkát, de egy egyszerű szövegszerkesztő is megfelel.

---

![Kereshető PDF létrehozásának munkafolyamata](image-placeholder.png "Diagram a kereshető PDF folyamatáról beolvasott képekből a végső PDF-ig")

## 1. lépés: Állítsd be az OCR motort **Kereshető PDF létrehozására**

Az első dolog, amit az OCR motorral közölnöd kell, az a kívánt kimenet típusa. Alapértelmezés szerint sok SDK egyszerű szöveget vagy raszteres PDF-et ad ki, ami nem kereshető. A formátum átváltása elvégzi a nehéz munkát helyetted.

```java
// Step 1: Tell the engine we want a searchable PDF
engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

*Miért fontos ez*: A `PDF_SEARCHABLE` jelző azt utasítja a motort, hogy egy láthatatlan szövegréteget ágyazzon a beolvasott kép alá. A keresőeszközök ezután indexelni tudják a dokumentumot, így úgy viselkedik, mint bármely natív PDF, amelyet az Adobe Reader-ben nyitsz meg.

## 2. lépés: Tömörítés letiltása – **Hogyan kapcsoljuk ki a tömörítést** helyesen

Ha kihagyod ezt a lépést, a motor minden oldalt tömörít a helytakarékosság érdekében, de a tömörítés elmoshatja a finom részleteket – ami különösen problémás, ha később nagy felbontású képeket szeretnél kinyerni.

```java
// Step 2: Turn off PDF compression to keep original image quality
engine.getConfig().setPdfCompression(PdfCompression.NONE);
```

**Pro tipp**: A tömörítés letiltása elengedhetetlen, ha jogi dokumentumokat vagy orvosi beolvasásokat archiválsz, ahol minden pixel számít. A kapott fájl nagyobb lehet, de megőrzöd az eredeti méreteket és tisztaságot.

## 3. lépés: OCR végrehajtása és a kapott dokumentum lekérése

Miután a motor tudja, milyen kimenetet kell előállítania és hogyan kezelje a képeket, futtathatod a felismerést. A hívás egy `PdfDocument` objektumot ad vissza, amely készen áll a mentésre vagy további manipulációra.

```java
// Step 3: Run OCR and capture the searchable PDF in memory
PdfDocument pdf = engine.recognizeToPdf();
```

*Mi történik a háttérben?* A motor minden bemeneti oldalt feldolgozza, karakterfelismerést végez, és a rejtett szövegréteget a képre varrja. Ha több oldalad van, azok automatikusan összefűződnek.

## 4. lépés: **Kereshető PDF** mentése lemezre

Végül írd a memóriában lévő PDF-et egy fájlba. Válassz egy olyan helyet, ahol írási jogosultságod van, és adj a fájlnak egy értelmes nevet.

```java
// Step 4: Persist the searchable PDF on disk
pdf.save("YOUR_DIRECTORY/searchable.pdf");
```

Amikor megnyitod a `searchable.pdf` fájlt egy megjelenítőben, észre fogod venni, hogy ki tudod jelölni és keresni a szöveget – még akkor is, ha a látható tartalom továbbra is az eredeti beolvasott kép.

### Teljes működő példa

Az alábbi önálló Java osztály négy lépést egyesít. Nyugodtan másold be, állítsd be a bemeneti útvonalat, és futtasd úgy, ahogy van.

```java
import com.abbyy.ocrsdk.Engine;
import com.abbyy.ocrsdk.OcrOutputFormat;
import com.abbyy.ocrsdk.PdfCompression;
import com.abbyy.ocrsdk.PdfDocument;

/**
 * Demonstrates how to create searchable PDF from scanned images.
 * This example uses the ABBYY FineReader Engine Java API.
 */
public class SearchablePdfCreator {

    public static void main(String[] args) {
        // ---- 1. Initialize the OCR engine -------------------------------------------------
        Engine engine = new Engine();
        // (Assume license activation and engine initialization are handled elsewhere)

        // ---- 2. Configure output to be a searchable PDF ----------------------------------
        engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);

        // ---- 3. Disable compression for a PDF without compression -------------------------
        engine.getConfig().setPdfCompression(PdfCompression.NONE);

        // ---- 4. Load the scanned image(s) --------------------------------------------------
        // For simplicity, we let the engine auto‑detect images in the working folder.
        // You could also call engine.addImage("path/to/image.tif") for explicit control.
        engine.addImage("YOUR_DIRECTORY/scanned-page.tif");

        // ---- 5. Perform OCR and retrieve the PDF -----------------------------------------
        PdfDocument pdf = engine.recognizeToPdf();

        // ---- 6. Save the result -----------------------------------------------------------
        pdf.save("YOUR_DIRECTORY/searchable.pdf");

        System.out.println("✅ Searchable PDF created successfully at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**Várható kimenet** – A program futtatása után a fenti konzolüzenetet fogod látni, és a `searchable.pdf` fájl megjelenik a `YOUR_DIRECTORY` könyvtárban. Bármely PDF-olvasóban megnyitva a következőket teheted:

* Szöveg kiemelése.  
* A beépített keresés (Ctrl + F) használata a szavak megtalálásához.  
* A rejtett szövegréteg exportálása, ha szükséges.  

---

## Miért kapcsoljuk ki a tömörítést? A **PDF tömörítés nélkül** megértése

Elgondolkodhatsz: „Nem lenne-e a tömörítés mindig jó ötlet?” A válasz árnyalt:

| Helyzet | Tömörítés megtartása (`NORMAL`) | Tömörítés letiltása (`NONE`) |
|-----------|-----------------------------|------------------------------|
| Jogi szerződések archiválása | ❌ Megváltoztathatja a pixel pontosságot | ✅ Garantálja az eredeti megjelenést |
| Nagy mennyiségű alacsony felbontású beolvasás | ✅ Helyet takarít meg | ❌ Növeli a méretet előny nélkül |
| OCR pontosságra van szükség apró betűk esetén | ❌ Elmosja a finom részleteket | ✅ Megőrzi minden vonást |

## Beolvasott kép PDF közvetlen átalakítása

Néha már van egy PDF-ed, amely beolvasott képeket tartalmaz (egy „csak képet tartalmazó PDF”). Ahhoz, hogy **beolvasott kép PDF-et** kereshető változattá alakítsd, a teljes PDF-et átadhatod a motorba az egyes képek helyett:

```java
engine.addPdf("YOUR_DIRECTORY/scanned-image-only.pdf");
PdfDocument searchable = engine.recognizeToPdf();
searchable.save("YOUR_DIRECTORY/searchable-from-pdf.pdf");
```

Ugyanazok a konfigurációs jelzők (`PDF_SEARCHABLE` és `PdfCompression.NONE`) érvényesek, így **pdf-t tömörítés nélkül** kapsz még akkor is, ha PDF konténerből indulsz.

## Gyakori buktatók és hogyan kerüld el őket

* **Elfelejtetted beállítani a kimeneti formátumot** – A motor alapértelmezés szerint raszteres PDF-et ad, ami nem kereshető. Mindig hívd meg a `setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE)` metódust a `recognizeToPdf()` előtt.  
* **Memóriahiány nagy mennyiségű feldolgozásnál** – Tölts be és dolgozz fel oldalakat darabokban, vagy használd a streaming API-t, ha a SDK-d biztosít ilyet.  
* **Helytelen fájlútvonalak** – Használj abszolút útvonalakat vagy győződj meg róla, hogy a munkakönyvtár helyesen van beállítva; különben a `pdf.save()` `IOException`-t dob.  
* **Licenc nincs aktiválva** – A legtöbb kereskedelmi OCR SDK érvényes licencet igényel; ha hiányzik, a motor futásidejű kivételt dob.  

---

## Következtetés

Most már egy komplett, azonnal futtatható megoldással rendelkezel, amely bemutatja, **hogyan hozzunk létre kereshető PDF fájlokat** beolvasott képekből, hogyan **alakítsuk át a beolvasott kép PDF-et**, és pontosan **hogyan kapcsoljuk ki a tömörítést**, hogy **pdf-t tömörítés nélkül** kapjunk. A kulcsfontosságú lépések:

1. Állítsd be a kimeneti formátumot `PDF_SEARCHABLE`-ra.  
2. Kapcsold ki a PDF tömörítést a `PdfCompression.NONE` használatával.  
3. Futtasd az OCR-t és rögzítsd a `PdfDocument` objektumot.  
4. Mentsd a fájlt lemezre.  

Innen tovább kísérletezhetsz betűtípusokkal, vízjelek hozzáadásával, vagy egész mappák kötegelt feldolgozásával. Ha érdekel az OCR nyelvi csomagok hozzáadása, többoldalas TIFF-ek kezelése, vagy a munkafolyamat webszolgáltatásba való integrálása, nézd meg a közeljövőben megjelenő útmutatóinkat a „OCR nyelvválasztás Java-ban” és a „Streaming OCR nagy dokumentumkészletekhez” témakörökben.

Van kérdésed, vagy hibát találtál? Hagyj egy megjegyzést alább – jó kódolást, és élvezd az újonnan kereshető PDF-eket!

## Mit érdemes következőként megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett működő kódrészleteket tartalmaz lépésről-lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [PDF szöveg felismerése – OCR műveletek Aspose.OCR for Java-val](/ocr/english/java/ocr-operations/)
- [OCR PDF dokumentumok felismerése Aspose.OCR for Java-ban](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Képek konvertálása PDF-re C# – Többoldalas OCR eredmény mentése](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}