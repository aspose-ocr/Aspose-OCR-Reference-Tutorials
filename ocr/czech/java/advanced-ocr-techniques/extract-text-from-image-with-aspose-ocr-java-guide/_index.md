---
category: general
date: 2026-02-14
description: Extrahujte text z obrázku pomocí Aspose OCR v Javě. Naučte se, jak extrahovat
  text z formulářových polí s oblastmi zájmu pro přesné výsledky.
draft: false
keywords:
- extract text from image
- extract text from form
language: cs
og_description: Extrahujte text z obrázku pomocí Aspose OCR v Javě. Tento tutoriál
  ukazuje, jak extrahovat text z formulářových polí pomocí oblastí zájmu.
og_title: Extrahujte text z obrázku pomocí Aspose OCR – Java průvodce
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Extrahujte text z obrázku pomocí Aspose OCR – Java průvodce
url: /cs/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z obrázku pomocí Aspose OCR – průvodce pro Java

Už jste někdy potřebovali **extrahovat text z obrázku**, ale skončili tím, že jste parsovali celý obrázek, plýtvali CPU cykly a získávali šumivé výsledky? Nejste v tom sami. V mnoha reálných aplikacích – například skenery faktur, čtečky pasů nebo formuláře pro zadávání dat – vás zajímá jen několik polí, ne celý plátno.

Dobrou zprávou je, že Aspose OCR vám umožňuje **extrahovat text z obrázku** *i* z konkrétních oblastí formuláře definováním polygonů. V tomto tutoriálu uvidíte přesně, jak **extrahovat text z polí formuláře** pomocí Javy, proč je tento přístup důležitý a co upravit, když něco nefunguje.

Níže pokryjeme vše od nastavení knihovny po řešení obtížných okrajových případů, takže na konci budete mít připravený úryvek kódu, který získá jen data, která potřebujete.

## Co budete potřebovat

- Java 17 (nebo jakýkoli novější JDK) – novější verze mají lepší podporu Unicode.  
- Aspose.OCR pro Java 23.10 (nebo nejnovější verzi v době čtení).  
- Ukázkový obrázek pojmenovaný `form.png` s jasně definovanými poli.  
- IDE nebo jednoduchý textový editor – IntelliJ IDEA, VS Code nebo i Poznámkový blok vám postačí.

Pro základní ukázku není potřeba žádná Maven/Gradle magie; stačí přidat JAR Aspose OCR do classpath.

---

## Krok 1 – Inicializace OCR enginu a načtení obrázku

Prvním, co engine potřebuje, je bitmapa, na které bude pracovat. Ukážeme mu soubor `form.png`, který leží ve stejné složce jako zdrojový soubor.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

*Proč je to důležité:*  
Vytvoření nového `OcrEngine` vám dává čistý start, takže žádná předchozí nastavení neovlivní běh. Načtení obrázku hned na začátku také ověří, že soubor existuje, a vyhodí užitečnou výjimku dříve, než ztratíte čas na dalších krocích.

> **Tip:** Pokud je váš obrázek velký (více než 5 MB), zvažte jeho zmenšení. Aspose OCR pracuje rychleji s obrázky menšími než 2000 px v libovolném rozměru.

---

## Krok 2 – Definování polygonů pro pole, která chcete číst

*Region of Interest* (ROI) je jen polygon, který říká enginu, kde má hledat. Níže vytvoříme dva obdélníky – jeden pro „First Name“ a druhý pro „Date of Birth“. Přizpůsobte souřadnice podle svého formuláře.

```java
        // Polygon for the first field (e.g., First Name)
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},   // X‑coordinates
                new int[]{100, 100, 150, 150}, // Y‑coordinates
                4);

        // Polygon for the second field (e.g., Date of Birth)
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);
```

*Proč polygon místo obdélníku?*  
Polygony vám dávají flexibilitu při zpracování šikmých nebo nepravidelných polí – což je časté u skenovaných tištěných formulářů, které nejsou dokonale zarovnané.

---

## Krok 3 – Řekněte Aspose OCR, aby se zaměřil jen na tyto oblasti

Nyní svázeme polygony s enginem. Metoda `setRegionsOfInterest` přijímá seznam, takže můžete přidat libovolný počet polí.

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*Co se děje pod kapotou?*  
Aspose OCR ořízne každý polygon do samostatné bitmapy, spustí rozpoznávací algoritmus a pak výsledky spojí. Tím se dramaticky sníží falešně pozitivní detekce z okolní grafiky.

---

## Krok 4 – Spuštění OCR procesu

Po nastavení všeho spustíme OCR. Volání `process()` vrací objekt `OcrResult`, který obsahuje extrahovaný text a skóre důvěry.

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

