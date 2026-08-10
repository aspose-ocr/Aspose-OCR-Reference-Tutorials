---
category: general
date: 2026-05-06
description: Készíts kereshető PDF-et egy képből az Aspose OCR Java használatával.
  Tanulja meg, hogyan konvertálja a képet PDF-be, engedélyezze a helyesírási javítást,
  és használja az OCR GPU-t a gyors eredményekért.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- enable spell correction
- use ocr gpu
- process image ocr
language: hu
og_description: Készítsen kereshető PDF-et egy képből az Aspose OCR Java használatával.
  Ez az útmutató bemutatja, hogyan konvertálja a képet PDF-be, hogyan engedélyezze
  a helyesírási javítást, és hogyan használja az OCR GPU-t.
og_title: Készíts kereshető PDF-et képből Java OCR-rel
tags:
- OCR
- Java
- PDF
title: Kereshető PDF létrehozása képből Java OCR-rel
url: /hu/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása képből Java OCR-rel

Valaha szükséged volt **kereshető PDF** létrehozására egy beolvasott képből, de nem tudtad, hol kezdj? Nem vagy egyedül – a legtöbb fejlesztő ezzel a problémával találkozik, amikor először foglalkozik képalapú PDF‑ekkel. Szerencsére az Aspose OCR for Java‑val **konvertálhatod a képet PDF‑be**, a szöveget választható tartalommá alakíthatod, és még helyesírási javítást is hozzáadhatsz a kifinomult eredményhez.

Ebben a bemutatóban egy teljes, azonnal futtatható példán keresztül mutatjuk be, hogyan **használhatod az OCR GPU‑t**, ha elérhető, hogyan **feldolgozhatod hatékonyan a képet OCR‑rel**, és miért fontos a helyesírási javítás engedélyezése a későbbi kereséshez. A végére egy egykattintásos megoldást kapsz, amellyel kereshető PDF‑et generálhatsz, amelyet felhasználóknak szállíthatsz vagy archiválhatsz megfelelőség céljából.

> **Pro tipp:** Ha olyan gépen futtatod, amelynek nincs GPU-ja, a kód elegánsan visszatér a CPU‑ra, így nem kell semmit átírnod.

---

## Amire szükséged lesz

- **Java 8+** (a kód JDK 8‑kal és újabb verziókkal fordítható)
- **Aspose OCR for Java** könyvtár (töltsd le a legújabb JAR‑t az Aspose weboldaláról)
- Egy **bemeneti kép** (JPEG, PNG, TIFF stb.), amelyet kereshető PDF‑é szeretnél alakítani
- (Opcionális) **GPU** CUDA‑támogatással, ha a lehető leggyorsabb felismerést szeretnéd

Nincs szükség extra keretrendszerekre, Maven/Gradle varázslatra – csak egy JAR a classpath‑on, és már indulhat a munka.

## 1. lépés: Az OCR motor inicializálása – A folyamat szíve  

Először létrehozunk egy `OcrEngine` példányt, és a forrásfájlra mutatunk. Ez az objektum a munkavégző, amely beolvassa a képet, futtatja a neurális hálót, és visszaadja a szöveget.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to convert
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

*Miért fontos:* A motor egyszeri inicializálása és újrahasználata elkerüli a natív könyvtárak többszöri betöltésének költségét – egy apró teljesítményelőny, amely sok fájl kötegelt feldolgozásakor összeadódik.

## 2. lépés: A feldolgozó eszköz kiválasztása – Használd az OCR GPU‑t, ha lehetséges  

Ha a munkaállomásod kompatibilis GPU‑val rendelkezik, megmondhatod az Aspose‑nak, hogy a nehéz feladatot arra bízza. Ellenkező esetben a motor automatikusan CPU‑ra vált.

```java
        // Prefer GPU; fall back to CPU if no compatible device is found
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
```

*Mi a haszon?* A GPU‑gyorsítás másodperceket spórolhat minden egyes oldalon, különösen nagy felbontású beolvasásoknál. A visszaesés biztosítja, hogy ugyanaz a kód mindenhol működjön, ezért ajánljuk a **use OCR GPU** beállítást alapértelmezettként.

## 3. lépés: A beolvasás felgyorsítása – Használd ki az összes CPU magot  

Még ha a GPU is le van terhelve, a környező előfeldolgozó lépések párhuzamosíthatók. A szálak számának beállítása a rendelkezésre álló processzorok számával lehetővé teszi, hogy a motor egyszerre több darabot dolgozzon fel.

```java
        // Use all logical cores for preprocessing and language detection
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());
```

*Megjegyzés:* Egy 4‑magos laptop négy szálat indít; egy 16‑magos munkaállomás a teljes előnyt élvezi. Csak tartsd szem előtt, hogy több szál nagyobb memóriahasználatot jelent.

## 4. lépés: A kép tisztítása – Előfeldolgozó szűrők  

Egy homályos vagy zajos beolvasás szemét szöveget eredményez. Néhány beépített szűrő hozzáadása drámai módon javítja a pontosságot.

```java
        // Deskew the image so text lines are horizontal
        ocrEngine.getPreprocessing().add(new DeskewFilter());

        // Remove speckles and background noise
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());
```

*Miért ezek a szűrők?* A `DeskewFilter` korrigálja a forgatást, amely gyakran előfordul, ha a dokumentumot szögben helyezik a szkennerbe. A `NoiseRemovalFilter` eltávolítja a szóró pixeleket, amelyek egyébként karakterként lennének értelmezve. Olyan, mintha a OCR motor egy tiszta papírlapra olvasna.

