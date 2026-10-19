---
category: general
date: 2026-05-03
description: Az Aspose OCR Java példa bemutatja, hogyan töltsünk be képet OCR-hez,
  és néhány kódsorral nyerjünk ki szöveget egy területről.
draft: false
keywords:
- aspose ocr java example
- load image for OCR
- extract text from region
language: hu
og_description: Az Aspose OCR Java példa bemutatja, hogyan töltsünk be egy képet OCR-hez,
  és hogyan nyerjünk ki szöveget egy meghatározott területről, ami tökéletes számlafeldolgozáshoz.
og_title: Aspose OCR Java példa – Régió szövegkivonás
tags:
- Aspose OCR
- Java
- Image Processing
title: 'Aspose OCR Java példa: Szöveg kinyerése egy régióból'
url: /hu/java/ocr-operations/aspose-ocr-java-example-extract-text-from-a-region/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Java példa: Szöveg kinyerése egy területről

Keres egy **Aspose OCR Java példát**, amely lehetővé teszi, hogy csak a képből a szükséges részt nyerje ki? Ebben az útmutatóban végigvezetjük a **kép betöltését OCR-hez** és a **szöveg kinyerését egy területről**, ami tökéletes számlaszámok, űrlapmezők vagy bármely adatdarab kinyerésére, amely egy nagyobb képen belül helyezkedik el.

Talán azon tűnődik, miért érdemes egy téglalapra korlátozni az OCR-t a teljes oldal szkennelése helyett. A rövid válasz: sebesség és pontosság. Amikor a motor csak egy meghatározott szeletet vizsgál, kihagyja a felesleges zajt, gyorsabban fut, és gyakran tisztább eredményt ad. A tutorial végére egy önálló Java programmal fog rendelkezni, amely pontosan ezt teszi, valamint néhány tippet is kap a gyakori buktatók elkerüléséhez.

## Amire szüksége lesz

Mielőtt belevágna, győződjön meg róla, hogy rendelkezik a következőkkel:

- **Java Development Kit (JDK) 11** vagy újabb telepítve.
- **Aspose.OCR for Java** könyvtár (a legújabb JAR-t a Maven Central tárolóból vagy az Aspose letöltési portálról szerezheti be).
- Egy képállomány, amely tartalmazza a beolvasni kívánt szöveget – a bemutatóhoz a `invoice.png` fájlt használjuk, amely a számlaszámot a jobb felső sarok közelében tartalmazza.
- Kedvenc IDE vagy egyszerű szövegszerkesztő plusz egy terminál; bármely build eszköz (Maven, Gradle vagy egyszerű `javac`) megfelel.

Ennyi. Nincs szükség extra OCR motorokra, natív binárisokra, csak tiszta Java és Aspose.

![Aspose OCR Java example screenshot](/images/aspose-ocr-java-example.png "Aspose OCR Java example showing region extraction")

## Aspose OCR Java példa – Az OCR motor inicializálása

Az első dolog, amire bármely OCR munkafolyamatnak szüksége van, egy motorpéldány. Az Aspose egy könnyű `OcrEngine` osztályt biztosít, amely mindent kezel a kép betöltésétől a nyelvválasztásig.

```java
import com.aspose.ocr.*;

public class RegionOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

**Miért fontos:** A motor előzetes létrehozása egy tiszta objektumot ad a konfiguráláshoz. Ugyanazt a `OcrEngine`-t újra felhasználhatja több képhez, ha kötegelt feldolgozást végez, ami memóriát és inicializálási időt takarít meg.

## Kép betöltése OCR-hez

Ezután megadjuk a motor számára, hogy melyik képet szkennelje. Az Aspose a `ImageStream.fromFile` segédfüggvényt kínálja, amely elrejti az alacsony szintű `FileInputStream` boilerplate‑t.

```java
        // Step 2: Load the image that contains the invoice
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Tipp:** Cserélje le a `YOUR_DIRECTORY`‑t egy abszolút vagy relatív útvonalra, amely a `invoice.png` fájl helyét mutatja. Ha a fájl nem található, az Aspose `IOException`‑t dob, ezért érdemes ezt try‑catch blokkba helyezni a termelési kódban.

## Terület definiálása és szöveg kinyerése

Most jön a főszereplő: a téglalap, amely megmondja a motornak, hol keressen. A `java.awt.Rectangle` konstruktor a `(x, y, width, height)` paramétereket várja – mind pixelben mérve.

```java
        // Step 3: Define the region where the invoice number is located (x, y, width, height)
        java.awt.Rectangle invoiceRegion = new java.awt.Rectangle(120, 250, 300, 80);
        ocrEngine.setRegion(invoiceRegion);   // restrict recognition to this area
```

**Hogyan működik:** A `setRegion` meghívásával az OCR szkennelést egy 300 pixel széles szeletre korlátozza, amely 120 pixellel a bal szélről és 250 pixellel a felső szélről indul. Igazítsa ezeket a számokat a saját elrendezéséhez; egy gyors módszer a megtalálásukra, ha a képet bármely grafikus szerkesztőben megnyitja, amely pixelkoordinátákat mutat.

## Nyelv engedélyezése és felismerés futtatása

Az Aspose OCR tucatnyi nyelvet támogat, de egy számlaszámhoz csak az angolra van szükség. A megfelelő nyelv engedélyezése drámaian csökkenti a hamis pozitív eredményeket.

