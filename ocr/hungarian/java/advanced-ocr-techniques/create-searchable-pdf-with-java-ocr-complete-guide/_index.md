---
category: general
date: 2026-05-25
description: Kereshető PDF létrehozása Java-ban az Aspose OCR segítségével. Tanulja
  meg, hogyan konvertálhat PDF-et kereshető PDF-re, hogyan tölthet be PDF-et OCR-hez,
  és hogyan gyorsíthatja GPU-val.
draft: false
keywords:
- create searchable pdf
- convert pdf to searchable pdf
- load pdf for ocr
- ocr pdf with gpu
language: hu
og_description: Kereshető PDF létrehozása Java-ban az Aspose OCR-rel. Ez az útmutató
  bemutatja, hogyan konvertálhat PDF-et kereshető PDF-be, hogyan tölthet be PDF-et
  OCR-hez, és hogyan használhat GPU gyorsítást.
og_title: Kereshető PDF létrehozása Java OCR-rel – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to convert
    PDF to searchable PDF, load PDF for OCR, and accelerate with GPU.
  headline: Create Searchable PDF with Java OCR – Complete Guide
  type: TechArticle
- description: Create searchable PDF in Java using Aspose OCR. Learn how to convert
    PDF to searchable PDF, load PDF for OCR, and accelerate with GPU.
  name: Create Searchable PDF with Java OCR – Complete Guide
  steps:
  - name: Runs OCR on each page image.
    text: Runs OCR on each page image.
  - name: Generates an invisible text layer that matches the visual content.
    text: Generates an invisible text layer that matches the visual content.
  - name: Embeds that layer into a new PDF, preserving the original appearance.
    text: Embeds that layer into a new PDF, preserving the original appearance.
  type: HowTo
tags:
- OCR
- Java
- PDF
- Aspose
title: Kereshető PDF létrehozása Java OCR-rel – Teljes útmutató
url: /hu/java/advanced-ocr-techniques/create-searchable-pdf-with-java-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása Java OCR-rel – Teljes útmutató

Valaha is szükséged volt **kereshető PDF** fájlok létrehozására beolvasott dokumentumokból, de nem tudtad, hol kezdj? Nem vagy egyedül. Sok fejlesztő ugyanabba a helyzetbe ütközik, amikor csak képet tartalmazó PDF-eket szeretne szöveg‑kereshetővé alakítani, különösen, ha a teljesítmény fontos.

Ebben a bemutatóban egy gyakorlati megoldáson keresztül vezetünk végig, amely **kereshető PDF** fájlokat hoz létre az Aspose OCR for Java használatával. Megmutatjuk, hogyan **konvertálj PDF-et kereshető PDF‑é**, **tölts be PDF-et OCR‑hez**, és még **OCR PDF‑t GPU‑val** gyorsítva – mindezt egyetlen, könnyen olvasható szkriptben. A végére lesz egy futtatható programod, és világos megértésed lesz arról, miért fontos minden egyes lépés.

> **Mit fogsz megtanulni**  
> * Egy komplett Java projekt, amely vegyes nyelvű PDF‑et olvas be  
> * GPU‑val támogatott OCR, amely felgyorsítja a feldolgozást modern hardveren  
> * Kereshető PDF kimenet, amely bármely dokumentumkezelő rendszerbe beilleszthető  

## Előfeltételek

Mielőtt belevágnánk, győződj meg róla, hogy a következők rendelkezésre állnak:

* Java 17 (vagy újabb) telepítve – a régebbi verziók hiányozhatnak a szükséges API‑kból.  
* Maven vagy Gradle a függőségkezeléshez – a példákban Maven‑t használunk.  
* Aspose OCR for Java licenc (az ingyenes próba verzió teszteléshez elegendő).  
* Egy PDF fájl, amely beolvasott oldalakat tartalmaz (a demó `mixed_lang.pdf`‑t használ).  

Ha bármelyik ismeretlennek tűnik, ne aggódj – az alábbi lépések pontos parancsokat tartalmaznak a gyors beüzemeléshez.

