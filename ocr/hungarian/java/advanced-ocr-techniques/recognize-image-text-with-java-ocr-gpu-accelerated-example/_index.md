---
category: general
date: 2026-03-28
description: Tanulja meg, hogyan ismerje fel a képek szövegét Java-ban az Aspose OCR
  segítségével, hogyan extraháljon szöveget PNG fájlokból, és hogyan használjon GPU
  gyorsítást a nagy képek gyors OCR-hoz.
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: hu
og_description: Fedezze fel, hogyan ismerheti fel a képen lévő szöveget Java-ban,
  hogyan nyerhet ki szöveget PNG-fájlokból, és hogyan használhat GPU-gyorsítást nagy
  képek OCR-hez.
og_title: Képszöveg felismerése Java OCR-rel – GPU-gyorsított példa
tags:
- OCR
- Java
- GPU
title: Képszöveg felismerése Java OCR-rel – GPU‑gyorsított példa
url: /hu/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# képek szövegének felismerése Java OCR-rel – GPU‑gyorsított példa

Volt már szükséged arra, hogy **képek szövegét** felismerd egy hatalmas PNG‑ből, de a CPU‑os változat lassú volt? Nem vagy egyedül. Sok valós környezetben – gondolj a számlák beolvasására vagy a történelmi dokumentumok archiválására – a képméret könnyen óriási lehet, és az alapértelmezett OCR‑motor egyszerűen nem tud lépést tartani.  

Jó hír: az Aspose OCR for Java lehetővé teszi, hogy **GPU gyorsítást** használj a folyamat felgyorsításához, és a kód meglepően kompakt. Ebben az útmutatóban egy teljes, futtatható Java OCR példát látsz, amely **kivonja a szöveget PNG** fájlokból, CUDA‑támogatott GPU‑t használ, és egy **OCR nagy képet** kezel néhány kódsorral. A végére pontosan tudni fogod, hogyan illeszd be ezt a saját Java projektedbe, és miért fontosak az egyes beállítások.

## Mit fogsz megtanulni

- Hogyan állítsd be az Aspose OCR‑t Maven vagy Gradle projektben.  
- A lépésről‑lépésre folyamat a **képek szövegének** GPU‑n történő felismeréséhez.  
- Miért javíthatja a teljesítményt a GPU‑streamek számának beállítása.  
- Hogyan ellenőrizd a kimenetet és oldd meg a gyakori hibákat.  

> **Előfeltételek** – Java 17 (vagy újabb), CUDA‑kompatibilis GPU a legújabb driverrel, és érvényes Aspose OCR for Java licenc (az ingyenes próbaverzió értékeléshez elegendő). Egyéb külső könyvtárak nem szükségesek.

---

## 1. lépés: Aspose OCR függőség hozzáadása

Először is hozd be az Aspose OCR könyvtárat a buildbe. Ha **Maven**‑t használsz, add hozzá a következő kódrészletet a `pom.xml`‑hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

**Gradle** esetén helyezd ezt a `build.gradle`‑ba:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tipp:** A legújabb verzió (2026 márciusától) tartalmaz teljesítményjavításokat a GPU‑feladatokhoz, ezért mindig a legfrissebb kiadást használd.

---

## 2. lépés: OCR motor inicializálása és GPU engedélyezése

OCR motor létrehozása egyszerű. A lényeges rész a GPU jelző bekapcsolása – különben a motor CPU módra vált vissza.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // 3️⃣ (Optional) Set the number of GPU streams for parallel processing
        //    More streams can improve throughput on multi‑core GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);
