---
category: general
date: 2026-03-07
description: Futtass OCR-t képen Java-val. Tanuld meg, hogyan ismerj fel szöveget
  PNG-ből, hogyan nyerj ki szöveget egy nyugtáról, és hogyan tölts be képet OCR-hez
  egy teljes Java OCR példával.
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: hu
og_description: Futtass OCR-t képen Java-val. Ez az útmutató bemutatja, hogyan ismerjünk
  fel szöveget PNG-ből, hogyan nyerjünk ki szöveget egy nyugtából, és hogyan töltsünk
  be képet OCR-hez egy teljes Java OCR példával.
og_title: OCR futtatása képen Java-val – GPU-val támogatott szövegkinyerés
tags:
- OCR
- Java
- GPU
- Image Processing
title: OCR futtatása képen Java-val – GPU-val támogatott szövegkinyerés
url: /hu/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR futtatása képen Java‑val – GPU‑val gyorsított szövegkinyerés

Szükséged volt már **OCR futtatására képfájlokon**, de nem tudtad, hol kezdjed Java‑ban? Nem vagy egyedül – sok fejlesztő ugyanabba a falba ütközik, amikor először próbál szöveget kinyerni egy beolvasott nyugtáról vagy egy PNG képernyőképről.  

Ebben a tutorialban végigvezetünk egy **teljes Java OCR példán**, amely nem csak **szöveget ismer fel PNG** fájlokból, hanem megmutatja, hogyan **nyerj ki szöveget nyugta‑képekről**, miközben a GPU gyorsítást használja a sebesség növelése érdekében. A végére egy kész‑programmal leszel felvértezve, amely betölti a képet OCR‑hez, feldolgozza, és kiírja a nyers szöveget.

## Mit fogsz megtanulni

- Hogyan **tölts be képet OCR‑hez** egy egyszerű `ImageInputStream`‑el.
- GPU‑támogatás engedélyezése, hogy a motor gyorsabban fusson modern hardveren.
- A pontos lépések a **szöveg felismeréséhez PNG‑ból** és a hasznos karakterláncok kinyeréséhez egy nyugtáról.
- Gyakori buktatók (pl. rossz GPU‑eszköz‑azonosító) és legjobb gyakorlatok.
- Egy teljes, futtatható kódrészlet, amelyet egyszerűen beilleszthetsz a kedvenc IDE‑dbe.

**Előfeltételek**

- Java 17 vagy újabb (a kód a `var` kulcsszót használja a tömörség kedvéért, de Java 8‑on is helyettesítheted explicit típusokkal).
- Egy OCR könyvtár, amely biztosítja az `OcrEngine`, `ImageInputStream` és `OcrResult` osztályokat (például a fiktív *FastOCR* SDK; cseréld le a saját általad használt könyvtárra).
- GPU‑val felszerelt gép, ha a teljesítménybeli előnyt szeretnéd (opcionális, de ajánlott).

---

## 1. lépés: OCR futtatása képen – GPU gyorsítás engedélyezése

Az első teendő az OCR motor létrehozása és a GPU használatának beállítása. Ez a lépés kritikus, mert GPU‑támogatás nélkül a motor a CPU‑ra vált vissza, ami jelentősen lassabb lehet nagy felbontású nyugták esetén.

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**Miért fontos:**  
A GPU gyorsítás átvállalja az OCR motorok által végzett nehéz mátrix‑számításokat. Ha több GPU‑d is van, a `setGpuDeviceId` érték módosításával választhatod ki a legtöbb memóriával rendelkező eszközt. A GPU engedélyezésének elhagyása gyakori oka a „miért olyan lassú az OCR‑om?” panaszoknak.

> **Pro tipp:** Ha a gépednek nincs kompatibilis GPU‑ja, a `setUseGpu(true)` hívás egyszerűen figyelmen kívül marad – nem omlik össze, csak lassabb lesz a feldolgozás.

---

## 2. lépés: Kép betöltése OCR‑hez

Most, hogy a motor készen áll, be kell táplálnunk egy képet. Az alábbi példa megmutatja, hogyan tölts be egy lemezen tárolt PNG nyugtát. A fájlútvonalat bármilyen, az OCR könyvtárad által támogatott képtípusra cserélheted.

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**Szélsőséges eset:**  
Ha a fájl nem létezik vagy az útvonal hibás, az `ImageInputStream` `IOException`‑t dob. Tedd a hívást try‑catch blokkba, és naplózz egy hasznos üzenetet:

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## 3. lépés: Szöveg felismerése PNG‑ból