![Kereshető PDF létrehozása Aspose OCR Java-val](https://example.com/images/create-searchable-pdf.png "Kereshető PDF létrehozása Aspose OCR Java-val")

## 1. lépés: A projekt beállítása és **Create Searchable PDF** – Projekt inicializálás

Először hozz létre egy Maven projektet. Nyiss egy terminált, és futtasd:

```bash
mvn archetype:generate -DgroupId=com.example.ocr \
    -DartifactId=SearchablePdfDemo -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

Navigálj a mappába:

```bash
cd SearchablePdfDemo
```

Add hozzá az Aspose OCR függőséget a `pom.xml`‑hez:

```xml
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- check Maven Central for the latest -->
    </dependency>
</dependencies>
```

> **Miért fontos:** A **create searchable pdf** folyamat a `OcrEngine` osztályra támaszkodik, amely az Aspose OCR könyvtárban található. A helytelen verzióval fordítási hibákat vagy hiányzó funkciókat kapsz.

Most hozd létre a fő Java osztályt `QuickDemo.java` a `src/main/java/com/example/ocr/` könyvtárban.

## 2. lépés: GPU gyorsítás engedélyezése – **OCR PDF with GPU**

A GPU gyorsítás perceket takaríthat meg egy többoldalas OCR feladatnál. Az Aspose OCR egyetlen sorral kapcsolható be:

```java
// Enable GPU processing
engine.getEngineOptions().setUseGpu(true);
```

Ha a géped kompatibilis NVIDIA vagy AMD GPU‑val rendelkezik, és a megfelelő illesztőprogramok telepítve vannak, az OCR motor a nehéz munkát a grafikus kártyára bízza. Ellenkező esetben a hívás biztonságosan visszatér a CPU feldolgozáshoz – nem omlik össze, csak lassabb lesz a futás.

> **Pro tipp:** Linuxon előfordulhat, hogy a `LD_LIBRARY_PATH`‑t a CUDA könyvtárakra kell mutatni a JVM indítása előtt.

## 3. lépés: **Load PDF for OCR** és nyelvi támogatás beállítása

Most ténylegesen **load pdf for ocr**. Az Aspose OCR a PDF oldalakat belsőleg képként kezeli, így egyszerűen csak a fájlra mutatsz:

```java
// Load the source PDF document (image‑only PDF)
engine.getImage().loadFromFile("YOUR_DIRECTORY/mixed_lang.pdf");
```

Ezután add meg, melyik nyelvet vársz. A demónkban a thai nyelvre fókuszálunk, de átadhatsz egy nyelvválasztékot, ha a dokumentum több írásrendszert kever:

```java
engine.getEngineOptions().setLanguage(OcrLanguage.THAI);
```

Ha saját szótárad van (például domain‑specifikus kifejezések), azt is beillesztheted:

```java
engine.getEngineOptions().getSpellCorrectorOptions()
      .setUserDictionaryPath("YOUR_DIRECTORY/thai_custom.txt");
```

> **Miért állíts be nyelvet?** Az OCR pontossága a nyelvi modellen alapul. A megfelelő `OcrLanguage` megadása drámaian csökkenti a hibás felismeréseket, különösen a nem latin írásrendszerek esetén.

## 4. lépés: **Convert PDF to Searchable PDF** egy hívással

Az Aspose OCR azért kiemelkedő, mert egyetlen metódushívással **convert PDF to searchable PDF** képes végrehajtani – nincs szükség képek és szövegrétegek kézi összefűzésére.

```java
// Export a searchable PDF in a single operation
engine.saveToSearchablePdf("YOUR_DIRECTORY/mixed_lang_searchable.pdf");
```

A motor a háttérben:

1. OCR‑t futtat minden egyes oldal képen.  
2. Létrehoz egy láthatatlan szövegréteget, amely megegyezik a vizuális tartalommal.  
3. Beágyazza ezt a réteget egy új PDF‑be, megőrizve az eredeti megjelenést.

Az eredmény egy olyan fájl, amely vizuálisan megegyezik a bemenettel, de bármely PDF‑olvasó indexelni tudja.

## 5. lépés: Felismert szöveg lekérése és a kimenet ellenőrzése

Bár már elmentettünk egy kereshető PDF‑et, előfordulhat, hogy a nyers szöveget is szeretnéd naplózni vagy további feldolgozásra használni:

```java
// Output the recognized text to the console
System.out.println(engine.recognize().getText());
```

A program futtatásakor a konzolon meg kell jelennie a kinyert thai szövegnek, majd a könyvtáradban megjelenik egy új `mixed_lang_searchable.pdf` fájl.

### Várható konzolkimenet (rövidítve)

```
สวัสดีครับ นี่คือเอกสารตัวอย่าง...
...
```

Nyisd meg a generált PDF‑et az Adobe Readerben vagy bármely más nézőprogramban, nyomd meg a **Ctrl + F** kombinációt, és keresni tudsz a konzolban megjelenő szavakra. Ez bizonyítja, hogy sikeresen **create searchable pdf** fájlokat hoztunk létre.

## 6. lépés: Gyakori hibák és **Pro tippek** a nagy teljesítményű OCR‑hez

| Probléma | Tünet | Megoldás |
|----------|-------|----------|
| **GPU nem észlelhető** | Nincs gyorsulás, a motor visszatér a CPU‑ra | Győződj meg róla, hogy a CUDA illesztőprogramok telepítve vannak, és a `java.library.path` tartalmazza a GPU könyvtárakat. |
| **Hiányzó betűkészletek** | A szövegréteg torz karaktereket mutat | Telepítsd a megfelelő nyelvi betűkészleteket a host OS‑re, vagy ágyazd be őket a `engine.getEngineOptions().setEmbedFonts(true)` hívással. |
| **Nagy PDF‑ek (> 500 oldal)** | Memóriahiány hibák | Növeld a JVM heap‑et (`-Xmx4g`) és állítsd be a `engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors())` értéket, hogy a munkát több magra oszd szét. |
| **Egyéni szótár nem alkalmazódik** | A helyesírás‑javító úgy tűnik, figyelmen kívül marad | Ellenőrizd, hogy az útvonal abszolút, és a fájl UTF‑8 kódolású. |

> **Ne feledd:** A `engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors());` sor kulcsfontosságú, ha **ocr pdf with gpu**‑t szeretnél használni, és teljes mértékben ki akarod aknázni a többmagos CPU‑kat. Ez egy munkavállalót indít minden magra, így a GPU folyamatosan foglalt marad, míg a CPU a elő‑ és utófeldolgozást végzi.

## Teljes működő példa

Az alábbi kódrészlet a teljes, azonnal futtatható Java programot tartalmazza, amely minden korábban tárgyalt lépést integrál. Cseréld ki a helyőrző útvonalakat a saját könyvtáraidra.

```java
import com.aspose.ocr.*;

