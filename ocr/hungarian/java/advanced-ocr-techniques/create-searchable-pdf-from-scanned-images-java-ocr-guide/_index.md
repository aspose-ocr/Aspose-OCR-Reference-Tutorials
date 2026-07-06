---
category: general
date: 2026-06-22
description: Készíts kereshető PDF-et Java-ban az Aspose OCR-rel. Tanulja meg, hogyan
  konvertáljon beolvasott PDF-et, kezelje a vegyes nyelvű OCR-t, és növelje a pontosságot.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- how to ocr document
- mixed language ocr
- aspose ocr java
language: hu
og_description: Kereshető PDF létrehozása Java-ban az Aspose OCR használatával. Ez
  az útmutató bemutatja, hogyan lehet OCR-rel feldolgozni egy dokumentumot, kezelni
  a vegyes nyelvű szöveget, és kimenetként kereshető PDF-et előállítani.
og_title: Kereshető PDF létrehozása beolvasott képekből – Java OCR útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Java with Aspose OCR. Learn how to convert
    scanned PDF, handle mixed language OCR and boost accuracy.
  headline: Create Searchable PDF from Scanned Images – Java OCR Guide
  type: TechArticle
- description: Create searchable PDF in Java with Aspose OCR. Learn how to convert
    scanned PDF, handle mixed language OCR and boost accuracy.
  name: Create Searchable PDF from Scanned Images – Java OCR Guide
  steps:
  - name: Expected Output
    text: 'When you open `processed.pdf` in Adobe Reader (or any PDF viewer), you
      should be able to:'
  - name: 1. What if my document contains more than two languages?
    text: '`config.setLanguage` accepts a var‑args list, so you can pass as many `OcrLanguage`
      constants as you need:'
  - name: 2. Can I run this on a headless server without a GPU?
    text: Absolutely. Set `config.setUseGpu(false)` or simply omit the call. The engine
      will fall back to multi‑core CPU processing, which is still fast thanks to the
      thread pool we configured.
  - name: 3. How do I handle huge PDFs (hundreds of pages)?
    text: Aspose OCR streams pages one‑by‑one, so memory usage stays modest. However,
      you might want to split the PDF into smaller chunks using Aspose PDF’s `split`
      method, process each chunk, then merge the results back together.
  - name: 4. Is there a way to keep the original PDF’s metadata (author, creation
      date)?
    text: 'Yes. After you obtain `searchablePdf`, you can copy metadata from the original
      PDF:'
  type: HowTo
tags:
- OCR
- Java
- PDF
title: Kereshető PDF létrehozása beolvasott képekből – Java OCR útmutató
url: /hu/java/advanced-ocr-techniques/create-searchable-pdf-from-scanned-images-java-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása beolvasott képekből – Java OCR útmutató

Gondolkodtál már azon, hogyan **hozhatsz létre kereshető PDF-et** egy csomó beolvasott oldalból anélkül, hogy hatalmas összeget költenél harmadik fél szolgáltatásaira? Nem vagy egyedül. Sok fejlesztő ugyanabba a problémába ütközik, amikor **beolvasott PDF** fájlokat kell **átalakítani** olyanná, amit a felhasználók ténylegesen kereshetnek.  

Ebben az útmutatóban egy teljes, futtatható példán keresztül vezetünk, amely a **Aspose OCR for Java**-t használja **hogyan OCR‑eljünk dokumentumszintű** feladatokat, megoldja a **kevert nyelvű OCR**-t, és végül egy kifinomult kereshető PDF-et állít elő. A végére egy önálló programod lesz, amelyet bármely Maven vagy Gradle projektbe beilleszthetsz, és már ma elkezdheted a dokumentumok feldolgozását.

## Előkövetelmények – Amire szükséged lesz