```

### Miért engedélyezzük a GPU‑t?

Amikor bekapcsolod a `setUseGpu(true)`‑t, az Aspose a nehéz konvolúciós neurális hálózat számításait a grafikus kártyára terheli át. Ez néhány másodpercet takaríthat meg egy **ocr nagy kép** feldolgozási idejéből, különösen ha a kép mérete meghaladja a 4000 × 4000 px‑et. Ha a környezetedben nincs kompatibilis GPU, a hívás egyszerűen nem csinál semmit, és a motor a CPU‑n folytatja – nem omlik össze, csak lassabb a teljesítmény.

## 3. lépés: PNG kép felismerése és a szöveg kinyerése

Most irányítsd a motort arra a fájlra, amelyet feldolgozni szeretnél. A példa a `sample-large.png`‑t használja, de bármilyen PNG vagy JPEG fájlra cserélheted.

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Program futtatásakor valami ilyesmit kell látnod:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

Ez a kimenet megerősíti, hogy a **képek szövegének** felismerése sikeres volt, és hogy sikeresen **kivontad a szöveget png** tartalomból.

## 4. lépés: GPU kihasználtság ellenőrzése (opcionális, de hasznos)

Ha kíváncsi vagy, hogy a GPU valóban használatban van-e, nyisd meg a rendszer GPU‑monitorozó eszközét (pl. `nvidia-smi` Linuxon). Amíg a Java folyamat fut, egy mérsékelt memóriaterhelés és számítási kihasználtság növekedést kell látnod.

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

Ha nem látsz aktivitást, ellenőrizd a következőket:

1. A CUDA driver egyezik a GPU modelljével.  
2. A `setUseGpu(true)` hívás nem kerül felülírásra később a kódban.  
3. A licencfájlod (ha van) nem korlátozza a GPU használatát.

## 5. lépés: Gyakori szélsőséges esetek kezelése

### Nagy képek, amelyek meghaladják a GPU memória kapacitását

Ha egy kép hatalmas (pl. 8000 × 8000 px), a GPU memóriája kifogyhat. Egy gyors megoldás, hogy a képet lecsökkented, mielőtt az Aspose‑nak átadod:

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage original = ImageIO.read(new File("sample-large.png"));
int maxDim = 4000; // target max dimension
int width = original.getWidth();
int height = original.getHeight();

float scale = Math.min((float)maxDim / width, (float)maxDim / height);
int newWidth = Math.round(width * scale);
int newHeight = Math.round(height * scale);

BufferedImage resized = new BufferedImage(newWidth, newHeight, original.getType());
// Simple scaling (for demo purposes)
resized.getGraphics().drawImage(original, 0, 0, newWidth, newHeight, null);
ImageIO.write(resized, "png", new File("sample-resized.png"));
```

Ezután add át a `"sample-resized.png"`‑t a `recognizeImage`‑nek. Így az OCR pontos marad, miközben a GPU korlátokon belül marad.

### Többoldalas PDF‑ek

Az Aspose OCR képes a PDF‑eket oldalanként kezelni. Ciklusban végigmenj minden oldalon, konvertáld képpé, és add át a motorba. Az ugyanaz a **use gpu acceleration** jelző érvényes, így egy gyors PDF‑szöveg csővezetéked lesz.

## Teljes működő példa (másolás‑beillesztés kész)

Az alábbiakban a teljes Java osztály látható, amely készen áll a fordításra és futtatásra. Cseréld le a `YOUR_DIRECTORY`‑t a PNG fájlod elérési útjára.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // Step 3: (Optional) Set the number of GPU streams for parallel processing
        // Using 2 streams works well on most modern GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);

        // Step 4: Perform OCR on the input image
        // This will **recognize image text** from a PNG file.
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // Step 5: Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Várható kimenet** – egy egyszerű szöveges ábrázolás mindenről, amit a motor a képből ki tud olvasni. Ha a kép táblázatot tartalmaz, a cellák tartalmát sortörésekkel összefűzve kapod; az Aspose nem őrzi meg a layoutot, de szükség esetén utófeldolgozhatod a szöveget.

## Gyakran Ismételt Kérdések

| Kérdés | Válasz |
|----------|--------|
| **Szükségem van fizetett licencre?** | A próbaverzió legfeljebb 200 oldalra működik, és eltávolítja a vízjelet az OCR‑ből. Produkcióban a licenc eltávolítja a korlátokat és feloldja a teljes GPU stacket. |
| **Mi van, ha a GPU‑m régebbi (pl. GTX 750)?** | A régebbi GPU‑k még működhetnek, de csökkentett sebességgel; győződj meg róla, hogy legalább Compute Capability 3.0‑val rendelkeznek. |
| **Feldolgozhatok JPG vagy BMP fájlokat?** | Természetesen – a `recognizeImage` bármely, a Java ImageIO által támogatott formátumot elfogad. |
| **Van mód sok képet kötegelt feldolgozni?** | Az OCR hívást egy ciklusba helyezheted, és érdemes növelni a `setGpuStreams` értékét, hogy megfeleljen a kívánt egyidejű streamek számának. |
| **Mi a teendő, ha meg kell őrizni a layoutot?** | Használd az Aspose OCR `LayoutOptions`‑át a körülhatároló dobozok lekéréséhez; ez túlmutat a gyors útmutató keretein, de dokumentálva van az API‑ban. |

## Következtetés

Most már van egy tömör, vég‑a‑végig **java ocr példa**, amely **képek szövegét** felismeri, **kivonja a szöveget png** formátumból, és **GPU gyorsítást** használ az **ocr nagy kép** feldolgozásának felgyorsításához. A GPU stream számának finomhangolásával és szükség esetén a túl nagy képek lecsökkentésével a megoldást szinte bármilyen hardverkörnyezethez igazíthatod.

Készen állsz a következő lépésre? Próbáld meg egy mappa beolvasott nyugtáit betáplálni ugyanabba a csővezetékbe, vagy kísérletezz az Aspose `TextRegion` API‑jával, hogy megőrizd az eredeti layoutot. Ha bármilyen problémába ütközöl, az Aspose fórumok és a Javadoc kiváló források – csak tartsd szem előtt az itt bemutatott alapokat.

Boldog kódolást, és legyen az OCR‑d villámgyors!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}