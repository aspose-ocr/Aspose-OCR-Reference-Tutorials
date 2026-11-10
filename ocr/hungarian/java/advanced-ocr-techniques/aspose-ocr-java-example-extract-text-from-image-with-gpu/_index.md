---
category: general
date: 2026-06-28
description: Tanuljon meg egy Aspose OCR Java példát, amellyel szöveget nyerhet ki
  képekből Java projektekben, és állítsa be a GPU memória korlátot a gyorsabb eredmények
  érdekében.
draft: false
keywords:
- aspose ocr java example
- extract text from image java
- set gpu memory limit
- gpu accelerated OCR Java
- Aspose OCR licensing
language: hu
og_description: Aspose OCR Java példa, amely bemutatja, hogyan lehet Java kóddal szöveget
  kinyerni egy képből, miközben a GPU memória korlátját állítja be az optimális teljesítmény
  érdekében.
og_title: Aspose OCR Java példa – Gyors GPU‑gyorsított szövegkinyerés
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn an Aspose OCR Java example to extract text from image Java projects
    and set GPU memory limit for faster results.
  headline: Aspose OCR Java Example – Extract Text from Image with GPU
  type: TechArticle
tags:
- Aspose OCR
- Java
- GPU
title: Aspose OCR Java példa – Szöveg kinyerése képből GPU-val
url: /hu/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-image-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Java példa – Szöveg kinyerése képből GPU-val

Gondolkodtál már azon, hogyan **extract text from image Java** alkalmazásokban lehet szöveget kinyerni a képből anélkül, hogy a CPU-dat leállítaná? Nem vagy egyedül. Sok valós helyzetben—például nyugta beolvasás, személyazonosság ellenőrzés vagy tömeges dokumentum archiválás—az szűk keresztmetszet maga az OCR motor.

Jó hír: ez a **Aspose OCR Java example** végigvezet egy teljes, azonnal futtatható programon, amely GPU gyorsítást használ, és még megmutatja, hogyan **set GPU memory limit** a szervered boldog maradjon. A útmutató végére egy működő Java osztályod lesz, amely beolvassa a kép fájlt, a GPU-n futtatja az OCR-t, és kiírja a felismert szöveget a konzolra. Nincs homályos hivatkozás, csak konkrét kód és világos magyarázat.

Mindent lefedünk a licenceléstől a GPU finomhangolásáig, így akár tapasztalt Java fejlesztő vagy, akár csak most ismerkedsz a számítógépes látással, itt hasznos információkat találsz. Az egyetlen előfeltétel egy Java fejlesztői környezet (JDK 8 vagy újabb) és egy CUDA‑ vagy OpenCL‑kompatibilis GPU elérése.

---

## Előkövetelmények

- **Java Development Kit (JDK) 8+** – letöltheted az Oracle‑tól vagy az OpenJDK‑t használhatod.  
- **Aspose.OCR for Java** library – szerezd be a JAR‑t az Aspose weboldaláról vagy a Maven Central‑ról.  
- **A valid Aspose OCR license file** (`Aspose.OCR.Java.lic`). A ingyenes próba működik teszteléshez, de a licenc eltávolítja a kiértékelési vízjeleket.  
- **GPU with CUDA or OpenCL support** – a demó automatikusan felismeri a legjobb módot, de a drivereket telepíteni kell.  
- **An image to test** – egy tiszta PNG vagy JPEG nyugta, jel vagy bármilyen nyomtatott szöveg képe.  

Ha bármelyik ismeretlennek tűnik, ne ess pánikba. Az alábbi lépések a pontos letöltési linkekre mutatnak, és megmutatják, hová kell elhelyezni a fájlokat.

---

## 1. lépés: Aspose OCR Java Example – A projekt beállítása

Először hozz létre egy új Maven projektet (vagy egy egyszerű mappát, ha a sima `javac`-t részesíted előnyben). Add hozzá az Aspose OCR függőséget a `pom.xml`-hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **Pro tip:** A Maven letölti az összes transzitív függőséget, beleértve a GPU támogatású könyvtárakat is, így nem kell extra JAR‑okat keresned.

