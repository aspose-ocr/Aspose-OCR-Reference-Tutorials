---
description: Tanulja meg, hogyan mentheti el az OCR eredményeket az Aspose.OCR for
  .NET segítségével – konvertálja a képet PDF-be, nyerjen ki szöveget PNG-ből, és
  mentse a felismert szöveget DOCX, TXT, PDF vagy XLSX formátumba.
linktitle: How to Save OCR Result as Document
second_title: Aspose.OCR .NET API
title: Hogyan menthetjük el az OCR eredményt dokumentumként
url: /hu/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan mentse el az OCR eredményt dokumentumként

## Bevezetés

Ebben az útmutatóban megtudja, **hogyan mentse el az OCR** kimenetet az Aspose.OCR for .NET segítségével. Lépésről‑lépésre végigvezetjük a szöveg felismerésén egy képen, majd a szöveg átalakításán népszerű dokumentumformátumokba, mint a DOCX, TXT, PDF és XLSX. A végére képes lesz automatizálni az adatok képekből történő kinyerését, és kereshető, szerkeszthető fájlokként tárolni őket – tökéletes archiváláshoz, jelentéskészítéshez vagy további feldolgozáshoz.

## Gyors válaszok
- **Mit jelent a „hogyan mentse el az ocr”?** Ez arra vonatkozik, hogy a képről felismert szöveget egy olyan fájlformátumba, mint a DOCX, PDF stb. mentjük.  
- **Milyen formátumokba exportálhatok?** A DOCX, TXT, PDF és XLSX alapból támogatott.  
- **Szükség van licencre?** Az ingyenes próba a kiértékeléshez elegendő; a kereskedelmi licenc a termeléshez kötelező.  
- **Közvetlenül PDF‑be konvertálhatom a képet?** Igen — mentse el az OCR eredményt PDF‑ként, hogy kereshető PDF dokumentumot kapjon.  
- **Támogatott a PNG?** Természetesen; **kivonhat szöveget PNG** képekből ugyanazzal az API‑val.

## Mi az OCR és miért érdemes a eredményeket dokumentumokba menteni?

Az Optikai Karakterfelismerés (OCR) a nyomtatott vagy kézzel írott szöveget képekben gép‑olvasható karakterláncokká alakítja. Ezeket a karakterláncokat dokumentumokba mentve:

* Készíthet kereshető PDF‑eket megfelelőség céljából.  
* Kitölthet táblázatokat (XLSX) adat‑elemzéshez.  
* Létrehozhat szerkeszthető jelentéseket (DOCX).  
* Archiválhat egyszerű szöveges naplókat (TXT) gyors kereséshez.

## Előfeltételek

Mielőtt elkezdenénk, győződjön meg róla, hogy:

- Telepítve van az Aspose.OCR for .NET. Letöltheti **[itt](https://releases.aspose.com/ocr/net/)**.  
- Van egy mappa a gépén, amely a forrásképeket és a kimeneti dokumentumokat tartalmazza. A kódban frissítse a `dataDir` változót, hogy erre a mappára mutasson.

## Névterek importálása

Néhány .NET névtérre szükségünk van a fájl‑I/O és az Aspose OCR osztályok eléréséhez.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### 1. lépés: Aspose.OCR inicializálása

Állítsa be a munkakönyvtár útvonalát, és hozza létre az OCR motor egy példányát.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### 2. lépés: Kép felismerése

Adja át a képfájlt (például egy PNG‑t) a felismerőnek. Itt **felismerjük a szöveges képeket**, és `RecognitionResult`‑á alakítjuk őket.

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### 3. lépés: Eredmény mentése különböző formátumokba

Most exportáljuk a felismert szöveget. Válassza ki a munkafolyamatához leginkább illő formátumot — legyen szó **kép PDF‑be konvertálásáról**, **szöveg PNG‑ből kinyeréséről**, vagy táblázat generálásáról.

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### 4. lépés: Sikerüzenet megjelenítése

Egy egyszerű konzolos üzenet jelzi, hogy a folyamat hibamentesen befejeződött.

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## Gyakori hibák és tippek

- **Fájlútvonalak:** Mindig használjon abszolút útvonalakat, vagy győződjön meg róla, hogy a `dataDir` végén van útvonal‑elválasztó (`\` vagy `/`).  
- **Képminőség:** A nagy felbontású képek javítják a pontosságot; fontolja meg az előfeldolgozást (kiegyenesítés, zajszűrés) a jobb eredmény érdekében.  
- **Licenc mód:** Kiértékelő módban a kimenet vízjelet tartalmazhat; egy érvényes licenc eltávolítja azt.

## Gyakran feltett kérdések

**Q1. Az Aspose.OCR kompatibilis különböző képformátumokkal?**  
A1: Igen, az Aspose.OCR széles körű képformátumot támogat, így rugalmasan használható az OCR feladatokhoz.

**Q2: Testreszabhatom a felismerési beállításokat a pontosság növelése érdekében?**  
A2: Teljesen! Az Aspose.OCR biztosítja a `RecognitionSettings`‑et, amellyel finomhangolhatja a folyamatot saját igényei szerint.

**Q3: Van ingyenes próba?**  
A3: Igen, ingyenes próba verziót indíthat **[itt](https://releases.aspose.com/)**.

**Q4: Hogyan szerezhetek ideiglenes licencet az Aspose.OCR‑hez?**  
A4: Ideiglenes licenceket **[itt](https://purchase.aspose.com/temporary-license/)** kaphat.

**Q5: Hol kérhetek segítséget vagy csatlakozhatok a közösséghez?**  
A5: Csatlakozzon az Aspose.OCR közösséghez a **[Aspose Fórumon](https://forum.aspose.com/c/ocr/16)** támogatás és beszélgetés céljából.

---

**Utolsó frissítés:** 2026-02-12  
**Tesztelt verzió:** Aspose.OCR 24.11 for .NET  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}