Miután a kép betöltődött, az OCR motor most már varázsolhat. Ez a lépés **szöveget ismer fel PNG‑ból** (vagy bármely más támogatott formátumból), és egy `OcrResult` objektumot ad vissza.

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**Mi történik a háttérben?**  
A motor előfeldolgozást végez (kiegyenesítés, binarizálás), egy neurális hálózatot futtat a karakterek felismerésére, majd a karaktereket szövegsorokká állítja össze. Mivel korábban engedélyeztük a GPU‑t, ezek a neurális‑hálózati számítások a grafikus kártyán zajlanak, így másodperceket takarítunk meg a teljes futási időből.

---

## 4. lépés: Szöveg kinyerése nyugtáról

A felismerés után általában csak a nyers szöveget szeretnéd. Az `OcrResult` osztály általában egy `getText()` metódust biztosít, amely egy `String`‑et ad vissza. Ezt aztán tovább feldolgozhatod (pl. regex‑szel kinyerheted az összegeket, dátumokat stb.).

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Tipikus nyugta‑kimenet:**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Ezt a karakterláncot most már átadhatod a saját parserednek, hogy kinyerje a végösszeget, a tételeket vagy az adóinformációkat.

---

## 5. lépés: Teljes Java OCR példa – Kész a futtatásra

Összegezve, itt van a **teljes Java OCR példa**, amelyet egyszerűen beilleszthetsz egy `Main.java` fájlba. Győződj meg róla, hogy az OCR könyvtár a classpath‑on van.

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Várható konzol‑kimenet** (a fenti mintanyugta alapján):

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Ha a kimenet értelmetlennek tűnik, ellenőrizd, hogy a kép tiszta‑e (magas DPI) és hogy az OCR nyelvi csomag megegyezik a nyugta nyelvével.

---

## Gyakori kérdések és buktatók

| Kérdés | Válasz |
|----------|--------|
| *Mi van, ha a GPU‑m nem kerül felismerésre?* | A motor automatikusan visszaesik a CPU‑ra. Ellenőrizd a drivereket, és hogy a `setGpuDeviceId` egy létező eszközre mutat (`nvidia-smi` Linuxon segíthet). |
| *Feldolgozhatok JPEG vagy TIFF fájlokat is?* | Igen – csak változtasd meg a fájlkiterjesztést az `ImageInputStream`‑ben. Az OCR könyvtár általában automatikusan felismeri a formátumot. |
| *Létezik-e mód tömeges nyugta‑feldolgozásra?* | Csomagold a felismerési kódot egy ciklusba, és használd ugyanazt az `OcrEngine` példányt; minden képhez újra inicializálni felesleges GPU‑memóriát pazarol. |
| *Hogyan javíthatom a pontosságot alacsony kontrasztú nyugtákon?* | Előfeldolgozd a képet (növeld a kontrasztot, konvertáld szürkeárnyalatba) mielőtt az OCR motorhoz adnád. Néhány könyvtár `preprocess` API‑t kínál. |

---

## Összegzés

Most már tudod, **hogyan futtass OCR‑t képfájlokon Java‑ban**, a kép betöltésétől a nyugta‑szöveg tiszta kinyeréséig. A bemutató lefedte a **szöveg felismerését PNG‑ból**, a **szöveg kinyerését nyugtáról**, és egy **java OCR példát**, amelyet bármely projekthez adaptálhatsz.  

Mi a következő lépés? Próbáld ki a GPU flag kikapcsolását, hogy lásd a teljesítménykülönbséget, kísérletezz különböző képfelbontásokkal, vagy integrálj egy regex‑alapú parsert a totalok automatikus kinyeréséhez. Ha mélyebben érdekel a téma, nézd meg az **OCR utófeldolgozást**, a **nyelvi modell‑korrekciót**, vagy a **tömeges feldolgozási pipeline‑okat**.

Jó kódolást, és legyenek mindig olvasható nyugtáid!  

![run OCR on image example](/images/run-ocr-on-image.png "run OCR on image – Java example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}