---
category: general
date: 2026-02-17
description: Tanulja meg, hogyan használhatja az OCR-t Java-ban szöveg felismerésére
  képfájlokból, szöveg kinyerésére PNG nyugtákról, és a nyugtát JSON formátumba konvertálhatja
  az Aspose OCR segítségével.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: hu
og_description: Lépésről lépésre útmutató arról, hogyan használjunk OCR-t Java-ban
  a képről szöveg felismeréséhez, PNG nyugták szövegének kinyeréséhez és a nyugtát
  JSON formátumba konvertáláshoz.
og_title: Hogyan használjunk OCR-t Java-ban – Szöveg felismerése képből
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Hogyan használjunk OCR-t Java-ban – Szöveg gyors felismerése képből
url: /hu/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjunk OCR-t Java-ban – Szöveg felismerése képről gyorsan

Valaha is elgondolkodtál **hogyan használjunk OCR-t**, hogy szöveget nyerjünk ki egy nyugta fényképéből? Lehet, hogy már próbáltál néhány online eszközt, csak hogy összekuszálódott karakterekkel vagy olyan formátummal állsz szemben, amit nem tudsz feldolgozni. A jó hír, hogy néhány Java sorral **szöveget felismerhetsz képfájlokból**, **szöveget nyerhetsz ki PNG** nyugtákból, és még **nyugtát konvertálhatsz JSON-re** a további feldolgozáshoz.  

Ebben az útmutatóban végigvezetünk a teljes munkafolyamaton – a Aspose OCR könyvtár licencelésétől egy tiszta JSON payload elkészítéséig, amelyet adatbázisba vagy gépi tanulási modellbe táplálhatsz. Nincs felesleges szöveg, csak egy gyakorlati, futtatható példa, amelyet egyszerűen beilleszthetsz az IDE-dbe. A végére egy önálló programod lesz, amely a `receipt.png` fájlt veszi, és egy használatra kész JSON karakterláncot ad vissza.

## Amire szükséged lesz

- **Java Development Kit (JDK) 8+** – bármelyik újabb verzió működik.
- **Aspose OCR for Java** könyvtár (a Maven artefakt: `com.aspose:aspose-ocr`).
- Egy **érvényes Aspose OCR licencfájl** (`Aspose.OCR.lic`). A ingyenes próba a teszteléshez működik, de egy megfelelő licenc eltávolítja a kiértékelési korlátokat.
- Egy képfájl (PNG, JPEG, stb.), amely a kívánt szöveget tartalmazza – nevezzük `receipt.png`-nek, és helyezzük egy ismert mappába.
- A kedvenc IDE-d (IntelliJ IDEA, Eclipse, VS Code…) – szabadon választható.

> **Pro tipp:** Tartsd a licencfájlt a forrásmappán kívül, és hivatkozz rá abszolút vagy relatív úton, hogy elkerüld a verziókezelőbe való beillesztést.

Most, hogy a követelmények egyértelműek, merüljünk el a tényleges kódban.

## Hogyan használjunk OCR-t – Alapvető lépések

Az alábbiakban egy magas szintű áttekintést láthatsz a végrehajtandó műveletekről:

1. **Töltsd be az Aspose OCR könyvtárat** és alkalmazd a licencet.  
2. **Hozz létre egy `OcrEngine` példányt** – ez a motor, amely a nehéz munkát végzi.  
3. **Készíts egy `OcrInput` objektumot**, amely a feldolgozni kívánt képre mutat.  
4. **Hívd meg a `recognize` metódust `ResultFormat.JSON` paraméterrel**, hogy JSON reprezentációt kapj a kinyert szövegről.  
5. **Kezeled a JSON kimenetet** – nyomtasd ki, írd fájlba, vagy dolgozd fel tovább.

Minden lépést részletesen kifejtünk az alábbi szakaszokban.

## 1. lépés – Aspose OCR telepítése és a licenc alkalmazása

Először add hozzá az Aspose OCR függőséget a `pom.xml`-hez, ha Maven-t használsz:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Most a Java kódban töltsd be a licencet. Ez a lépés elengedhetetlen; licenc nélkül a könyvtár értékelő módban fut, és vízjelet helyezhet el a kimenetben.

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **Miért fontos:** A `License` objektum jelzi az OCR motor számára, hogy jogosult vagy a teljes funkciókészlet használatára, beleértve a magas pontosságú felismerést és a JSON exportot. Ennek a lépésnek a kihagyása még mindig lehetővé teszi a **szöveg felismerését képről**, de az eredmények lelassulhatnak.

## 2. lépés – OCR motor példány létrehozása

Az `OcrEngine` osztály az összes OCR művelet belépési pontja. Gondolj rá úgy, mint egy “agyra”, amely a pixeleket olvassa, és meghatározza, milyen karaktereket képviselnek.

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

A motort később testreszabhatod (például nyelv beállítása, deskew engedélyezése), ha a nyugtáid nem latin betűket tartalmaznak vagy szögben lettek beolvasva. A legtöbb US‑alapú nyugta esetén az alapértelmezett beállítások tökéletesen működnek.

## 3. lépés – A feldolgozandó kép betöltése

