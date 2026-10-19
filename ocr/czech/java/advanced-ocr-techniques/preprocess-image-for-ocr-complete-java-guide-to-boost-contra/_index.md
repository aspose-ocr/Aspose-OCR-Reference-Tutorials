---
category: general
date: 2026-02-17
description: Předzpracování obrázku pro OCR pomocí Aspose OCR v Javě. Naučte se zvýšit
  kontrast obrázku, nastavit úroveň kontrastu a rozpoznat text z obrázku během několika
  minut.
draft: false
keywords:
- preprocess image for ocr
- boost image contrast
- recognize text from image
- extract text using OCR
- set contrast level
language: cs
og_description: Předzpracování obrázku pro OCR pomocí Aspose OCR Java. Tento návod
  ukazuje, jak zvýšit kontrast obrázku, nastavit úroveň kontrastu a rychle rozpoznat
  text z obrázku.
og_title: Předzpracování obrázku pro OCR – Java tutoriál pro zvýšení kontrastu a extrakci
  textu
tags:
- Java
- OCR
- Image Processing
title: Předzpracování obrázku pro OCR – Kompletní Java průvodce pro zvýšení kontrastu
  a extrakci textu
url: /cs/java/advanced-ocr-techniques/preprocess-image-for-ocr-complete-java-guide-to-boost-contra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Předzpracování obrazu pro OCR – Kompletní průvodce v Javě

Už jste někdy potřebovali **preprocess image for OCR**, ale nebyli jste si jisti, které nastavení skutečně dělá rozdíl? Nejste v tom sami. Většina vývojářů hodí obrázek do OCR enginu a doufá, že se stane kouzlo, jen aby získali nečitelný výstup. V tomto tutoriálu projdeme praktickým, end‑to‑end příkladem, který **boosts image contrast**, upraví **contrast level** a nakonec **recognizes text from image** pomocí Aspose OCR pro Java.

Do konce budete mít znovupoužitelný úryvek kódu, který **extracts text using OCR** spolehlivě, i na špinavých skenech. Žádné skryté triky, jen jasné kroky a zdůvodnění za každým z nich.

## Co budete potřebovat

- Java 17 nebo novější (kód se kompiluje s jakýmkoli recentním JDK)
- Knihovna Aspose OCR pro Java (stáhněte z oficiálního webu Aspose)
- Platný licenční soubor Aspose OCR (`Aspose.OCR.lic`)
- Vstupní obrázek (`input.jpg`), který chcete načíst
- Oblíbené IDE nebo jednoduché nastavení příkazové řádky

Pokud už to máte, skvělé — pojďme rovnou do toho.

## Krok 1: Načtení licence Aspose OCR (Základní nastavení)

Než OCR engine něco udělá, musí vědět, že máte licenci. Jinak narazíte na vodotisk z trial verze.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Load the Aspose OCR license – this disables the evaluation limits
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Proč je to důležité:** Bez řádné licence běží engine v evaluačním režimu, což může ořezávat výsledky nebo přidávat vodotisky. Nastavení licence brzy také zajišťuje, že všechny následné možnosti předzpracování jsou aplikovány v plno‑funkčním režimu.

## Krok 2: Inicializace OCR enginu

Vytvoření instance `OcrEngine` vám poskytuje přístup k rozpoznávacím i předzpracovacím pipeline.

```java
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Tip:** Uchovávejte engine jako singleton, pokud plánujete zpracovávat mnoho obrázků v dávce; kešuje interní zdroje a urychluje následné volání.

## Krok 3: Konfigurace předzpracování – Deskew, Denoise a zvýšení kontrastu

Zde **preprocess image for OCR**. Tři ovládací prvky, které nastavíme, jsou:

1. **Deskew** — koriguje mírné rotace.
2. **Denoise** — odstraňuje šmouhy, které zmatení segmentaci znaků.
3. **Contrast enhancement** — zvýrazní tmavý text oproti pozadí.

```java
        // Access preprocessing settings
        PreprocessingSettings preprocessing = ocrEngine.getPreprocessing();

        // Enable automatic deskew (helps with scanned pages that are a few degrees off)
        preprocessing.setDeskew(true);
        preprocessing.setDeskewAngleTolerance(0.1); // tolerance in degrees

        // Turn on denoising – median works well for salt‑and‑pepper noise
        preprocessing.setDenoise(true);
        preprocessing.setDenoiseMode(DenoiseMode.MEDIAN); // alternatives: GAUSSIAN

        // Boost contrast – this is the “boost image contrast” step
        preprocessing.setContrastEnhance(true);
        preprocessing.setContrastLevel(1.3f); // 1.0 = no change, >1.0 = stronger contrast
```

### Proč upravit úroveň kontrastu?

Zvýšení úrovně kontrastu roztahuje histogram obrazu, čímž tmavé pixely ztmaví a světlé pixely zesvětlí. V praxi **contrast level** `1.3f` často poskytuje nejlepší rovnováhu pro tištěné dokumenty, zatímco hodnota nad `1.5f` může přepálit tenké tahy. Klidně experimentujte; nastavení je levné na změnu a může dramaticky zlepšit úspěšnost **recognize text from image**.

## Krok 4: Příprava vstupního obrázku

Třída `OcrInput` abstrahuje práci se soubory. Můžete přidat více obrázků, pokud potřebujete dávkové zpracování.

```java
        // Prepare the image for OCR – you can add more files to the same OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.jpg");
