---
category: general
date: 2026-04-06
description: Hur du ställer in licens i Aspose OCR med C# – lär dig hur du bäddar
  in en resurs, hämtar den inbäddade resursen och laddar licensen från en fil eller
  ström på bara några steg.
draft: false
keywords:
- how to set license
- how to embed resource
- get embedded resource
- how to load license
- use license stream
language: sv
og_description: Hur du ställer in licensen i Aspose OCR förklaras steg för steg. Lär
  dig hur du bäddar in licensen, hämtar den och använder ett licensflöde för sömlös
  integration.
og_title: Hur man ställer in licens i Aspose OCR – Komplett C#‑guide
tags:
- Aspose OCR
- C#
- .NET licensing
title: Hur man ställer in licens i Aspose OCR – Komplett C#‑guide
url: /sv/net/ocr-configuration/how-to-set-license-in-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man anger licens i Aspose OCR – Komplett C#-guide

Att ange licens i Aspose OCR är ett vanligt hinder för utvecklare. I den här handledningen går vi igenom de exakta stegen för att ange licensen, bädda in den som en resurs och ladda den från en ström—så att du kan börja OCR:a utan den irriterande vattenstämpeln i provläget.

Har du någonsin försökt köra ett OCR-jobb bara för att se en “Evaluation version”-banner? Det är symtomet på en saknad eller felaktigt tillämpad licens. I slutet av den här guiden har du en fullt licensierad Aspose OCR-instans, oavsett om du har `.lic`-filen sida‑vid‑sida med dina binärer eller gömmer den i ditt assembly.

## Vad du behöver

- **Aspose.OCR for .NET** (senaste NuGet‑paketet vid skrivande – 23.10)
- En **giltig Aspose OCR-licensfil** (`Aspose.OCR.lic`)
- Visual Studio 2022 eller någon C#‑kompatibel IDE
- Grundläggande kunskap om .NET-resursinbäddning (vi kommer att gå igenom det)

Inga extra tredjepartsbibliotek krävs; allt finns i Aspose‑paketet.

![Illustration för hur man anger licens](image.png "Hur man anger licens")

## Steg 1: Installera Aspose.OCR NuGet‑paketet

Innan du kan röra någon licenskod, se till att biblioteket är refererat:

```bash
dotnet add package Aspose.OCR
```

Eller, via Visual Studios NuGet‑hanterare, sök efter **Aspose.OCR** och klicka på *Install*. Detta hämtar `Aspose.OCR.dll` och dess beroenden.

> **Proffstips:** Sikta på .NET 6 eller senare för att få den senaste API‑ytan och bättre prestanda.

## Steg 2: Skapa ett License‑objekt – Kärnan i “Hur man anger licens”

Aspose använder en enkel `License`‑klass för att tillämpa den kommersiella nyckeln. Att instansiera den är den första raden i alla licensierade arbetsflöden:

```csharp
using Aspose.OCR;

// Step 2: Create a License object
var ocrLicense = new License();
```

Varför detta är viktigt: `License`‑instansen läser innehållet i `.lic`‑filen och registrerar den globalt för den aktuella AppDomain. När den är registrerad kommer varje `OcrEngine` du skapar att köras i full‑funktionellt läge.

## Steg 3: Tillämpa licensen från en fil (klassisk “Hur man laddar licens”)

Om du föredrar att ha licensfilen bredvid din körbara fil, anropa `SetLicense` med filsökvägen:

