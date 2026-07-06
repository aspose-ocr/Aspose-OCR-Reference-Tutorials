---
category: general
date: 2026-02-17
description: Jak používat OCR v Javě k extrakci textu z PDF, převodu PDF na obrázky
  a provádění OCR na naskenovaných PDF souborech pomocí Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- convert pdf to images
- perform OCR on pdf
- recognize scanned pdf
language: cs
og_description: Jak používat OCR v Javě k extrahování textu z PDF souborů. Naučte
  se převádět PDF na obrázky a rozpoznávat skenované PDF pomocí Aspose.OCR.
og_title: Jak používat OCR v Javě – kompletní průvodce
tags:
- OCR
- Java
- Aspose
title: Jak používat OCR v Javě – Extrahovat text z PDF pomocí Aspose.OCR
url: /cs/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR v Javě – Extrahovat text z PDF pomocí Aspose.OCR

Už jste se někdy zamýšleli **jak používat OCR** k převodu naskenovaného PDF na prohledávatelný text? Nejste v tom jediní. Většina vývojářů narazí na problém, když PDF přijde jako sada obrázků, a běžné extraktory textu prostě nic nevrátí. Dobrá zpráva? S několika řádky Javy a Aspose.OCR můžete **extrahovat text z PDF**, **převést PDF na obrázky** a **rozpoznat naskenované PDF** v jednom, bezbolestném pracovním postupu.

V tomto tutoriálu projdeme vše, co potřebujete vědět – od licencování knihovny až po vytištění konečného výsledku. Na konci budete mít připravený program, který vytáhne prostý text z libovolné naskenované zprávy, faktury nebo e‑knihy. Žádné externí služby, žádná magie – pouze čistý Java kód, který máte pod kontrolou.

## Co budete potřebovat

- **Java Development Kit (JDK) 8+** – jakákoli aktuální verze funguje.  
- **Aspose.OCR for Java** JAR (stáhněte z webu Aspose).  
- Platný **soubor licence Aspose.OCR** (`Aspose.OCR.lic`). Bezplatná zkušební verze funguje, ale licence odemkne plnou přesnost.  
- **Ukázkový naskenovaný PDF** (např. `scanned-report.pdf`).  
- IDE nebo jednoduchý textový editor plus terminál.

To je vše. Žádný Maven, žádný Gradle, žádné další závislosti – pouze Aspose.OCR JAR ve vašem classpathu.

![how to use OCR example](image-placeholder.png "how to use OCR example")

## Krok 1 – Načtěte svou licenci Aspose.OCR (Proč je to důležité)

Než engine může běžet na plnou rychlost, musíte mu říct, kde se nachází vaše licence. Přeskočení tohoto kroku přinutí knihovnu do režimu hodnocení, který přidává vodoznaky do výstupu a může omezit přesnost.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – required for unrestricted OCR
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Proč to funguje:** Třída `License` načte soubor `.lic` a zaregistruje jej globálně. Jakmile je nastaveno, každý `OcrEngine`, který vytvoříte, bude automaticky používat licencované funkce.

## Krok 2 – Vytvořte OCR engine (Motor za kouzlem)

Instance `OcrEngine` je pracovním koněm, který skenuje obrázky a vypisuje text. Považujte ji za mozek, který interpretuje pixlové vzory.

```java
        // Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Pro tip:** Můžete ladit jazyk, prahy důvěry nebo dokonce povolit akceleraci GPU pomocí vlastností engine. Pro většinu anglických PDF jsou výchozí nastavení v pořádku.

## Krok 3 – Připravte vstup: Přidejte své PDF (Převod PDF na obrázky pod kapotou)

Aspose.OCR zachází s každou stránkou PDF jako s obrázkem. Když zavoláte `addPdf`, knihovna tiše rasterizuje každou stránku, což je přesně to, co potřebujete k **převodu PDF na obrázky** před rozpoznáním.

```java
        // Prepare OCR input – each PDF page becomes an image internally
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");
```

**Co se děje:**  
- PDF je otevřeno.  
- Každá stránka je vykreslena při 300 dpi (výchozí) pro zachování detailu znaků.  
- Vykreslené bitmapové objekty jsou uloženy v kolekci `OcrInput`.

Pokud někdy budete potřebovat surové obrázky (pro ladění nebo vlastní předzpracování), zavolejte po tomto kroku `ocrInput.getPages()`.

## Krok 4 – Spusťte OCR proces (Provést OCR na PDF)

Nyní začíná těžká práce. Metoda `recognize` prochází každý obrázek, spouští rozpoznávací algoritmus a agreguje výsledky do objektu `OcrResult`.

```java
        // Run OCR on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Proč by vás to mělo zajímat:** `OcrResult` obsahuje nejen prostý text, ale také skóre důvěry, ohraničovací rámečky a odkaz na původní obrázek. Pro většinu případů použití budete potřebovat jen `getText()`.

