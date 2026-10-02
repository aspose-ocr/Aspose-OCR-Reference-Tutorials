---
category: general
date: 2026-01-10
description: Načtěte vložený zdroj a nastavte licenci Aspose v C#. Naučte se, jak
  používat GetManifestResourceStream, vložit licenční soubor a získat spouštějící
  sestavu .NET v jednom tutoriálu.
draft: false
keywords:
- read embedded resource
- set aspose license
- use getmanifestresourcestream
- how to embed license
- get executing assembly .net
language: cs
og_description: Přečtěte vložený zdroj v .NET a rychle nastavte licenci Aspose. Podrobný
  návod krok za krokem, který zahrnuje GetManifestResourceStream, vložení licence
  a použití spouštějícího sestavení.
og_title: Čtení vloženého zdroje – Nastavení licence Aspose v .NET
tags:
- C#
- .NET
- Aspose OCR
- Embedded Resources
title: Čtení vloženého zdroje v .NET – Kompletní průvodce nastavením licence Aspose
url: /cs/net/ocr-configuration/read-embedded-resource-in-net-complete-guide-to-set-aspose-l/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Čtení vloženého zdroje – Kompletní průvodce nastavením licence Aspose

Už jste někdy potřebovali **číst vložený zdroj** za běhu a přemýšleli, jak získat licenci pro knihovnu Aspose OCR bez pevně zakódovaných cest? Nejste v tom sami. V mnoha podnikových aplikacích je soubor licence umístěn uvnitř sestavení, takže nemusíte distribuovat další soubory ani se obávat chybějících oprávnění. Tento tutoriál vám přesně ukáže, jak načíst vložený zdroj a nastavit licenci Aspose pomocí metody .NET `GetManifestResourceStream`.

Projdeme vše, co potřebujete: vložení souboru `.lic`, jeho načtení pomocí `GetExecutingAssembly` a nakonec aplikaci na třídu Aspose OCR `License`. Na konci budete mít samostatné řešení, které funguje v jakémkoli projektu .NET — bez externích souborů.

## Co se naučíte

- **Jak vložit licenční soubor** do .NET projektu, aby se stal součástí zkompilovaného DLL.
- Správný způsob, jak **použít GetManifestResourceStream** k načtení toho vloženého zdroje.
- Jak **nastavit licenci Aspose** programově bez zásahu do souborového systému.
- Tipy pro řešení běžných úskalí, jako jsou špatně napsané názvy zdrojů nebo chybějící akce sestavení.
- Kompletní, spustitelný ukázkový kód, který můžete vložit do svého řešení.

### Předpoklady

- .NET 6.0 nebo novější (kód funguje také na .NET Framework 4.x, stačí upravit soubor projektu).
- Nainstalovaný NuGet balíček Aspose.OCR (`dotnet add package Aspose.OCR`).
- Základní znalost C# a Visual Studio (nebo vašeho oblíbeného IDE).

Pokud už máte tyto komponenty připravené, skvělé — pojďme se ponořit.

## Krok 1: Vložte licenční soubor Aspose do svého sestavení

Prvním krokem je skutečný licenční soubor (`Aspose.OCR.lic`). Místo jeho kopírování vedle spustitelného souboru jej vložíte jako **zdroj**.

1. Přidejte soubor `.lic` do svého projektu (např. vytvořte složku `Resources` a soubor tam umístěte).
2. V jeho vlastnostech nastavte **Build Action** na `Embedded Resource`.  
   *Pro tip:* udržujte strukturu složek jednoduchou; plně kvalifikovaný název zdroje bude `YourNamespace.Resources.Aspose.OCR.lic`.

```text
MyApp/
 └─ Resources/
     └─ Aspose.OCR.lic   ← Build Action = Embedded Resource
```

Proč vložit? Protože sestavení nyní nese licenci uvnitř sebe, čímž se eliminuje riziko chybějícího souboru na produkčním serveru.

## Krok 2: Získejte vložený zdroj pomocí GetExecutingAssembly

Nyní, když licence žije uvnitř DLL, potřebujete způsob, jak **číst vložený zdroj** za běhu. Třída .NET `Assembly` vám přesně to poskytne.

```csharp
using System.Reflection;

// Get the assembly that contains the embedded resource
Assembly currentAssembly = Assembly.GetExecutingAssembly();
```

Metoda `GetExecutingAssembly` vrací sestavení, které právě běží — ideální pro vyhledání zdrojů, které jsou umístěny vedle vašeho kódu.

## Krok 3: Otevřete stream licence pomocí GetManifestResourceStream

S odkazem na sestavení v ruce můžete zavolat `GetManifestResourceStream`. Tato metoda vrací `Stream`, který můžete předat přímo Aspose.

```csharp
// Build the fully qualified resource name
string resourceName = "MyApp.Resources.Aspose.OCR.lic";

// Attempt to open the resource stream
using Stream? licenseStream = currentAssembly.GetManifestResourceStream(resourceName);

if (licenseStream == null)
{
    throw new InvalidOperationException(
        $"Unable to locate embedded resource '{resourceName}'. " +
        "Check the namespace and Build Action settings.");
}
```

Všimněte si, že používáme **null‑conditional** `using` deklaraci (`using Stream?`), aby byl stream automaticky uvolněn. Pokud je název špatný, vyhodíme jasnou výjimku — tím se vyhnete tichým selháním později.

## Krok 4: Aplikujte licenci na Aspose OCR

Třída `License` od Aspose očekává `Stream`. Ten už máme, takže poslední krok je přímočarý.

