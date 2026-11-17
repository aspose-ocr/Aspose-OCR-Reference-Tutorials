---
category: general
date: 2026-03-28
description: Naučte se rozpoznávat text na obrázcích v Javě pomocí Aspose OCR, extrahovat
  textové soubory PNG a využívat akceleraci GPU pro rychlé OCR velkých obrázků.
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: cs
og_description: Objevte, jak rozpoznávat text na obrázcích v Javě, extrahovat text
  z PNG souborů a využívat akceleraci GPU pro OCR velkých obrázků.
og_title: Rozpoznání textu na obrázku pomocí Java OCR – příklad s GPU akcelerací
tags:
- OCR
- Java
- GPU
title: Rozpoznání textu na obrázku pomocí Java OCR – Příklad s GPU akcelerací
url: /cs/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznat text na obrázku pomocí Java OCR – příklad s akcelerací GPU

Už jste někdy potřebovali **rozpoznat text na obrázku** z obrovského PNG, ale CPU verze byla příliš pomalá? Nejste v tom sami. V mnoha reálných pipelinech — například při skenování faktur nebo archivaci historických dokumentů — může velikost obrázku narůst a výchozí OCR engine jednoduše nestačí.

Dobrá zpráva: Aspose OCR pro Java vám umožní **použít akceleraci GPU** a výrazně tak zrychlit proces, přičemž kód je překvapivě stručný. V tomto tutoriálu uvidíte kompletní, spustitelný Java OCR příklad, který **extrahuje text z PNG** souborů, využívá CUDA‑povolené GPU a zvládá **OCR velký obrázek** pomocí několika řádků kódu. Na konci budete přesně vědět, jak to zapojit do vlastního Java projektu a proč každé nastavení má význam.

## Co se naučíte

- Jak nastavit Aspose OCR v Maven nebo Gradle projektu.  
- Krok za krokem proces **rozpoznání textu na obrázku** na GPU.  
- Proč nastavení počtu GPU streamů může zvýšit propustnost.  
- Jak ověřit výstup a řešit běžné problémy.  

> **Předpoklady** – Java 17 (nebo novější), CUDA‑kompatibilní GPU s nejnovějším driverem a platná licence Aspose OCR pro Java (zdarma zkušební verze stačí pro hodnocení). Žádné další externí knihovny nejsou vyžadovány.

---

## Krok 1: Přidejte závislost Aspose OCR

