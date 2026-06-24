---
category: general
date: 2026-06-19
description: Rozpoznávejte text z obrázku pomocí Aspose OCR v Javě. Naučte se, jak
  povolit kontrolu pravopisu, přidat slovník a provést OCR s kontrolou pravopisu v
  jednom tutoriálu.
draft: false
keywords:
- recognize text from image
- how to enable spellcheck
- how to add dictionary
- ocr with spell check
language: cs
og_description: Rozpoznávejte text z obrázku pomocí Aspense OCR v Javě. Tento průvodce
  ukazuje, jak povolit kontrolu pravopisu, přidat slovník a spustit OCR s kontrolou
  pravopisu.
og_title: Rozpoznání textu z obrázku – Tutoriál kontroly pravopisu pomocí Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Recognize text from image with Aspose OCR in Java. Learn how to enable
    spellcheck, add dictionary, and perform OCR with spell check in a single tutorial.
  headline: Recognize Text from Image in Java – Complete Aspose OCR Spell‑Check Guide
  type: TechArticle
- description: Recognize text from image with Aspose OCR in Java. Learn how to enable
    spellcheck, add dictionary, and perform OCR with spell check in a single tutorial.
  name: Recognize Text from Image in Java – Complete Aspose OCR Spell‑Check Guide
  steps:
  - name: How to Enable SpellCheck
    text: 'The spell checker lives inside the engine, but it’s disabled by default.
      Flip the switch with a single line:'
  - name: Expected Output
    text: 'Assuming `receipt.png` contains the line “Totel: $12.99” and your custom
      dictionary includes “Total”, the console will display:'
  - name: What if I need multiple languages?
    text: You can call `ocrEngine.setLanguage(Language.English, Language.French)`
      to enable multilingual recognition. Spell‑checking will follow each language’s
      rules, but you still need to enable it with `setEnable(true)`.
  - name: How does the engine handle unknown words?
    text: If a word isn’t in the internal dictionary *and* not in your custom dictionary,
      the spell checker attempts a best‑guess correction based on Levenshtein distance.
      For truly unknown terms, add them to `my-terms.txt`.
  - name: Does the spell checker work on numbers?
    text: By default, numeric strings are left untouched. If you have alphanumeric
      codes (e.g., “AB12C”), add them to your custom dictionary; otherwise the engine
      may try to “fix” them to real words.
  - name: Performance considerations
    text: Enabling spell checking adds a modest overhead—roughly 10‑15 % extra CPU
      per page. For batch processing, consider disabling it on the first pass, then
      re‑run only on pages that failed quality checks.
  type: HowTo
tags:
- OCR
- Java
- SpellCheck
title: Rozpoznání textu z obrázku v Javě – Kompletní průvodce kontrolou pravopisu
  Aspose OCR
url: /cs/java/advanced-ocr-techniques/recognize-text-from-image-in-java-complete-aspose-ocr-spell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rozpoznání textu z obrázku v Javě – Kompletní průvodce Aspose OCR s kontrolou pravopisu

Už jste někdy potřebovali **rozpoznat text z obrázku**, ale obávali se, že výstup bude plný překlepů? Nejste v tom sami. V mnoha projektech skenování účtenek nebo digitalizace dokumentů vypadá surový OCR text, jako kdyby ho psala ospalá kočka. Dobrá zpráva? S Aspose OCR můžete ten hlučný výpis převést na čistý, pravopisně opravený text – přímo v Javě.

V tomto tutoriálu projdeme připravený příklad, který ukazuje **jak povolit kontrolu pravopisu**, **jak přidat položky do slovníku** pro specifické termíny a nakonec **jak provést OCR s kontrolou pravopisu**. Na konci budete mít samostatný program, který načte soubor s obrázkem, opraví pravopis za běhu a vytiskne vylepšený výsledek.

## Co se naučíte

- Jak použít licenci Aspose OCR, aby API běželo na plný výkon.  
- Přesné kroky k **povolení kontroly pravopisu** v OCR enginu.  
- Správný způsob **přidání vlastního slovníku** pro slova jako kódy produktů nebo názvy značek.  
- Jak zavolat `recognizeImage` a získat čistý, opravený text.  