```csharp
using Aspose.OCR;

// Create a License instance and set the license from the stream
License ocrLicense = new License();
ocrLicense.SetLicense(licenseStream);
```

A to je vše! Engine Aspose OCR je nyní plně licencován a připraven zpracovávat obrázky bez vodotisku z trial verze.

## Kompletní funkční příklad

Níže je kompletní program připravený ke zkopírování a vložení, který demonstruje celý proces. Obsahuje potřebné `using` direktivy, ošetření chyb a jednoduché volání OCR pro ověření, že je licence aktivní.

```csharp
// Program.cs
using System;
using System.IO;
using System.Reflection;
using Aspose.OCR;

namespace MyApp
{
    class Program
    {
        static void Main()
        {
            try
            {
                // Step 1: Get the current executing assembly
                Assembly currentAssembly = Assembly.GetExecutingAssembly();

                // Step 2: Build the resource name (adjust namespace/folder as needed)
                const string resourceName = "MyApp.Resources.Aspose.OCR.lic";

                // Step 3: Retrieve the embedded license stream
                using Stream? licenseStream = currentAssembly.GetManifestResourceStream(resourceName);
                if (licenseStream == null)
                {
                    Console.WriteLine($"Failed to locate embedded resource: {resourceName}");
                    return;
                }

                // Step 4: Apply the license
                License ocrLicense = new License();
                ocrLicense.SetLicense(licenseStream);
                Console.WriteLine("Aspose OCR license applied successfully.");

                // Optional: Quick test – recognize text from a sample image
                var ocrEngine = new OcrEngine();
                ocrEngine.Image = ImageStream.FromFile("sample.png"); // replace with your image path
                if (ocrEngine.Process())
                {
                    Console.WriteLine("OCR Result:");
                    Console.WriteLine(ocrEngine.Text);
                }
                else
                {
                    Console.WriteLine("OCR processing failed.");
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

### Očekávaný výstup

Po spuštění programu na stroji s platnou vloženou licencí byste měli vidět:

```
Aspose OCR license applied successfully.
OCR Result:
[Detected text from sample.png]
```

Pokud se stream licence nepodaří najít, konzole vypíše chybějící název zdroje a nasměruje vás k dvojité kontrole **Build Action** a jmenného prostoru.

## Časté úskalí a jak se jim vyhnout

| Problém | Proč k tomu dochází | Řešení |
|-------|----------------|-----|
| **Resource name mismatch** | .NET sestaví název zdroje z výchozího jmenného prostoru + cesty složky. | Použijte `Assembly.GetManifestResourceNames()` k vypsání dostupných názvů a ověřte přesný řetězec. |
| **License file not set as Embedded Resource** | Výchozí Build Action je `Content`. | Změňte ji na `Embedded Resource` ve vlastnostech souboru. |
| **Running from a different assembly** | Pokud voláte kód z knihovny tříd, `GetExecutingAssembly()` může vrátit knihovnu místo hlavního exe. | Použijte `Assembly.GetEntryAssembly()` nebo předávejte správné sestavení explicitně. |
| **Stream disposed before use** | Náhodně použijete `using` blok, který uzavře stream příliš brzy. | Nechte `using` blok obklopovat volání `SetLicense`, jak je ukázáno výše. |
| **Aspose.OCR version mismatch** | Novější verze mohou vyžadovat jiný formát licence. | Vždy stáhněte nejnovější licenci ze svého Aspose účtu a znovu ji vložte. |

## Použití stejné techniky pro jiné vložené soubory

Vzor — **číst vložený zdroj**, pak **použít GetManifestResourceStream** — funguje pro jakýkoli typ souboru: JSON konfigurace, obrázky, dokonce nativní DLL. Stačí upravit `resourceName` a způsob, jakým stream spotřebujete.

```csharp
// Example: Load an embedded JSON config
string jsonName = "MyApp.Resources.Config.appsettings.json";
using var jsonStream = Assembly.GetExecutingAssembly()
                               .GetManifestResourceStream(jsonName);
using var reader = new StreamReader(jsonStream);
string json = await reader.ReadToEndAsync();
```

## Vizualní přehled

![Diagram ukazující, jak číst vložený zdroj a nastavit licenci Aspose](read-embedded-resource-diagram.png)

*Alt text:* čtení vloženého zdroje – diagram ukazující vložení, načtení pomocí GetManifestResourceStream a aplikaci licence Aspose.

## Shrnutí

Probrali jsme, jak **číst vložený zdroj** v .NET sestavení, přesné kroky k **použití GetManifestResourceStream** a čistý způsob, jak **nastavit licenci Aspose** bez odhalování souborů na disku. Vložením licence odstraníte problémy s nasazením a udržíte aplikaci přenosnou.

## Co dál?

- **Automatizujte aktualizace licence:** Napište malý skript během sestavení, který nahradí vložený `.lic` soubor při obnovení předplatného Aspose.
- **Zabezpečte zdroj:** Zvažte šifrování licence před vložením a její dešifrování za běhu pro zvýšenou ochranu.
- **Prozkoumejte další produkty Aspose:** Stejný přístup funguje pro Aspose.Words, Aspose.PDF atd., každý s vlastní třídou `License`.

Klidně experimentujte — možná vložíte více licencí pro různé moduly, nebo přejdete na název zdroje řízený konfigurací. Možnosti jsou neomezené.

---

*Šťastné programování! Pokud narazíte na potíže, zanechte komentář níže nebo navštivte fóra Aspose pro další příklady.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}