Nejprve přidejte knihovnu Aspose OCR do svého buildu. Pokud používáte **Maven**, vložte následující úryvek do souboru `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

Pro **Gradle** umístěte tento kód do `build.gradle`:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Tip:** Nejnovější verze (k březnu 2026) obsahuje vylepšení výkonu pro GPU úlohy, takže vždy používejte nejčerstvější release.

---

## Krok 2: Inicializujte OCR engine a povolte GPU

Vytvoření OCR engine je jednoduché. Klíčová část je zapnutí GPU flagu — jinak se engine vrátí do CPU režimu.

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

### Proč povolit GPU?

Když zapnete `setUseGpu(true)`, Aspose přesune těžké výpočty konvolučních neuronových sítí na grafickou kartu. To může u **ocr velkého obrázku** ušetřit několik sekund, zejména když obrázek přesáhne 4000 × 4000 px. Pokud vaše prostředí nemá kompatibilní GPU, volání se jednoduše ignoruje a engine pokračuje na CPU — žádná havárie, jen pomalejší výkon.

---

## Krok 3: Rozpoznání PNG obrázku a extrakce textu

Nyní nasměrujte engine na soubor, který chcete zpracovat. Příklad používá `sample-large.png`, ale můžete ho nahradit libovolným PNG nebo JPEG.

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Po spuštění programu byste měli vidět něco jako:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

Tento výstup potvrzuje, že operace **rozpoznání textu na obrázku** proběhla úspěšně a že jste úspěšně **extrahovali text z png**.

---

## Krok 4: Ověření využití GPU (volitelné, ale užitečné)

Pokud vás zajímá, zda je GPU opravdu používáno, otevřete monitorovací nástroj GPU (např. `nvidia-smi` na Linuxu). Během běhu Java procesu byste měli zaznamenat mírný nárůst využití paměti a výpočetního výkonu.

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

Pokud žádná aktivita nevidíte, zkontrolujte:

1. Odpovídá CUDA driver modelu GPU.  
2. Volání `setUseGpu(true)` není později v kódu přepsáno.  
3. Váš licenční soubor (pokud jej máte) neomezuje použití GPU.

---

## Krok 5: Řešení běžných okrajových případů

### Velké obrázky přesahující paměť GPU

Když je obrázek obrovský (např. 8000 × 8000 px), GPU může dojít paměti. Rychlým řešením je před zpracováním obrázek zmenšit:

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

Pak předáte `"sample-resized.png"` metodě `recognizeImage`. OCR zůstane přesné a zároveň se vejde do limitů GPU.

### Více‑stránkové PDF

Aspose OCR dokáže také zpracovávat PDF stránku po stránce. Projděte každou stránku, převedete ji na obrázek a předáte engine. Stejný flag **use gpu acceleration** platí i zde, což vám poskytne rychlý PDF‑na‑text pipeline.

---

## Kompletní funkční příklad (připravený ke zkopírování)

Níže je kompletní Java třída, připravená ke kompilaci a spuštění. Nahraďte `YOUR_DIRECTORY` cestou k vašemu PNG souboru.

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

**Očekávaný výstup** — čistý textový řetězec se vším, co engine z obrázku přečetl. Pokud obrázek obsahuje tabulku, získáte obsah buněk spojený zalomeními řádků; Aspose nezachovává rozložení, ale řetězec můžete po‑zpracovat podle potřeby.

---

## Často kladené otázky

| Otázka | Odpověď |
|----------|--------|
| **Potřebuji placenou licenci?** | Zkušební verze funguje až pro 200 stran a odstraňuje vodoznak pro OCR. Pro produkci licence odstraňuje limity a odemyká plný GPU stack. |
| **Co když mám starší GPU (např. GTX 750)?** | Starší GPU mohou fungovat, ale s nižší rychlostí; ujistěte se, že máte alespoň Compute Capability 3.0. |
| **Mohu zpracovávat JPG nebo BMP soubory?** | Ano — `recognizeImage` přijímá jakýkoli formát podporovaný Java ImageIO. |
| **Existuje způsob, jak hromadně zpracovat mnoho obrázků?** | Zabalte volání OCR do smyčky a zvažte zvýšení `setGpuStreams` tak, aby odpovídalo počtu souběžných streamů, které chcete použít. |
| **Jak zachovat rozložení dokumentu?** | Použijte `LayoutOptions` v Aspose OCR pro získání ohraničujících boxů; to přesahuje rámec tohoto rychlého návodu, ale je zdokumentováno v API. |

---

## Závěr

Máte nyní stručný, end‑to‑end **java ocr příklad**, který **rozpozná text na obrázku**, **extrahuje text z png** a **využívá akceleraci GPU** pro zrychlení zpracování **ocr velkého obrázku**. Úpravou počtu GPU streamů a případným zmenšením příliš velkých obrázků můžete řešení přizpůsobit prakticky jakékoli hardwarové konfiguraci.

Jste připraveni na další krok? Zkuste nasměrovat složku naskenovaných účtenek do stejného pipeline, nebo experimentujte s Aspose `TextRegion` API, abyste zachovali původní rozložení. A pokud narazíte na problémy, fóra Aspose a Javadoc jsou skvělé zdroje — jen si pamatujte základy, které jsme zde probírali.

Šťastné kódování a ať je vaše OCR bleskově rychlé!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}