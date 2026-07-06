---
category: general
date: 2026-03-18
description: Jak rychle narovnat obrázek pomocí Aspose OCR Java. Naučte se předzpracovat
  obrázek pro OCR, vyčistit naskenovaný obrázek a zlepšit přesnost OCR během několika
  kroků.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- clean scanned image
- improve ocr accuracy
language: cs
og_description: Jak vyrovnat šikmost obrázku pomocí Aspose OCR Java, předzpracovat
  obrázek pro OCR, vyčistit naskenovaný obrázek a zlepšit přesnost OCR.
og_title: Jak narovnat obrázek pro OCR – Java průvodce
tags:
- OCR
- Java
- Image Processing
title: Jak vyrovnat sklon obrázku pro OCR – Průvodce předzpracováním v Javě
url: /cs/java/advanced-ocr-techniques/how-to-deskew-image-for-ocr-java-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vyrovnat obrázek pro OCR – Průvodce předzpracováním v Javě

Už jste se někdy ptali, **jak vyrovnat obrázek** soubory, které vyjdou ze skeneru pod divným úhlem? Nejste jediní – mnoho vývojářů narazí na tento problém, když se snaží extrahovat text z dokumentů plných obrázků. Dobrá zpráva? S několika řádky Javy a Aspose OCR můžete obrázek narovnat, odšumět a získat čistý text bez námahy.

V tomto tutoriálu projdeme celý pracovní postup: načtení špinavého, otočeného skenu, aplikaci filtru pro vyrovnání, odstranění vizuálního nepořádku a nakonec **extrahování textu z obrázku**. Na konci budete vědět, jak **předzpracovat obrázek pro OCR**, **vyčistit naskenovaný obrázek** a **zlepšit přesnost OCR** pro jakýkoli projekt, který potřebuje spolehlivé získávání textu.

## Co budete potřebovat

- Java 17 (nebo jakýkoli aktuální JDK) – kód používá standardní jazykové funkce.
- Knihovna Aspose OCR pro Java (bezplatná zkušební verze je vhodná pro experimenty).
- Vzorek obrázku, který je jak špinavý, tak otočený (např. `noisy-rotated.png`).
- Vaše oblíbené IDE (IntelliJ IDEA, Eclipse, VS Code…) – cokoliv, co umí kompilovat Javu.

Žádné další frameworky, žádné kouzla s Maven/Gradle; jediné importy jsou ty, které jsou zobrazeny níže.

---

## Jak vyrovnat obrázek pomocí Aspose OCR