```

**Hraniční případ:** Pokud je váš obrázek v nestandardním formátu (např. TIFF s více stránkami), můžete načíst každou stránku zvlášť nebo jej nejprve převést na PNG/JPEG.

## Krok 5: Provedení rozpoznání

Nyní engine spustí předzpracovací pipeline, kterou jsme právě nakonfigurovali, a poté předá vyčištěný obrázek jádru OCR algoritmu.

```java
        // Run OCR – this returns a result object containing the extracted text
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Co se děje pod kapotou?** Aspose OCR nejprve aplikuje transformaci deskew, poté spustí filtr denoise a nakonec upraví kontrast před předáním obrázku svému rozpoznávači založenému na neuronové síti. Pořadí je úmyslné; jeho změna může vést k suboptimálním výsledkům.

## Krok 6: Výstup rozpoznaného textu

Nakonec vytiskneme extrahovaný řetězec do konzole. Ve skutečné aplikaci jej můžete zapsat do souboru nebo odeslat po síti.

```java
        // Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

### Očekávaný výstup

Pokud `input.jpg` obsahuje frázi „Hello World!“, měla by konzole zobrazit:

```
Hello World!
```

Pokud výstup vypadá poškozeně, dvakrát zkontrolujte hodnoty předzpracování — zejména **contrast level** a **denoise mode** — a zkuste jiný formát obrázku.

## Bonus: Vizualizace předzpracovaného obrázku (volitelné)

Někdy chcete vidět, co engine vidí po deskew, denoise a zvýšení kontrastu. Aspose OCR vám umožní exportovat mezilehlý bitmap:

```java
        // Export the pre‑processed image for debugging
        BufferedImage processed = preprocessing.getProcessedImage();
        ImageIO.write(processed, "png", new File("processed.png"));
```

Otevřete `processed.png` vedle originálu; všimnete si rovnějšího horizontu a ostřejšího textu. Tento krok je užitečný při odhalování, proč konkrétní sken selhává.

![příklad předzpracování obrazu pro OCR](/images/ocr-preprocess-example.png "předzpracování obrazu pro OCR – před a po zvýšení kontrastu")

*Obrázek výše ukazuje, jak zvýšení kontrastu a odšumění promění rozmazaný sken na čistý, připravený pro OCR obrázek.*

## Časté úskalí a jak se jim vyhnout

| Problém | Proč se to děje | Oprava |
|---------|----------------|--------|
| **Přetížení kontrastu** (`setContrastLevel` příliš vysoký) | Světlé pozadí se stane bílým, vymazávajíc slabé znaky | Udržujte úroveň mezi 1.1 a 1.4 pro většinu tištěného textu |
| **Nízká tolerance deskew** | Malé rotace zůstávají neopravené | Zvyšte `setDeskewAngleTolerance` na 0.2 nebo 0.3 pro skenované knihy |
| **Použití GAUSSIAN denoise na binárních obrazech** | Rozmazává hrany, spojuje znaky | Používejte `DenoiseMode.MEDIAN` pro černobílé skeny |
| **Chybějící licence** | Engine přechází do trial režimu, ořezává výstup | Ověřte cestu k `Aspose.OCR.lic` a že soubor je čitelný |

## Další kroky: Přesah základního předzpracování

Nyní, když můžete **preprocess image for OCR** a **extract text using OCR**, zvažte tyto rozšíření:

- **Language packs** — načtěte specifické jazykové slovníky pro zlepšení přesnosti u textu neanglického.
- **Region‑of‑interest (ROI) cropping** — zaměřte se na podčást obrázku, pokud potřebujete jen část stránky.
- **Batch processing** — projděte adresář obrázků, znovu použijte stejnou instanci `OcrEngine` pro rychlost.
- **Integrate with PDF** — kombinujte Aspose OCR s Aspose PDF pro převod skenovaných PDF na prohledávatelná PDF v jedné pipeline.

Každé z těchto témat přirozeně zahrnuje naše sekundární klíčová slova: stále budete **boost image contrast**, **set contrast level**, a nadále **recognize text from image** v mnoha scénářích.

## Závěr

Probrali jsme vše, co potřebujete k **preprocess image for OCR** pomocí Aspose OCR pro Java: načtení licence, konfiguraci deskew, denoise a zvýšení kontrastu, předání obrázku a nakonec **recognizing text from image**. S kompletním, spustitelným příkladem výše můžete nyní **extract text using OCR** na jakémkoli vhodně připraveném obrázku.

Vyzkoušejte kód, upravte **contrast level** a sledujte, jak přesnost stoupá. Až budete připraveni, prozkoumejte jazykově specifické modely nebo dávkové pipeline, abyste tuto ukázku s jedním obrázkem proměnili v řešení připravené pro produkci.

*Šťastné kódování a ať jsou vaše skeny vždy ostré!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}