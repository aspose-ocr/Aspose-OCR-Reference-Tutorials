---
category: general
date: 2026-03-07
description: Képről szöveg kinyerése Java OCR-rel. Tanulja meg, hogyan töltsön be
  képet OCR-hez, hogyan állítsa be a nyelvet, és hogyan hajtson végre egy teljes Java
  OCR oktatót percek alatt.
draft: false
keywords:
- extract text from image
- load image for ocr
- use OCR in java
- java ocr tutorial
language: hu
og_description: Képről szöveg kinyerése Java OCR-rel. Ez az útmutató bemutatja, hogyan
  töltsünk be egy képet OCR-hez, állítsuk be a nyelvet, és hajtsuk végre a Java OCR
  lépésről lépésre tutorialt.
og_title: Szöveg kinyerése képből Java-ban – Teljes OCR útmutató
tags:
- OCR
- Java
- Image Processing
title: Szöveg kinyerése képből Java-ban – Java OCR útmutató
url: /hu/java/ocr-basics/extract-text-from-image-in-java-java-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép szövegének kinyerése Java-ban – Teljes OCR útmutató

Valaha is szükséged volt **kép szövegének kinyerésére**, de nem tudtad, hol kezdjed Java-ban? Nem vagy egyedül – a fejlesztők gyakran ütköznek ebbe a falba, amikor beolvasott táblákat, nyugtákat vagy kézzel írt jegyzeteket szeretnének kereshető karakterláncokká alakítani.  

A jó hír? Néhány perc alatt működő OCR csővezetéked lehet, amely Kannada, angol vagy bármely támogatott nyelvet olvas. Ebben a tutorialban **betöltjük a képet OCR-hez**, konfiguráljuk a motort, és végigvezetünk egy **Java OCR tutorialon**, amelyet ma másolhatsz‑beilleszthetsz és futtathatsz.

## Mit fed le ez az útmutató

Először felsoroljuk a szükséges eszközöket, majd egy **lépésről‑lépésre** megvalósítással vágunk bele. A végére képes leszel:

* Betölteni egy képfájlt Java `ImageInputStream`‑be.
* Konfigurálni egy OCR motort, hogy egy adott nyelvet (például Kannadát) ismerjen fel.
* Futtatni a felismerési folyamatot és kiírni a kinyert szöveget.
* Beállításokat finomhangolni a jobb pontosság érdekében, és kezelni a gyakori buktatókat.

Külső dokumentációra nincs szükség – minden, amire szükséged van, itt van.  

**Előfeltételek**: Java 17 vagy újabb, egy build eszköz, például Maven vagy Gradle, és egy OCR könyvtár, amely `OcrEngine` osztályt biztosít (például a hipotetikus *SimpleOCR* SDK). Ha Maven‑t használsz, add hozzá a később bemutatott függőséget.

---

## 1. lépés – Projekt beállítása és az OCR könyvtár hozzáadása

Mielőtt kódot írnánk, győződj meg róla, hogy a projekted láthatja az OCR osztályokat. Maven‑nel helyezd ezt a kódrészletet a `pom.xml`‑be:

```xml
<!-- Maven dependency for SimpleOCR (replace with your actual OCR SDK) -->
<dependency>
    <groupId>com.example</groupId>
    <artifactId>simple-ocr</artifactId>
    <version>1.4.2</version>
</dependency>
```

Ha Gradle‑t részesíted előnyben, az ekvivalens:

```gradle
implementation 'com.example:simple-ocr:1.4.2'
```

> **Pro tipp:** Tartsd naprakészen a könyvtár verzióját; az újabb kiadások gyakran tartalmaznak nyelvi modell‑javításokat, amelyek növelik a pontosságot.

Miután a függőség feloldódott, frissítsd az IDE‑det, és már kódolhatsz is.

## 2. lépés – Szükséges osztályok importálása

Az alábbi lista tartalmazza a példához szükséges importokat. Szándékosan minimálisra korlátoztuk őket, hogy pontosan lásd, melyik osztály mire jó.

```java
import com.example.ocr.OcrEngine;      // Main OCR engine
import com.example.ocr.OcrResult;      // Holds recognition result
import com.example.io.ImageInputStream; // Wrapper for image files
import java.nio.file.Paths;             // Convenient path handling
import java.io.IOException;             // For proper exception handling
```

> **Miért ezek az importok?** `OcrEngine` és `OcrResult` a OCR folyamat szíve, míg az `ImageInputStream` elrejti a fájl‑olvasási boilerplate‑t. A `java.nio.file.Paths` használata a kódot operációs rendszer‑függetlenné teszi.

## 3. lépés – Kép betöltése OCR‑hez

Most jön az a rész, ami gyakran elakadja az embereket: a megfelelő képformátum átadása a motor számára. Az OCR SDK egy `ImageInputStream`‑et vár, amelyet bármely lemezre mentett fájlból előállíthatsz.

```java
// Step 3: Load the image that contains the text you want to extract
String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));
```

> **Szélső eset:** Ha a kép sérült vagy nem támogatott formátumú (pl. GIF), a konstruktor `IOException`‑t dob. Tedd a hívást try‑catch blokkba, vagy előre ellenőrizd a fájlt.

## 4. lépés – A motor konfigurálása egy adott nyelv felismerésére

A legtöbb OCR motor többnyelvű támogatással érkezik. A pontosság javítása érdekében mondd meg a motornak, pontosan melyik nyelvet keresse. Mi a példában a `"kn"` nyelvkódot használjuk a Kannadához.

```java
// Step 4: Create and configure the OCR engine for Kannada
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setLanguage("kn"); // 'kn' = Kannada
```

> **Miért állítjuk be a nyelvet?** A karakterkészlet korlátozása csökkenti a hamis pozitív találatokat, különösen olyan írásrendszerek esetén, ahol sok hasonló glif van.

