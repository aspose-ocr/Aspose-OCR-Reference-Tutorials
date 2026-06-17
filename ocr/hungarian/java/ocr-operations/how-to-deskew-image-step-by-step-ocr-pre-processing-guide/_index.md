---
category: general
date: 2026-02-19
description: Tanulja meg, hogyan lehet kiegyenesíteni a képet és eltávolítani a zajt
  az OCR-hez. Ez az útmutató bemutatja, hogyan lehet felismerni a szöveges képet,
  kijavítani a kép forgását, és előfeldolgozni a képet OCR-hez az Aspose OCR segítségével.
draft: false
keywords:
- how to deskew image
- recognize text image
- how to remove noise
- correct image rotation
- preprocess image ocr
language: hu
og_description: Hogyan korrigáljuk a kép ferdeségét és távolítsuk el a zajt, hogy
  gyorsan felismerhessük a szöveges képet. Kövesse ezt az útmutatót a kép forgatásának
  helyesbítéséhez és az OCR előfeldolgozásához az Aspose-szal.
og_title: Hogyan kiegyenesítsük a képet – Teljes OCR előfeldolgozási útmutató
tags:
- OCR
- Java
- Image Processing
title: Hogyan egyenesítsük a képet — Lépésről lépésre OCR előfeldolgozási útmutató
url: /hu/java/ocr-operations/how-to-deskew-image-step-by-step-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan korrigáljuk a kép dőlését — Teljes OCR előfeldolgozási útmutató

Gondolkodtál már azon, **hogyan korrigáljuk a kép dőlését** a fájloknál, mielőtt egy OCR motorba táplálnád őket? Lehet, hogy egy csomó nyugtát szkenneltél, és az oldalak kissé ferdenek tűnnek, vagy a szkennelés véletlenszerű pontokkal van tele. Ez egy gyakori probléma – a ferde, zajos képek megnehezítik a szövegfelismerést.  

A jó hír? Néhány Java sorral kiegyenesítheted (korrigálhatod a kép forgását) és eltávolíthatod a zajt (hogyan távolítsuk el a zajt) az Aspose.OCR segítségével. Ebben az útmutatóban végigvezetünk a teljes folyamaton: egy zajos‑ferde PNG betöltésétől, a deskew + median denoise alkalmazásáig, egészen a **recognize text image** lépésig és az eredmény kiírásáig. A végére egy újrahasználható kódrészletet kapsz, amelyet bármely Java projektbe beilleszthetsz.

## Amire szükséged lesz

- **Java 17** vagy újabb (a kód régebbi verziókkal is lefordítható, de a 17 a legoptimálisabb).  
- **Aspose.OCR for Java** – a legújabb JAR‑t a Maven Central‑ról szerezheted be (`com.aspose:aspose-ocr`).  
- Egy olyan képfájl, amely egyszerre ferde és zajos (például `noisy-rotated.png`).  
- Egy egyszerű IDE (IntelliJ, Eclipse vagy akár VS Code).  

Nem szükséges semmilyen bonyolult build eszköz; egy egyszerű `javac` + `java` futtatás is megfelelő.

---

## 1. lépés – Hozd létre az OCR motor példányát  

Az első dolog, amit megteszel, hogy elindítod az `OcrEngine`‑t. Gondolj rá úgy, mint egy agyra, amely később elolvassa helyetted a karaktereket.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Hasznos tipp:** Tartsd a motort singletonként, ha sok képet dolgozol fel; újrahasználja a belső puffereket és felgyorsítja a feldolgozást.

## 2. lépés – Engedélyezd a Deskew és a Median Denoise funkciókat (Hogyan távolítsuk el a zajt)

Most megmondjuk a motornak, hogy **korrigálja a kép forgását** és **hogyan távolítsuk el a zajt**. Mindkét szűrő opcionális, de együtt drámaian javítják a pontosságot.

```java
        // Turn on preprocessing filters
        ocrEngine.getPreprocessing().setDeskew(true);          // fixes rotation
        ocrEngine.getPreprocessing().setMedianDenoise(true);   // smooths out speckles
```

Miért median denoise? Megőrzi a széleket (azokat a vonalakat, amelyek a karaktereket definiálják), miközben eltávolítja az elszigetelt pixeleket – pontosan azt, amire tiszta OCR‑hoz szükség van.

## 3. lépés – Töltsd be a feldolgozni kívánt képet  

Itt mutatjuk meg a motornak, melyik fájlt kell megtisztítania. Az `ImageStream.fromFile` beolvassa a PNG‑t a memóriába.

```java
        // Load the noisy‑rotated image
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/noisy-rotated.png"));
```