public class QuickDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Enable GPU acceleration and use all available CPU cores
        engine.getEngineOptions().setUseGpu(true);
        engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 3: Configure language support and a custom spell‑corrector dictionary
        engine.getEngineOptions().setLanguage(OcrLanguage.THAI);
        engine.getEngineOptions().getSpellCorrectorOptions()
              .setUserDictionaryPath("YOUR_DIRECTORY/thai_custom.txt");

        // Step 4: Load the source PDF document (this is where we **load pdf for ocr**)
        engine.getImage().loadFromFile("YOUR_DIRECTORY/mixed_lang.pdf");

        // Step 5: Export a searchable PDF in a single operation (**convert pdf to searchable pdf**)
        engine.saveToSearchablePdf("YOUR_DIRECTORY/mixed_lang_searchable.pdf");

        // Step 6: Output the recognized text to the console
        System.out.println(engine.recognize().getText());
    }
}
```

Fordítás és futtatás:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.QuickDemo"
```

Ha minden helyesen van beállítva, a konzolon megjelenik a kinyert szöveg, és egy új kereshető PDF a eredeti fájl mellett.

## Összegzés

Most bemutattuk, hogyan **create searchable pdf** fájlokat készítsünk Java‑ban az Aspose OCR segítségével, a projekt beállításától a GPU‑val gyorsított feldolgozásig. A **load pdf for OCR**, a nyelvi támogatás beállítása és a egy soros **convert pdf to searchable pdf** metódus meghívásával egy teljesen indexelhető dokumentumot kapsz, amely készen áll a keresőmotorok vagy belső visszakereső rendszerek számára.

Mi a következő? Próbáld ki a `OcrLanguage.THAI` helyett a `OcrLanguage.ENGLISH` használatát, vagy kombináld több nyelvet a többnyelvű PDF‑ekhez. Kísérletezz a `engine.getEngineOptions().setResolution(300)` beállítással, hogy lásd, a DPI hogyan befolyásolja a pontosságot, vagy ágyazz be egyedi betűkészleteket a régebbi nézők jobb megjelenítése érdekében.

Kérdésed van a teljesítményhangolással, licenceléssel vagy a workflow Spring Boot szolgáltatásba való integrálásával kapcsolatban? Írj kommentet alább, vagy nézd meg az Aspose OCR Java dokumentációt a mélyebb részletekért. Boldog kódolást, és élvezd, ahogy a statikus beolvasott anyagok kereshető kincsekké válnak!

## Kapcsolódó bemutatók

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}