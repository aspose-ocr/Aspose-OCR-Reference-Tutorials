---
category: general
date: 2026-02-17
description: Tanulja meg, hogyan ismerje fel a szöveget képről, és hogyan töltsön
  be képet OCR-hez az Aspose OCR Java könyvtár használatával. Lépésről‑lépésre útmutató
  helyesírás‑javítóval.
draft: false
keywords:
- recognize text from image
- load image for OCR
- Aspose OCR Java
- spell corrector OCR
- OCR engine setup
language: hu
og_description: Szöveg felismerése képről az Aspose OCR Java segítségével. Ez az útmutató
  bemutatja, hogyan töltsünk be képet OCR-hez, engedélyezzük a helyesírási javítást,
  és hogyan állítsunk elő tiszta szöveget.
og_title: szöveg felismerése képről – Teljes Aspose OCR Java útmutató
tags:
- Java
- OCR
- Aspose
title: Képről szöveg felismerése az Aspose OCR segítségével – Java útmutató
url: /hu/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-tutorial/
---

produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg felismerése képről az Aspose OCR – Java útmutató

Valaha szükséged volt **szöveg felismerésére képről**, de nem tudtad, melyik könyvtárat válaszd? Nem vagy egyedül. Sok valós projektben—gondolj csak a számlák beolvasására, a kézírásos jegyzetek digitalizálására vagy a képernyőképek feliratainak kinyerésére—az pontos OCR‑eredmények elérése kulcsfontosságú.  

Ebben az útmutatóban végigvezetünk a kép betöltésén OCR‑hez, az Aspose OCR beépített helyesírás‑javító bekapcsolásán, és végül a megtisztított szöveg kiíratásán. A végére egy azonnal futtatható Java programod lesz, amely **szöveget felismer képről** néhány kódsorral.

## Mit fed le ez az útmutató

- Hogyan alkalmazd az Aspose OCR licencet (így a demó vízjel nélkül fut)  
- Az `OcrEngine` példány létrehozása és az angol nyelv kiválasztása felismerési nyelvként  
- **Kép betöltése OCR‑hez** a `OcrInput` használatával, és egy hibás szavakat tartalmazó PNG‑re mutatva  
- A helyesírás‑javító engedélyezése, opcionálisan egy egyéni szótárra mutatva  
- A felismerés futtatása és a javított eredmény kiírása  

Nincsenek külső szolgáltatások, rejtett konfigurációs fájlok—csak tiszta Java és az Aspose OCR JAR.

> **Pro tipp:** Ha új vagy az Aspose‑ban, szerezz be egy ingyenes 30‑napos próba licencet az Aspose weboldaláról, és helyezd a `.lic` fájlt egy olyan mappába, amelyre a kódból hivatkozhatsz.

## Előfeltételek

- Java 8 vagy újabb (a kód JDK 11‑gyel is lefordítható)  
- Aspose.OCR for Java JAR a classpath‑odban  
- Érvényes `Aspose.OCR.lic` fájl (vagy futtathatod értékelő módban, de a demó vízjelet helyez be)  
- Egy képfájl (`misspelled.png`), amely szándékos helyesírási hibákat tartalmazó szöveget tartalmaz—tökéletes a helyesírás‑javító működésének megtekintéséhez  

Megvan mindez? Remek—merüljünk el.

## 1. lépés: Az Aspose OCR licenc alkalmazása

Mielőtt a motor bármilyen nehéz feladatot végezne, tudnia kell, hogy licencelt vagy. Ellenkező esetben a kimenetben egy „Trial version” felirat jelenik meg.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – replace the path with where you stored your .lic file
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

*Miért fontos:* A licencelt állapot kikapcsolja a próba vízjelet és feloldja a teljes helyesírás‑javító szótárat. Ennek a lépésnek a kihagyása működik, de a kimeneted „Aspose OCR Demo” szöveggel lesz szennyezve.

## 2. lépés: OCR motor létrehozása és konfigurálása

Most elindítjuk a motort és megadjuk, melyik nyelvet használja. Az angol a leggyakoribb, de az Aspose tucatokat támogat.

```java
        // Step 2: Instantiate the OCR engine
        OcrEngine engine = new OcrEngine();

        // Choose English for recognition – you could pick French, German, etc.
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);
```

*Miért állítjuk be a nyelvet:* A nyelvi modell meghatározza a karakterkészletet és befolyásolja a helyesírás‑javító javaslatait. Rossz nyelv használata drámaian csökkentheti a pontosságot.

## 3. lépés: Helyesírás‑javítás engedélyezése és (opcionálisan) egy egyéni szótár megadása

Az Aspose OCR egy beépített angol szótárral érkezik, de megadhatsz sajátot, ha speciális szakterületi kifejezéseid vannak (gondolj orvosi zsargonnal vagy termékkódokra).

