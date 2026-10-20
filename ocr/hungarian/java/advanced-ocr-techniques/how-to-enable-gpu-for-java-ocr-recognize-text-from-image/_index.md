---
category: general
date: 2026-02-22
description: Tanulja meg, hogyan engedélyezheti a GPU-t a Java OCR-ben, hogy képről
  szöveget ismerjen fel, és gyorsan kinyerje a számla szövegét az Aspose OCR használatával.
draft: false
keywords:
- how to enable gpu
- recognize text from image
- extract text from invoice
- java ocr example
- load image for ocr
language: hu
og_description: Hogyan engedélyezzük a GPU-t a Java OCR-ben, felismerjük a szöveget
  a képen, és kinyerjük a szöveget a számláról egy teljes Java OCR példával.
og_title: Hogyan engedélyezzük a GPU-t a Java OCR-hez – Gyors útmutató
tags:
- Java
- OCR
- GPU
- Aspose
title: Hogyan engedélyezzük a GPU-t a Java OCR-hez – Szöveg felismerése képről
url: /hu/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan engedélyezzük a GPU-t a Java OCR-hez – Szöveg felismerése képről

Valaha is elgondolkodtál **hogyan engedélyezzük a GPU-t**, amikor OCR-t végzel Java-ban? Nem vagy egyedül – sok fejlesztő teljesítménykorlátba ütközik nagy, nagy felbontású dokumentumok, például számlák feldolgozásakor. A jó hír? Az Aspose OCR segítségével egyetlen kapcsolót átkapcsolva a grafikus kártya elvégzi a nehéz munkát. Ebben az útmutatóban végigvezetünk egy **java ocr example**-en, amely betölt egy képet, engedélyezi a GPU feldolgozást, és villámgyorsan kinyeri a szöveget egy számláról.

Mindent lefedünk a könyvtár telepítésétől a hiányzó GPU‑illesztőprogramokkal kapcsolatos edge case‑ek kezeléséig. A végére képes leszel **szöveget felismerni képről** fájlokból valós időben, és lesz egy stabil sablonod minden jövőbeli OCR projekthez. Nem szükséges külső hivatkozás – csak tiszta, futtatható kód.

## Előfeltételek

- **Java Development Kit (JDK) 11** vagy újabb telepítve a gépeden.  
- **Maven** (vagy Gradle) a függőségkezeléshez.  
- **GPU‑képes rendszer** naprakész illesztőprogramokkal (NVIDIA, AMD vagy Intel).  
- Egy számla képfájlja (pl. `large_invoice_300dpi.png`).  

Ha valamelyik hiányzik, először szerezd be; a további útmutató feltételezi, hogy mind megvan.

## 1. lépés: Aspose OCR hozzáadása a projekthez

Az első dolog, amire szükségünk van, az Aspose OCR könyvtár. Maven-nel egyszerűen illeszd be a következő kódrészletet a `pom.xml`-edbe:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

> **Pro tip:** A verziószám rendszeresen változik; ellenőrizd a Maven Central‑t a legújabb kiadásért, hogy naprakész maradj.

Ha inkább Gradle-t használsz, az ekvivalens:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

Miután a függőség feloldódik, készen állsz arra, hogy kódot írj, amely kommunikál az OCR motorral.

## 2. lépés: GPU engedélyezése az Aspose OCR motorban

Most jön a főszereplő – a GPU feldolgozás bekapcsolása. Az Aspose OCR három feldolgozási módot kínál:

| Mode | Description |
|------|-------------|
| `CPU_ONLY` | Tiszta CPU, minden gépen biztonságos. |
| `GPU_ONLY` | Kényszeríti a GPU-t, hibát jelez, ha nincs kompatibilis eszköz. |
| `AUTO_GPU` | Felismeri a GPU-t és használja, ha elérhető, egyébként visszatér a CPU-hoz. |

A legtöbb esetben a **`AUTO_GPU`** módot ajánljuk, mert a legjobb kombinációt nyújtja. Így engedélyezheted:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Enable GPU processing (AUTO_GPU uses GPU when available)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // The rest of the steps follow...
    }
}
```

> **Why this matters:** A GPU engedélyezése akár a 300 dpi‑os számla feldolgozási idejét is több másodpercről egy másodpercnél kevesebbre csökkentheti, a hardvertől függően.

## 3. lépés: Kép betöltése OCR-hez – Szöveg felismerése képről

Mielőtt a motor bármit olvasna, meg kell adnod neki egy képet. Az Aspose OCR `OcrInput` osztálya fájlutakat, stream‑eket vagy akár `BufferedImage` objektumokat is elfogad. Egyszerűség kedvéért fájlutatot használunk:

```java
// Step 3.1: Prepare the input image
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png"); // <-- replace with your actual path
```

> **Edge case:** Ha a kép nagyobb, mint 5 MB, fontold meg a lejjebb mintavételezést, hogy elkerüld a GPU‑memória kifogyását.

## 4. lépés: OCR végrehajtása és szöveg kinyerése a számláról

Most megkérjük a motort, hogy csinálja a varázslatát. A `recognize` metódus egy `OcrResult` objektumot ad vissza, amely a kinyert szöveget, a biztonsági pontszámokat és a layout információkat tartalmazza.

```java
// Step 4.1: Run the recognition
OcrResult ocrResult = ocrEngine.recognize(ocrInput);