První věc, kterou je třeba řešit, je náklon obrázku. Pokud řádky textu nejsou vodorovné, OCR engine bude špatně číst znaky. `DeskewFilter` odvede těžkou práci.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
import com.aspose.ocr.preprocess.DeskewFilter;
import com.aspose.ocr.preprocess.DenoiseFilter;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the raw scanned image
        Image scannedImage = Image.load("YOUR_DIRECTORY/noisy-rotated.png");

        // Step 3: Correct the image orientation (deskew)
        DeskewFilter deskewFilter = new DeskewFilter();
        scannedImage = deskewFilter.apply(scannedImage);

        // Step 4: Reduce visual noise (denoise)
        DenoiseFilter denoiseFilter = new DenoiseFilter();
        scannedImage = denoiseFilter.apply(scannedImage);

        // Step 5: Perform OCR on the cleaned image
        String recognizedText = ocrEngine.recognize(scannedImage);

        // Step 6: Output the extracted text
        System.out.println(recognizedText);
    }
}
```

> **Proč je to důležité:** `DeskewFilter` analyzuje geometrii obrázku, odhaduje úhel rotace a otočí bitmapu zpět na úroveň horizontu. Bez tohoto kroku většina OCR engine‑ů považuje šikmé písmena za zcela odlišné glyfy, což snižuje vaše úsilí o **zlepšení přesnosti OCR**.

> **Tip:** Pokud pracujete s dokumenty, které mohou být vzhůru nohama, povolte příznak `setAutoRotate` na `DeskewFilter` (k dispozici v novějších verzích Aspose). Automaticky otočí o 180° podle potřeby.

![Diagram ukazující před a po rotaci – jak vyrovnat obrázek](https://example.com/deskew-diagram.png "příklad, jak vyrovnat obrázek")

*Text alternativy obrázku: příklad, jak vyrovnat obrázek*

---

## Předzpracování obrázku pro OCR – Odšumování a čištění

Jakmile je obrázek narovnaný, dalším překážkou je vizuální šum – ty skvrny, artefakty komprese nebo slabé pozadí, které zmatení OCR engine. `DenoiseFilter` použije jemný vyhlazovací algoritmus, který zachová hrany (písmena) a zároveň odstraní zrnitost.

```java
// Step 4 (continued): Reduce visual noise (denoise)
DenoiseFilter denoiseFilter = new DenoiseFilter();
scannedImage = denoiseFilter.apply(scannedImage);
```

### Kdy upravit nastavení odšumování

- **Velmi tmavé skeny:** Zvyšte sílu filtru (`denoiseFilter.setStrength(2)`) pro odstranění stínů na pozadí.
- **Jemné písmo:** Snižte sílu, aby nedošlo k rozmazání drobných serif.
- **Barevné dokumenty:** Nejprve převeďte na odstíny šedi (`scannedImage = scannedImage.toGrayscale();`) – OCR engine funguje nejlépe na jednokanálových obrázcích.

Tyto úpravy jsou součástí osvědčených postupů **čistého naskenovaného obrázku**; čistší bitmapa přímo vede k vyššímu skóre důvěry od OCR engine.

---

## Extrahování textu z obrázku – Spuštění OCR engine

Nyní, když je obrázek narovnaný a čistý, je čas **extrahovat text z obrázku**. Třída `OcrEngine` řeší vše v pozadí: segmentaci, klasifikaci znaků a modelování jazyka.

```java
// Step 5: Perform OCR on the cleaned image
String recognizedText = ocrEngine.recognize(scannedImage);
System.out.println(recognizedText);
```

#### Očekávaný výstup

Pokud váš zdrojový soubor obsahuje řádek “**Invoice # 12345**”, konzole by měla vypsat něco jako:

```
Invoice # 12345
Date: 2026-03-18
Total: $1,250.00
```

Pokud výstup vypadá poškozeně, zkontrolujte předchozí kroky – zejména vyrovnání. I náklon o 1 stupeň může poškodit čísla a symboly.

---

## Časté úskalí a tipy pro **zlepšení přesnosti OCR**

| Problém | Proč snižuje přesnost | Rychlé řešení |
|-------|----------------------|-----------|
| **Zbytková rotace** | OCR očekává vodorovné základní linie. | Ověřte pomocí `deskewFilter.getAngle()` a zaznamenejte hodnotu. |
| **Přehnané odšumování** | Rozmazává tenké tahy, mění “i” na “l”. | Použijte `setStrength(0.5)` pro jemné písmo. |
| **Špatný formát obrázku** | JPEG komprese přidává artefakty. | Upřednostněte PNG nebo TIFF pro bezztrátové uložení. |
| **Nesprávný jazyk** | Engine výchozí na angličtinu; jiné abecedy vyžadují explicitní nastavení. | `ocrEngine.setLanguage(OcrEngine.Language.Spanish);` |
| **Nízké DPI (≤150)** | Nedostatek pixelových dat pro spolehlivou segmentaci. | Převzorkujte na 300 DPI před zpracováním (`scannedImage = scannedImage.resample(300);`). |

### Bonus: Hromadné zpracování

Pokud máte složku se skeny, zabalte ukázku do smyčky:

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.endsWith(".png"))) {
    Image img = Image.load(file.getAbsolutePath());
    img = new DeskewFilter().apply(img);
    img = new DenoiseFilter().apply(img);
    String text = ocrEngine.recognize(img);
    System.out.println("=== " + file.getName() + " ===");
    System.out.println(text);
}
```

Tento vzor vám umožní **předzpracovat obrázek pro OCR** ve velkém měřítku, udržet kódovou základnu přehlednou a výkon předvídatelný.

---

## Shrnutí a další kroky

Probrali jsme **jak vyrovnat obrázek** soubory, **předzpracovat obrázek pro OCR** a nakonec **extrahovat text z obrázku** pomocí Aspose OCR Java. Narovnáním skenu, odstraněním šumu a předáním čisté bitmapy do engine‑u výrazně **zlepšíte přesnost OCR** napříč všemi projekty.

Co dál? Zvažte tyto rozšíření:

- **Detekce jazyka** – přepněte `ocrEngine.setLanguage` podle detekovaného skriptu.
- **PDF výstup** – předávejte rozpoznaný text do generátoru PDF pro prohledávatelné dokumenty.
- **Post‑processing strojového učení** – spusťte kontrolu pravopisu nebo vlastní slovníky na výsledek OCR.

Vyzkoušejte tyto nápady, experimentujte s různými silami filtrů a brzy budete mít pevný pipeline pro jakýkoli projekt digitalizace dokumentů.

*Šťastné kódování! Pokud narazíte na problém, zanechte komentář níže – pomohu vám doladit parametry vyrovnání a odšumění.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}