Helyezd el az `Aspose.OCR.Java.lic` fájlt a projekt gyökerében (vagy bármely mappában, amelyre később hivatkozol). A **aspose ocr java example**, amelyet építünk, a licenc útvonalát `"Aspose.OCR.Java.lic"`-nek várja.

---

## 2. lépés: Az Aspose OCR licenc alkalmazása

A licenc lépés kritikus—nélküle az OCR motor értékelő módban fut, és a kimenetet vízjellel látja el. Íme a minimális kód, amire szükséged van:

```java
import com.aspose.ocr.*;

public class LicenseUtil {
    public static void applyLicense() throws Exception {
        License license = new License();
        // Adjust the path if your license file lives elsewhere
        license.setLicense("Aspose.OCR.Java.lic");
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

Ennek egyszeri futtatása az alkalmazás indításakor garantálja, hogy **all subsequent OCR calls** teljesen licencelt legyen.

---

## 3. lépés: GPU gyorsítás beállítása – GPU memória limit beállítása

Most jön a szórakoztató rész: megmondani az Aspose-nak, hogy használja a GPU-t, és opcionálisan **set GPU memory limit**. A könyvtár a `GpuEngineOptions`-t tartalmazza, amely lehetővé teszi a GPU mód be- és kikapcsolását, eszköz kiválasztását, és a memóriahasználat korlátozását. A memória korlátozása hasznos megosztott szervereken, ahol nem akarod, hogy az OCR feladatod elnyelje az egész GPU-t.

```java
import com.aspose.ocr.gpu.*;

public class GpuConfig {
    public static GpuEngineOptions createOptions() {
        GpuEngineOptions gpuOptions = new GpuEngineOptions();
        gpuOptions.setEnableGpu(true);          // turn on GPU acceleration
        gpuOptions.setDeviceId(0);              // use the first GPU device
        gpuOptions.setMemoryLimitMb(2048);      // **set GPU memory limit** to 2 GB
        System.out.println("GPU options configured (memory limit = 2048 MB).");
        return gpuOptions;
    }
}
```

> **Why set a memory limit?** Ha az OCR feladataid nagyon nagy képeket tartalmaznak vagy sok egyidejű feladatot futtatsz, a GPU gyorsan kifogyhat a VRAM‑ból, ami összeomláshoz vezet. A lefoglalás korlátozásával a folyamatot biztonságos keretek között tartod, és más terhelések is békésen együttműködhetnek.

---

## 4. lépés: Extract Text from Image Java – Kép betöltése

A licencelés és a GPU beállítások után végre **extract text from image Java** kódot írhatsz. Az alábbi részlet létrehozza az `OcrEngine`-t a GPU beállításokkal, betölti a kép fájlt, és elvégzi a felismerést.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the license
        LicenseUtil.applyLicense();

        // 2️⃣ Set up GPU options (including memory limit)
        GpuEngineOptions gpuOptions = GpuConfig.createOptions();

        // 3️⃣ Create the OCR engine with GPU acceleration
        OcrEngine ocrEngine = new OcrEngine(gpuOptions);

        // 4️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        // Replace the placeholder with your actual image path
        ocrInput.add("YOUR_DIRECTORY/receipt.png");

        // 5️⃣ Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 6️⃣ Output the recognized text
        System.out.println("Recognized Text (GPU):");
        System.out.println(ocrResult.getText());
    }
}
```

**Kulcsfontosságú pontok** in this **aspose ocr java example**:

- `OcrInput.add()` több képet is elfogadhat; a motor sorban dolgozza fel őket.  
- `ocrResult.getText()` egy egyszerű szöveges karakterláncot ad vissza, megőrizve a sortöréseket, de nem a layout információkat.  
- Az egész folyamat a GPU-n fut, ami **5‑10× gyorsabb** lehet, mint a csak CPU‑s feldolgozás nagy felbontású képeknél.

---

