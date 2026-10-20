---
category: general
date: 2026-03-07
description: Spusťte OCR na obrázku pomocí Javy. Naučte se rozpoznávat text z PNG,
  extrahovat text z účtenky a načíst obrázek pro OCR s kompletním příkladem OCR v
  Javě.
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: cs
og_description: Spusťte OCR na obrázku pomocí Javy. Tento průvodce ukazuje, jak rozpoznat
  text z PNG, extrahovat text z účtenky a načíst obrázek pro OCR pomocí kompletního
  příkladu OCR v Javě.
og_title: Spusťte OCR na obrázku v Javě – Extrakce textu pomocí GPU
tags:
- OCR
- Java
- GPU
- Image Processing
title: Spusťte OCR na obrázku v Javě – Extrakce textu s podporou GPU
url: /cs/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spusťte OCR na obrázku v Javě – Extrakce textu s využitím GPU

Už jste někdy potřebovali **spustit OCR na obrázku** soubory, ale nebyli jste si jisti, kde v Javě začít? Nejste v tom sami — mnoho vývojářů narazí na stejnou překážku, když poprvé zkusí získat text ze skenované účtenky nebo PNG snímku.  

V tomto tutoriálu vás provedeme **kompletním Java OCR příkladem**, který nejen **rozpozná text z PNG** souborů, ale také ukáže, jak **extrahovat text z účtenky**, a to vše s využitím akcelerace GPU pro vyšší rychlost. Na konci budete mít připravený program, který načte obrázek pro OCR, zpracuje jej a vytiskne výsledek jako prostý text.

## Co se naučíte

- Jak **načíst obrázek pro OCR** pomocí jednoduchého `ImageInputStream`.
- Povolení podpory GPU, aby engine běžel rychleji na moderním hardwaru.
- Přesné kroky k **rozpoznání textu z PNG** a získání užitečných řetězců z účtenky.
- Časté úskalí (např. špatné ID GPU zařízení) a tipy na nejlepší postupy.
- Kompletní, spustitelný úryvek kódu, který můžete zkopírovat a vložit do svého IDE.

**Požadavky**

- Java 17 nebo novější (kód používá klíčové slovo `var` pro stručnost, ale můžete jej nahradit explicitními typy, pokud používáte Java 8).
- OCR knihovna, která poskytuje třídy `OcrEngine`, `ImageInputStream` a `OcrResult` (např. fiktivní *FastOCR* SDK; nahraďte skutečnou knihovnou, kterou používáte).
- Počítač s podporou GPU, pokud chcete zvýšit výkon (volitelné, ale doporučené).

---

## Krok 1: Spusťte OCR na obrázku – Povolení akcelerace GPU

Prvním krokem je vytvořit OCR engine a nastavit, aby používal GPU. Tento krok je zásadní, protože bez podpory GPU engine přejde na CPU, což může být výrazně pomalejší u vysoce rozlišených účtenek.

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**Proč je to důležité:**  
Akcelerace GPU odlehčuje těžké maticové výpočty, které OCR engine provádí. Pokud máte více GPU, můžete si vybrat ten s největší pamětí změnou hodnoty `setGpuDeviceId`. Zapomenutí povolit GPU je častým zdrojem stížností typu „proč je moje OCR tak pomalé?“.

> **Pro tip:** Pokud váš počítač nemá kompatibilní GPU, volání `setUseGpu(true)` bude jednoduše ignorováno — nedojde k pádu, jen bude zpracování pomalejší.

---

## Krok 2: Načtěte obrázek pro OCR

Nyní, když je engine připravený, musíme mu předat obrázek. Níže uvedený příklad ukazuje, jak načíst PNG účtenku uloženou na disku. Cestu můžete nahradit libovolným formátem obrázku, který vaše OCR knihovna podporuje.

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**Hraniční případ:**  
Pokud soubor neexistuje nebo je cesta špatná, `ImageInputStream` vyhodí `IOException`. Zabalte volání do try‑catch bloku a zalogujte užitečnou zprávu:

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## Krok 3: Rozpoznání textu z PNG

S načteným obrázkem může OCR engine provést svou magii. Tento krok **rozpozná text z PNG** (nebo jakéhokoli jiného podporovaného formátu) a vrátí objekt `OcrResult`.

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**Co se děje pod kapotou?**  
Engine provádí předzpracování (odklon, binarizaci), spouští neuronovou síť pro detekci znaků a poté je skládá do řádků textu. Protože jsme dříve povolili GPU, výpočty neuronové sítě probíhají na grafické kartě, což ušetří sekundy z celkového běhu.

---

## Krok 4: Extrahování textu z účtenky

Po rozpoznání budete obvykle chtít jen čistý text. Třída `OcrResult` obvykle poskytuje metodu `getText()`, která vrací jediný `String`. Ten můžete následně post‑processovat (např. regulárním výrazem vyextrahovat částky, data atd.).

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Typický výstup z účtenky:**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Nyní můžete tento řetězec předat vlastnímu parseru a získat celkovou částku, položky nebo daňové informace.

---

## Krok 5: Kompletní Java OCR příklad – připravený ke spuštění

Sestavením všeho dohromady získáte **kompletní Java OCR příklad**, který můžete vložit do souboru `Main.java`. Ujistěte se, že máte OCR knihovnu ve své classpath.

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Očekávaný výstup v konzoli** (při použití ukázkové účtenky výše):

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Pokud výstup vypadá poškozeně, zkontrolujte, že je obrázek čistý (vysoké DPI) a že jazykový balíček OCR odpovídá jazyku vaší účtenky.

---

## Časté otázky a úskalí

| Otázka | Odpověď |
|----------|--------|
| *Co když moje GPU není detekováno?* | Engine automaticky přejde na CPU. Ověřte ovladače a že `setGpuDeviceId` odpovídá existujícímu zařízení (`nvidia-smi` na Linuxu může pomoci). |
| *Mohu zpracovávat soubory JPEG nebo TIFF?* | Ano — stačí změnit příponu souboru v `ImageInputStream`. OCR knihovna obvykle automaticky rozpozná formát. |
| *Existuje způsob, jak hromadně zpracovat mnoho účtenek?* | Zabalte kód rozpoznání do smyčky a znovu použijte stejnou instanci `OcrEngine`; opětovná inicializace pro každý obrázek plýtvá GPU pamětí. |
| *Jak zlepšit přesnost u nízkokontrastních účtenek?* | Předzpracujte obrázek (zvyšte kontrast, převedte na odstíny šedi) před předáním OCR engine. Některé knihovny nabízejí API `preprocess`. |

---

## Závěr

Nyní víte, **jak spustit OCR na obrázku** v Javě, od načtení souboru až po extrakci čistého textu z účtenky. Prošli jsme **rozpoznáním textu z PNG**, **extrahováním textu z účtenky** a ukázali **java OCR příklad**, který můžete přizpůsobit libovolnému projektu.  

Další kroky? Zkuste vypnout GPU flag a porovnat výkon, experimentujte s různými rozlišeními obrázků nebo integrujte regex‑based parser pro automatické získávání částek. Pokud vás zajímají pokročilejší témata, podívejte se na **post‑processing OCR**, **korekci jazykovým modelem** nebo **pipeline pro hromadné zpracování**.

Happy coding, and may your receipts always be readable!  

![run OCR on image example](/images/run-ocr-on-image.png "run OCR on image – Java example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}