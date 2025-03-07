---
title: OCR végrehajtása nyelvválasztással az Aspose.OCR-ben
linktitle: OCR végrehajtása nyelvválasztással az Aspose.OCR-ben
second_title: Aspose.OCR Java API
description: Oldja fel a képekből a precíz szövegkivonást az Aspose.OCR for Java segítségével. Kövesse lépésenkénti útmutatónkat a pontos OCR és a nyelv kiválasztásához.
weight: 11
url: /hu/java/ocr-operations/perform-ocr-language-selection/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR végrehajtása nyelvválasztással az Aspose.OCR-ben

## Bevezetés

A technológia folyamatosan fejlődő világában az Optical Character Recognition (OCR) kulcsszerepet játszik abban, hogy értelmes információt nyerjen ki a képekből. Az Aspose.OCR for Java hatékony eszközként tűnik ki, amely lehetővé teszi a fejlesztők számára, hogy zökkenőmentesen integrálják az OCR-képességeket Java-alkalmazásaikba. Ebben a lépésenkénti útmutatóban megvizsgáljuk, hogyan hajthat végre OCR-t nyelvválasztással az Aspose.OCR használatával, felszabadítva a sokféle tartalom precíz feldolgozásának lehetőségét.

## Előfeltételek

Mielőtt belevágna az oktatóanyagba, győződjön meg arról, hogy a következő előfeltételek teljesülnek:

- Java fejlesztői környezet: Győződjön meg arról, hogy a Java telepítve van a rendszeren, és a fejlesztői környezet be van állítva.

-  Aspose.OCR Library: Töltse le és telepítse a Java Aspose.OCR könyvtárat. Megtalálható a könyvtár és a kapcsolódó dokumentáció[itt](https://reference.aspose.com/ocr/java/).

- Képfájl: Készítsen egy képfájlt, amely a kicsomagolni kívánt szöveget tartalmazza. Például használjunk egy „p3.png” nevű fájlt.

## Csomagok importálása

Java-projektjében importálja a szükséges csomagokat az Aspose.OCR funkciók kihasználásához. Adja hozzá a következő sorokat a Java fájl elejéhez:

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

## 1. lépés: Állítsa be a dokumentumkönyvtárat

```java
// A dokumentumok könyvtárának elérési útja.
String dataDir = "Your Document Directory";
```

Cserélje ki a "Saját dokumentumkönyvtár" elemet annak a könyvtárnak az elérési útjára, ahol a képfájl található.

## 2. lépés: Határozza meg a kép elérési útját

```java
// A kép útja
String file = dataDir + "p3.png";
```

Állítsa be a fájlváltozót úgy, hogy az adott képfájlra mutasson.

## 3. lépés: Hozzon létre Aspose.OCR API-példányt

```java
// API-példány létrehozása
AsposeOCR api = new AsposeOCR();
```

Inicializálja az AsposeOCR objektumot a funkciók eléréséhez.

## 4. lépés: Állítsa be a felismerési beállításokat

```java
// Állítsa be a felismerési beállításokat
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Testreszabhatja a felismerési beállításokat az Ön igényei szerint. Állítsa be a paramétereket, például a ferdeséget, a nyelvet és a felismerési területeket.

## 5. lépés: Végezze el az OCR-t és kérje le az eredményeket

```java
// Eredményobjektum lekérése
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Hajtsa végre az OCR műveletet a megadott képfájl és beállítások használatával. Rögzítse az eredményt a RecognitionResult objektumban.

## 6. lépés: Nyomtassa ki és használja fel az eredményeket

```java
// Eredmény nyomtatása
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

Nyomtassa ki a kivont szöveget, a felismerési területeket, a JSON-ábrázolást, a ferde szöget és az esetleges figyelmeztetéseket. Az eredményeket szükség szerint használja az alkalmazásában.

## Következtetés

Ebben az oktatóanyagban az Aspose.OCR for Java zökkenőmentes integrációjával foglalkoztunk, hogy nyelvválasztással végezzen OCR-t. Ez a nagy teljesítményű könyvtár a lehetőségek világát nyitja meg a fejlesztők számára, akik célja, hogy szöveget pontosan kinyerjenek a képekből.

## GYIK

### 1. kérdés: Használhatom az Aspose.OCR-t több nyelvhez egyetlen felismerési folyamat során?

1. válasz: Igen, több nyelvet is beállíthat a RecognitionSettingsben, hogy javítsa a többnyelvű tartalom felismerésének pontosságát.

### 2. kérdés: Hogyan kezelhetem a különböző képformátumokat az Aspose.OCR segítségével?

2. válasz: Az Aspose.OCR különféle képformátumokat támogat, beleértve a PNG-t, JPEG-et és TIFF-et. Egyszerűen adja meg a helyes fájl elérési utat a kép elérési út változójában.

### 3. kérdés: Van-e korlátozás az Aspose.OCR által feldolgozható kép méretére?

3. válasz: Az Aspose.OCR különböző méretű képeket képes kezelni, de a nagyobb képek több feldolgozási időt és erőforrást igényelhetnek.

### 4. kérdés: Finomhangolhatom a felismerési beállításokat a kép bizonyos régióihoz?

A4: Abszolút. Használja a RecognitionAreas funkciót, hogy meghatározott téglalapokat határozzon meg a képen belül a célzott felismerés érdekében.

### 5. kérdés: Az Aspose.OCR alkalmas személyes és kereskedelmi projektekre is?

5. válasz: Igen, az Aspose.OCR rugalmas licencelési lehetőségeket kínál, így személyes és kereskedelmi használatra egyaránt alkalmas.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
