---
description: Lär dig hur du anger tillåtna tecken för OCR med Aspose.OCR för .NET
  och känner igen siffror i bilder effektivt. Följ en steg‑för‑steg‑guide för att
  begränsa OCR till endast siffror.
linktitle: Specify Allowed Characters OCR – Using Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: Ange tillåtna tecken OCR – Använd Aspose.OCR för .NET
url: /sv/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ange tillåtna tecken OCR – Använd Aspose.OCR för .NET

I den här handledningen kommer du att lära dig hur du **specify allowed characters ocr** med Aspose.OCR för .NET, vilket gör att du kan begränsa OCR-utdata till endast de tecken du behöver. Detta är särskilt praktiskt när du behöver **recognize digits image** filer såsom serienummer, faktura‑ID eller streckkodsliknande strängar. Vi går igenom installationen, koden och ett par praktiska scenarier så att du kan tillämpa tekniken direkt.

## Snabba svar
- **What does “specify allowed characters ocr” do?** Den begränsar OCR till en fördefinierad uppsättning tecken, vilket förbättrar noggrannheten för måldata.  
- **Which characters can I allow?** Vilken kombination du behöver—siffror, bokstäver eller anpassade symboler (t.ex. “0123456789”).  
- **Why limit characters?** Minskar falska igenkänningar och snabbar upp bearbetningen när den förväntade teckenuppsättningen är känd.  
- **Do I need a license?** En gratis provversion fungerar för utveckling; en kommersiell licens krävs för produktion.  
- **Which .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Vad är “specify allowed characters ocr”?
När OCR skannar en bild försöker den matcha varje visuellt mönster mot hela alfabetet av möjliga tecken. Genom att **specify allowed characters ocr** talar du om för motorn att ignorera allt som ligger utanför din vitlista, vilket dramatiskt förbättrar igenkänningsnoggrannheten för begränsade datamängder.

## Varför använda Aspose.OCR för att känna igen digits image?
Aspose.OCR erbjuder ett rent, flytande API för .NET‑utvecklare. Dess inbyggda `AllowedCharacters`‑alternativ låter dig fokusera på scenarier som bara innehåller siffror utan att skriva anpassad efterbehandlingslogik. Detta är perfekt för:
- Läsning av mätaravläsningar, fakturanummer eller produktkoder.  
- Validering av användarinmatade data som fångats från skannade formulär.  
- Påskyndande av batch‑bearbetning där teckenuppsättningen är känd i förväg.

## Förutsättningar

Innan du dyker ner i koden, se till att du har:

- En fungerande kunskap om .NET‑utveckling.  
- **Aspose.OCR for .NET**‑biblioteket. Du kan ladda ner det [here](https://releases.aspose.com/ocr/net/).  
- Visual Studio (eller någon annan föredragen .NET‑IDE).  

## Importera namnrymder

I ditt .NET‑projekt importerar du de nödvändiga namnrymderna för att utnyttja Aspose.OCR‑funktionaliteten:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Låt oss nu dela upp handledningen i en serie omfattande steg:

## Så här anger du tillåtna tecken OCR – Steg‑för‑steg‑guide

### Steg 1: Ange sökvägen till din bildmapp

Först, definiera var dina exempelbilder lagras.

```csharp
string dataDir = "Your Document Directory";
```

### Steg 2: Initiera Aspose.OCR med en vitlista som bara innehåller siffror

Skapa en `AsposeOcr`‑instans och skicka de tecken du vill tillåta—i detta fall alla siffror.

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### Steg 3: Känn igen en enskild rad som innehåller siffror

Använd metoden `RecognizeLine` för att extrahera texten från en bild som bara innehåller siffror.

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### Steg 4: Skriv ut de igenkända siffrorna

Skriv ut resultatet till konsolen så att du kan verifiera utdata.

```csharp
Console.WriteLine(result);
```

### Steg 5: Använd RecognitionSettings för mer kontroll

Om du behöver finare kontroll—t.ex. tvinga enradig igenkänning—kan du använda överlagringen som accepterar `RecognitionSettings`.

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

### Steg 6: Visa resultatet för det andra fallet

```csharp
Console.WriteLine(result2.RecognitionText);
```

### Steg 7: Bekräfta lyckad körning

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Genom att följa dessa steg har du lärt dig hur du **specify allowed characters ocr** och effektivt **recognize digits image** innehåll med Aspose.OCR för .NET.

## Vanliga fallgropar och felsökning

- **Empty result:** Se till att bildkvaliteten är tillräcklig (klar kontrast, minimal brus).  
- **Wrong characters returned:** Dubbelkolla att vitlistesträngen exakt matchar de tecken du förväntar dig.  
- **File not found:** Verifiera att `dataDir` pekar på rätt mapp och att filnamnet matchar skiftlägeskänsligt.

## Vanliga frågor

### Q1: Är Aspose.OCR för .NET lämplig för både nybörjare och erfarna utvecklare?  
**A:** Absolut! API:et är designat för att vara intuitivt för nybörjare samtidigt som det erbjuder avancerade alternativ för erfarna användare.

### Q2: Kan jag använda Aspose.OCR för .NET för att känna igen tecken på flera språk?  
**A:** Ja, Aspose.OCR stödjer ett brett spektrum av språk. Du kan kombinera språkpaket med funktionen för tillåtna tecken för flerspråkiga scenarier.

### Q3: Hur ofta uppdateras Aspose.OCR för .NET?  
**A:** Uppdateringar släpps regelbundet för att lägga till nya funktioner, förbättra noggrannheten och säkerställa kompatibilitet. Kontrollera [documentation](https://reference.aspose.com/ocr/net/) för detaljer om den senaste versionen.

### Q4: Finns det en gratis provversion av Aspose.OCR för .NET?  
**A:** Ja, du kan utforska funktionerna genom att ladda ner [free trial](https://releases.aspose.com/).

### Q5: Var kan jag söka hjälp eller ansluta till communityn för support?  
**A:** Besök [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) för att ställa frågor, dela erfarenheter och få hjälp från både Aspose‑ingenjörer och andra utvecklare.

---

**Senast uppdaterad:** 2026-02-15  
**Testad med:** Aspose.OCR 24.11 för .NET  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}