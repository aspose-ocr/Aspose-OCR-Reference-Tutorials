---
category: general
date: 2026-05-06
description: Hogyan használjuk az OCR-t szöveg kinyerésére képből Java-ban. Ismerje
  meg az OCR kép‑szöveg átalakítást, javítsa az OCR hibákat, és töltse be a képet
  OCR-hez az Aspose OCR segítségével.
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: hu
og_description: Hogyan használjuk az OCR-t Java-ban a képről szöveg kinyeréséhez,
  az OCR hibák javításához és a kép betöltéséhez OCR-hez az Aspose OCR segítségével.
og_title: Hogyan használjuk az OCR-t Java-ban – Teljes útmutató
tags:
- OCR
- Java
- Aspose
title: Hogyan használjunk OCR-t Java-ban – Szöveg kinyerése képből helyesírási javítással
url: /hu/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjuk az OCR-t Java‑ban – Szöveg kinyerése képből helyesírási javítással

Gondolkodtál már azon, **hogyan használjuk az OCR-t**, hogy egy elmosódott nyugta fotót tiszta, kereshető szöveggé alakítsunk? Nem vagy egyedül. Sok projektben – költségkövető alkalmazásokban, számla‑digitalizálási folyamatokban vagy akár egy gyors jegyzetkészítő szkriptben – a megbízható szöveg kinyerése a képből az első akadály.

Ez a bemutató pontosan megmutatja, hogyan használjuk az OCR-t Java‑ban, a kép betöltésétől a hibák javításáig, hogy az eredmény úgy olvasható legyen, mintha ember gépelte volna. A végére **kép‑szöveg kinyerést**, **OCR image to text** konverziót és a gyakori felismerési hibák automatikus javítását is elsajátítod.

## Mit fogunk építeni

Készítünk egy apró Java konzolprogramot, amely:

1. Betölti a PNG‑t (vagy bármely támogatott formátumot) az Aspose OCR motorba.  
2. Engedélyezi a beépített helyesírás‑javító funkciót a **OCR hibák javításához**.  
3. Elindítja a felismerési folyamatot és kiírja a megtisztított szöveget.  

Nincs külső szolgáltatás, nincs nehéz keretrendszer – csak egy JAR és néhány kódsor.

### Előfeltételek

- Java Development Kit (JDK) 8 vagy újabb.  
- Maven (vagy bármely build eszköz) az Aspose OCR könyvtár letöltéséhez.  
- Egy képfájl (pl. `receipt.png`), amelyet elemezni szeretnél.  

Ha hiányzik az Aspose OCR JAR, add hozzá ezt a függőséget a `pom.xml`‑hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **Pro tipp:** Az ingyenes értékelő verzió teszteléshez megfelelő, de egy licenc eltávolítja az értékelő vízjelet.

## 1. lépés – Az OCR motor inicializálása (Primary Keyword in Action)

Az első dolog, amit meg kell tenned, egy `OcrEngine` példány létrehozása. Gondolj rá úgy, mint a “agyra”, amely a pixeleket karakterekké alakítja.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*Miért fontos:* A motor inicializálása beállítja a belső erőforrásokat (nyelvi modellek, szótárak stb.). Ennek kihagyása `NullPointerException`‑t eredményez, amikor később képet próbálsz betölteni.

## 2. lépés – Kép betöltése OCR‑hez

Most ténylegesen **betöltjük a képet OCR‑hez**. Az Aspose egy kényelmes `ImageStream.fromFile` segédfüggvényt biztosít, de ha szeretnéd, `byte[]`‑ként is betáplálhatod.

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*Gyakori buktató:* A fájl útvonalának abszolútnak vagy a munkakönyvtárhoz relatívnak kell lennie. Ha a kép nem található, a motor `IOException`‑t dob. Ellenőrizd az útvonalat, különösen IDE‑ból vagy csomagolt JAR‑ból futtatva.

## 3. lépés – Helyesírás‑javítás engedélyezése a **OCR hibák javításához**