```csharp
// Step 3: Apply the license from a file (replace with your actual path)
ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

### Saker att hålla utkik efter

- **Absoluta vs. relativa sökvägar:** Relativa sökvägar löses mot *arbetskatalogen* för processen, vilket ofta är bin‑mappen.
- **Filbehörigheter:** Kontot som kör appen måste ha läsrättighet till `.lic`‑filen.
- **Undantagshantering:** `SetLicense` kastar `FileNotFoundException` om sökvägen är fel, så omslut det i ett `try/catch` om du behöver en mjuk nedtrappning.

## Steg 4: Hur man bäddar in resurs – Lagrar licensen i ditt assembly

Att bädda in licensen eliminerar behovet av att skicka en separat fil. Så här **bäddar du in resurs** i ett .NET‑projekt:

1. Lägg till `.lic`‑filen i ditt projekt (t.ex. under en mapp som heter `Resources`).
2. Högerklicka på filen → *Properties* → sätt **Build Action** till **Embedded Resource**.
3. Bygg projektet; licensen blir en del av den kompilerade DLL‑en.

Nu kan du hämta den med logik för **get embedded resource**.

## Steg 5: Hämta inbäddad resursström

Följande kodsnutt demonstrerar **get embedded resource** med hjälp av reflection. Justera namnrymden och resursnamnet så att de matchar din projektstruktur:

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

> **Varför reflection?** `Assembly.GetExecutingAssembly()` pekar på den för närvarande körande assemblyn, vilket säkerställer att koden fungerar oavsett om du är i en konsolapp, webbplats eller Azure Function.

## Steg 6: Använd licensström – Mönstret “use license stream”

Nu när du har strömmen, **use license stream** för att tillämpa licensen utan att röra filsystemet:

```csharp
// Step 6: Apply the license using the stream
ocrLicense.SetLicense(licenseStream);
```

När `SetLicense` får en `Stream` läser Aspose bytes direkt, registrerar licensen och frigör strömmen när du lämnar `using`‑blocket. Detta är det renaste sättet att hålla licensen dold.

### Fullt fungerande exempel

När vi sätter ihop allt, här är ett självständigt program som demonstrerar alla tre tillvägagångssätt (fil, inbäddad resurs och ström). Kommentera bort de sektioner du inte behöver.

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

**Förväntad output**

```
License applied successfully!
Recognized text:
[Your OCR result here]
```

Om licensen inte tillämpas kastar Aspose ett `LicenseException` eller så ser du utvärderingsvattenstämpeln i OCR‑resultaten.

## Vanliga fallgropar & hur man undviker dem

| Symptom | Trolig orsak | Lösning |
|---------|--------------|-----|
| “Evaluation version”-banner visas fortfarande | Licensen är inte laddad eller sökvägen fel | Dubbelkolla filsökvägen eller det inbäddade resursnamnet. |
| `NullReferenceException` på `GetManifestResourceStream` | Resursnamn stavfel eller Build Action inte satt till Embedded Resource | Verifiera det namnrymd‑kvalificerade namnet och sätt Build Action korrekt. |
| Licensen fungerar lokalt men misslyckas efter distribution | Saknade läsrättigheter på servern | Ge app‑pool‑identiteten läsrättighet till `.lic`‑filen, eller bädda in licensen för att undvika filsystemproblem. |
| Flera `License`‑objekt har ingen effekt | Du anropade `SetLicense` på en *annan* instans efter den första | Behåll en enda `License`‑instans per AppDomain; återanvänd den eller anropa `SetLicense` en gång vid start. |

## När man ska välja varje tillvägagångssätt

- **Fil‑baserad** – Snabb prototypning, lätt att ersätta utan ombyggnad.
- **Inbäddad resurs** – Idealisk för skrivbords‑ eller bibliotekdistribution där du inte vill att licensen ska sväva omkring.
- **Ström‑baserad** – Perfekt för molnmiljöer (Azure Functions, AWS Lambda) där du kan hämta licensen från ett säkert valv och mata in den direkt.

## Nästa steg – Utöka din licenskunskap

Nu när du har bemästrat **how to set license**, kanske du vill utforska:

- **How to embed resource** i mer komplexa multi‑projekt‑lösningar.
- **Get embedded resource** från satellit‑assemblys för lokalanpassningsscenarier.
- **How to load license** dynamiskt från Azure Key Vault eller AWS Secrets Manager.
- **Use license stream** tillsammans med dependency injection för renare startkod.

Var och en av dessa ämnen bygger på grunderna som täcks här och hjälper dig att hålla din licensstrategi både säker och underhållbar.

---

### TL;DR

Vi har visat dig **how to set license** i Aspose OCR med tre pålitliga tekniker: laddning från en fil, inbäddning av `.lic` som en resurs och tillämpning via en ström. Följ koden, respektera fallgroparna, så kommer din OCR‑motor att köra på full hastighet—utan provvattenstämplar, utan överraskningar.

Lycka till med kodningen, och må dina OCR‑resultat vara kristallklara!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}