```java
        // Step 3: Turn on the spell corrector
        engine.getSpellCorrector().setEnable(true); // activate spell‑checking

        // Optional: use a custom dictionary folder
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english");
```

*Mit csinál a javító:* Amikor az OCR motor olyan szót talál, ami nincs a szótárban, megpróbálja a legközelebbi egyezésre cserélni. Ezért tudja a demó a „recieve” szót automatikusan „receive”‑re változtatni.

## 4. lépés: Kép betöltése OCR‑hez

Itt van a rész, amely közvetlenül a **kép betöltése OCR‑hez** kérdésre válaszol. Létrehozunk egy `OcrInput` objektumot és hozzáadjuk a PNG fájlt.

```java
        // Step 4: Prepare the image input
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // path to the image you want to process
```

*Miért használjuk a `OcrInput`‑t:* Elrejti a fájl‑olvasási logikát, és lehetővé teszi, hogy később több oldalt adj hozzá, ha többoldalas PDF‑et vagy képek sorozatát kell feldolgozni.

## 5. lépés: Felismerés futtatása és a javított szöveg lekérése

A motor most elvégzi a nehéz munkát—karakterek felismerése, a nyelvi modell alkalmazása, és végül a helyesírás javítása.

```java
        // Step 5: Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Step 6: Output the corrected text to the console
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

*Várt kimenet:* Feltételezve, hogy a `misspelled.png` a „Ths is a smple test” kifejezést tartalmazza, a konzol a következőt írja ki:

```
Corrected text:
This is a simple test
```

Vedd észre, hogy a helytelen szavak (`Ths`, `smple`) automatikusan javítva lettek.

## Teljes, azonnal futtatható példa

Az alábbiakban a teljes program egy blokkban látható. Másold be, állítsd be az elérési útvonalakat, és nyomd meg a **Run** gombot.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose.OCR license (replace with your license file)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Select the language for recognition (e.g., English)
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);

        // Enable the built‑in spell corrector and optionally set a custom dictionary
        engine.getSpellCorrector().setEnable(true);                     // activate spell‑checking
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english"); // optional

        // Prepare the input image containing the text to be recognized
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // load image for OCR

        // Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Output the corrected text
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

**Tipp:** Ha JPEG‑et vagy BMP‑t szeretnél feldolgozni PNG helyett, csak cseréld a fájlkiterjesztést—az Aspose OCR támogatja az összes gyakori raszter formátumot.

## Gyakori kérdések és speciális esetek

- **Mi van, ha a kép alacsony felbontású?**  
  Növeld a DPI‑t, mielőtt az Aspose‑nek átadod, például a `java.awt.Image` könyvtárral átméretezve. A magasabb DPI több pixelt biztosít a motor számára, ami általában javítja a pontosságot.

- **Felismerhetek több nyelvet ugyanabban a képen?**  
  Igen. Hívd a `engine.getLanguage().setLanguage(OcrLanguage.MULTI_LANGUAGE);` metódust, és opcionálisan adj meg egy nyelvlistát a `engine.getLanguage().addLanguage(OcrLanguage.SPANISH);` segítségével.

- **Az egyéni szótáram nem kerül felhasználásra—miért?**  
  Győződj meg róla, hogy a mappa egyszerű szövegfájlokat tartalmaz, soronként egy szóval, és hogy az útvonal abszolút vagy helyesen relatív a munkakönyvtáradhoz.

- **Hogyan nyerhetem ki a megbízhatósági pontszámokat?**  
  A `result.getConfidence()` egy 0 és 1 közötti float értéket ad vissza az egész oldalra. Karakterenkénti megbízhatóságért vizsgáld meg a `result.getWordList()`-et.

## Következtetés

Most már tudod, hogyan **szöveget felismerj képről** az Aspose OCR for Java segítségével, hogyan **képet tölts be OCR‑hez**, és hogyan engedélyezd a helyesírás‑javítót a gyakori elírások tisztításához. A fenti teljes példa készen áll, hogy bármely Maven vagy Gradle projektbe beilleszd, és néhány módosítással kötegelt mappafeldolgozásra, webszolgáltatásba való integrálásra vagy dokumentumkezelő rendszerbe való beágyazásra skálázható.

Készen állsz a következő lépésre? Próbálj meg egy többoldalas PDF‑et betáplálni, kísérletezz egy egyéni szótárral az iparágspecifikus terminológiához, vagy láncold a kimenetet egy fordítási API‑hoz. A lehetőségek végtelenek, és az alapminta—licenc → motor → nyelv → helyesírás‑javító → bemenet → felismerés → kimenet—változatlan marad.

Boldog kódolást, és legyenek az OCR eredményeid mindig pontosak!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}