---
category: general
date: 2026-04-06
description: Jak nastavit licenci v Aspose OCR pomocí C# – naučte se, jak vložit zdroj,
  získat vložený zdroj a načíst licenci ze souboru nebo proudu během několika kroků.
draft: false
keywords:
- how to set license
- how to embed resource
- get embedded resource
- how to load license
- use license stream
language: cs
og_description: Jak nastavit licenci v Aspose OCR je vysvětleno krok po kroku. Naučte
  se, jak vložit licenci, získat ji a použít proud licence pro bezproblémovou integraci.
og_title: Jak nastavit licenci v Aspose OCR – Kompletní průvodce C#
tags:
- Aspose OCR
- C#
- .NET licensing
title: Jak nastavit licenci v Aspose OCR – Kompletní průvodce C#
url: /cs/net/ocr-configuration/how-to-set-license-in-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak nastavit licenci v Aspose OCR – Kompletní průvodce pro C#  

Nastavení licence v Aspose OCR je běžnou překážkou pro vývojáře. V tomto tutoriálu projdeme přesné kroky, jak licenci nastavit, vložit ji jako zdroj a načíst ji ze streamu – abyste mohli spustit OCR bez otravného vodoznaku v režimu zkušební verze.  

Už jste někdy zkusili spustit úlohu OCR a místo toho se zobrazil banner „Evaluation version“? To je příznak chybějící nebo nesprávně aplikované licence. Na konci tohoto průvodce budete mít plně licencovanou instanci Aspose OCR, ať už budete soubor `.lic` uchovávat vedle svých binárek nebo jej skrýt uvnitř sestavení.  

## Co budete potřebovat  

- **Aspose.OCR for .NET** (nejnovější NuGet balíček v době psaní – 23.10)  
- **Platný licenční soubor Aspose OCR** (`Aspose.OCR.lic`)  
- Visual Studio 2022 nebo jakékoli IDE kompatibilní s C#  
- Základní znalost vkládání zdrojů v .NET (vysvětlíme to)  

Žádné další knihovny třetích stran nejsou potřeba; vše je součástí balíčku Aspose.  

![How to set license illustration](image.png "How to set license")  

## Krok 1: Nainstalujte NuGet balíček Aspose.OCR  

Než se pustíte do jakéhokoli licenčního kódu, ujistěte se, že je knihovna referencována:  

```bash
dotnet add package Aspose.OCR
```  

Nebo přes správce NuGet ve Visual Studiu vyhledejte **Aspose.OCR** a klikněte na *Install*. Tím se stáhne `Aspose.OCR.dll` a jeho závislosti.  

> **Tip:** Cílová platforma .NET 6 nebo novější vám poskytne nejnovější API a lepší výkon.  

## Krok 2: Vytvořte objekt License – jádro „Jak nastavit licenci“  

Aspose používá jednoduchou třídu `License` k aplikaci komerčního klíče. Její vytvoření je první řádek jakéhokoli licencovaného workflow:  

```csharp
using Aspose.OCR;

// Step 2: Create a License object
var ocrLicense = new License();
```  

Proč je to důležité: instance `License` načte obsah `.lic` a zaregistruje jej globálně pro aktuální AppDomain. Jakmile je zaregistrována, každý vytvořený `OcrEngine` bude fungovat v plném režimu.  

## Krok 3: Aplikujte licenci ze souboru (klasické „Jak načíst licenci“)  

Pokud dáváte přednost mít licenční soubor vedle spustitelného souboru, zavolejte `SetLicense` s cestou k souboru:  

```csharp
// Step 3: Apply the license from a file (replace with your actual path)
ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```  

### Na co si dát pozor  

- **Absolutní vs. relativní cesty:** Relativní cesty jsou řešeny vůči *pracovnímu adresáři* procesu, který je často složka bin.  
- **Oprávnění k souboru:** Účet, pod kterým aplikace běží, musí mít právo čtení souboru `.lic`.  
- **Zpracování výjimek:** `SetLicense` vyhodí `FileNotFoundException`, pokud je cesta špatná, takže ji obalte do `try/catch`, pokud potřebujete elegantní degradaci.  

## Krok 4: Jak vložit zdroj – uložení licence do vašeho sestavení  

Vložení licence eliminuje potřebu distribuovat samostatný soubor. Zde je návod, jak **vložit zdroj** do .NET projektu:  

1. Přidejte soubor `.lic` do svého projektu (např. do složky `Resources`).  
2. Klikněte pravým tlačítkem na soubor → *Properties* → nastavte **Build Action** na **Embedded Resource**.  
3. Sestavte projekt; licence se stane součástí zkompilovaného DLL.  

Nyní ji můžete získat pomocí logiky **získat vložený zdroj**.  

## Krok 5: Získání streamu vloženého zdroje  

Následující úryvek ukazuje **získání vloženého zdroje** pomocí reflexe. Přizpůsobte jmenný prostor a název zdroje tak, aby odpovídaly struktuře vašeho projektu:  

```csharp
using System.Reflection;

// Step 5: Load the embedded license stream
using var licenseStream = Assembly.GetExecutingAssembly()
                                 .GetManifestResourceStream("MyApp.Resources.Aspose.OCR.lic");

if (licenseStream == null)
{
    throw new InvalidOperationException("Embedded license not found. Check the resource name.");
}
```  