Žádné externí nástroje, žádné ručně psané knihovny pro kontrolu pravopisu – jen čistá Java a Aspose OCR.

## Předpoklady

- Java 8+ (kód se kompiluje s jakýmkoli aktuálním JDK).  
- Licenční soubor Aspose OCR (`Aspose.OCR.lic`). Pokud jen testujete, funguje i bezplatná zkušební verze, ale přidá vodoznak.  
- Maven nebo Gradle pro stažení závislosti `aspose-ocr`, nebo můžete JAR soubory přidat ručně.  
- Ukázkový obrázek (např. PNG s účtenkou) a textový soubor obsahující vlastní termíny.

> **Tip:** Uložte svůj vlastní slovník v kódování UTF‑8 a po jednom termínu na řádek – Aspose OCR jej načte přímo ze souborového systému.

---

## Krok 1: Nastavení projektu a přidání závislosti Aspose OCR

Pokud používáte Maven, přidejte následující úryvek do souboru `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.8</version> <!-- use the latest version -->
</dependency>
```

Pro Gradle je to stejný princip:

```groovy
implementation 'com.aspose:aspose-ocr:23.8'
```

Po vyřešení závislosti vytvořte novou třídu Java s názvem `SpellCheckDemo`. Zde se odehraje kouzlo.

## Krok 2: Použití licence Aspose OCR

Před jakoukoliv prací s OCR musíte Aspose oznámit, že může běžet neomezeně. Vynechání tohoto kroku vyvolá výjimku za běhu.

```java
// Apply the Aspose OCR license – this removes evaluation watermarks
License license = new License();
license.setLicense("Aspose.OCR.lic");   // path to your .lic file
```

> **Proč je to důležité:** Licence odemkne plný OCR engine, včetně vestavěného modulu pro kontrolu pravopisu. Bez ní engine stále funguje, ale odmítne použít některé prémiové funkce.

## Krok 3: Vytvoření a konfigurace OCR enginu

Nyní vytvoříme jádro `OcrEngine` a nastavíme jazyk na angličtinu. To je výchozí bod jak pro rozpoznávání, tak pro kontrolu pravopisu.

```java
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.setLanguage(Language.English);   // choose the language that matches your image
```

### Jak povolit kontrolu pravopisu

Kontrola pravopisu žije uvnitř enginu, ale ve výchozím nastavení je vypnutá. Zapněte ji jediným řádkem:

```java
ocrEngine.getSpellChecker().setEnable(true);   // enables spell‑checking
```

Tento řádek splňuje požadavek **jak povolit kontrolu pravopisu**. Po zapnutí engine automaticky porovná každé rozpoznané slovo s interním slovníkem a navrhne opravy.

## Krok 4: Načtení vlastního slovníku (Jak přidat slovník)

Pokud vaše dokumenty obsahují žargon – např. SKU produktů, lékařské termíny nebo názvy značek – budete chtít naučit kontrolu pravopisu o nich. Aspose OCR vám umožní ukázat na prostý textový soubor, po jednom termínu na řádek.

```java
// Load a custom word list for spell‑checking
Path customDict = java.nio.file.Paths.get("YOUR_DIRECTORY/my-terms.txt");
ocrEngine.getSpellChecker().addUserDictionary(customDict);
```

> **Co když soubor není nalezen?** API vyhodí `FileNotFoundException`. Zabalte volání do `try/catch`, pokud potřebujete elegantní degradaci.

Nyní engine zná „AcmeWidget“ nebo „RX‑9000“ a neoznačí je jako chybu.

## Krok 5: Rozpoznání textu z obrázku

S připraveným enginem můžete konečně **rozpoznat text z obrázku**. Metoda `recognizeImage` vrací objekt `OcrResult`, který obsahuje surový i opravený text.

```java
// Recognize text from the image file
OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/receipt.png");
```

Protože jsme dříve zapnuli kontrolu pravopisu, volání `getText()` již vrací opravenou verzi.

## Krok 6: Výstup opraveného textu

Zbývá jen vytisknout (nebo uložit) vyčištěný řetězec.

```java
// Output the corrected, spell‑checked text
System.out.println(ocrResult.getText());
```

