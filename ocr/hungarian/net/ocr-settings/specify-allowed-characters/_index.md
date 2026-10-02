---
description: Tudja meg, hogyan adhatja meg az engedélyezett karaktereket az Aspose.OCR
  for .NET segítségével, és hatékonyan ismerje fel a számjegyeket tartalmazó képeket.
  Kövesse a lépésről‑lépésre útmutatót, hogy az OCR csak számjegyekre korlátozódjon.
linktitle: Specify Allowed Characters OCR – Using Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: Engedélyezett karakterek megadása OCR – Aspose.OCR használata .NET-hez
url: /hu/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Engedélyezett karakterek megadása OCR – Aspose.OCR használata .NET-hez

Ebben az oktatóanyagban megtanulja, hogyan **specify allowed characters ocr** használatával az Aspose.OCR for .NET segítségével korlátozhatja az OCR kimenetet csak a szükséges karakterekre. Ez különösen hasznos, ha **recognize digits image** fájlokat kell felismerni, például sorozatszámokat, számlaazonosítókat vagy vonalkód‑szerű karakterláncokat. Végigvezetjük a beállításon, a kódon és néhány gyakorlati példán, hogy azonnal alkalmazni tudja a technikát.

## Gyors válaszok
- **Mi a “specify allowed characters ocr” funkciója?** Az OCR-t egy előre meghatározott karakterkészletre korlátozza, ezáltal javítva a célzott adatok pontosságát.  
- **Milyen karaktereket engedélyezhetek?** Bármilyen kombináció, amire szüksége van – számjegyek, betűk vagy egyedi szimbólumok (pl. “0123456789”).  
- **Miért korlátozzuk a karaktereket?** Csökkenti a hibás felismeréseket és felgyorsítja a feldolgozást, ha a várt karakterkészlet ismert.  
- **Szükségem van licencre?** A fejlesztéshez egy ingyenes próba elegendő; a termeléshez kereskedelmi licenc szükséges.  
- **Mely .NET verziók támogatottak?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Mi az “specify allowed characters ocr”?
Amikor az OCR egy képet szkennel, megpróbálja minden vizuális mintát a lehetséges karakterek teljes ábécéjéhez illeszteni. A **specify allowed characters ocr** segítségével azt mondja a motornak, hogy hagyja figyelmen kívül mindazt, ami nincs a fehérlistán, ami drámaian javítja a felismerés pontosságát korlátozott adatkészletek esetén.

## Miért használja az Aspose.OCR-t a számjegyeket tartalmazó képek felismerésére?
Az Aspose.OCR tiszta, folyékony API-t biztosít .NET fejlesztőknek. A beépített `AllowedCharacters` opció lehetővé teszi, hogy csak számjegyekre fókuszáljon anélkül, hogy egyedi utófeldolgozási logikát kellene írnia. Ez tökéletes:
- Mérőállások, számlaszámok vagy termékkódok olvasásához.  
- A beolvasott űrlapokról származó felhasználó által megadott adatok ellenőrzéséhez.  
- A kötegelt feldolgozás felgyorsításához, amikor a karakterkészlet előre ismert.

## Előfeltételek

Mielőtt belemerülne a kódba, győződjön meg róla, hogy rendelkezik:

- A .NET fejlesztés alapvető ismerete.  
- **Aspose.OCR for .NET** könyvtár. Letöltheti [itt](https://releases.aspose.com/ocr/net/).  
- Visual Studio (vagy bármely kedvelt .NET IDE).  

## Névterek importálása

A .NET projektjében importálja a szükséges névtereket az Aspose.OCR funkcionalitás kihasználásához:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Most bontsuk le az oktatóanyagot egy sor átfogó lépésre:

## Hogyan adjon meg engedélyezett karaktereket OCR – Lépésről‑lépésre útmutató

### 1. lépés: Állítsa be a képmappa útvonalát

Először határozza meg, hol tárolja a mintaképeket.

```csharp
string dataDir = "Your Document Directory";
```

### 2. lépés: Inicializálja az Aspose.OCR-t csak számjegyeket tartalmazó fehérlistával

Hozzon létre egy `AsposeOcr` példányt, és adja meg a megengedett karaktereket – ebben az esetben az összes számjegyet.

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### 3. lépés: Számjegyeket tartalmazó egyetlen sor felismerése

Használja a `RecognizeLine` metódust a szöveg kinyeréséhez egy olyan képről, amely csak számokat tartalmaz.

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### 4. lépés: A felismert számjegyek kiírása

Írja ki az eredményt a konzolra, hogy ellenőrizhesse a kimenetet.

```csharp
Console.WriteLine(result);
```

### 5. lépés: RecognitionSettings használata a nagyobb irányításért

Ha finomabb irányításra van szüksége – például egyetlen soros felismerés kényszerítésére – használhatja azt a túlterhelést, amely elfogadja a `RecognitionSettings` paramétert.

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

### 6. lépés: A második eset eredményének megjelenítése

```csharp
Console.WriteLine(result2.RecognitionText);
```

### 7. lépés: A sikeres végrehajtás megerősítése

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Ezeknek a lépéseknek a követésével megtanulta, hogyan **specify allowed characters ocr**, és hatékonyan **recognize digits image** tartalmat használva az Aspose.OCR for .NET-et.

## Gyakori buktatók és hibaelhárítás

- **Üres eredmény:** Győződjön meg arról, hogy a képminőség megfelelő (tiszta kontraszt, minimális zaj).  
- **Helytelen karakterek visszaadva:** Ellenőrizze újra, hogy a fehérlista karakterlánc pontosan megegyezik-e a várt karakterekkel.  
- **Fájl nem található:** Ellenőrizze, hogy a `dataDir` a helyes mappára mutat-e, és a fájlnév kis‑/nagybetű érzékenyen egyezik-e.

## Gyakran Ismételt Kérdések

### Q1: Alkalmas-e az Aspose.OCR for .NET kezdők és tapasztalt fejlesztők számára?  
**A:** Teljesen! Az API úgy van tervezve, hogy intuitív legyen az újoncok számára, miközben fejlett lehetőségeket kínál a haladó felhasználóknak.

### Q2: Használhatom az Aspose.OCR for .NET-et több nyelv karaktereinek felismerésére?  
**A:** Igen, az Aspose.OCR széles nyelvi támogatással rendelkezik. A nyelvi csomagokat kombinálhatja az engedélyezett karakterek funkcióval többnyelvű forgatókönyvekhez.

### Q3: Milyen gyakran frissül az Aspose.OCR for .NET?  
**A:** A frissítéseket rendszeresen kiadják új funkciók hozzáadására, a pontosság javítására és a kompatibilitás biztosítására. Tekintse meg a [dokumentációt](https://reference.aspose.com/ocr/net/) a legújabb verzió részleteiért.

### Q4: Elérhető ingyenes próba az Aspose.OCR for .NET-hez?  
**A:** Igen, a [free trial](https://releases.aspose.com/) letöltésével felfedezheti a lehetőségeket.

### Q5: Hol kérhetek segítséget vagy csatlakozhatok a közösséghez támogatásért?  
**A:** Látogassa meg az [Aspose.OCR fórumot](https://forum.aspose.com/c/ocr/16), ahol kérdéseket tehet fel, tapasztalatokat oszthat meg, és segítséget kaphat az Aspose mérnökeitől és a többi fejlesztőtől.

---

**Utolsó frissítés:** 2026-02-15  
**Tesztelt verzió:** Aspose.OCR 24.11 for .NET  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}