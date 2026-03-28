---
category: general
date: 2026-03-28
description: Proveďte OCR na obrázku pomocí Aspose OCR v Javě. Naučte se rozpoznávat
  text z PNG a zlepšit přesnost OCR pomocí vestavěné korekce pravopisu.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- read image text
- improve OCR accuracy
- Aspose OCR Java
- spell correction OCR
language: cs
og_description: Proveďte OCR na obrázku pomocí Aspose OCR pro Javu. Tento průvodce
  ukazuje, jak rozpoznat text z PNG a během několika minut zlepšit přesnost OCR.
og_title: Proveďte OCR na obrázku pomocí Javy – Kompletní průvodce
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Provést OCR na obrázku v Javě – Rozpoznat text z PNG
url: /cs/java/advanced-ocr-techniques/perform-ocr-on-image-with-java-recognize-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Provést OCR na obrázku pomocí Javy – Rozpoznat text z PNG

Už jste někdy potřebovali **provést OCR na obrázku** soubory, ale stále jste dostávali zkreslené výsledky? Nejste v tom sami—špinavé skeny, PNG s nízkým kontrastem a podivná písma mohou čistý dokument proměnit v chaotickou směs znaků.  

V tomto průvodci vás provedeme kompletním, připraveným příkladem v Javě, který **rozpozná text z PNG** pomocí Aspose OCR, a také vám ukážeme, jak **zlepšit přesnost OCR** pomocí funkce opravy pravopisu v knihovně. Na konci budete schopni **číst text z obrázku** spolehlivě, i když zdroj není dokonalý.

## Co se naučíte

- Jak nastavit Aspose OCR pro Javu v Maven projektu.  
- Přesné kroky k **provedení OCR na obrázku** dat, od načtení souboru po získání čistého textu.  
- Proč zapnutí opravy pravopisu může dramaticky zvýšit kvalitu výstupu.  
- Běžné úskalí (chybějící soubory, nepodporované formáty) a jak je elegantně řešit.  
- Úplný, připravený k zkopírování kód, který můžete spustit ještě dnes.

### Předpoklady

- Java 8 nebo novější nainstalovaná na vašem počítači.  
- Maven pro správu závislostí (každé IDE s podporou Maven bude stačit).  
- PNG obrázek, který obsahuje čitelný text – nejlépe takový, který je trochu špinavý, abyste mohli vidět výhodu opravy pravopisu.

> **Tip:** Pokud nemáte po ruce PNG, pořiďte si jakýkoli snímek obrazovky dokumentu nebo fotografii cedule. Čím „špinavější“ vypadá, tím více oceníte zvýšení přesnosti.

---

## Krok 1: Přidejte závislost Aspose OCR

Nejprve—přidejte knihovnu Aspose OCR do vašeho `pom.xml`. Tento jediný řádek stáhne nejnovější verzi (k březnu 2026) a vyřeší všechny tranzitivní závislosti.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

> **Proč je to důležité:** Bez knihovny nemůžete vytvořit `OcrEngine` a celý **workflow provedení OCR na obrázku** by selhal za běhu.

---

## Krok 2: Inicializujte OCR engine