Ha a képed egy távoli szerveren található, egyszerűen egy `InputStream`‑et adj át helyette – az Aspose ezt zökkenőmentesen kezeli.

## 4. lépés – Futtasd az OCR‑t és rögzítsd a felismert szöveget  

Az előfeldolgozás engedélyezése után a motor most a korrigált képet olvassa. A `recognize()` hívás egy `RecognitionResult`‑ot ad vissza, amely a kinyert karakterláncot tartalmazza.

```java
        // Perform OCR – the engine automatically applies deskew & denoise first
        String recognizedText = ocrEngine.recognize().getText();

        // Show the output
        System.out.println("=== Recognized Text ===");
        System.out.println(recognizedText);
    }
}
```

A konzolon tiszta, olvasható szöveget kell látnod, még akkor is, ha az eredeti kép ferde és szemcsés volt.

## 5. lépés – Ellenőrizd az eredményt (Mit várhatsz)

Ha minden rendben működik, a konzol valami ilyesmit fog kiírni:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑02‑15
Total: $1,234.56
```

Ha a kimenet még mindig torz karaktereket tartalmaz, ellenőrizd a következőket:

- A kép felbontása (≥ 300 dpi az ideális).  
- Hogy a fájl útvonala helyes‑e.  
- Vajon további szűrők (például `setContrastStretch`) segíthetnek‑e.

---

## Opcionális: Vizuális ellenőrzés egy példaképpel  

Alább egy kis előnézet egy ferde, zajos nyugtáról. Figyeld meg a dőlést – a kódunk kiegyenesíti azt számodra.

![hogyan korrigáljuk a kép dőlését példakép](deskew-demo.png "hogyan korrigáljuk a kép dőlését")

*Alt szöveg: hogyan korrigáljuk a kép dőlését – elő és utófeldolgozás.*

---

## Gyakran Ismételt Kérdések

### Működik ez PDF‑ekkel is, vagy csak PNG/JPEG fájlokkal?  
Az Aspose.OCR közvetlenül olvashat PDF‑eket; csak cseréld le az `ImageStream.fromFile`‑t `ImageStream.fromPdf`‑ra. Ugyanazok a előfeldolgozó zászlók érvényesek, így továbbra is **hogyan korrigáljuk a kép dőlését** és **hogyan távolítsuk el a zajt** kapod.

### Mit tehetek, ha későbbi lépésekhez meg kell őriznem az eredeti orientációt?  
Az előfeldolgozás előtt klónozhatod a képet:

```java
Image original = ocrEngine.getImage().clone();
ocrEngine.getPreprocessing().apply(); // modifies the internal copy
// Use original later if needed
```

### Manuálisan is beállíthatom a deskew szöget?  
Igen – a `setDeskewAngle(double degrees)` lehetővé teszi, hogy felülírd az automatikus detektálási algoritmust. Hasznos, ha az automata nem tud megbirkózni extrém forgatásokkal.

### Miben különbözik a median denoise a Gaussian blur‑tól?  
A median szűrő minden pixelt a szomszédjai mediánjával helyettesít, ezáltal megőrzi a széleket. A Gaussian blur mindent elmos, ami a karaktervonalkák elmosódásához vezethet – ezért a median a biztonságosabb választás OCR‑hez.

---

## Összegzés  

Ebben a tutorialban bemutattuk, **hogyan korrigáljuk a kép dőlését**, demonstráltuk **hogyan távolítsuk el a zajt**, és megmutattuk, hogyan **recognize text image** használatával végezzük el a szövegfelismerést az Aspose OCR beépített előfeldolgozásával. A `setDeskew(true)` és `setMedianDenoise(true)` engedélyezésével automatikusan **korrigálod a kép forgását** és megtisztítod a szemcséket, így egy rendezetlen szkennt tiszta szöveggé alakítasz.  

Nyugodtan kísérletezz: próbálj ki különböző zajszűrési stratégiákat, dolgozz PDF‑ekkel, vagy láncolj több képet egy ciklusban. Az ugyanaz a minta – motor → előfeldolgozás → felismerés – minden szituációra alkalmazható, így szilárd alapot nyújt bármely OCR pipeline-hoz.

**Következő lépések**, amelyeket érdemes felfedezni:

- **Kötegelt feldolgozás** – iterálj egy mappában lévő képek felett, és írd ki minden eredményt egy `.txt` fájlba.  
- **Nyelvi csomagok** – tölts be egy adott nyelvi szótárt a pontosság növelése érdekében nem‑angol szövegekhez.  
- **Haladó szűrők** – például `setContrastStretch` vagy `setBinarization` alacsony kontrasztú szkennek.  

Van még kérdésed? Hagyj egy megjegyzést, és jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}