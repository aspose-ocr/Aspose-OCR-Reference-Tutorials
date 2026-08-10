---
category: general
date: 2026-02-17
description: 'tutorial převodu obrázku na text v Javě: naučte se, jak extrahovat urdský
  text z obrázku pomocí Aspose OCR. Kompletní příklad OCR v Javě zahrnut.'
draft: false
keywords:
- image to text java
- how to extract text
- extract urdu text
- java ocr example
- load image ocr
language: cs
og_description: Tutoriál image to text java ukazuje, jak extrahovat urdský text z
  obrázku pomocí Aspose OCR. Sledujte kompletní příklad java OCR krok za krokem.
og_title: 'Obrázek na text Java: Extrahovat urdský text pomocí Aspose OCR'
tags:
- OCR
- Java
- Aspose
title: 'Obrázek na text v Javě: Extrahujte urdský text pomocí Aspose OCR'
url: /cs/java/ocr-operations/image-to-text-java-extract-urdu-text-with-aspose-ocr/
---

but there are none.

Proceed to produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# image to text java: Extrahujte text v urdštině pomocí Aspose OCR

Pokud potřebujete provést **image to text java** konverzi pro dokumenty v urdštině, jste na správném místě. Už jste se někdy zamýšleli, *jak extrahovat text* z obrázku ručně psané poznámky nebo naskenované novinové stránky? Tento průvodce vás provede **java ocr example**, který vytáhne urdské znaky přímo z obrázku pomocí Aspose OCR.

Probereme vše od licencování knihovny až po výpis výsledku do konzole. Na konci budete schopni **load image ocr** soubory, nastavit jazyk na Urdu a získat čistý Unicode výstup — bez dalších nástrojů.

## Co budete potřebovat

- **Java Development Kit (JDK) 8+** — kód funguje na jakémkoli aktuálním JDK.  
- **Aspose.OCR for Java** JAR (stáhněte z webu Aspose).  
- Platný **Aspose OCR license** soubor (`Aspose.OCR.lic`).  
- Obrázek obsahující urdský text, např. `urdu-sample.png`.  

Mít tyto základní věci připravené znamená, že můžete rovnou přejít ke kódu, aniž byste museli hledat chybějící závislosti.

## image to text java – Nastavení Aspose OCR

Nejprve musíme Aspose sdělit, že máme licenci. Bez ní knihovna běží v režimu hodnocení a přidá vodoznak do výstupu.

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Proč je to důležité:** Licencování odstraňuje 5‑sekundové omezení zpracování a odemyká plný Urdu jazykový balíček, který byl přidán ve 3. čtvrtletí 2025. Pokud tento krok přeskočíte, OCR engine bude i nadále fungovat, ale ve výsledcích uvidíte malý štítek „Evaluation“.

## Jak extrahovat text – Inicializace OCR enginu

Nyní vytvoříme engine a výslovně mu řekneme, že nás zajímá Urdu. Konstantní `OcrLanguage.URDU` aktivuje správnou znakovou sadu a pravidla segmentace.

```java
        // Step 2: Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3
```

**Tip:** Pokud někdy potřebujete zpracovat více jazyků najednou, můžete předat čárkou oddělený seznam, např. `OcrLanguage.ENGLISH, OcrLanguage.URDU`. Engine automaticky detekuje každou oblast.

## Load Image OCR – Příprava vstupu

Aspose pracuje s objektem `OcrInput`, který může obsahovat jeden nebo více obrázků. Zde **load image ocr** data z lokálního souboru.

```java
        // Step 3: Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");
```

> **Poznámka:** Nahraďte `YOUR_DIRECTORY` absolutní cestou nebo relativní cestou od kořene vašeho projektu. Pokud soubor není nalezen, Aspose vyhodí `FileNotFoundException`. Rychlá kontrola pomocí `new File(path).exists()` vám může ušetřit spoustu času při ladění.

## Rozpoznání textu – Spuštění OCR procesu