Azonnal használható OCR gyakran zajos – gondolj a “l0ve” helyett “love” vagy “0” helyett “O” hibákra. A helyesírás‑javítás bekapcsolása azt mondja a motornak, hogy egy utófeldolgozó lépést hajtson végre a tipikus hibák kijavítására.

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*Miért érdemes:* Helyesírás‑javítás nélkül manuálisan kell tisztítanod a kimenetet, ami aláássa az automatizálás célját. A beépített szótár jól működik angolul és több más nyelven is.

## 4. lépés – Felismerés végrehajtása (**OCR Image to Text**)

Miután a kép betöltődött és a helyesírás‑javítás be van kapcsolva, végre kérhetjük a motort, hogy ismerje fel a szöveget.

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*Szélsőséges eset:* Ha a kép alacsony kontrasztú vagy erősen ferde, az eredmény még mindig értelmetlen karaktereket tartalmazhat. Fontold meg előfeldolgozást (pl. binarizálás, kiegyenesítés) a motorba való betáplálás előtt.

## 5. lépés – A megtisztított szöveg kiírása

Az utolsó lépés egyszerűen a végeredmény kiírása. Egy valódi alkalmazásban adatbázisba vagy fájlba írnád, de a bemutatóhoz a `System.out` elegendő.

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Várt kimenet

Tegyük fel, hogy a `receipt.png` egy tiszta tételeket tartalmazó listát mutat, akkor valami ilyesmit láthatsz:

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

Vedd észre, hogy a “Qty” és a “Price” helyesen van leírva, még akkor is, ha az eredeti szken egy “Qy” hibát tartalmazott.

## Teljes működő példa

Az alábbi programot másold be egy `SpellCorrectDemo.java` nevű fájlba. Győződj meg róla, hogy az Aspose OCR JAR a classpath‑on van.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

Futtasd a következővel:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

Most már a megtisztított szöveget kell látnod a konzolon.

## Bónusz: Beállítások finomhangolása a jobb pontosságért

Bár az alapértelmezett konfiguráció a legtöbb nyomtatott dokumentumnál működik, speciális esetekben érdemes néhány paramétert módosítani:

| Beállítás | Mit csinál | Mikor változtass |
|-----------|------------|-------------------|
| `setLanguage(OcrLanguage.English)` | Angol szótárat kényszerít (csökkenti a hamis pozitívokat) | Ha a képen csak angol szöveg van. |
| `setResolution(300)` | A forráskép DPI‑ját adja meg a motor számára | Magas felbontású szkennelés esetén. |
| `setEnableAutoSkewCorrection(true)` | Automatikusan kiegyenesíti a kissé ferde oldalakat | Telefonra készült képek esetén. |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## Gyakran Ismételt Kérdések

**K: Működik ez PDF‑ekkel?**  
V: Igen. Konvertáld a PDF minden oldalát képpé (pl. az Aspose PDF‑el), majd add az OCR motorhoz.

**K: Mi van, ha a képem BMP formátumú?**  
V: Az `ImageStream.fromFile` natívan támogatja a PNG, JPEG, BMP, TIFF és GIF formátumokat. Csak cseréld le a fájlkiterjesztést.

**K: Kikapcsolhatom a helyesírás‑javítást?**  
V: Természetesen – állítsd `setEnableSpellCorrection(false)`‑ra, ha nyers OCR kimenetre van szükséged a további feldolgozáshoz.

## Összegzés

Most már tudod, **hogyan használjuk az OCR-t** Java‑ban **szöveg kinyeréséhez képből**, automatikusan **OCR hibák javításával**, és helyesen **képet betöltve OCR‑hez** az Aspose OCR‑del. Az öt lépéses folyamat – inicializálás, betöltés, helyesírás‑javítás engedélyezése, felismerés és kiírás – lefedi a mindennapi OCR feladatok nagy részét.

Innen tovább gondolhatod, hogy a logikát adatbázis‑visszaírással, REST‑endpointtal vagy kötegelt feldolgozóval láncolod, hogy egyszerre több tucat nyugtát kezelj. Kísérletezz a fenti beállítási táblázattal, hogy a lehető legmagasabb pontosságot érd el.

Boldog kódolást, és legyen az OCR eredményed mindig tisztább, mint a kávé‑foltos nyugtáid! 

![how to use ocr diagram showing image → OCR engine → corrected text flow]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}