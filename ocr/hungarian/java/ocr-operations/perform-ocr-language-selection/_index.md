---
date: 2026-06-24
description: Tanulja meg, hogyan OCR-eljük a képen lévő szöveget nyelvválasztással
  az Aspose.OCR for Java használatával. Ez a lépésről‑lépésre útmutató lefedi az extract
  text java, az OCR ferde korrekciót és még sok mást.
keywords:
- ocr skew correction
- ocr language support
- improve ocr accuracy
- extract text image java
- ocr image java
linktitle: Hogyan végezzünk OCR ferde korrekciót és nyelvválasztást az Aspose.OCR
  segítségével
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  headline: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  type: TechArticle
- description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  name: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  steps:
  - name: Set up Your Document Directory
    text: Create a `File` object that points to the folder containing your source
      image. This makes the path handling portable across operating systems. Replace
      `"Your Document Directory"` with the absolute path where `p3.png` resides.
  - name: Define the Image Path
    text: Instantiate a `File` object for the specific image you want to process.
      Using a `File` object gives you easy access to file metadata if you need it
      later. Make sure the `file` variable points to the exact image you intend to
      process.
  - name: Create Aspose.OCR API Instance
    text: The `AsposeOCR` class is the entry point for all OCR operations. It encapsulates
      the engine, manages resources, and provides the `recognizePage` method. The
      `AsposeOCR` object gives you access to all OCR operations.
  - name: Set Recognition Options (Language Selection)
    text: '`RecognitionSettings` is Aspose.OCR''s configuration container that lets
      you fine‑tune the OCR process. Here we: 1. Disable auto‑skew because we provide
      a manual skew value. 2. Define a rectangular region (`RecognitionAreas`) to
      limit OCR to the part of the image that actually contains text. 3. Set t'
  - name: Perform OCR and Retrieve Results
    text: Calling `recognizePage` runs the OCR engine using the image and the settings
      you defined. The outcome is stored in a `RecognitionResult` object, which aggregates
      all useful data. The `RecognizePage` call runs the OCR engine using the image
      and the settings you defined. The outcome is stored in a `Re
  - name: Print and Utilize Results
    text: 'The console output shows: - The full extracted text (`recognitionText`).
      - Text for each defined rectangle (`recognitionAreasText`). - Bounding rectangle
      coordinates. - A JSON representation for easy downstream processing. - Detected
      skew angle and any warnings. The console output shows the full ext'
  type: HowTo
- questions:
  - answer: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable
      multilingual recognition.
    question: Can I recognize multiple languages in a single OCR call?
  - answer: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct
      file path.
    question: Which image formats does Aspose.OCR support?
  - answer: There’s no hard limit, but processing images larger than 10 MB can increase
      memory usage and runtime. Consider resizing large files.
    question: Is there a size limit for the image?
  - answer: Purchase a license from the Aspose website and apply it via the `License`
      class as shown in the Aspose documentation.
    question: How do I obtain a production license?
  - answer: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g.,
      using Aspose.PDF) and then run OCR.
    question: Can I extract text from a PDF page directly?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Hogyan végezzünk OCR ferde korrekciót és nyelvválasztást az Aspose.OCR segítségével
url: /hu/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk OCR ferde korrekciót és nyelvválasztást az Aspose.OCR-rel

## Bevezetés

A képfájlokból történő szövegkinyerés gyakori igény, legyen szó beolvasott dokumentumok digitalizálásáról, nyugták feldolgozásáról vagy kereshető archívumok építéséről. Ebben az oktatóanyagban egy teljes, gyakorlati példán keresztül mutatjuk be, **hogyan OCR-eljük a képszöveget** egy adott nyelvi beállítással, így még ma megbízható OCR-t integrálhat Java‑alkalmazásaiba. Emellett megismerheti az **OCR ferde korrekció** és a régió‑alapú felismerés kezelését a legjobb pontosság érdekében, amelyek együtt **30 %‑kal javíthatják az OCR pontosságát** a ferde beolvasásoknál.

## Gyors válaszok
- **Melyik könyvtár kezeli az OCR-t Java-ban?** Aspose.OCR for Java  
- **Melyik beállítás választja ki a nyelvet?** `settings.setLanguage(Language.Eng)` (vagy bármely támogatott nyelv)  
- **Szükségem van licencre fejlesztéshez?** Egy ingyenes értékelő licenc elegendő a teszteléshez; a termeléshez kereskedelmi licenc szükséges.  
- **Korlátozhatom az OCR-t a kép egy részére?** Igen, használja a `RecognitionSettings.setRecognitionAreas()` metódust téglalapokkal.  
- **Milyen a tipikus futási idő?** Néhány másodperc oldalanként egy átlagos laptopon, a kép méretétől és a nyelv összetettségétől függően.  

`Language` egy felsorolás, amely az Aspose.OCR által támogatott OCR‑nyelveket sorolja fel, például angol, francia, spanyol stb.

## Mi az OCR ferde korrekció?

Az OCR ferde korrekció a ferde szövegsorok felismerése és kiegyenesítése a karakterfelismerés előtt. A szöveg alapvonalának igazításával az OCR‑motor hatékonyabban alkalmazhatja nyelvi modelljeit, csökkentve a ferde beolvasások által okozott hibákat. Ez a lépés javítja a bemeneti kép vizuális minőségét, lehetővé téve, hogy a felismerő algoritmusok a valódi karakterformákra koncentráljanak a forgatás által bevezetett torzítások helyett.

## Miért javítja az OCR ferde korrekció a pontosságot

Ha a szöveg ferde, a karakterformák torzulnak, ami akár 20 %‑os hibaarány növekedéshez vezethet. Az **ocr ferde korrekció** eltávolítja ezt a torzítást, így a motor a tényleges glifákra fókuszálhat. Benchmark tesztekben az Aspose.OCR 15‑30 %-os pontosságnövekedést ért el 10‑15°‑os forgatású dokumentumok esetén a ferde korrekció alkalmazása után.

## Miért használjuk az Aspose.OCR‑t nyelvválasztással?

A forrás szöveg pontos nyelvének megadása lehetővé teszi az OCR‑motor számára, hogy nyelvspecifikus szótárakat és karaktermodelleket használjon, ami drámaian növeli a felismerési pontosságot és csökkenti a feldolgozási időt. Emellett az Aspose.OCR finomhangolt vezérlést biztosít a ferde korrekció, a régió‑kiválasztás és a kimeneti formátumok felett, így sokoldalú választás a többnyelvű dokumentumfeldolgozó csővezetékekhez.

- **Többnyelvű támogatás** – Válassza ki a képen jelen lévő pontos nyelvet/nyelveket a pontosság növelése érdekében.  
- **Finomhangolt vezérlés** – Állítsa be a ferde korrekciót, definiálja a felismerési területeket, és konfigurálja az automatikus ferde viselkedést.  
- **Tiszta Java API** – Nincsenek natív függőségek, könnyen integrálható bármely Java projektbe.  
- **Gazdag eredményadat** – Egy hívással kapja meg a sima szöveget, JSON‑t, határoló téglalapokat és figyelmeztetéseket.  
- **Mérhető képesség** – Az Aspose.OCR **50+** bemeneti és kimeneti formátumot támogat, és **500‑oldalas** képbatch‑eket képes feldolgozni a teljes dokumentum memóriába töltése nélkül.

## Előfeltételek

Mielőtt elkezdené, győződjön meg róla, hogy rendelkezik:

- **Java Development Kit (JDK)** telepítve (JDK 8 vagy újabb).  
- **Aspose.OCR for Java** könyvtárral – töltse le a hivatalos oldalról [itt](https://reference.aspose.com/ocr/java/).  
- Egy olyan képfájllal, amely a kinyerni kívánt szöveget tartalmazza, például `p3.png`.  

## Csomagok importálása

Az alábbi importok hozzáférést biztosítanak a fő OCR osztályokhoz és a szabványos Java segédeszközökhöz.  
`import com.aspose.ocr.*;` – a fő OCR motor importálása.  
`import com.aspose.ocr.config.*;` – konfigurációs objektumok, például `RecognitionSettings`.  
`import java.awt.Rectangle;` – a felismerési területek meghatározásához használatos.  

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Hogyan alkalmazzuk az OCR ferde korrekciót Java-ban?

Töltse be a képet, tiltsa le az automatikus ferde detektálást, és adjon meg egy mérő szöget, vagy hagyja, hogy a motor a `settings.setAutoSkew(false)` használatával kiszámolja. Az OCR‑motor először a megadott vagy észlelt szög alapján egyenesíti a képet, majd a karakterfelismeréshez folytatja. Ez a kétlépéses megközelítés biztosítja, hogy minden ferde eltávolításra kerüljön, mielőtt a nyelvi modellek alkalmazásra kerülnének, így tisztább szövegkimenetet és kevesebb hibát eredményez.

## Lépésről‑lépésre útmutató

### 1. lépés: Dokumentumkönyvtár beállítása

Hozzon létre egy `File` objektumot, amely a forrásképet tartalmazó mappára mutat. Ez a megoldás a fájlútvonal kezelését operációs rendszerfüggetlené teszi.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Cserélje le a `"Your Document Directory"` szöveget arra az abszolút útvonalra, ahol a `p3.png` található.

### 2. lépés: Kép útvonalának meghatározása

Hozzon létre egy `File` objektumot a konkrét képfájlhoz, amelyet feldolgozni kíván. A `File` objektum használata egyszerű hozzáférést biztosít a fájl metaadataihoz, ha később szüksége lenne rá.

```java
// The image path
String file = dataDir + "p3.png";
```

Győződjön meg arról, hogy a `file` változó a pontosan feldolgozandó képre mutat.

### 3. lépés: Aspose.OCR API példány létrehozása

Az `AsposeOCR` osztály az összes OCR‑művelet belépési pontja. Magába foglalja a motort, kezeli az erőforrásokat, és biztosítja a `recognizePage` metódust.

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Az `AsposeOCR` objektum hozzáférést ad az összes OCR‑művelethez.

### 4. lépés: Felismerési beállítások megadása (nyelvválasztás)

A `RecognitionSettings` az Aspose.OCR konfigurációs tárolója, amely lehetővé teszi az OCR folyamat finomhangolását.  

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Itt:

1. Letiltjuk az automatikus ferde korrekciót, mivel manuális ferde értéket adunk meg.  
2. Meghatározunk egy téglalap alakú területet (`RecognitionAreas`), hogy az OCR csak a tényleges szöveget tartalmazó képrészre korlátozódjon.  
3. Beállítjuk a **nyelvet** angolra (`Language.Eng`). Módosítsa ezt `Language.Fra`, `Language.Spa` stb.-re, a forráskép nyelvétől függően.

### 5. lépés: OCR végrehajtása és az eredmények lekérése

A `recognizePage` hívás elindítja az OCR‑motort a megadott képpel és beállításokkal. Az eredmény egy `RecognitionResult` objektumban tárolódik, amely összegyűjti az összes hasznos adatot.

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

A `RecognizePage` hívás elindítja az OCR‑motort a megadott képpel és beállításokkal. Az eredmény egy `RecognitionResult` objektumban tárolódik.

### 6. lépés: Eredmények kiírása és felhasználása

A konzol kimenet mutatja:

- A teljes kinyert szöveget (`recognitionText`).  
- Az egyes téglalapokhoz tartozó szöveget (`recognitionAreasText`).  
- A határoló téglalap koordinátáit.  
- Egy JSON ábrázolást a könnyű további feldolgozáshoz.  
- A detektált ferde szöget és esetleges figyelmeztetéseket.

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

A konzol kimenet mutatja a teljes kinyert szöveget, a régió‑specifikus szöveget, a határoló dobozokat, a JSON‑t, a ferde szöget és a figyelmeztetéseket. Most már felhasználhatja a `result.recognitionText` értéket üzleti logikájában – tárolhatja, indexelheti vagy továbbíthatja egy másik szolgáltatásnak.

## Gyakori problémák és megoldások

| Probléma | Ok | Megoldás |
|----------|----|----------|
| **Rossz karakterek** | Helytelen nyelv kiválasztása | Állítsa be a megfelelő `Language` enum-ot (pl. `Language.Fra` francia nyelvhez). |
| **Nincs szöveg visszaadva** | A felismerési terület nem fedi le a szöveget | Állítsa be a `Rectangle` koordinátákat, vagy távolítsa el a `RecognitionAreas`-t, hogy a teljes képet feldolgozza. |
| **Lassú teljesítmény** | Nagyon nagy kép vagy magas felbontás | Méretezze le a képet OCR előtt, vagy növelje a JVM memória allokációt. |
| **Figyelmeztetések a nem támogatott formátumról** | A képformátum nem ismert | Konvertálja a képet PNG, JPEG vagy TIFF formátumba a feldolgozás előtt. |

## Gyakran Ismételt Kérdések

**Q: Felismerhetek több nyelvet egyetlen OCR hívásban?**  
A: Igen. Használja a `settings.setLanguage(Language.Eng | Language.Fra)`‑t a többnyelvű felismerés engedélyezéséhez.

**Q: Milyen képformátumokat támogat az Aspose.OCR?**  
A: PNG, JPEG, BMP, TIFF, GIF és több más formátum. Csak adja meg a helyes fájlútvonalat.

**Q: Van méretkorlát a képre?**  
A: Nincs szigorú korlát, de a 10 MB‑nál nagyobb képek feldolgozása növelheti a memóriahasználatot és a futási időt. Fontolja meg a nagy fájlok átméretezését.

**Q: Hogyan szerezhetek termelési licencet?**  
A: Vásároljon licencet az Aspose weboldaláról, és alkalmazza a `License` osztályon keresztül, ahogy az Aspose dokumentációjában szerepel.

**Q: Kivonhatok szöveget egy PDF oldalról közvetlenül?**  
A: Nem közvetlenül az Aspose.OCR‑rel. Először konvertálja a PDF oldalt képpé (pl. az Aspose.PDF használatával), majd futtassa az OCR‑t.

## Következtetés

Most már látta, hogyan **nyerhet ki szöveget képből** az Aspose.OCR for Java segítségével, miközben a megfelelő nyelvet választja ki, és **OCR ferde korrekciót** alkalmaz a megbízhatóság növelése érdekében. Ez a megközelítés pontos, nagy teljesítményű OCR‑t biztosít, amely beágyazható bármely Java‑alapú munkafolyamatba – a dokumentumkezelő rendszerektől az adatgyűjtő csővezetékekig. Kísérletezzen különböző `Language` enum‑okkal, finomhangolja a `RecognitionAreas`‑t, és integrálja a JSON‑kimenetet a downstream analitikába egy valóban vég‑végi megoldásért.

---

**Utolsó frissítés:** 2026-06-24  
**Tesztelve ezzel:** Aspose.OCR 24.11 for Java  
**Szerző:** Aspose

## Kapcsolódó oktatóanyagok

- [Hogyan számítsuk ki a ferde szöget Java-ban az Aspose.OCR használatával](/ocr/java/ocr-basics/calculate-skew-angle/)
- [Hogyan OCR-eljünk képszöveget nyelvválasztással az Aspose.OCR használatával](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [OCR PDF dokumentumok felismerése az Aspose.OCR for Java-ban](/ocr/java/ocr-operations/recognize-pdf/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}