Vytvoření engine je jednoduché, ale existuje jemný důvod, proč udržet inicializaci oddělenou od volání rozpoznání: poskytuje vám místo, kde můžete doladit nastavení jako jazyk, DPI nebo, co je pro nás nejdůležitější, opravu pravopisu.

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {

    public static void main(String[] args) {
        try {
            // Step 2: Initialize the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Pro tip: you can set the language here if you need something other than English
            // ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

Všimněte si komentáře—nastavení jazyka může být záchranou, když váš PNG obsahuje ne‑anglické znaky.

---

## Krok 3: Povolit opravu pravopisu pro **zlepšení přesnosti OCR**

Aspose OCR obsahuje vestavěný modul opravy pravopisu, který funguje jako lehký slovník. Zapnutí je jednorázový řádek, ale dopad na konečný výstup může být obrovský, zejména u špinavých obrázků.

```java
            // Step 3: Enable spell correction to improve OCR accuracy on noisy text
            ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);
```

> **Co když to nepotřebujete?** Můžete jednoduše nastavit příznak na `false`. Vypnutí může být užitečné pro text specifický pro doménu, kde by slovník označil legitimní termíny jako chyby.

---

## Krok 4: Načtěte a rozpoznávejte PNG

Nyní skutečně **čteme text z obrázku** ze souboru. Metoda `recognizeImage` přijímá řetězec cesty, ale můžete jí také předat `java.io.InputStream`, pokud obrázek získáváte z databáze nebo webu.

```java
            // Step 4: Perform OCR on the input image
            String imagePath = "YOUR_DIRECTORY/noisy-image.png"; // replace with your actual path
            OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

Pokud soubor není nalezen, Aspose vyhodí popisnou výjimku—není potřeba ručně kontrolovat `File.exists()`. Přesto zabalení volání do `try/catch` (jak děláme) poskytne uživateli čistou chybovou zprávu.

---

## Krok 5: Výstup opraveného textu

Nakonec vytiskněte výsledek do konzole. Ve skutečné aplikaci byste jej pravděpodobně zapisovali do databáze nebo do následné služby, ale konzole je ideální pro rychlou ukázku.

```java
            // Step 5: Output the corrected text
            System.out.println("Corrected text:\\n" + ocrResult.getText());
        } catch (Exception e) {
            System.err.println("Error during OCR processing: " + e.getMessage());
        }
    }
}
```

**Očekávaný výstup** (předpokládáme, že PNG obsahuje frázi „Aspose OCR library“ s nějakým šumem):

```
Corrected text:
Aspose OCR library
```

Pokud vypnete opravu pravopisu, můžete místo toho vidět něco jako „Asp0se OCR libr@ry“ – přesně proto, že **zlepšení přesnosti OCR** je důležité.

---

## Krok 6: Ověřte výsledek – Opravdu **čte text z obrázku**?

Je lákavé slepě důvěřovat výstupu v konzoli, ale rychlá kontrola může později ušetřit hodiny. Zde je několik způsobů, jak ověřit extrahovaný text:

1. **Kontrola délky** – Porovnejte `ocrResult.getText().length()` s očekávaným počtem znaků.  
2. **Vyhledávání klíčových slov** – Použijte `String.contains("Aspose")`, aby se ujistili, že se klíčové termíny objeví.  
3. **Jednotkový test** – Pokud integrujete toto do většího systému, napište JUnit test, který ověří, že výstup odpovídá známé správné hodnotě.

```java
// Example sanity check
if (ocrResult.getText().contains("Aspose")) {
    System.out.println("✅ Text successfully read from image.");
} else {
    System.out.println("⚠️ Unexpected OCR result – consider tweaking settings.");
}
```

---

## Běžné okrajové případy a jak je řešit

| Situace | Proč se to děje | Rychlé řešení |
|-----------|----------------|-----------|
| **Soubor nenalezen** | Špatná cesta nebo chybějící oprávnění | Ověřte `imagePath` a použijte `Files.isReadable(Paths.get(imagePath))` před voláním `recognizeImage`. |
| **Nepodporovaný formát** | Aspose OCR podporuje PNG, JPEG, BMP, TIFF atd. | Převěďte obrázek nejprve na PNG (např. pomocí ImageIO) nebo použijte `ocrEngine.recognizeImage(InputStream)`. |
| **Velmi nízké DPI** | OCR engine potřebuje alespoň ~300 DPI pro slušnou přesnost | Zvětšete obrázek pomocí `BufferedImage` a `Graphics2D` před předáním engine. |
| **Doménově specifický žargon** | Oprava pravopisu může nahradit platné termíny slovy ze slovníku | Vypněte opravu pravopisu (`setEnableSpellCorrection(false)`) nebo poskytněte vlastní slovník přes `ocrEngine.getRecognitionSettings().setCustomDictionary(...)`. |

---

## Kompletní funkční příklad (připravený ke zkopírování)

Níže je celý zdrojový soubor, připravený ke kompilaci a spuštění. Nahraďte `YOUR_DIRECTORY/noisy-image.png` skutečnou cestou k vašemu testovacímu obrázku.

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {
    public static void main(String[] args) {
        try {
            // Initialize the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Enable spell correction to improve OCR accuracy on noisy text
            ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);

            // Path to the PNG you want to process
            String imagePath = "YOUR_DIRECTORY/noisy-image.png";

            // Perform OCR on the input image
            OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

            // Output the corrected text
            System.out.println("Corrected text:\\n" + ocrResult.getText());

            // Simple verification that we actually read image text
            if (ocrResult.getText().toLowerCase().contains("aspose")) {
                System.out.println("✅ OCR succeeded – key term found.");
            } else {
                System.out.println("⚠️ OCR may need tweaking – key term missing.");
            }
        } catch (Exception e) {
            System.err.println("Error during OCR processing: " + e.getMessage());
        }
    }
}
```

Spusťte jej pomocí:

```bash
mvn compile exec:java -Dexec.mainClass=SpellCorrectExample
```

Měli byste vidět vytištěný **opravený text**, což potvrzuje, že jste úspěšně **provedli OCR na obrázku**.

---

## Vizualizace

![Perform OCR on image example](/images/ocr-example.png){alt="provedení OCR na obrázku – před a po korekci pravopisu"}

Snímek obrazovky ukazuje špinavý PNG vlevo a čistý, opravený výstup vpravo.

---

## Závěr

Právě jsme prošli kompletním řešením od začátku do konce, jak **provést OCR na obrázku** soubory pomocí Aspose OCR pro Javu. Zapnutím vestavěného příznaku opravy pravopisu můžete **zlepšit

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}