## 5. lépés: A demó futtatása és a kimenet ellenőrzése

Fordítsd le és futtasd a programot:

```bash
mvn compile exec:java -Dexec.mainClass=GpuOcrDemo
```

Ha minden helyesen van beállítva, valami ilyesmit kell látnod:

```
Aspose OCR license applied successfully.
GPU options configured (memory limit = 2048 MB).
Recognized Text (GPU):
Item   Qty   Price
Apple   2    $1.20
Banana  5    $0.75
Total          $5.85
```

A pontos szöveg a képedtől függ, de a lényeg, hogy a konzol kiírja **the recognized text** a “Evaluation version” vízjel nélkül. Ha `CUDA driver not found` hibát kapsz, ellenőrizd, hogy a GPU drivered naprakész-e, és a CUDA toolkit a rendszer útvonalában van-e.

---

## Gyakori hibák és elkerülésük

| Tünet | Valószínű ok | Megoldás |
|---------|--------------|-----|
| `OutOfMemoryError: CUDA out of memory` | GPU memória túllépése | Csökkentsd a `setMemoryLimitMb` értékét (pl. 1024) vagy dolgozz kisebb képrészletekkel. |
| `LicenseException` | Licencfájl hiányzik vagy az útvonal hibás | Győződj meg róla, hogy az `Aspose.OCR.Java.lic` elérhető és az útvonal helyes. |
| No text returned | A kép túl homályos vagy rossz színtér | Előfeldolgozd a képet (növeld a kontrasztot, konvertáld szürkeárnyalatba) mielőtt az OCR-nek adnád. |
| GPU not used | `setEnableGpu(false)` vagy hiányzó driver | Ellenőrizd a `gpuOptions.setEnableGpu(true)` beállítást és telepítsd újra a GPU drivereket. |

---

## A példa bővítése

Miután már van egy stabil **aspose ocr java example**, esetleg szeretnél:

- **Batch process a folder** – fájlok bejárása és az eredmények adatbázisba mentése.  
- **Detect language** – használd a `ocrEngine.setLanguage(OcrLanguage.English)`-t vagy adj hozzá több nyelvet.  
- **Apply post‑processing** – tisztítsd meg a nyers karakterláncot regex‑szel vagy küldd egy helyesírás-ellenőrzőnek.  

Ezek a bővítések mind ugyanazt a licencelési és GPU konfigurációs kódot használják, így csak az üzleti logikát kell hozzáadnod.

---

## Záró gondolatok

Most láttál egy teljes **aspose ocr java example**-t, amely **extracts text from image Java** alkalmazásokból szöveget nyer ki, miközben **setting GPU memory limit** a robusztus teljesítményért. A fő ötletek—korai licenc, GPU konfigurálás, kép betáplálása, szöveg olvasása—újra felhasználhatók számtalan projektben, a nyugtaolvasóktól az automatizált űrlapkitöltő rendszerekig.

Innen nyugodtan kísérletezhetsz különböző `GpuEngineOptions` értékekkel, próbálj nagyobb képeket, vagy integráld az OCR lépést egy Spring Boot mikroservice-be. A határ a csillagos ég, és a GPU gyorsításnak köszönhetően ez a határ sokkal magasabb, mint korábban.

Van kérdésed, vagy segítségre van szükséged a memória beállítások finomhangolásához a saját hardveredhez? Írj egy megjegyzést alább, és jó kódolást!

---

![Aspose OCR Java Example diagram showing flow from image input → GPU‑accelerated OCR → text output](https://example.com/images/aspose-ocr-java-example-diagram.png "aspose ocr java example diagram")

## Mit érdemes következőként megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódpéldákat lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan állíts be licencet és ellenőrizd az Aspose.OCR licencet Java-ban](/ocr/english/java/ocr-basics/set-license/)
- [Szöveg kinyerése képből Java-val az Aspose.OCR Detect Areas móddal](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Kép konvertálása szöveggé Java-ban az Aspose.OCR BufferedImage használatával](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}