S nakonfigurovaným enginem a načteným obrázkem nakonec zavoláme `recognize`. Metoda vrátí `OcrResult`, který obsahuje extrahovaný řetězec.

```java
        // Step 4: Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Co se děje pod kapotou?** OCR engine rozdělí obrázek na řádky, pak na znaky a aplikuje urdsky‑specifická pravidla tvarování (jako spojování tvarů). Proto je nastavení jazyka na začátku klíčové; jinak získáte zkomolené latinské zástupce.

## Výpis rozpoznaného urdského textu

Posledním krokem je jednoduše vypsat výsledek. Protože Urdu používá skript zprava doleva, ujistěte se, že vaše konzole podporuje Unicode (většina moderních terminálů ano).

```java
        // Step 5: Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

**Očekávaný výstup (příklad):**

```
Urdu text:
یہ ایک مثال کا متن ہے جو تصویر سے نکالا گیا ہے۔
```

Pokud vidíte otazníky nebo prázdné řetězce, zkontrolujte, že kódování vaší konzole je nastaveno na UTF‑8 (`chcp 65001` ve Windows, nebo spusťte Javu s `-Dfile.encoding=UTF-8`).

## Kompletní funkční příklad – Všechny kroky na jednom místě

Níže je kompletní, připravený k zkopírování program. Žádné externí odkazy, jen jediný Java soubor.

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3

        // Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");

        // Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

Spusťte jej pomocí:

```bash
javac -cp "aspose-ocr-23.10.jar" UrduDemo.java
java -cp ".:aspose-ocr-23.10.jar" UrduDemo
```

Nahraďte verzi JAR (`23.10`) tou, kterou jste si stáhli. Konzole by měla zobrazit urdskou větu extrahovanou z vašeho PNG.

## Časté problémy a okrajové případy

| Problém | Proč se vyskytuje | Jak opravit |
|---------|-------------------|-------------|
| **Prázdný výstup** | Obrázek je příliš tmavý nebo má nízké rozlišení. | Předzpracujte obrázek (zvyšte kontrast, binarizujte) pomocí `BufferedImage` před předáním Aspose. |
| **Špatné znaky** | Nesprávně nastavený jazyk (výchozí je angličtina). | Ujistěte se, že je voláno `ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU);` před `recognize`. |
| **Licence nenalezena** | Chybná cesta nebo chybějící soubor. | Použijte absolutní cestu nebo umístěte soubor `.lic` do classpath a zavolejte `license.setLicense("Aspose.OCR.lic");`. |
| **Nedostatek paměti u velkých obrázků** | Velké PNG zabírají heap. | Zavolejte `ocrEngine.setMaxImageSize(2000);` pro interní zmenšení, nebo obrázek zmenšete sami. |

## Rozšíření demonstrace

- **Dávkové zpracování:** Procházejte složku, přidávejte každý soubor do stejného `OcrInput` a sbírejte výsledky do CSV.  
- **Různé jazyky:** Vyměňte `OcrLanguage.URDU` za `OcrLanguage.ARABIC` nebo kombinujte více jazyků.  
- **Ukládání do souboru:** Použijte `Files.write(Paths.get("output.txt"), ocrResult.getText().getBytes(StandardCharsets.UTF_8));`.  

Všechny tyto nápady staví na **java ocr example**, který jsme právě vytvořili, a umožňují vám přizpůsobit řešení reálným projektům.

## Závěr

Nyní máte solidní **image to text java** workflow, který extrahuje urdské znaky z obrázku pomocí Aspose OCR. Tutoriál pokryl každý krok — od licencování a výběru jazyka po načtení obrázku a výpis výsledku — takže můžete kód vložit do libovolného Java projektu a sledovat, jak funguje.

Dále zkuste experimentovat s většími PDF, různými skripty nebo dokonce integrovat OCR krok do Spring Boot REST endpointu. Stejné principy — **how to extract text**, **load image o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}