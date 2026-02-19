---
category: general
date: 2026-02-19
description: Képről szöveg kinyerése Java OCR-rel. Tanulj meg egy Java OCR példát,
  amely betölti a képet OCR-hez, és néhány lépésben kinyeri a szöveget a számla fájlokból.
draft: false
keywords:
- extract text from image
- java ocr example
- load image for ocr
- extract text from invoice
language: hu
og_description: Szöveg kinyerése képről Java OCR-rel. Ez az útmutató bemutatja, hogyan
  töltsünk be képet OCR-hez, és hogyan nyerjünk ki szöveget számlákból egy egyszerű
  Java OCR példával.
og_title: Szöveg kinyerése képből Java-ban – Teljes OCR példa
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Szöveg kinyerése képből Java-ban – Teljes OCR példa
url: /hu/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg kinyerése képből Java‑val – Teljes OCR példa

Valaha is szükséged volt **szöveg kinyerésére képből**, de nem tudtad, melyik könyvtárat válaszd? Nem vagy egyedül – sok fejlesztő szembesül ezzel a problémával számlák automatizálása vagy kereshető archívumok építése közben. A jó hír? Néhány Java sorral betöltheted a képet OCR‑hez, meghatározhatsz egy érdeklődési területet (ROI), és kinyerheted a pontos szöveget, amire szükséged van.

Ebben az útmutatóban végigvezetünk egy **java ocr example**-n, amely megmutatja, hogyan **load image for OCR**, állíts be egy ROI‑t, és **extract text from invoice** fájlokból az Aspose.OCR segítségével. A végére egy futtatható programod lesz, amelyet bármely Java projektbe beilleszthetsz.

## Mit tanulhatsz meg

- Hogyan hozd létre az `OcrEngine` példányt, és miért fontos ez.
- A helyes **load image for OCR** módszer az Aspose `ImageStream`‑jével.
- **Region of interest (ROI)** beállítása, hogy csak a számlaösszeget tartalmazó képrészletet dolgozd fel.
- A felismert szöveg kinyerése és a konzolra írása.
- Gyakori hibák (pl. rossz téglalap koordináták) és gyors megoldások.

**Előfeltételek**

- Telepített Java 8 vagy újabb.
- Maven vagy Gradle a Aspose.OCR könyvtár (`com.aspose:aspose-ocr`) beszerzéséhez.
- Egy minta számla kép (`invoice.png`) egy ismert könyvtárban.

Minden megvan? Remek – vágjunk bele.

![Szöveg kinyerése képből Java OCR‑rel](/images/extract-text-from-image-java.png "szöveg kinyerése képből példa")

## Szöveg kinyerése képből – Lépésről‑lépésre Java OCR példa

Az alábbiakban a teljes forráskód található. Nyugodtan másold be a `RoiOcrExample.java` fájlba, és futtasd közvetlenül.

```java
import com.aspose.ocr.*;

public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance.
        // The engine holds all configuration and performs the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image.
        // You can point to any PNG, JPG, or TIFF file. Here we use a sample invoice.
        String imagePath = "YOUR_DIRECTORY/invoice.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Define the region of interest (ROI) you want to recognize.
        // x = 120, y = 340, width = 500, height = 120 – tweak these values for your own layout.
        Rectangle regionOfInterest = new Rectangle(120, 340, 500, 120);
        ocrEngine.setRegionOfInterest(regionOfInterest);

        // Step 4: Perform OCR on the specified ROI and retrieve the text.
        // recognize() returns an OcrResult object; getText() extracts the plain string.
        String extractedText = ocrEngine.recognize().getText();

        // Step 5: Output the recognized text.
        System.out.println("ROI text: " + extractedText);
    }
}
```

### Miért fontos minden egyes lépés