Pokud potřebujete důvěru pro jednotlivá pole, můžete prozkoumat `ocrResult.getRegions()` – každá oblast nese své vlastní skóre. Pro většinu jednoduchých formulářů stačí celkový text.

---

## Krok 5 – Zobrazení (nebo uložení) extrahovaného textu

Nakonec výsledek vypíšeme do konzole. Ve skutečné aplikaci byste ho možná uložili do databáze, JSON souboru nebo odeslali přes API.

```java
        // Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Očekávaný výstup (příklad):**

```
=== Extracted Text ===
John Doe
12/04/1990
```

Tyto dva řádky odpovídají dvěma polygonům, které jsme definovali. Pokud vidíte nadbytečné mezery, odstraňte je pomocí `String.trim()`.

---

## Jak extrahovat text z formuláře, když máte mnoho polí

Když formulář obsahuje desítky vstupů, ruční zadávání souřadnic se stává únavným. Zde je rychlý vzor, který můžete použít:

1. **Vytvořte CSV**, kde každý řádek obsahuje `fieldName, x1, y1, x2, y2, x3, y3, x4, y4`.  
2. **Načtěte CSV** za běhu, projděte každý řádek, vytvořte `Polygon` a přidejte ho do seznamu ROI.  

```java
List<Polygon> rois = new ArrayList<>();
try (BufferedReader br = new BufferedReader(new FileReader("fields.csv"))) {
    String line;
    while ((line = br.readLine()) != null) {
        String[] parts = line.split(",");
        int[] xs = { Integer.parseInt(parts[1]), Integer.parseInt(parts[3]),
                    Integer.parseInt(parts[5]), Integer.parseInt(parts[7]) };
        int[] ys = { Integer.parseInt(parts[2]), Integer.parseInt(parts[4]),
                    Integer.parseInt(parts[6]), Integer.parseInt(parts[8]) };
        rois.add(new Polygon(xs, ys, 4));
    }
}
ocrEngine.getEngineOptions().setRegionsOfInterest(rois);
```

*Proč to dělat?*  
Automatizace generování ROI vám umožní použít stejný Java kód napříč různými rozvrženími formulářů a udržet projekt DRY (Don’t Repeat Yourself).

---

## Okrajové případy a tipy, na které jste možná nepomysleli

- **Otočené skeny:** Pokud je celý obrázek otočen, zavolejte `ocrEngine.getEngineOptions().setRotateAngle(degrees)`.  
- **Nízký kontrast:** Nastavte `ocrEngine.getEngineOptions().setContrast(1.5f)` pro zlepšení čitelnosti.  
- **Není‑latinské skripty:** Přepněte jazyk pomocí `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)` (nebo jakýkoli podporovaný jazyk).  
- **Částečné selhání OCR:** Vždy kontrolujte `ocrResult.getConfidence()`; pokud klesne pod 80 %, zvažte vyzvání uživatele k ruční kontrole.  

---

## Kompletní funkční příklad (připravený ke zkopírování)

Níže je celý program, připravený ke kompilaci a spuštění. Nahraďte `YOUR_DIRECTORY` složkou, která obsahuje `form.png`.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Step 1 – Initialize engine and load image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));

        // Step 2 – Define polygons for each form field
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},
                new int[]{100, 100, 150, 150},
                4);
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);

        // Step 3 – Limit OCR to those regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));

        // Step 4 – Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // Step 5 – Show the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Kompilace:

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

Měli byste vidět dva řádky textu, které patří k definovaným ROI.

---

## Často kladené otázky

**Q: Funguje to i s PDF?**  
A: Ne přímo. Nejprve převěďte každou stránku PDF na obrázek (např. pomocí Aspose PDF) a pak obrázek předáte OCR engine.

**Q: Co když má můj formulář zaškrtávací políčka?**  
A: OCR nedokáže číst boolean hodnoty, ale můžete oblast zaškrtávacího políčka považovat za ROI a zkontrolovat hustotu pixelů pro odhad, zda je zaškrtnuté.

**Q: Můžu extrahovat text z více‑stránkového formuláře najednou?**  
A: Projděte každou stránku jako obrázek, znovu použijte stejný seznam ROI a výsledky spojte.

---

## Závěr

Prošli jsme kompletním, end‑to‑end řešením pro **extrahování textu z obrázku** pomocí Aspose OCR a ukázali, jak stejnou techniku využít k **extrahování textu z polí formuláře** s přesnou přesností. Definováním polygonů, omezením zaměření enginu a řešením běžných úskalí získáte rychlé, čisté data bez zbytečného zpracování celého obrázku.

Jste připraveni na další krok? Zkuste propojit tento OCR výstup s JSON payloadem nebo ho předat modelu strojového učení pro validaci. Možnosti jsou neomezené a nyní je máte ve svých rukou.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}