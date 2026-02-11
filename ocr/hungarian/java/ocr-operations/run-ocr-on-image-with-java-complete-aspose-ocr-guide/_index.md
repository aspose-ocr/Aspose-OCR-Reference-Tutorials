---
category: general
date: 2026-02-09
description: Futtass OCR-t képen az Aspose OCR Java használatával – tanuld meg, hogyan
  nyerj ki szöveget PNG-ből, és engedélyezd az automatikus nyelvfelismerést néhány
  lépésben.
draft: false
keywords:
- run OCR on image
- extract text from PNG
- auto detect language OCR
- Aspose OCR Java
- Hindi OCR example
language: hu
og_description: Futtass OCR-t a képen azonnal. Ez az útmutató bemutatja, hogyan lehet
  szöveget kinyerni PNG fájlokból, és hogyan engedélyezhető az automatikus nyelvfelismerés
  az Aspose OCR for Java használatával.
og_title: OCR futtatása képen Java-val – Teljes Aspose OCR útmutató
tags:
- OCR
- Java
- Aspose
title: OCR futtatása képen Java-val – Teljes Aspose OCR útmutató
url: /hu/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/
---

optional) → szöveg kinyerése PNG". Keep "language configuration" maybe keep English because it's a term? Could translate to "nyelvi konfiguráció". But it's a phrase. Let's translate to Hungarian: "nyelvi konfiguráció". So final line: "OCR futtatása képen → nyelvi konfiguráció → automatikus nyelvfelismerés OCR (optional) → szöveg kinyerése PNG". Keep optional in parentheses.

Now ensure we didn't translate any code placeholders.

Now produce final output with all content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR futtatása képen Java-val – Teljes Aspose OCR útmutató

Valaha szükséged volt **OCR futtatása képen** fájlok futtatására, de nem tudtad, hol kezdj hozzá? Lehet, hogy van néhány PNG képernyőfotód, amelyek hindi szöveget tartalmaznak, és azon tűnődsz, hogy a Java ki tudja-e nyerni a szavakat anélkül, hogy hatalmas gépi tanulási környezetre lenne szükség. A jó hír: meg tudod, és meglepően egyszerű az Aspose OCR használatával.

Ebben a tutorialban egy valós példán keresztül vezetünk végig, amely **szöveg kinyerése PNG** fájlokból, megmutatja, hogyan lehet engedélyezni a **automatikus nyelvfelismerés OCR**-t, és egy kész‑futtatható Java programot ad. A végére egy működő kódrészletet kapsz, amely hindi karaktereket nyomtat a konzolra, és megérted, miért fontos minden sor.

## Amire szükséged lesz

- **Java Development Kit (JDK) 8** vagy újabb – a kód bármely friss verzióval lefordítható.  
- **Aspose.OCR for Java** könyvtár – töltsd le a legújabb JAR-t az Aspose weboldaláról vagy a Maven Centralból.  
- Egy minta kép (`hindi_sample.png`) Devanagari írással – bármilyen képernyőfelvétel‑eszközzel létrehozhatsz egyet.  
- Egy IDE vagy egyszerű szövegszerkesztő – én az IntelliJ IDEA‑t használom, de a `javac` is működik.

Nincs külső szolgáltatás, nincs felhő API kulcs, csak egy helyi JAR és egy kép. Egyszerű, ugye?

## 1. lépés: Aspose OCR hozzáadása a projekthez

Először győződj meg róla, hogy az Aspose OCR JAR a classpath‑on van. Ha Maven‑t használsz, add hozzá ezt a függőséget:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

Ha a manuális megoldást részesíted előnyben, töltsd le a `aspose-ocr-23.10.jar`‑t, helyezd a `libs/` mappába, majd fordítsd a következővel:

```bash
javac -cp "libs/*" LanguageExample.java
```

> **Pro tip:** Tartsd a JAR verziószámot egy megjegyzésben a forrásfájlod tetején – segít a későbbi önnek emlékezni, melyik API felületet céloztad meg.

## 2. lépés: OCR motor példány létrehozása

Most elindítjuk a magobjektumot, amely minden nehéz feladatot elvégez. Tekintsd a `OcrEngine`‑t a művelet agyának.

```java
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

Miért példányosítod itt? A motor tárolja a konfigurációs beállításokat (például a nyelvet) és újrahasználható erőforrásokat, így egyszeri létrehozása az alkalmazáson belül csökkenti a terhelést.

## 3. lépés: Nyelvi beállítások konfigurálása (és az Auto‑Detect engedélyezése)

Ha előre tudod a nyelvet – például Hindi –, megmondhatod a motornak, hogy a Devanagari‑ra fókuszáljon. Ez növeli a pontosságot és felgyorsítja a feldolgozást.

```java
// Step 3a: Force Hindi (Devanagari) recognition
ocrEngine.getConfiguration().setLanguage(Language.HINDI);