- Java 17 (vagy bármely friss JDK) telepítve és a PATH‑on beállítva.  
- Egy IDE vagy szerkesztő, amiben kényelmesen dolgozol (IntelliJ IDEA, Eclipse, VS Code…).  
- Aspose.OCR for Java könyvtár – a legújabb JAR‑t letöltheted az [Aspose Maven repository](https://repo.aspose.com/repo/com/aspose/aspose-ocr/) oldalról.  
- Egy többoldalas beolvasott PDF, amelyet kereshetővé szeretnél tenni.  
- (Opcionális) GPU‑t támogató gép, ha a `setUseGpu(true)` használatával szeretnél gyorsabb feldolgozást.

Ha ezek a komponensek készen állnak, akkor egyszerűen másolhatod a lenti kódot, és **Run**‑ra kattintva futtathatod, anélkül hogy hiányzó függőségeket keresnél.

## 1. lépés: A projekt beállítása és az Aspose OCR importálása

Először hozz létre egy új Maven modult (vagy Gradle projektet), és add hozzá az Aspose OCR függőséget:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- replace with the latest version -->
</dependency>
```

Ha a Gradle-t részesíted előnyben, az ekvivalens sor a következő:

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

Miután a build szinkronizálódik, importálni tudod a szükséges osztályokat.

## 2. lépés: Az OCR motor inicializálása

A motor létrehozása egyszerű, de érdemes megérteni, miért csináljuk ezt korán. A `OcrEngine` objektum tartalmazza a konfigurációt, a szálkezelést és a GPU beállításokat, amelyek minden későbbi műveletet befolyásolnak.

```java
import com.aspose.ocr.*;

public class AdvancedOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine – this is the heart of the create searchable pdf process
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pro tipp:** A motor egyszeri példányosítása és többszöri újrahasználata több fájl esetén csökkenti a terhelést, különösen, ha PDF‑k kötegét dolgozod fel.

## 3. lépés: A beolvasott PDF (vagy képfolyam) betöltése

Az Aspose OCR képfolyamokkal dolgozik, ezért közvetlenül a beolvasott PDF‑et adjuk át. A könyvtár belsőleg rasterizálja az egyes oldalakat, ezért egy PDF‑ből egy lépésben indulhatsz ki, és egy kereshető PDF‑et kapsz.

```java
        // Load the source PDF – replace the path with your actual file location
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page_scanned.pdf"));
```

Ha helyette TIFF‑ek vagy JPEG‑ek gyűjteménye van, egyszerűen a `ImageStream.fromFile`‑t irányítsd ezekre a fájlokra; a csővezeték többi része változatlan marad.

## 4. lépés: OCR beállítások finomhangolása kevert nyelvi támogatáshoz

Itt mutatkozik meg a **kevert nyelvi OCR** ereje. Több `OcrLanguage` enum átadásával azt mondod a motornak, hogy ugyanazon az oldalon keressen angol és orosz (vagy bármely más kombináció) szöveget.

```java
        // Grab the mutable config object
        OcrConfig config = ocrEngine.getConfig();

        // Enable English + Russian detection – you can add more languages as needed
        config.setLanguage(OcrLanguage.ENGLISH, OcrLanguage.RUSSIAN);

        // Speed vs. accuracy trade‑off: use all available cores
        config.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Turn on GPU acceleration if the runtime detects a compatible device
        config.setUseGpu(true);

        // Spell‑check improves accuracy for noisy scans
        config.setEnableSpellCorrection(true);

        // Tell Aspose we want a searchable PDF as the final output
        config.setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

> **Miért fontos:** Ha nem adod meg a nyelveket, a motor alapértelmezés szerint csak angolt használ, ami drámaian csökkenti a felismert arányt a cirill vagy más írásrendszert tartalmazó dokumentumok esetén.

## 5. lépés: Előfeldolgozó szűrők hozzáadása a beolvasás tisztításához

A beolvasott PDF‑ek gyakran sikkadtak, foltosak vagy alacsony kontrasztúak. Egy `DeskewFilter` és egy `DenoiseFilter` hozzáadása segít az OCR motornak a karaktereket tisztábban látni.

```java
        // Set up image preprocessing
        ImagePreprocessOptions preprocess = new ImagePreprocessOptions();
        preprocess.addFilter(new DeskewFilter());   // Straighten tilted pages
        preprocess.addFilter(new DenoiseFilter()); // Reduce background noise
        ocrEngine.setPreprocessOptions(preprocess);
```

További szűrőket is láncolhatsz – például `ContrastFilter` vagy `BinarizationFilter` – ha a forrásanyag különösen piszkos.

## 6. lépés: OCR futtatása és a kereshető PDF generálása

Most kezdődik a nehéz munka. A `recognizeToPdf()` hívás lefuttatja az OCR csővezetéket, alkalmazza az előfeldolgozó lépéseket, és a felismert szöveget egy láthatatlan szövegrétegként írja a PDF‑be.

```java
        // Perform OCR and retrieve a searchable PDF document object
        PdfDocument searchablePdf = ocrEngine.recognizeToPdf();
```

A visszakapott `PdfDocument` egy teljes értékű Aspose PDF objektum, ami azt jelenti, hogy a mentés előtt további metaadatokat szerkeszthetsz, könyvjelzőket adhatsz hozzá, vagy más PDF‑ekkel egyesítheted.

## 7. lépés: Az eredmény mentése és ellenőrzése

Végül írd ki a kimenetet a lemezre. A konzol üzenet gyors vizuális visszajelzést ad, hogy minden rendben működött.

```java
        // Save the searchable PDF to the desired location
        searchablePdf.save("YOUR_DIRECTORY/processed.pdf");
        System.out.println("OCR completed – searchable PDF saved at YOUR_DIRECTORY/processed.pdf");
    }
}
```

### Várható kimenet

Amikor megnyitod a `processed.pdf`-et az Adobe Readerben (vagy bármely PDF‑nézőben), a következőket kell tudnod:

1. **Szöveg kijelölése** – kattints és húzd az egeret egy szó felett, majd másold.  
2. **Keresés** – nyomd meg a `Ctrl+F`-et, és írj be egy kifejezést, amely a eredeti beolvasások valamelyikén szerepel.  
3. **Az eredeti elrendezés megőrzése** – a vizuális megjelenés azonos marad a beolvasott forrással; csak egy láthatatlan szövegréteg lett hozzáadva.

Ha torz karaktereket vagy hiányzó oldalakat látsz, ellenőrizd a nyelvi beállításokat, és győződj meg arról, hogy a forrás PDF nincs jelszóval védve.

## Gyakori kérdések és különleges esetek

### 1. Mi van, ha a dokumentum több mint két nyelvet tartalmaz?

`config.setLanguage` változó‑argumentum listát fogad, így annyi `OcrLanguage` konstanst adhatunk meg, amennyire szükség van:

```java
config.setLanguage(OcrLanguage.ENGLISH, OcrLanguage.RUSSIAN, OcrLanguage.CHINESE_SIMPLIFIED);
```

Csak ne feledd, hogy minden további nyelv kissé megnöveli a feldolgozási időt.

### 2. Futtatható ez fej nélküli szerveren GPU nélkül?

Természetesen. Állítsd be `config.setUseGpu(false)`‑t, vagy egyszerűen hagyd ki a hívást. A motor visszatér a többmagos CPU feldolgozáshoz, amely a konfigurált szálkészletnek köszönhetően továbbra is gyors.

### 3. Hogyan kezeljem a hatalmas PDF‑eket (száz oldalakat)?

Az Aspose OCR egyesével streameli az oldalakat, így a memóriahasználat mérsékelt marad. Azonban érdemes lehet a PDF‑et kisebb darabokra bontani az Aspose PDF `split` metódusával, minden darabot feldolgozni, majd az eredményeket újra összeolvasztani.

### 4. Van mód megőrizni az eredeti PDF metaadatait (szerző, létrehozás dátuma)?

Igen. Miután megkaptad a `searchablePdf`-et, másolhatod a metaadatokat az eredeti PDF‑ből:

```java
PdfDocument original = new PdfDocument("YOUR_DIRECTORY/multi_page_scanned.pdf");
searchablePdf.getInfo().setAuthor(original.getInfo().getAuthor());
// repeat for other metadata fields
```

## Profi tippek a termelés‑kész OCR-hez

- **Kötegelt feldolgozás:** Csomagold az egész folyamatot egy ciklusba, amely egy könyvtár fájljait iterálja. Használd újra egyetlen `OcrEngine` példányt, hogy elkerüld az ismételt inicializációs terhet.  
- **Hibakezelés:** Kapd el az `OcrException`‑t, hogy naplózd a sikertelen fájlokat, majd folytasd a következő dokumentummal.  
- **Teljesítményfigyelés:** Használd a `System.nanoTime()`‑t a `recognizeToPdf()` előtt és után, hogy naplózd az egyes fájlok feldolgozási idejét; ez segít eldönteni, hogy fel kell-e skálázni egy felhő‑munkaerő poolra.  
- **Biztonság:** Ha érzékeny dokumentumokat kezelsz, fontold meg a kimeneti PDF titkosítását a `searchablePdf.encrypt(...)` használatával a mentés előtt.

## Összegzés

Most mindent áttekintettünk, ami ahhoz szükséges, hogy **kereshető PDF** fájlokat hozz létre beolvasott forrásokból a **Aspose OCR for Java** segítségével. Az útmutató megmutatta, hogyan **alakítsd át a beolvasott PDF‑et**, hogyan konfiguráld a **kevert nyelvi OCR‑t**, és hogyan finomhangold az előfeldolgozó szűrőket – mindezt úgy, hogy a kód tömör és termelés‑kész legyen.  

Innen tovább felfedezheted az OCR‑generált bélyegképek hozzáadását, egy dokumentumkezelő rendszerrel való integrációt, vagy akár a kinyert szöveg betáplálását egy keresőindexbe, például Elasticsearch‑be. A lehetőségek olyan széleskörűek, mint a digitalizálandó dokumentumok.  

Van még kérdésed a **hogyan OCR‑eljünk dokumentumot** Java‑ban, vagy szeretnél mélyebben belemerülni a PDF manipulációba? Hagyj egy megjegyzést alább, és jó kódolást!

## Mit érdemes még megtanulni?

Az alábbi útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API‑funkciókat, és alternatív megvalósítási megközelítéseket fedezhess fel saját projektjeidben.

- [PDF szöveg felismerése – OCR műveletek Aspose.OCR for Java-val](/ocr/english/java/ocr-operations/)
- [OCR PDF dokumentumok felismerése Aspose.OCR for Java-ban](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Hogyan OCR‑elj PDF-et .NET‑ben az Aspose.OCR használatával](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}