```java
        // Step 4: Enable English language for recognition
        ocrEngine.getLanguage().setEnglish(true);

        // Step 5: Perform recognition and output the extracted text
        if (ocrEngine.recognize()) {
            System.out.println("Extracted region text: " + ocrEngine.getText());
        } else {
            System.err.println("OCR recognition failed.");
        }
    }
}
```

**Miért csak angolt engedélyezünk?** Az OCR motor megpróbálja a karaktereket minden engedélyezett nyelvi készletből egyeztetni, ami összezavarhatja, ha a szöveg egyszerű alfanumerikus. A nyelvi kör korlátozása javítja mind a sebességet, mind a pontosságot.

### Várható kimenet

Ha minden megfelelően van beállítva, a következőhöz hasonló eredményt fog látni:

```
Extracted region text: INV-12345
```

Ha a téglalap néhány pixellel el van tolva, a kimenet torz vagy üres lehet. Ez egy egyszerű ellenőrzés: futtassa a programot, nézze meg a konzolt, és ellenőrizze, hogy a szöveg megegyezik-e a képen láthatóval.

## A kód futtatása és a kimenet ellenőrzése

Feltételezve, hogy Maven‑t használ, adja hozzá az Aspose OCR függőséget a `pom.xml`‑hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

Fordítsa le és hajtsa végre:

```bash
mvn compile exec:java -Dexec.mainClass=RegionOcrExample
```

Vagy ha egyszerű `javac`‑et részesíti előnyben:

```bash
javac -cp "aspose-ocr-23.10.jar" RegionOcrExample.java
java -cp ".:aspose-ocr-23.10.jar" RegionOcrExample
```

A konzolon meg kell jelennie a **Extracted region text** sornak. Ha “OCR recognition failed” üzenetet kap, ellenőrizze újra a fájl útvonalát, és győződjön meg arról, hogy a terület valóban olvasható karaktereket tartalmaz.

## Szélhelyzetek és gyakori variációk

| Helyzet | Mit kell módosítani |
|-----------|----------------|
| **Több nyelv** (pl. angol + spanyol) | Hívja a `ocrEngine.getLanguage().setSpanish(true);`‑t az angol mellett. |
| **Terület a kép határain kívül** | Az Aspose csendben levágja a téglalapot, de adatveszteség keletkezik. Használja az `ImageInfo`‑t (`ocrEngine.getImage().getWidth()`) a méretek ellenőrzésére a terület beállítása előtt. |
| **Dinamikus számlák** (különböző elrendezések) | Fontolja meg egy könnyű elő‑szkennelés futtatását a teljes képen, hogy megtalálja a “Invoice #” kulcsszót, majd programozottan számolja ki a téglalapot. |
| **Magas DPI‑jú képek** | Növelje a `ocrEngine.getImage().setResolution(300);` értéket a beolvasott dokumentumok pontosságának javításához. |
| **Teljesítményhangolás** | Tiltsa le a felesleges nyelveket, tartsa a területet a lehető legkisebbre, és használja ugyanazt a `OcrEngine` példányt sok fájl feldolgozásához. |

## Profi tippek a frontvonalról

- **Pro tipp:** Ha csak számjegyekre van szüksége (gyakori a számlaszámoknál), engedélyezze a numerikus módot a `ocrEngine.getLanguage().setDigits(true);`‑val. Ez megszünteti az alfabetikus zajt.
- **Vigyázzon a:** Átlátszó PNG‑kre. Az Aspose néha félreérti az alfa csatornát; a kép előzetes konvertálása egy szilárd háttérrel rendelkező JPEG‑re megoldhatja a furcsa üres kimeneteket.
- **Ne felejtse el:** A téglalap a kép natív koordináta‑rendszerét használja, nem a képernyőn látható UI méretezést. Mindig tesztelje a pontos fájllal, amelyet a termelésben fog feldolgozni.

## Mi következik?

Most, hogy megvan egy stabil **Aspose OCR Java példa** a terület‑alapú kinyeréshez, több hasznos irányba is bővítheti:

- **Kötegelt feldolgozás:** Egy mappában lévő számlákat iteráljon, ugyanazt a `OcrEngine`‑t újrahasználva a teljesítmény növelése érdekében.
- **Adatvalidáció:** A kinyert szöveget adja át egy reguláris kifejezésnek, például `INV-\\d{5}`, hogy biztosan érvényes számlaszámot kapjon.
- **PDF integráció:** Használja az Aspose.PDF‑t a kinyert szöveg visszahelyezésére az eredeti dokumentumba audit‑nyomokhoz.
- **Felhőbe telepítés:** Csomagolja a kódot egy könnyű REST szolgáltatásba (Spring Boot), hogy más rendszerek igény szerint meghívhassák.

Ezek a lépések mind ugyanazokat az alapfogalmakat használják – **kép betöltése OCR‑hez**, **szöveg kinyerése egy területről**, és az eredmények kezelése – így a váltás zökkenőmentes lesz.

---

*Boldog kódolást! Ha elakad, hagyjon megjegyzést alul, vagy nézze meg az Aspose fórumokat, ahol a közösség valós életbeli finomításokat oszt meg nehéz elrendezésekhez.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}