// Step 3b (optional): Let the engine guess the language if you're unsure
ocrEngine.getConfiguration().setAutoDetectLanguage(true);
```

A `setAutoDetectLanguage(true)` sor a **auto detect language OCR** kapcsoló. Ha vegyes nyelvű képet adsz a motorhoz, az automatikusan megpróbálja azonosítani minden írást. Hasznos kötegelt feladatoknál, ahol nem tudod manuálisan címkézni minden fájlt.

## 4. lépés: OCR futtatása a PNG képen

Itt történik a tényleges **OCR futtatása képen** adatfeldolgozás. A `recognize` metódus elfogad egy fájlútvonalat, beolvassa a bitmapet, és visszaad egy `RecognitionResult`‑ot.

```java
// Step 4: Perform OCR on the PNG file
RecognitionResult result = ocrEngine.recognize("YOUR_DIRECTORY/hindi_sample.png");
```

Cseréld le a `YOUR_DIRECTORY`‑t a valódi mappára. Ha a fájl nem található, az Aspose egy egyértelmű kivételt dob – nem kell később kitalálni, miért sikertelen.

## 5. lépés: Kinyert szöveg lekérése és megjelenítése

Végül vedd ki a felismert karakterláncot a result objektumból, és írd ki. Hindi esetén Unicode karaktereket látsz a konzolon, ha a terminálod támogatja az UTF‑8‑at.

```java
// Step 5: Output the recognized Hindi text
System.out.println("Hindi text:");
System.out.println(result.getText());
```

**Várható kimenet** (feltételezve, hogy a minta kép azt mondja: “नमस्ते दुनिया”):

```
Hindi text:
नमस्ते दुनिया
```

Ha engedélyezted az auto‑detect-et, és a kép angolt is tartalmazott, a kimenet mindkét írást tartalmazná, szépen keveredve.

## Teljes működő példa

Az alábbiakban a teljes, futtatható program látható. Másold be a `LanguageExample.java`‑ba, állítsd be a kép útvonalát, és már indulhat is.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Specify the language to be recognized (Hindi – Devanagari script)
        ocrEngine.getConfiguration().setLanguage(Language.HINDI);

        // Step 3: (Optional) Enable automatic fallback to language detection
        ocrEngine.getConfiguration().setAutoDetectLanguage(true);

        // Step 4: Run OCR on the input image
        RecognitionResult result = ocrEngine.recognize("YOUR_DIRECTORY/hindi_sample.png");

        // Step 5: Print the extracted Hindi text
        System.out.println("Hindi text:");
        System.out.println(result.getText());
    }
}
```

> **Megjegyzés:** Ha IDE‑t használsz, győződj meg róla, hogy a projekt build útvonala tartalmazza az Aspose OCR JAR‑t. IntelliJ‑ben menj a *File → Project Structure → Libraries* menüpontra, és add hozzá a JAR‑t ott.

## Gyakori kérdések és szélhelyzetek

### Mi van, ha a PNG alacsony felbontású?

Az OCR pontossága drasztikusan csökken 150 dpi alatt. Növeld fel a képet egy olyan eszközzel, mint az ImageMagick (`convert input.png -resize 200% output.png`), mielőtt a motorhoz adnád. Az `auto detect language OCR` jelző továbbra is működik, de kevesebb hibás felismerést látsz.

### Feldolgozhatok több képet egy ciklusban?

Természetesen. Csomagold be a `recognize` hívást egy `for` ciklusba, és használd újra ugyanazt az `OcrEngine` példányt. A motor újrahasználata elkerüli a nyelvi modellek minden iterációban történő újratöltését, ami memóriát és CPU‑időt takarít meg.

```java
String[] files = {"img1.png", "img2.png", "img3.png"};
for (String file : files) {
    RecognitionResult r = ocrEngine.recognize(file);
    System.out.println("Text from " + file + ":");
    System.out.println(r.getText());
}
```

### Hogyan kezelem a nem Unicode konzolokat?

Ha a terminálod torz szimbólumokat mutat, állítsd a fájl kódolását UTF‑8‑ra, amikor elindítod a Java‑t:

```bash
java -Dfile.encoding=UTF-8 -cp "libs/*" LanguageExample
```

### Van mód a bizalmi pontszámok lekérésére?

Igen. A `RecognitionResult` tartalmazza a `getConfidence()`‑t, amely 0 és 1 közötti float értéket ad vissza minden felismert sorra. Iterálhatsz a `result.getLines()`‑on, hogy kinyerd ezeket az értékeket – hasznos alacsony bizalmi eredmények szűréséhez.

## Pro tippek a termeléshez

- **Cache language models**: Ha több ezer képet dolgozol fel, tartsd a motort élő állapotban a teljes köteghez.  
- **Parallel processing**: Csomagolj minden képet egy `Callable`‑ba, és add át egy szálkészletnek. Ne feledd, hogy a motor nem szálbiztos; példányosíts egyet szálanként.  
- **Logging**: Használj megfelelő naplózót (SLF4J) a `System.out.println` helyett nagy feladatoknál.  
- **Memory management**: Hívd meg az `ocrEngine.dispose()`‑t, miután befejezted, hogy felszabadítsd a natív erőforrásokat.

## Vizualizált áttekintés

![Run OCR on image example diagram](ocr_flow.png "Run OCR on image example diagram")

A fenti diagram szemlélteti a folyamatot: **OCR futtatása képen → nyelvi konfiguráció → automatikus nyelvfelismerés OCR (optional) → szöveg kinyerése PNG**.

## Következtetés

Most bemutattuk, hogyan **OCR futtatása képen** fájlokat használhatunk az Aspose OCR for Java‑val, hogyan **szöveg kinyerése PNG** nyelvspecifikus beállításokkal, és hogyan kapcsolható be a **auto detect language OCR** rugalmas, többnyelvű helyzetekhez. A teljes kódminta készen áll a másolásra, fordításra és futtatásra – nincsenek rejtett lépések, nincs külső szolgáltatás.

Készen állsz a következő kihívásra? Próbáld megcserélni a `Language.HINDI`‑t `Language.AUTO`‑ra, és adj egy vegyes írású dokumentumot, vagy kísérletezz PDF bemenettel (az Aspose OCR PDF‑et is támogat). Ezt a kódrészletet be is illesztheted egy Spring Boot REST végpontra, hogy OCR‑t webszolgáltatásként biztosíts.

Boldog kódolást, és legyenek a képeid mindig olvashatóak!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}