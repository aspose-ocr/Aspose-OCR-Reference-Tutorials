---
category: general
date: 2026-02-27
description: Előfeldolgozza a képet OCR-rel, hogy szöveget nyerjen ki a képből az
  Aspose OCR Java használatával. Tanulja meg, hogyan javíthatja az OCR pontosságát,
  és hogyan konvertálhatja hatékonyan a beolvasott képek szövegét.
draft: false
keywords:
- preprocess image OCR
- extract text from image
- improve OCR accuracy
- java OCR example
- convert scanned image text
language: hu
og_description: Előfeldolgozza a képes OCR-t, hogy szöveget nyerjen ki a képből az
  Aspose OCR segítségével. Ez az útmutató bemutatja, hogyan javítható az OCR pontossága,
  és hogyan konvertálható a beolvasott képek szövege Java-ban.
og_title: Kép OCR előfeldolgozása Java-ban – Növeld a pontosságot és nyerd ki a szöveget
tags:
- OCR
- Java
- Image Processing
title: Kép OCR előfeldolgozása Java-ban – Növeld a pontosságot és nyerd ki a szöveget
url: /hu/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Képek OCR előfeldolgozása – Teljes Java útmutató

Volt már, hogy **képek OCR előfeldolgozása** közben a kinyert szöveg hibásan jelent meg? Nem vagy egyedül. Sok projektben a nyers szkennelés ferde, szemcsés vagy alacsony kontrasztú, és ezek az apró hibák könnyen tönkretehetik az egész kinyerési folyamatot.

A jó hír? Néhány előfeldolgozási lépés – kiegyenesítés, zajszűrés és binarizálás – alkalmazásával drámaian javítható az OCR eredmény. Ebben az útmutatóban egy **java OCR példát** mutatunk be, amely pontosan bemutatja, hogyan **kell szöveget kinyerni képfájlokból**, növelni a pontosságot, és végül **a szkennelt kép szövegét** tiszta, kereshető karakterláncokká alakítani.

> **Mit kapsz:** egy azonnal futtatható Java programot az Aspose OCR használatával, magyarázatot arra, miért fontos minden beállítás, valamint tippeket a széljegyek kezeléséhez, például erősen elfordított oldalak vagy alacsony felbontású szkennelések esetén.

---

## Amire szükséged lesz

- **Java Development Kit (JDK) 8** vagy újabb.  
- **Aspose.OCR for Java** könyvtár (a cikk írásakor legújabb verzió, 23.10).  
- Egy minta TIFF/PNG/JPEG fájl, amit be szeretnél olvasni – legyen ez `input.tif`.  
- Kedvenc IDE-d (IntelliJ IDEA, Eclipse, VS Code… bármelyik megfelel).

További natív függőségek vagy külső eszközök nem szükségesek; az Aspose OCR motor mindent elvégez.

---

## Képek OCR előfeldolgozása – A motor beállítása

Először létrehozzuk az `OcrEngine` példányt. Ez az objektum tartalmazza az összes későbbi előfeldolgozást irányító konfigurációt.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the configuration follows...
```

**Miért fontos:** A motor a minden funkció kapuja – ha ezt a lépést kihagyod, a későbbi beállítások sosem lépnek életbe. Olyan, mintha a szerszámládát nyitnád ki, mielőtt elkezdenél kalapálni.

---

## Kiegyenesítés engedélyezése a forgatás korrigálásához

A szkennelt oldalak ritkán tökéletesen igazodnak. Egy enyhe dőlés miatt a karakterek félreolvashatók. A kiegyenesítés bekapcsolása azt mondja a motornak, hogy automatikusan felismerje és visszaforgassa a képet 0°-ra.

```java
        // Step 2: Turn on automatic deskew
        ocrEngine.getConfig().setDeskewEnabled(true);
```

*Pro tipp:* A kiegyenesítés a legjobban működik olyan képeken, ahol a szövegsorok egyértelműen láthatóak. Ha kézzel írott jegyzetet dolgozol fel, érdemes kísérletezni a `setDeskewAngleTolerance` metódussal (itt nem látható) a érzékenység finomhangolásához.

---

## Zajszűrés alkalmazása a zaj eltávolításához

A zaj – azok a véletlenszerű szemcsék vagy háttérszemcsék – összezavarják az OCR algoritmust. A zajszűrés bekapcsolása simítja a képet, megőrizve a vonalakat, miközben eldobja a felesleges pixeleket.

```java
        // Step 3: Enable denoising to clean up speckles
        ocrEngine.getConfig().setDenoiseEnabled(true);
```

**Széljegy:** Nagyon alacsony felbontású szkennelések (150 dpi alatt) esetén a túl erős zajszűrés elmoshatja a halvány karaktereket. Ilyenkor érdemes alacsonyabbra állítani a `setDenoiseLevel`‑t (alapértelmezett a közepes), vagy akár kihagyni ezt a lépést.

---

## Binarizálási küszöb beállítása a jobb kontraszthoz

A binarizálás a szürkeárnyalatos képet fekete‑fehérre konvertálja, élesítve a tinta és a papír közti kontrasztot. A küszöbérték (0‑255) határozza meg, hol történik a vágás. A 180 érték a legtöbb tiszta szkennelésnél jól működik, de előfordulhat, hogy finomhangolni kell.

```java
        // Step 4: Set a custom binarization threshold
        ocrEngine.getConfig().setBinarizationThreshold(180);
