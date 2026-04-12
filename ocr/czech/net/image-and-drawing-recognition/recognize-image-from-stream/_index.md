---
date: 2026-04-12
description: Naučte se, jak provádět extrakci textu z obrázků ze streamů pomocí Aspose
  OCR pro .NET. Tento krok‑za‑krokem příklad ukazuje snadnou extrakci OCR textu.
keywords:
- image text extraction
- image to memorystream
- ocr png file
- image stream ocr
- read image stream c#
linktitle: Rozpoznat obrázek ze streamu v OCR rozpoznávání obrazu
second_title: Aspose.OCR .NET API
title: Jak provést extrakci textu z obrázku ze streamu pomocí Aspose OCR
url: /cs/net/image-and-drawing-recognition/recognize-image-from-stream/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést extrakci textu z obrázku ze streamu pomocí Aspose OCR

Vítejte ve světě **image text extraction** s **Aspose.OCR for .NET**. V tomto tutoriálu uvidíte, jak načíst stream obrázku, spustit OCR na souboru PNG a získat rozpoznaný text do vaší C# aplikace. Ať už budujete pipeline pro zpracování dokumentů, nástroj pro automatizaci zadávání dat, nebo jen experimentujete s OCR, následující kroky vás během několika minut přivedou od surového obrázku k prohledávatelnému textu.

## Rychlé odpovědi
- **Co tento tutoriál demonstruje?** Extrahování textu z obrázku poskytnutého jako stream pomocí Aspose OCR.  
- **Jaké primární klíčové slovo je cílem?** *image text extraction* (používá se v celém průvodci).  
- **Potřebuji licenci pro vývoj?** Bezplatná zkušební verze funguje pro testování; pro produkční použití je vyžadována komerční licence.  
- **Mohu zpracovávat soubory PNG přímo?** Ano – Aspose OCR zpracovává formáty **ocr png file** bez další konverze.  
- **Které verze .NET jsou podporovány?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Co je extrakce textu z obrázku?
Extrakce textu z obrázku (také nazývaná OCR) převádí vizuální znaky v obrázku na editovatelný, prohledávatelný text. S Aspose OCR můžete předat `MemoryStream`, který obsahuje jakýkoli podporovaný obrázek (PNG, JPEG, BMP, atd.) a získat rozpoznaný řetězec v jediném volání.

## Proč zvolit Aspose OCR pro extrakci textu z obrázku?
- **Široká podpora jazyků** – funguje s desítkami jazyků ihned po instalaci.  
- **Jednoduché API** – několik řádků C# převádí **image to memorystream** na čitelný text.  
- **Vysoká přesnost** – pokročilé algoritmy zvládnou špinavé skeny a PNG s nízkým rozlišením.  
- **Cross‑platform** – běží na Windows, Linuxu a macOS s .NET Core.

## Požadavky

Než začneme, ujistěte se, že máte:

- Aspose.OCR for .NET nainstalováno (stáhněte z [Aspose.OCR for .NET Documentation](https://reference.aspose.com/ocr/net/)).  
- Ukázkový soubor obrázku (např. **sample.png**) umístěný ve složce, na kterou můžete odkazovat z kódu.

## Importovat jmenné prostory

Add the required namespaces to your C# file:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## Průvodce krok za krokem

### Krok 1: Nastavit adresář dokumentu
```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```
Nahradťe **"Your Document Directory"** skutečnou složkou, která obsahuje *sample.png*.

### Krok 2: Inicializovat Aspose OCR Engine
```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```
Vytvořením objektu `AsposeOcr` získáte přístup ke všem metodám OCR.

### Krok 3: Načíst stream obrázku a rozpoznat text
```csharp
// Recognize image
using (MemoryStream ms = new MemoryStream())
using (FileStream file = new FileStream(dataDir + "sample.png", FileMode.Open, FileAccess.Read))
{
    file.CopyTo(ms);
    result = api.RecognizeImage(ms);
}
```
Zde otevřeme **sample.png**, zkopírujeme jeho bajty do `MemoryStream` a předáme tento stream metodě `RecognizeImage`. To demonstruje **image stream ocr** a vzor **read image stream c#** v jednom průběhu.

### Krok 4: Zobrazit rozpoznaný text
```csharp
// Display the recognized text
Console.WriteLine(result);
```
Výsledek OCR je vytištěn do konzole; můžete jej také uložit do databáze nebo souboru.

### Krok 5: Potvrdit úspěšné provedení
```csharp
Console.WriteLine("RecognizeImageFromStream executed successfully");
```
Jednoduché potvrzení vám dává vědět, že proces byl dokončen bez výjimek.

## Časté problémy a řešení

| Problém | Řešení |
|-------|----------|
| *Výsledek je prázdný* | Ověřte cestu k obrázku, ujistěte se, že soubor je čitelný, a potvrďte, že obrázek obsahuje jasný, vysokokontrastní text. |
| *Nepodporovaný formát obrázku* | Před voláním `RecognizeImage` převěďte zdroj na PNG nebo JPEG. |
| *Výjimka licence* | Použijte dočasnou licenci během vývoje nebo zakupte plnou licenci pro produkci (viz níže). |

## Často kladené otázky

**Q: Dokáže Aspose.OCR zpracovat více jazyků?**  
A: Ano, Aspose.OCR podporuje širokou škálu jazyků, což ho činí vhodným pro globální OCR projekty.

**Q: Existuje zkušební verze, kterou mohu použít?**  
A: Rozhodně! Můžete si vyzkoušet Aspose.OCR pro .NET s bezplatnou zkušební verzí [zde](https://releases.aspose.com/).

**Q: Kde mohu získat pomoc, pokud narazím na problémy?**  
A: Navštivte [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) pro komunitní a odbornou podporu.

**Q: Jak získám dočasnou licenci pro testování?**  
A: Dočasná licence je k dispozici [zde](https://purchase.aspose.com/temporary-license/) pro evaluační účely.

**Q: Kde mohu zakoupit trvalou licenci?**  
A: Pro přidání Aspose.OCR do vašeho produkčního nástroje navštivte [stránku nákupu](https://purchase.aspose.com/buy).

## Závěr

Nyní jste zvládli **image text extraction** ze streamu pomocí Aspose OCR pro .NET. Stručné API vám umožní převést jakýkoli podporovaný obrázek – například **ocr png file** – na prohledávatelný text pomocí několika řádků kódu. Experimentujte s různými zdroji obrázků, jazykovými balíčky a pokročilými nastaveními, abyste vyladili výstup OCR pro váš konkrétní scénář.

---

**Poslední aktualizace:** 2026-04-12  
**Testováno s:** Aspose.OCR 24.12 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}