Po spuštění programu byste měli vidět pěkně naformátovanou účtenku s korektním pravopisem, i když původní obrázek obsahoval rozmazané znaky.

---

## Kompletní funkční příklad

Níže je celý, připravený ke spuštění, Java program. Zkopírujte jej do svého IDE, upravte cesty k souborům a stiskněte **Run**.

```java
import com.aspose.ocr.*;

import java.nio.file.Path;
import java.nio.file.Paths;

public class SpellCheckDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");   // <-- replace with your license path

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(Language.English);

        // Step 3: Load a custom word list for spell‑checking
        Path dictPath = Paths.get("YOUR_DIRECTORY/my-terms.txt"); // <-- your dictionary file
        ocrEngine.getSpellChecker().addUserDictionary(dictPath);
        ocrEngine.getSpellChecker().setEnable(true); // <-- how to enable spellcheck

        // Step 4: Recognize text from the image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/receipt.png"); // <-- your image

        // Step 5: Output the corrected text
        System.out.println(ocrResult.getText());
    }
}
```

### Očekávaný výstup

Předpokládejme, že `receipt.png` obsahuje řádek „Totel: $12.99“ a váš vlastní slovník zahrnuje slovo „Total“. Konzole zobrazí:

```
Total: $12.99
```

Chyba „Totel“ byla automaticky opravena díky **ocr with spell check**.

---

## Často kladené otázky a okrajové případy

### Co když potřebuji více jazyků?

Můžete zavolat `ocrEngine.setLanguage(Language.English, Language.French)` a povolit tak vícejazykové rozpoznávání. Kontrola pravopisu bude následovat pravidla každého jazyka, ale stále ji musíte zapnout pomocí `setEnable(true)`.

### Jak engine zachází s neznámými slovy?

Pokud slovo není v interním slovníku *a* není ve vašem vlastním slovníku, kontrola pravopisu se pokusí o nejlepší odhad na základě Levenshteinovy vzdálenosti. Pro skutečně neznámé termíny je přidejte do `my-terms.txt`.

### Funguje kontrola pravopisu i na číslech?

Ve výchozím nastavení jsou číselné řetězce ponechány beze změny. Pokud máte alfanumerické kódy (např. „AB12C“), přidejte je do vlastního slovníku; jinak se engine může pokusit „opravit“ na skutečná slova.

### Úvahy o výkonu

Povolení kontroly pravopisu přidá mírnou režii – přibližně 10‑15 % extra CPU na stránku. Pro dávkové zpracování zvažte její vypnutí při první průchodu a následně znovu spustit jen na stránkách, které neprošly kontrolou kvality.

---

## Shrnutí

Probrali jsme vše, co potřebujete k **rozpoznání textu z obrázku** pomocí Aspose OCR v Javě a zároveň udržet výstup čistý. Kroky byly:

1. Použít licenci.  
2. Vytvořit `OcrEngine` a nastavit jazyk.  
3. **Jak přidat slovník** – načíst vlastní seznam slov.  
4. **Jak povolit kontrolu pravopisu** – přepnout kontrolu pravopisu.  
5. Spustit `recognizeImage` (hlavní volání **ocr with spell check**).  
6. Vytisknout opravený text.

To je celý pipeline – od surových pixelů po vylepšené, pravopisně opravené řetězce.

---

## Co dál?

- **Dávkové zpracování:** Procházet složku s obrázky a zapisovat každý výsledek do samostatného souboru `.txt`.  
- **PDF výstup:** Použít Aspose PDF k vložení opraveného textu zpět do prohledávatelného PDF.  
- **Pokročilé slovníky:** Načíst více uživatelských slovníků pro různé domény (např. finance vs. medicína).  
- **Skóre důvěry:** Prozkoumat `ocrResult.getConfidence()` a filtrovat výsledky s nízkou jistotou.

Klidně experimentujte – změňte jazyk, upravte slovník nebo zkombinujte s knihovnami pro předzpracování obrazu pro ještě vyšší přesnost.

Pokud narazíte na problémy, zanechte komentář níže. Šťastné kódování a ať je váš OCR vždy s kontrolou pravopisu!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}