```

*Miért 180?* Elég magas ahhoz, hogy a sötét szöveg fekete maradjon, míg a világos háttér fehérre vált, ezáltal az OCR motor a valódi karakterekre fókuszál. Ha a forrás egy fakó, régi dokumentum, próbálj alacsonyabb értéket, például 120‑at.

---

## Kép feldolgozása és szöveg kinyerése

Most, hogy a motor fel van készítve, átadjuk neki a fájl útvonalát. A `processImage` metódus egy `OcrResult` objektumot ad vissza, amely a felismert szöveget és a biztonsági pontszámokat tartalmazza.

```java
        // Step 5: Process the image file
        OcrResult ocrResult = ocrEngine.processImage("YOUR_DIRECTORY/input.tif");
```

**Mi van, ha a fájl nem található?** A metódus `IOException`‑t dob. Éles környezetben ezt a hívást try‑catch blokkba kell helyezni, és barátságos hibaüzenetet naplózni.

---

## Az eredmény ellenőrzése

Végül kiírjuk a kinyert karakterláncot a konzolra. Itt láthatod, hogy az előfeldolgozás ténylegesen segített‑e.

```java
        // Step 6: Output the recognized text
        System.out.println("=== OCR Result ===");
        System.out.println(ocrResult.getText());
    }
}
```

Várt kimenet (rövidítve):

```
=== OCR Result ===
The quick brown fox jumps over the lazy dog.
```

Ha az eredmény még mindig szemét karaktereket tartalmaz, nézd át a küszöböt, vagy fontold meg egy egyedi szűrő (pl. morfológiai nyitás) alkalmazását, mielőtt az Aspose OCR‑nak átadnád a képet.

---

## Hogyan nyerjünk ki szöveget képből az Aspose OCR segítségével

A fenti kód egy **java OCR példát** mutat be, amely a teljes folyamatot demonstrálja – a kép betöltésétől a tiszta szöveg kiírásáig. Mivel minden előfeldolgozás a `Config` objektumon keresztül történik, egyes lépéseket könnyedén ki‑ vagy be lehet kapcsolni anélkül, hogy a fő logikát át kellene írni.

**Gyors ellenőrzőlista a kinyeréshez:**

1. **Töltsd be** a képet a `processImage`‑el.  
2. **Engedélyezd** a `Deskew`‑et és a `Denoise`‑t, ha a forrás egy szkennelt dokumentum.  
3. **Hangold** a `BinarizationThreshold`‑ot a vizuális ellenőrzés alapján.  
4. **Olvasd** a `ocrResult.getText()`‑et, és tárold el ahol szükséges – adatbázisban, fájlban vagy UI‑ban.

---

## Tippek az OCR pontosságának javításához Java‑ban

- **Felbontás számít:** Legalább 300 dpi‑t célozz meg szkenneléskor. A magasabb DPI több pixeladatot ad a motornak.  
- **Szín vs. szürkeárnyalat:** A színes szkenneléseket konvertáld szürkeárnyalatra a feldolgozás előtt; ez csökkenti a feldolgozási időt anélkül, hogy a pontosság romlana.  
- **Kötegelt feldolgozás:** Ha tucatnyi fájlod van, használd ugyanazt az `OcrEngine` példányt – az újbóli létrehozás fölösleges terhet jelent.  
- **Nyelvi csomagok:** Az Aspose OCR több nyelvet támogat; állítsd be például `ocrEngine.getConfig().setLanguage(OcrLanguage.English)`‑t (vagy másik nyelvet) a nem‑angol szövegek jobb felismeréséhez.

---

## Szkennelt kép szövegének konvertálása szerkeszthető karakterláncokká

Miután megvan a nyers szöveg, gyakran érdemes tovább tisztítani – sortöréseket eltávolítani, szóközöket normalizálni vagy helyesírás-ellenőrzést végezni. A Java `String` metódusai és az Apache Commons Text‑hez hasonló könyvtárak ezt egyszerűvé teszik.

```java
String cleaned = ocrResult.getText()
                          .replaceAll("\\s+", " ")
                          .trim();
System.out.println("Cleaned text: " + cleaned);
```

Most a szöveg készen áll egy `.txt` fájlba mentésre, PDF‑be beillesztésre, vagy egy downstream NLP pipeline‑ba való továbbításra.

---

![preprocess image OCR example](/images/preprocess-ocr-demo.png "preprocess image OCR example showing console output")

*A fenti képernyőkép a teljes Java program futtatása után megjelenő konzolkimenetet mutatja.*

---

## Összegzés

Most már tudod, hogyan **előfeldolgozd a képek OCR‑ját** Java‑ban, a kiegyenesítést, zajszűrést és binarizálást engedélyezve, hogy **szöveget nyerj ki képfájlokból** sokkal megbízhatóbban. Néhány konfigurációs flag finomhangolásával **javíthatod az OCR pontosságát**, kezelheted a nehéz szkenneléseket, és végül **a szkennelt kép szövegét** tiszta, kereshető karakterláncokká alakíthatod – mindezt egy kompakt, önálló **java OCR példában**.

Készen állsz a következő lépésre? Próbáld meg a kinyert szöveget adatbázisba menteni, generálj kereshető PDF‑eket az Aspose PDF‑el, vagy kísérletezz a többnyelvű támogatással. Ugyanaz a előfeldolgozási folyamat működik PDF‑ekkel, PNG‑kkel és JPEG‑ekkel is, így könnyedén skálázhatod ezt a mintát bármilyen dokumentum‑digitalizálási projektben.

Boldog kódolást, és legyen az OCR eredményed mindig kristálytiszta!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}