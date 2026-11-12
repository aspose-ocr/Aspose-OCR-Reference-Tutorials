---
category: general
date: 2026-04-11
description: Tanulja meg, hogyan tilthatja le az OCR-t az Aspose OCR for C#-ban, hogy
  offline működjön, internetkapcsolat nélkül szöveget nyerjen ki a képből, és helyesen
  töltse be a képet az OCR-hez.
draft: false
keywords:
- how to disable OCR
- extract text from image
- load image for OCR
- offline OCR C#
- Aspose OCR resources
language: hu
og_description: Hogyan tiltsuk le az OCR-t az Aspose OCR C#-ban, és futtassuk offline
  módon, internetkapcsolat nélkül nyerjünk ki szöveget a képből, valamint könnyen
  töltsünk be képet az OCR-hez.
og_title: Hogyan tiltsuk le az OCR-t C#-ban – Offline Aspose OCR útmutató
tags:
- C#
- OCR
- Aspose
- Offline Processing
title: Hogyan tiltsuk le az OCR-t C#-ban – Offline Aspose OCR útmutató
url: /hu/net/ocr-configuration/how-to-disable-ocr-in-c-offline-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan tiltsuk le az OCR-t C#‑ban – Offline Aspose OCR útmutató

Gondolkodtál már azon, **hogyan lehet letiltani az OCR‑t**, amikor valóban offline megoldásra van szükséged? Lehet, hogy egy biztonságos asztali alkalmazást építesz, amely nem támaszkodhat hálózati kapcsolatra, vagy egyszerűen csak el akarod kerülni a váratlan letöltéseket. Akármi is legyen az ok, a jó hír, hogy az Aspose OCR lehetővé teszi az automatikus erőforrás‑letöltés kikapcsolását, egy helyi mappára mutatást, és minden adatot a helyszínen tart. Ebben az útmutatóban azt is megmutatjuk, hogyan **vonj ki szöveget képfájlokból** és hogyan **tölts be képet OCR‑hez** problémamentesen.

Végigvezetünk egy teljes, azonnal futtatható példán, amely minden lépést bemutat – az motor inicializálásától a felismert japán szöveg kiírásáig. Nincs külső dokumentáció, nincs rejtett varázslat; csak tiszta C# kód, amelyet ma beilleszthetsz a projektedbe. A végére megérted, miért fontos az automatikus letöltés letiltása, hogyan állítsd be az erőforrás‑útvonalat, és milyen csapdákat kerülj el.

## Előfeltételek

- .NET 6.0 (vagy bármely friss .NET verzió) telepítve a gépeden.  
- Aspose.OCR for .NET NuGet csomag (`Install-Package Aspose.OCR`).  
- Egy mappa, amely már tartalmazza a szükséges nyelvi erőforrásokat (pl. a japán modellt).  
- Egy képfájl (`japan_doc.png`), amelyen OCR‑t szeretnél futtatni.  

Ha hiányoznak a nyelvi csomagok, szerezd be őket egyszer az Aspose portálról, csomagold ki egy `AsposeOCRResources` nevű mappába, és már készen is vagy. Az automatikus letöltés letiltása után további letöltések nem fognak megtörténni.

![Hogyan tiltsuk le az OCR-t offline](/images/how-to-disable-ocr.png "hogyan tiltsuk le az OCR illusztrációja")

## 1. lépés – Az OCR motor példányosítása  

Az első dolog, amit megteszel, hogy példányosítod az `OcrEngine`‑t. Gondolj erre az objektumra úgy, mint a „agyra”, amely elolvassa a képedet.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Miért fontos:** Motor nélkül nem tudsz semmit konfigurálni. Az objektum tartalmazza az összes beállítást, köztük azt a kulcsfontosságú jelzőt, amely megmondja a könyvtárnak, hogy szabad‑e internethez fordulnia.

## 2. lépés – Az automatikus erőforrás‑letöltés letiltása  

Alapértelmezés szerint az Aspose OCR megpróbálja letölteni a hiányzó nyelvi fájlokat „repülő” módban. Az offline működéshez állítsd a `AutoDownloadResources` kapcsolót `false`‑ra.

```csharp
        // Step 2: Disable automatic resource download to work offline
        ocrEngine.Settings.AutoDownloadResources = false;
```

> **Pro tipp:** Ennek kikapcsolása nem csak a magánszférát garantálja, hanem felgyorsítja az első felismerést is, mivel a motor nem vesztegeti az időt a frissítések ellenőrzésére.

## 3. lépés – A helyi erőforrás‑mappa megadása  

Most mondd meg a motornak, hol találhatók a előre letöltött nyelvi csomagok. Ez az útvonal, amelyet az előfeltételekben állítottál be.

```csharp
        // Step 3: Point the engine to the folder containing pre‑downloaded resources
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";
```

