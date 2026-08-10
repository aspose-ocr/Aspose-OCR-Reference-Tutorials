---
category: general
date: 2026-02-14
description: Képről szöveg kinyerése Aspose OCR segítségével Java-ban. Tanulja meg,
  hogyan nyerhet ki szöveget űrlapmezőkből érdeklődési területekkel a pontos eredményekért.
draft: false
keywords:
- extract text from image
- extract text from form
language: hu
og_description: Képről szöveg kinyerése az Aspose OCR Java verziójával. Ez az útmutató
  bemutatja, hogyan lehet szöveget kinyerni űrlapmezőkből a érdeklődési területeken
  keresztül.
og_title: Szöveg kinyerése képből az Aspose OCR segítségével – Java útmutató
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Kép szövegének kinyerése az Aspose OCR-rel – Java útmutató
url: /hu/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Képről szöveg kinyerése Aspose OCR-rel – Java útmutató

Valaha is szükséged volt **szöveg kinyerésére a képről**, de végül az egész képet kellett feldolgozni, CPU‑ciklusokat pazarolva és zajos eredményeket kapva? Nem vagy egyedül. Sok valós alkalmazásban—gondoljunk csak számlabeolvasókra, útlevélolvasókra vagy adatbeviteli űrlapokra—csak néhány mező érdekel, nem az egész vászon.  

A jó hír, hogy az Aspose OCR lehetővé teszi **szöveg kinyerését a képről** *és* a specifikus űrlapterületekről poligonok definiálásával. Ebben az útmutatóban pontosan megmutatjuk, hogyan **nyerheted ki a szöveget űrlap** mezőkből Java használatával, miért fontos ez a megközelítés, és mit kell finomhangolni, ha valami nem a tervek szerint alakul.

Az alábbiakban mindent áttekintünk a könyvtár beállításától a bonyolult edge case-ek kezeléséig, így a végére egy kész‑használatra szánt kódrészletet kapsz, amely csak a szükséges adatokat nyeri ki.

## Amire szükséged lesz

- Java 17 (vagy bármely újabb JDK) – az újabb verziók jobb Unicode támogatással rendelkeznek.  
- Aspose.OCR for Java 23.10 (vagy a legfrissebb verzió a olvasás időpontjában).  
- Egy minta kép `form.png` néven, amely egyértelműen definiált mezőket tartalmaz.  
- Egy IDE vagy egyszerű szövegszerkesztő – IntelliJ IDEA, VS Code vagy akár a Notepad is megfelel.

A core demóhoz nincs szükség Maven/Gradle varázslatra; egyszerűen add hozzá az Aspose OCR JAR‑t az osztályútvonaladhoz.

---

## 1. lépés – Az OCR motor inicializálása és a kép betöltése

Az első dolog, amire a motornak szüksége van, egy bitmap, amin dolgozhat. A `form.png` fájlra mutatunk, amely az forrásfájlhoz ugyanabban a mappában található.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

*Miért fontos ez:*  
Egy új `OcrEngine` létrehozása tiszta lappal indul, biztosítva, hogy nincsenek maradék beállítások, amelyek befolyásolhatják a futást. A kép korai betöltése ellenőrzi, hogy a fájl létezik, így hasznos kivételt kapsz, mielőtt időt vesztegetnél a későbbi lépéseken.

> **Pro tipp:** Ha a képed hatalmas (több mint 5 MB), fontold meg először átméretezni. Az Aspose OCR gyorsabban működik 2000 px alatti képeken bármelyik dimenzióban.

---

## 2. lépés – Poligonok definiálása a kívánt mezőkhöz

Egy *Region of Interest* (ROI) egyszerűen egy poligon, amely megmondja a motornak, hol keressen. Lent két téglalapot hozunk létre – egyet a „First Name” (keresztnév) és egyet a „Date of Birth” (születési dátum) számára. Állítsd be a koordinátákat a saját űrlapodnak megfelelően.

```java
        // Polygon for the first field (e.g., First Name)
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},   // X‑coordinates
                new int[]{100, 100, 150, 150}, // Y‑coordinates
                4);

        // Polygon for the second field (e.g., Date of Birth)
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);
```

*Miért poligonok a téglalapok helyett?*  
A poligonok rugalmasságot biztosítanak a ferde vagy nem téglalap alakú dobozok kezeléséhez – ami gyakori a nyomtatott űrlapok beolvasásakor, ha azok nem tökéletesen igazodnak.

---

## 3. lépés – Mondd meg az Aspose OCR‑nek, hogy csak ezeken a területeken dolgozzon

Most a poligonokat a motorhoz kötjük. A `setRegionsOfInterest` metódus egy listát fogad, így annyi mezőt adhatsz hozzá, amennyit csak szeretnél.

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*Mi történik a háttérben?*  
Az Aspose OCR minden poligont külön bitmapre vág, lefuttatja a felismerési algoritmust, majd összefűzi az eredményeket. Ez drámaian csökkenti a környező grafikákból származó hamis pozitív találatokat.

---

## 4. lépés – Az OCR folyamat futtatása

Miután minden be van állítva, elindítjuk az OCR‑t. A `process()` hívás egy `OcrResult` objektumot ad vissza, amely a kinyert szöveget és a biztonsági pontszámokat tartalmazza.

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