Most az OCR motort a nyugtát tartalmazó fájlra irányítjuk. Az `OcrInput` osztály több képet is elfogadhat, de ebben az útmutatóban egyetlen PNG-re korlátozódunk.

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

Ha valaha is **szöveget kell kinyerned PNG** fájlokból tömegesen, egyszerűen hívd meg az `input.add()` metódust többször, vagy adj át egy fájlútvonalak listáját.

## 4. lépés – Szöveg felismerése és a nyugta JSON-re konvertálása

Itt van a tutorial szíve. A motort arra kérjük, hogy felismerje a szöveget, és a eredményt JSON formátumban adja vissza. A `ResultFormat.JSON` jelző mindent elintéz helyettünk.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

A JSON payload tartalmazza minden felismert sort, annak keretét, a biztonsági pontszámot és a nyers szöveget. Ez a struktúra lehetővé teszi, hogy egyszerűen **nyugtát konvertálj JSON-re**, majd bármely downstream API-ba továbbítsd.

## 5. lépés – Összeállítás és a program futtatása

Az alábbiakban a teljes, futtatható Java osztály látható, amely mindent összekapcsol. Mentsd el `JsonExportDemo.java` néven (vagy bármilyen más néven), és futtasd az IDE‑ből vagy a parancssorból.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### Várható kimenet

A program futtatása egy a következőhöz hasonló JSON karakterláncot nyomtat (a pontos tartalom a nyugtádtól függ):

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

Most már ezt a JSON-t betáplálhatod egy adatbázisba, egy REST végpontra vagy egy adat‑elemzési csővezetékbe. A **nyugtát JSON-re konvertálás** lépés már el van végezve számodra.

## Gyakori kérdések és speciális esetek

### Mi van, ha a kép el van forgatva?

Az Aspose OCR automatikusan felismeri és korrigálja a enyhe elfordulásokat. Súlyosan ferde képek esetén hívd meg a `engine.getImagePreprocessingOptions().setDeskew(true)` metódust a felismerés előtt.

### Hogyan kezeljek több nyelvet?

Használd a `engine.getLanguage()` metódust a kívánt nyelv beállításához, például `engine.setLanguage(Language.FRENCH)`. Ez akkor hasznos, ha **szöveget kell felismerned képről**, amely többnyelvű nyugtákat tartalmaz.

### Ki tudok-e nyerni egyszerű szöveget JSON helyett?

Természetesen. Cseréld le a `ResultFormat.JSON`-t `ResultFormat.TEXT`-re, és hívd meg a `result.getText()` metódust.

### Van mód az OCR-t egy meghatározott területre korlátozni?

Igen – használhatod a `ocrInput.add(imagePath, new Rectangle(x, y, width, height))` metódust, hogy a nyugta területére fókuszálj, ami javíthatja a sebességet és a pontosságot.

## Profi tippek a termelés‑kész OCR-hez

- **Cache-eld a licenc** objektumot, ha sok fájlt dolgozol fel egy ciklusban; az ismételt létrehozás többletterhet jelent.  
- **Kötegelt feldolgozás**: töltsd be az összes nyugta útvonalát egyetlen `OcrInput`-ba, és hívd meg egyszer a `recognize`-t. A JSON egy oldalak tömbjét tartalmazza, mindegyik saját sorokkal.  
- **Validáld a JSON-t**: a karakterlánc megszerzése után parse-ld egy, például Jackson könyvtár segítségével, hogy megbizonyosodj a helyes formátumról, mielőtt tárolnád.  
- **Figyeld a biztonsági pontszámot**: a JSON minden sorhoz tartalmaz egy `confidence` mezőt. Szűrd ki az alacsonyabb (pl. 0,85 alatti) pontszámú sorokat, hogy elkerüld a szemét adatot.  
- **Biztosítsd a licencet**: tárold az `Aspose.OCR.lic` fájlt egy biztonságos tárolóban vagy környezeti változóban, különösen felhőalapú telepítések esetén.

## Összegzés

Áttekintettük, **hogyan használjunk OCR-t** Java-ban a **szöveg felismeréséhez képről**, **szöveg kinyeréséhez PNG** nyugtákból, és **nyugtát konvertáljunk JSON-re** – mindezt egy tömör, vég‑től‑végig példával. A lépések egyszerűek, a kód teljesen futtatható, és a JSON kimenet egy strukturált reprezentációt ad, amely készen áll bármely downstream rendszer számára.

A következő lépésben érdemes lehet fejlettebb forgatókönyveket felfedezni: a JSON-t Apache Kafka-ba küldeni valós‑idő feldolgozáshoz, regex mintákat alkalmazni a tételösszegek kinyeréséhez, vagy egy felhőalapú OCR szolgáltatással integrálni a skálázhatóság érdekében. Akármit is választasz, a most megtanult alapok változatlanok maradnak.

Van kérdésed, vagy elakadtál valahol a kipróbálás során? Hagyj egy megjegyzést alább, és együtt megoldjuk. Boldog kódolást, és élvezd, ahogy a rendezetlen nyugta képeket tiszta, kereshető adatokra változtatod!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}