> **Mi mehet félre?** Ha az útvonal hibás vagy a szükséges nyelvi fájl hiányzik, a motor `ResourceNotFoundException`‑t dob. Ellenőrizd a mappa nevét és azt, hogy a japán modell (`jpn.traineddata`) jelen van‑e.

## 4. lépés – A helyi nyelvi modell kiválasztása  

Válaszd ki a lemezen ténylegesen elérhető nyelvet. A példánkban japánt használunk, de a `Language.Japanese`‑t kicserélheted bármely letöltött nyelvre.

```csharp
        // Step 4: Select the language model that is available locally
        ocrEngine.Settings.Language = Language.Japanese;
```

> **Szélsőséges eset:** Egyes nyelvek további szótárakat igényelnek (pl. kínai). Győződj meg róla, hogy ezek a kiegészítő fájlok is ugyanabban a resources mappában vannak.

## 5. lépés – Kép betöltése OCR‑hez  

Itt **betöltjük a képet OCR‑hez**. Az `ImageStream.FromFile` metódus beolvassa a fájlt egy stream‑be, amelyet az Aspose feldolgozhat.

```csharp
        // Step 5: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/japan_doc.png");
```

> **Tipp:** Támogatott formátumok a PNG, JPEG, BMP és TIFF. Ha PDF‑eket kell kezelned, előbb konvertáld minden oldalt képpé.

## 6. lépés – A felismerési folyamat indítása  

Most a motor ténylegesen elolvassa a pixeleket, és megpróbálja szöveggé alakítani őket.

```csharp
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Miért lehet lassú:** Az OCR CPU‑igényes, különösen nagy felbontású képeknél. Ha a teljesítmény kritikus, fontold meg a kép lecsökkentését a felismerés előtt.

## 7. lépés – A kinyert szöveg kiírása  

Végül **kivonjuk a szöveget a képből** és kiírjuk a konzolra.

```csharp
        // Step 7: Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

A program futtatása után a `japan_doc.png`‑ben lévő japán karakterek jelennek meg. Ha minden helyesen van beállítva, egy tiszta Unicode szövegrészletet látsz a konzolon.

### Várható kimenet

```
これはサンプルの日本語テキストです。
```

(A tényleges kimenet a kép tartalmától függ.)

## Gyakori hibák és elkerülésük módja  

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| **Hiányzó nyelvi fájl** | `AutoDownloadResources` hamis, így a motor nem tudja letölteni. | Ellenőrizd, hogy a `ResourcesPath` a `jpn.traineddata`‑t tartalmazó mappára mutat. |
| **Helytelen képútvonal** | `ImageStream.FromFile` `FileNotFoundException`‑t dob. | Használj abszolút útvonalakat, vagy győződj meg róla, hogy a munkakönyvtár helyesen van beállítva. |
| **Nem támogatott képformátum** | Az Aspose csak bizonyos formátumokat olvas. | Konvertáld a képet PNG‑re vagy JPEG‑re, mielőtt a `FromFile`‑t hívod. |
| **Memóriahiány nagy képeknél** | Az OCR a teljes képet memóriába tölti. | Méretezd át vagy darabold fel a képet, vagy növeld a folyamat memóriahatárát. |

## A példa bővítése  

- **Kötegelt feldolgozás:** Egy könyvtár képeinek ciklusban történő beolvasása, ugyanazon felismerési kód meghívása, és minden eredmény külön `.txt` fájlba írása.  
- **Különböző nyelvek:** A `Language.Japanese` helyett használj `Language.English`‑t (vagy bármely másik nyelvet) a megfelelő erőforrás‑fájlok elhelyezése után.  
- **Egyedi előfeldolgozás:** Használd az Aspose.Imaging‑et a kép kiegyenesítésére vagy kontrasztjavításra OCR előtt a pontosság növelése érdekében.

## Összegzés  

Most már tudod, **hogyan tiltsuk le az OCR-t** az Aspose OCR‑ben C#‑ban, és hogyan futtassuk teljesen offline módon. A `AutoDownloadResources` `false`‑ra állításával, a motor helyi erőforrás‑mappára mutatásával, és a **kép betöltésével OCR‑hez**, megbízhatóan **kivonhatod a szöveget a képből** anélkül, hogy valaha is az internethez nyúlnál. Ez a megközelítés ideális biztonságos környezetekben, CI pipeline‑okban vagy bármilyen szituációban, ahol a hálózati hozzáférés korlátozott.

Készen állsz a következő lépésre? Próbáld ki egy egész mappa beolvasását beolvasott PDF‑ekből, kísérletezz különböző nyelvi csomagokkal, vagy integráld az OCR‑eredményt egy kereshető adatbázisba. Az ma felépített offline beállítás szilárd alapot nyújt bármely helyi dokumentum‑feldolgozó munkafolyamathoz.

Boldog kódolást, és nyugodtan hagyj kommentet, ha elakadsz!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}