Ha mezőnkénti biztonsági pontszámra van szükséged, megvizsgálhatod a `ocrResult.getRegions()`‑t – minden régió saját pontszámot hordoz. A legtöbb egyszerű űrlap esetén az összesített szöveg elegendő.

---

## 5. lépés – A kinyert szöveg megjelenítése (vagy tárolása)

Végül kiírjuk az eredményt a konzolra. Egy valódi alkalmazásban adatbázisba, JSON fájlba írhatod, vagy egy API‑n keresztül továbbíthatod.

```java
        // Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Várható kimenet (példa):**

```
=== Extracted Text ===
John Doe
12/04/1990
```

A két sor a definiált két poligonhoz tartozik. Ha extra szóközöket látsz, vágd le őket a `String.trim()`‑el.

---

## Hogyan nyerjünk ki szöveget űrlapból, ha sok mező van

Ha egy űrlap tucatnyi bemeneti mezőt tartalmaz, a koordináták kézi beírása fárasztóvá válik. Íme egy gyors minta, amit alkalmazhatsz:

1. **Hozz létre egy CSV‑t**, ahol minden sor a `fieldName, x1, y1, x2, y2, x3, y3, x4, y4` értékeket tartalmazza.  
2. **Töltsd be a CSV‑t** futásidőben, iterálj minden soron, építs egy `Polygon`‑t, és add hozzá az ROI listához.  

```java
List<Polygon> rois = new ArrayList<>();
try (BufferedReader br = new BufferedReader(new FileReader("fields.csv"))) {
    String line;
    while ((line = br.readLine()) != null) {
        String[] parts = line.split(",");
        int[] xs = { Integer.parseInt(parts[1]), Integer.parseInt(parts[3]),
                    Integer.parseInt(parts[5]), Integer.parseInt(parts[7]) };
        int[] ys = { Integer.parseInt(parts[2]), Integer.parseInt(parts[4]),
                    Integer.parseInt(parts[6]), Integer.parseInt(parts[8]) };
        rois.add(new Polygon(xs, ys, 4));
    }
}
ocrEngine.getEngineOptions().setRegionsOfInterest(rois);
```

*Miért éri meg?*  
Az ROI generálás automatizálása lehetővé teszi, hogy ugyanazt a Java kódot több űrlap elrendezésen is újrahasználd, így a projekt DRY (Don’t Repeat Yourself) marad.

---

## Edge case‑ek és tippek, amikre talán nem gondoltál

- **Elforgatott beolvasások:** Ha az egész kép el van forgatva, hívd a `ocrEngine.getEngineOptions().setRotateAngle(degrees)`‑t.  
- **Alacsony kontraszt:** Állítsd be a `ocrEngine.getEngineOptions().setContrast(1.5f)`‑t a olvashatóság növeléséhez.  
- **Nem latin írásrendszerek:** Válts nyelvet a `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)`‑val (vagy bármely támogatott nyelvvel).  
- **Részleges OCR hibák:** Mindig ellenőrizd a `ocrResult.getConfidence()`‑t; ha 80 % alá esik, fontold meg a felhasználó manuális ellenőrzésének kérését.  

---

## Teljes működő példa (másolás‑beillesztés kész)

Alább a teljes program, amely készen áll a fordításra és futtatásra. Cseréld le a `YOUR_DIRECTORY`‑t arra a mappára, amely a `form.png`‑t tartalmazza.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Step 1 – Initialize engine and load image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));

        // Step 2 – Define polygons for each form field
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},
                new int[]{100, 100, 150, 150},
                4);
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);

        // Step 3 – Limit OCR to those regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));

        // Step 4 – Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // Step 5 – Show the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Fordítás:

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

A két soros szöveget kell látnod, amely a definiált ROI‑khoz tartozik.

---

## Gyakran ismételt kérdések

**Q: Működik ez PDF‑ekkel?**  
A: Nem közvetlenül. Először konvertáld minden PDF oldalt képpé (pl. az Aspose PDF használatával), majd add az OCR motorhoz.

**Q: Mi van, ha az űrlapomnak jelölőnégyzetei vannak?**  
A: Az OCR nem tudja olvasni a logikai állapotokat, de a jelölőnégyzet területét ROI‑ként kezelheted, és a pixel sűrűség vizsgálatával következtethetsz a bejelölésre.

**Q: Kinyerhetünk szöveget egy többoldalas űrlapról egyszerre?**  
A: Iterálj minden oldal képen, használd újra ugyanazt az ROI listát, és fűzd össze az eredményeket.

---

## Következtetés

Végigvezettünk egy teljes, vég‑a‑végig megoldáson a **szöveg kinyeréséhez a képről** az Aspose OCR használatával, és bemutattuk, hogyan teszi lehetővé ugyanaz a technika a **szöveg kinyerését űrlap** mezőkből precíz pontossággal. Poligonok definiálásával, a motor fókuszának korlátozásával és a gyakori buktatók kezelésével gyors, tiszta adatokat kapsz anélkül, hogy az egész képet kellene feldolgozni.

Készen állsz a következő lépésre? Próbáld meg a OCR kimenetet JSON payload‑ba láncolni, vagy egy gépi‑tanulási modellnek átadni validációra. A lehetőségek határtalanok, és most te...

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}