## Krok 5 – Získejte a zobrazte extrahovaný text

Nakonec vytáhněte řetězec prostého textu z výsledku a vytiskněte jej. Můžete jej také zapsat do souboru, předat do vyhledávacího indexu nebo do následného NLP pipeline.

```java
        // Output the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

### Očekávaný výstup

Pokud `scanned-report.pdf` obsahuje jednoduchý odstavec, uvidíte něco jako:

```
Extracted text:
Quarterly Sales Report
Region: North America
Total Revenue: $4,527,000
...
```

Přesné formátování odráží původní rozložení a zachovává zalomení řádků, kde je to možné.

## Řešení běžných okrajových případů

### 1. Vícejazyčná PDF

Pokud váš dokument obsahuje francouzský nebo španělský text, nastavte jazyk před voláním `recognize`:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);
```

Můžete poskytnout pole jazyků, aby engine automaticky detekoval.

### 2. Skeny s nízkým rozlišením

Při práci se skeny 150 dpi zvyšte interní DPI renderování:

```java
ocrInput.addPdf("low-res.pdf", 600); // render at 600 dpi for better accuracy
```

Vyšší DPI zlepšuje čitelnost znaků, ale spotřebuje více paměti.

### 3. Velké PDF (správa paměti)

Pro PDF s desítkami stránek je zpracovávejte po dávkách:

```java
int batchSize = 10;
for (int i = 0; i < ocrInput.getPages().size(); i += batchSize) {
    List<OcrPage> batch = ocrInput.getPages().subList(i, Math.min(i + batchSize, ocrInput.getPages().size()));
    OcrInput batchInput = new OcrInput();
    batchInput.getPages().addAll(batch);
    OcrResult batchResult = ocrEngine.recognize(batchInput);
    // Append batchResult.getText() to your final output
}
```

Tento přístup zabraňuje nafouknutí haldy JVM.

## Kompletní, připravený k spuštění příklad

Níže je kompletní program – včetně importů a manipulace s licencí – takže jej můžete zkopírovat a okamžitě spustit.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (required for full functionality)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Step 2: Create an OCR engine instance that will perform the recognition
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Prepare the OCR input by adding the PDF file.
        // Each page of the PDF is internally converted to an image.
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");

        // Step 4: Run the OCR process on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

Spusťte to pomocí:

```bash
javac -cp "path/to/aspose-ocr.jar" PdfOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" PdfOcrDemo
```

Měli byste vidět extrahovaný text vytištěný do konzole.

## Shrnutí – Co jsme pokryli

- **Jak používat OCR** v Javě s Aspose.OCR.  
- Pracovní postup pro **extrahování textu z PDF** souborů.  
- Interně knihovna **převádí PDF na obrázky** před rozpoznáním znaků.  
- Tipy pro **provádění OCR na PDF** s více jazyky, skeny s nízkým rozlišením a velkými dokumenty.  
- Kompletní, spustitelný ukázkový kód, který můžete vložit do jakéhokoli Java projektu.

## Další kroky a související témata

Nyní, když můžete **rozpoznat naskenované PDF**, zvažte následující nápady:

- **Generování prohledávatelného PDF** – překrytí OCR textu zpět na originální PDF pro vytvoření prohledávatelného dokumentu.  
- **Služba dávkového zpracování** – zabalit kód do mikroservisu Spring Boot, který přijímá PDF přes REST.  
- **Integrace s Elasticsearch** – indexovat extrahovaný text pro rychlé full‑textové vyhledávání napříč úložištěm dokumentů.  
- **Předzpracování obrázků** – použít OpenCV k vyrovnání nebo odstranění šumu stránek před OCR pro ještě vyšší přesnost.

Každé z těchto témat staví na základních konceptech, které jsme probrali, takže klidně experimentujte a nechte OCR engine udělat těžkou práci.

---

*Šťastné kódování! Pokud narazíte na jakékoli potíže – například chyby licence nebo neočekávané null výsledky – zanechte komentář níže. Rád pomohu s laděním.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}