1. **Az OCR motor létrehozása** – motor nélkül nincs kontextus a képfeldolgozáshoz. Az objektum később lehetővé teszi a nyelvi csomagok finomhangolását, ha többnyelvű támogatásra van szükség.  
2. **A kép betöltése** – a `ImageStream.fromFile` elrejti a fájlformátum részleteit, biztosítva, hogy a motor helyesen olvassa a bájtokat. Ha ezt kihagyod, `NullPointerException`-t kapsz.  
3. **ROI beállítása** – az egész oldal feldolgozása pazarló. A téglalap szűkítése a számlaösszeg területére felgyorsítja a felismerést és csökkenti a zajt.  
4. **`recognize()` meghívása** – itt történik a varázslat. A metódus lefuttatja az OCR algoritmust a ROI‑n, és egy eredményobjektumot ad vissza.  
5. **Az eredmény kiírása** – valós projektekben valószínűleg adatbázisba mentenéd a szöveget, de a `System.out.println` tökéletes egy gyors demóhoz.

## Load Image for OCR

Ha azon gondolkodsz, hogy a útvonalnak abszolútnak vagy relatívnak kell-e lennie, a válasz: mindkettő működik – csak győződj meg róla, hogy a Java folyamat olvasni tudja a fájlt. Windows alatt a visszafelé perjeleket meg kell duplázni (`C:\\images\\invoice.png`), vagy használhatsz előre perjeleket (`C:/images/invoice.png`).

**Pro tipp:** Ha sok számlát dolgozol fel egy ciklusban, használd újra ugyanazt az `OcrEngine` példányt; ez belső erőforrásokat cache‑el, és növeli a teljesítményt.

## Define Region of Interest (ROI)

A megfelelő téglalap kiválasztása gyakran próbálgatást igényel. Egy egyszerű módszer a koordináták megtalálására, ha megnyitod a képet bármely grafikus szerkesztőben (pl. GIMP vagy Paint.NET), és az egérrel a terület fölé húzod – a státuszsorban megjelennek az X/Y értékek.

Külön eset: egyes számlák változó elrendezésűek. Ilyenkor először futtathatsz egy gyors elő‑szkennelést az egész képen, megkeresheted a „Total:” kulcsszót regex‑szel, majd dinamikusan állíthatod be az ROI‑t.

## Perform OCR and Get Text

A `recognize()` hívás szinkron – a szálad blokkolódik, amíg a motor be nem fejezi a munkát. Nagy köteg esetén érdemes szálkészletet indítani, és a képeket párhuzamosan feldolgozni. Ne feledd, hogy minden szálnak saját `OcrEngine` példányra van szüksége; a motor nem szálbiztos.

## Run and Verify Output

Fordítsd le és futtasd:

```bash
javac -cp "path/to/aspose-ocr.jar" RoiOcrExample.java
java -cp ".:path/to/aspose-ocr.jar" RoiOcrExample
```

A kimenet valami ilyesmi lesz:

```
ROI text: $1,254.00
```

Ha a kimenet értelmetlennek tűnik, ellenőrizd újra az ROI koordinátákat, és győződj meg róla, hogy a kép minősége magas (300 dpi vagy több a legjobb).

### Gyakori hibák és megoldások

| Tünet | Valószínű ok | Megoldás |
|-------|--------------|----------|
| Üres string | ROI kívül esik a kép határain | Ellenőrizd a téglalap értékeket a kép méreteivel szemben |
| Hibás szavak | Alacsony felbontás | Használj nagyobb felbontású forrást vagy alkalmazz előfeldolgozást (pl. binarizálás) |
| `java.lang.NoClassDefFoundError` | Hiányzó Aspose JAR a classpath‑on | Add hozzá az `aspose-ocr.jar`‑t a `-cp`‑hez, vagy használd a Maven/Gradle függőségkezelést |

## Conclusion

Most már tudod, hogyan **extract text from image** Java‑ban egy tömör **java ocr example** segítségével. A kép helyes betöltésével, egy fókuszált ROI meghatározásával és a `recognize()` meghívásával megbízhatóan **extract text from invoice** fájlokból nyerhetsz szöveget, és továbbadhatod azt downstream rendszereknek.

Mi a következő lépés? Próbáld ki az ROI cseréjét más mezőkre (dátum, szállító neve), kísérletezz nyelvi csomagokkal többnyelvű számlákhoz, vagy integráld az OCR lépést egy Spring Boot mikroservice‑be. Ugyanez a minta működik nyugtákkal, útlevelekkel vagy bármilyen dokumentummal, ahol pontos szövegkinyerésre van szükség.

Ha kérdésed van a megoldás skálázásával vagy zajos szkennelés kezelésével kapcsolatban, írj egy megjegyzést alább – jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}