// Step 4.2: Print the extracted text to console
System.out.println("=== Extracted Text ===");
System.out.println(ocrResult.getText());
```

A program futtatásakor valami ilyesmit kell látnod:

```
=== Extracted Text ===
Invoice #12345
Date: 2026-02-20
Total: $1,245.67
...
```

Ha a kimenet összezavarodott, ellenőrizd, hogy a kép tiszta-e, és hogy az OCR nyelv helyesen van-e beállítva (az Aspose alapértelmezés szerint angol, de módosítható például `ocrEngine.setLanguage(OcrEngine.Language.SPANISH)`‑nel).

## 5. lépés: Teljes működő példa (másolás-beillesztés készen)

Az alábbiakban a teljes, önálló Java osztály található. Illeszd be a kedvenc IDE-dbe, állítsd be a képútvonalat, és nyomd meg a **Run** gombot.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU (auto‑detect)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace with the absolute or relative path to your invoice image
        ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png");

        // 4️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Várható kimenet

A kód egy tiszta 300 dpi‑os számlán általában egy egyszerű szöveges ábrázolást ad minden sorra a dokumentumban. A pontos kimenet a számla elrendezésétől függ, de olyan mezőket látsz majd, mint *Invoice Number*, *Date*, *Total Amount* és a tétel leírásai.

## Gyakori hibák és megoldások

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| **`java.lang.UnsatisfiedLinkError`** | GPU driver hiányzik vagy inkompatibilis | Telepítsd a legújabb illesztőprogramot az NVIDIA/AMD/Intel weboldaláról. |
| **Very slow processing** | GPU visszaesik csendben CPU-ra | Ellenőrizd, hogy `ocrEngine.getProcessingMode()` `AUTO_GPU`‑t ad vissza, és hogy a `SystemInfo.isGpuAvailable()` igaz. |
| **Blank output** | A kép túl sötét vagy alacsony kontrasztú | Előfeldolgozással (kontraszt növelése, binarizálás) javítsd a képet, mielőtt OCR-nek adnád. |
| **Out‑of‑Memory** | Nagyon nagy kép (>10 MP) | Méretezd át vagy oszd fel a képet csempékre; dolgozd fel őket külön-külön. |

## Lépés‑ről‑lépésre összefoglaló (gyors referencia)

| Step | What You Did |
|------|--------------|
| 1 | Added Aspose OCR dependency |
| 2 | Created `OcrEngine` and set `AUTO_GPU` |
| 3 | Loaded an invoice image via `OcrInput` |
| 4 | Called `recognize` and printed `ocrResult.getText()` |
| 5 | Handled common errors and verified output |

## További lépések – Következő lépések

- **Batch processing:** Egy mappában lévő számlákon ciklus, és minden eredmény tárolása adatbázisban.  
- **Language support:** `ocrEngine.setLanguage(OcrEngine.Language.FRENCH)` használata többnyelvű számlákhoz.  
- **Post‑processing:** Reguláris kifejezésekkel mezők kinyerése, mint *Invoice Number* vagy *Total Amount* a nyers szövegből.  
- **GPU tuning:** Ha több GPU-d van, a `ocrEngine.setGpuDeviceId(int id)` segítségével válaszd ki a leggyorsabbat.

## Következtetés

Megmutattuk, **hogyan engedélyezzük a GPU-t** a Java OCR-hez, bemutattuk egy tiszta **java ocr example**-t, és végigvezettük a teljes folyamatot a **kép betöltése OCR-hez**‑től a **szöveg kinyerése a számláról**‑ig. Az Aspose `AUTO_GPU` módjának kihasználásával teljesítményjavulást érhetsz el anélkül, hogy feláldoznád a kompatibilitást – tökéletes fejlesztői gépekre és produkciós szerverekre egyaránt.

Próbáld ki, finomítsd a kép előfeldolgozást, és kísérletezz kötegelt feladatokkal. A lehetőségek határtalanok, ha a GPU gyorsítását egy robusztus OCR könyvtárral kombinálod.

---

![Diagram a GPU‑gyorsított OCR csővezetékről – hogyan engedélyezzük a GPU-t a Java OCR-hez](https://example.com/images/gpu-ocr-pipeline.png "hogyan engedélyezzük a gpu-t a Java OCR-hez")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}