> **Proč reflexe?** `Assembly.GetExecutingAssembly()` ukazuje na aktuálně běžící sestavení, což zajišťuje, že kód funguje jak v konzolové aplikaci, webu, tak v Azure Function.  

## Krok 6: Použití streamu licence – vzor „použít stream licence“  

Jakmile máte stream, **použijte stream licence** k aplikaci licence bez zásahu do souborového systému:  

```csharp
// Step 6: Apply the license using the stream
ocrLicense.SetLicense(licenseStream);
```  

Když `SetLicense` obdrží `Stream`, Aspose načte bajty přímo, zaregistruje licenci a uvolní stream po opuštění bloku `using`. To je nejčistší způsob, jak udržet licenci skrytou.  

### Kompletní funkční příklad  

Spojením všeho dohromady zde máte samostatný program, který demonstruje všechny tři přístupy (soubor, vložený zdroj a stream). Zakomentujte části, které nepotřebujete.  

```csharp
using System;
using System.Reflection;
using Aspose.OCR;

namespace LicenseDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣  Create the License object – core of how to set license
            // -------------------------------------------------
            var ocrLicense = new License();

            // -------------------------------------------------
            // 2️⃣  Option A: Load from external .lic file (how to load license)
            // -------------------------------------------------
            // Replace with your actual path or use a relative path.
            // ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

            // -------------------------------------------------
            // 3️⃣  Option B: Load from an embedded resource (how to embed resource)
            // -------------------------------------------------
            // Ensure the .lic file is added as an Embedded Resource.
            // string resourceName = "LicenseDemo.Resources.Aspose.OCR.lic";
            // using var licenseStream = Assembly.GetExecutingAssembly()
            //                                   .GetManifestResourceStream(resourceName);
            // if (licenseStream == null)
            // {
            //     Console.WriteLine("Embedded license not found.");
            //     return;
            // }
            // ocrLicense.SetLicense(licenseStream); // use license stream

            // -------------------------------------------------
            // 4️⃣  Verify the license – no exception means success
            // -------------------------------------------------
            Console.WriteLine("License applied successfully!");

            // -------------------------------------------------
            // 5️⃣  Run a quick OCR test to prove it works
            // -------------------------------------------------
            var engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample.png"); // replace with your image
            engine.Recognize();

            Console.WriteLine("Recognized text:");
            Console.WriteLine(engine.Text);
        }
    }
}
```  

**Očekávaný výstup**  

```
License applied successfully!
Recognized text:
[Your OCR result here]
```  

Pokud licence není aplikována, Aspose vyhodí `LicenseException` nebo uvidíte v OCR výsledcích vodoznak zkušební verze.  

## Časté úskalí a jak se jim vyhnout  

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Banner „Evaluation version“ se stále zobrazuje | Licence není načtena nebo je špatná cesta | Zkontrolujte znovu cestu k souboru nebo název vloženého zdroje. |
| `NullReferenceException` při volání `GetManifestResourceStream` | Chybný název zdroje nebo Build Action není nastaven na Embedded Resource | Ověřte název včetně jmenného prostoru a nastavte Build Action správně. |
| Licence funguje lokálně, ale selže po nasazení | Chybějící oprávnění ke čtení na serveru | Udělejte identitě aplikačního poolu oprávnění ke čtení souboru `.lic`, nebo vložte licenci, aby se předešlo problémům se souborovým systémem. |
| Více objektů `License` nemá žádný efekt | Volali jste `SetLicense` na *jiné* instanci po první | Udržujte jedinou instanci `License` na AppDomain; znovu ji použijte nebo zavolejte `SetLicense` jednou při startu. |

## Kdy zvolit který přístup  

- **Na souboru založený** – Rychlé prototypování, snadná výměna bez nutnosti přebudování.  
- **Vložený zdroj** – Ideální pro desktopové aplikace nebo distribuci knihoven, kde nechcete, aby licence „plavala“ kolem.  
- **Na streamu založený** – Perfektní pro cloudová prostředí (Azure Functions, AWS Lambda), kde můžete licenci načíst ze zabezpečeného úložiště a předat ji přímo.  

## Další kroky – rozšíření znalostí o licencování  

Nyní, když ovládáte **jak nastavit licenci**, můžete chtít prozkoumat:  

- **Jak vložit zdroj** v složitějších řešeních s více projekty.  
- **Získat vložený zdroj** ze satelitních sestavení pro scénáře lokalizace.  
- **Jak načíst licenci** dynamicky z Azure Key Vault nebo AWS Secrets Manager.  
- **Použít stream licence** společně s dependency injection pro čistší startovací kód.  

Každé z těchto témat staví na základech zde popsaných a pomáhá vám udržet licenční strategii bezpečnou a udržovatelnou.  

---  

### TL;DR  

Ukázali jsme vám **jak nastavit licenci** v Aspose OCR pomocí tří spolehlivých technik: načtení ze souboru, vložení `.lic` jako zdroje a aplikaci pomocí streamu. Dodržujte kód, berte v úvahu úskalí a váš OCR engine poběží na plný výkon – žádné zkušební vodoznaky, žádná překvapení.  

Šťastné programování a ať jsou vaše OCR výsledky krystalicky čisté!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}