Ha valaha más nyelvre kell váltanod, egyszerűen módosítsd a kódsztringet – egyéb változtatásra nincs szükség.

## 5. lépés – OCR folyamat futtatása és a szöveg kinyerése

A kép betöltése és a motor beállítása után a tényleges felismerés egyetlen metódushívás. Az eredményobjektum a tiszta szöveget, illetve opcionálisan a biztonsági pontszámokat adja vissza.

```java
// Step 5: Run OCR and retrieve the recognized text
OcrResult ocrResult = ocrEngine.recognize(imageStream);
String extractedText = ocrResult.getText();
```

> **Gyakori kérdés:** *Mi van, ha az OCR üres karakterláncot ad vissza?*  
> Általában ez azt jelenti, hogy a kép minősége túl alacsony (elmosódott, alacsony kontraszt), vagy a nyelv nincs helyesen beállítva. Próbáld meg előfeldolgozni a képet (kontraszt növelése, binarizálás) vagy ellenőrizd újra a nyelvkódot.

## 6. lépés – Az eredmény megjelenítése

Végül írd ki a kimenetet a konzolra. Egy valódi alkalmazásban esetleg adatbázisba mentheted, vagy keresőindexbe táplálhatod.

```java
// Step 6: Output the recognized Kannada text
System.out.println("Extracted text:");
System.out.println(extractedText);
```

### Várható kimenet

Ha a forráskép a „ಕರ್ನಾಟಕ” (Karnataka) kannada kifejezést tartalmazza, a konzol a következőt mutatja:

```
Extracted text:
ಕರ್ನಾಟಕ
```

Ennyi – egy komplett **use OCR in Java** munkafolyamat, amelyet bármely nyelvre vagy képforrendre adaptálhatsz.

---

## Teljes működő példa

Az alábbi program a teljes kód, készen áll a fordításra. Cseréld le a `YOUR_DIRECTORY`‑t a képfájlod tényleges elérési útjára.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrResult;
import com.example.io.ImageInputStream;
import java.nio.file.Paths;
import java.io.IOException;

public class KannadaOcrExample {
    public static void main(String[] args) {
        try {
            // Create OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Configure for Kannada (language code "kn")
            ocrEngine.getConfig().setLanguage("kn");

            // Load the image you want to extract text from
            String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
            ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));

            // Run the OCR process
            OcrResult ocrResult = ocrEngine.recognize(imageStream);

            // Print the extracted text
            System.out.println("Extracted text:");
            System.out.println(ocrResult.getText());
        } catch (IOException e) {
            System.err.println("Failed to load image or run OCR: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error during OCR: " + e.getMessage());
        }
    }
}
```

> **Tipp:** Production környezetben érdemes egyetlen `OcrEngine` példányt újra‑használni több kép feldolgozásához; az ismételt létrehozás költséges lehet.

---

## Gyakran Ismételt Kérdések és Szélső Esetek

### Hogyan javíthatom a pontosságot zajos fotókon?
- **Előfeldolgozás**: konvertáld szürkeárnyalatosra, alkalmazz medián szűrést, vagy növeld a kontrasztot.
- **Átméretezés**: legalább 300 DPI‑re, mivel a legtöbb OCR motor ezt a felbontást várja.
- **Whitelist** beállítása: ha tudod, milyen karakterekre számítasz (pl. csak számjegyek), korlátozd a lehetséges karakterkészletet.

### Használhatom ezt a megközelítést PDF‑ekhez?
Igen. A PDF minden oldalát képpé konvertáld (PDFBox vagy iText segítségével), majd add ugyanabba a csővezetékbe. A kód változatlan marad; csak a kép‑forrás változik.

### Mit tehetek, ha egy képen több nyelvet kell felismerni?
A legtöbb SDK enged meg vesszővel elválasztott listát, például `"en,kn"`. A motor megpróbálja egyezni a megadott írásrendszerek bármelyikét.

### Van mód a biztonsági pontszámok lekérésére?
Az `OcrResult` gyakran tartalmaz `getConfidence()` metódust, amely 0 és 1 közötti float értéket ad vissza soronként. Ezt felhasználhatod az alacsony biztonságú eredmények szűrésére.

---

## Következő lépések

Miután **kép szövegének kinyerését** megvalósítottad Java‑ban, érdemes továbbfejleszteni:

* **Kötegelt feldolgozás** – iterálj egy mappán képek felett, és írd az eredményeket CSV‑be.
* **Integráció Apache Tika‑val** – kombináld az OCR‑t dokumentum‑elemzéssel egy egységes keresőindexhez.
* **Szerver‑oldali API** – tedd elérhetővé az OCR logikát REST végponton (Spring Boot‑dal ez egyszerű).
* **Alternatív könyvtárak** – próbáld ki a Tesseract‑ot a `tess4j`‑val, ha nyílt forráskódú megoldásra van szükséged.

Ezek a témák mind a **java ocr tutorial**‑ban lefektetett alapokra épülnek, szóval bátran kísérletezz és bővítsd a kódot.

---

## Összegzés

Végigvettünk egy komplett Java példát, amely **kép szövegének kinyerését** mutatja be, részletesen bemutatva, hogyan **betöltsünk képet OCR‑hez**, állítsuk be a nyelvi beállításokat, és **használjuk az OCR‑t Java‑ban** a olvasható karakterláncok visszaszerzéséhez. A kódrészlet önálló, hibákat kedvesen kezeli, és bármely Java projektbe könnyedén beilleszthető minimális erőfeszítéssel.  

Próbáld ki, módosítsd a nyelvkódot, és hamarosan a beolvasott dokumentumokat kereshető adatokként fogod kezelni gond nélkül. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}