## 5. lépés: Okos funkciók bekapcsolása – Helyesírás-ellenőrzés és automatikus nyelvfelismerés engedélyezése  

Ha többnyelvű dokumentumokkal dolgozol, vagy egyszerűen kevesebb hibát szeretnél, kapcsold be a beépített helyesírás-ellenőrzőt, és engedd, hogy a motor kitalálja a nyelvet.

```java
        // Activate spell correction to fix common OCR mistakes
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Let the engine automatically detect the language of the input
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

*Mikor hasznos?* Tegyük fel, hogy a beolvasás tartalmaz angol és spanyol szakaszokat is. Az automatikus felismerés futás közben váltogatja a szótárakat, míg a helyesírás-ellenőrzés kijavítja a „0”‑t „O”‑ra hasonló hibákat. Ez a lépés elengedhetetlen egy **kereshető PDF** előállításához, amely valóban helyes eredményeket ad.

## 6. lépés: Az eredmény mentése – Kép konvertálása PDF‑be és kereshetővé tétele  

Végül megkérjük a motort, hogy írjon ki egy PDF‑et, ahol az eredeti kép egy láthatatlan szövegréteg mögött helyezkedik el. Ez a klasszikus **convert image to PDF** munkafolyamat, de a PDF most már kereshető.

```java
        // Generate a searchable PDF – the text layer sits behind the original image
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

A kimeneti fájl (`output-searchable.pdf`) bármely PDF‑olvasóval megnyitható; a szöveget kiválaszthatod, másolhatod és keresheted, mintha natív PDF‑ről lenne szó. Külön eszközök nem szükségesek.

## Teljes működő példa – Másolj és futtasd  

Az alábbi kódrészlet a teljes program, készen áll a fordításra. Cseréld le a `YOUR_DIRECTORY`‑t arra a mappára, amelyik a `input.jpg`‑t tartalmazza.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine and load the source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 2: Select the processing device (GPU if available, otherwise CPU)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Step 3: Use all available CPU cores to speed up recognition
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 4: Add preprocessing filters to improve image quality
        ocrEngine.getPreprocessing().add(new DeskewFilter());
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());

        // Step 5: Enable spell correction and automatic language detection
        ocrEngine.getSettings().setEnableSpellCorrection(true);
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // Step 6: Perform OCR and save the result as a searchable PDF
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

**Várható kimenet:** A program futtatásakor a konzolon megjelenik a *„Searchable PDF generated successfully.”* sor. Az `output-searchable.pdf` megnyitása az Adobe Reader‑ben lehetővé teszi, hogy a képen lévő szóból beírj egy keresett kifejezést, és az azonnal a megfelelő helyre ugrik.

## Gyakori kérdések és szélsőséges esetek  

- **Mi van, ha a GPU nem kerül felismerésre?**  
  A `setDeviceType(OcrDeviceType.GPU)` hívás nem dob kivételt; csak azt utasítja a motort, hogy először próbálja meg a GPU‑t. Ha ez nem sikerül, a motor csendben visszatér a CPU‑ra.

- **Feldolgozhatok több képet egy futtatás során?**  
  Igen. A kódot egy ciklusba helyezheted, minden iterációban megváltoztatva a fájlnevet, és ugyanazt az `OcrEngine` példányt újrahasználva alacsony memóriaigény mellett.

- **A PDF‑em hatalmas – hogyan tudom lecsökkenteni?**  
  OCR után használhatod az Aspose PDF optimalizáló API‑kat, vagy egyszerűen lecsökkentheted a forráskép felbontását a motorba való betáplálás előtt (`ImageStream.fromFile(...).setResolution(150)` 150 DPI‑ra).

- **Meg kell őriznem az eredeti kép felbontását jogi megfelelés miatt.**  
  A `PDF_SEARCHABLE` formátum pontosan megőrzi az eredeti bitmapet; a láthatatlan szövegréteg felül kerül anélkül, hogy a vizuális minőséget befolyásolná.

## Vizuális összefoglaló  

![create searchable pdf example](placeholder-image.png "create searchable pdf example")

*Alt szöveg:* *kereshető pdf példa – Java OCR motor, amely egy beolvasott JPG‑t kereshető PDF‑vé alakít.*

## Következtetés  

Most már rendelkezel egy **teljes, vég‑től‑végig megoldással**, amely bármely képet **kereshető PDF‑vé** alakít az Aspose OCR for Java segítségével. A **kép konvertálása PDF‑be**, a **helyesírás-ellenőrzés engedélyezése** és a **OCR GPU használata** (ha lehetséges) gyors, pontos és kereshető eredményeket biztosít, amelyek platformfüggetlenül működnek.

Mi a következő? Próbálj ki:

- **Különböző kimeneti formátumokat** (`PDF`, `DOCX`, `HTML`), hogy lásd, hogyan viselkedik a szövegréteg.
- **Egyedi szótárakat**, ha domain‑specifikus zsargont dolgozol fel.
- **Kötegelt feldolgozást**, hogy automatikusan több ezer beolvasást kezelj.

Nyugodtan módosítsd a szálak számát, cseréld ki a szűrőket, vagy építs be saját előfeldolgozó csővezetékedet. A fő minta változatlan marad: betöltés → előfeldolgozás → konfigurálás → OCR → mentés.

Boldog kódolást, és legyenek a PDF‑jeid mindig kereshetők!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}