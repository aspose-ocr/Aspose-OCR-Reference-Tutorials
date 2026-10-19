---
category: general
date: 2026-04-11
description: Leer hoe je OCR in Aspose OCR voor C# kunt uitschakelen om offline te
  werken, tekst uit een afbeelding kunt extraheren zonder internet, en de afbeelding
  correct kunt laden voor OCR.
draft: false
keywords:
- how to disable OCR
- extract text from image
- load image for OCR
- offline OCR C#
- Aspose OCR resources
language: nl
og_description: Hoe OCR in Aspose OCR voor C# uit te schakelen en offline uit te voeren,
  tekst uit een afbeelding te extraheren zonder internet, en afbeelding gemakkelijk
  voor OCR te laden.
og_title: Hoe OCR uitschakelen in C# – Offline Aspose OCR-gids
tags:
- C#
- OCR
- Aspose
- Offline Processing
title: Hoe OCR uitschakelen in C# – Offline Aspose OCR-gids
url: /nl/net/ocr-configuration/how-to-disable-ocr-in-c-offline-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te schakelen in C# – Offline Aspose OCR-gids

Heb je je ooit afgevraagd **hoe je OCR kunt uitschakelen** wanneer je een echt offline oplossing nodig hebt? Misschien bouw je een beveiligde desktopapp die niet op een netwerkverbinding kan vertrouwen, of wil je gewoon onverwachte downloads vermijden. Hoe dan ook, het goede nieuws is dat Aspose OCR je toestaat om het automatische ophalen van bronnen uit te schakelen, het naar een lokale map te wijzen, en alles on‑premises te houden. In deze tutorial zie je ook hoe je **tekst uit afbeelding kunt extraheren** en correct **afbeelding voor OCR laden** zonder problemen.

We lopen een compleet, kant‑klaar voorbeeld door dat elke stap toont — van het initialiseren van de engine tot het afdrukken van de herkende Japanse tekst. Geen externe documentatie, geen verborgen magie; gewoon platte C# code die je vandaag in je project kunt plaatsen. Aan het einde weet je waarom het uitschakelen van de auto‑downloadfunctie belangrijk is, hoe je het resources‑pad instelt, en op welke valkuilen je moet letten.

## Vereisten

- .NET 6.0 (of een recente .NET‑versie) geïnstalleerd op je machine.  
- Aspose.OCR for .NET NuGet‑pakket (`Install-Package Aspose.OCR`).  
- Een map die al de taalresources bevat die je nodig hebt (bijv. het Japanse model).  
- Een afbeeldingsbestand (`japan_doc.png`) waar je OCR op wilt uitvoeren.  

Als je de taalpakketten mist, haal ze dan één keer op van het Aspose‑portaal, pak ze uit in een map zoals `AsposeOCRResources`, en je bent klaar. Er zullen geen verdere downloads plaatsvinden zodra je de auto‑downloadfunctie hebt uitgeschakeld.

![How to disable OCR offline](/images/how-to-disable-ocr.png "how to disable OCR illustration")

## Stap 1 – Maak een OCR‑engine‑instantie  

Het eerste wat je doet is `OcrEngine` instantieren. Beschouw dit object als het brein dat je afbeelding zal lezen.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Waarom dit belangrijk is:** Zonder een engine kun je niets configureren. Het object bevat alle instellingen, inclusief de cruciale vlag die de bibliotheek vertelt of hij contact met het internet mag opnemen.

## Stap 2 – Schakel automatisch resource‑download uit  

Standaard probeert Aspose OCR ontbrekende taalbestaanden on‑the‑fly op te halen. Om alles offline te houden, zet je de `AutoDownloadResources`‑schakelaar op `false`.

```csharp
        // Step 2: Disable automatic resource download to work offline
        ocrEngine.Settings.AutoDownloadResources = false;
```

> **Pro‑tip:** Dit uitschakelen garandeert niet alleen privacy, maar versnelt ook de eerste herkenningsrun omdat de engine geen tijd meer verspilt aan het controleren op updates.

## Stap 3 – Verwijs naar je lokale resources‑map  

Vertel nu de engine waar de vooraf‑gedownloade taalpakketten zich bevinden. Dit is het pad dat je in de vereisten hebt opgezet.

```csharp
        // Step 3: Point the engine to the folder containing pre‑downloaded resources
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";
```

> **Wat kan er misgaan?** Als het pad onjuist is of het vereiste taalb bestand ontbreekt, zal de engine een `ResourceNotFoundException` werpen. Controleer de mapnaam zorgvuldig en zorg dat het Japanse model (`jpn.traineddata`) aanwezig is.

## Stap 4 – Selecteer het lokale taalmodel  

Kies de taal die je daadwerkelijk op schijf hebt. In ons voorbeeld gebruiken we Japans, maar je kunt `Language.Japanese` vervangen door elke andere taal die je hebt gedownload.

```csharp
        // Step 4: Select the language model that is available locally
        ocrEngine.Settings.Language = Language.Japanese;
```

> **Randgeval:** Sommige talen vereisen extra woordenboeken (bijv. Chinees). Zorg ervoor dat die aanvullende bestanden ook in dezelfde resources‑map staan.

## Stap 5 – Laad de afbeelding voor OCR  

Hier **laden we de afbeelding voor OCR**. De `ImageStream.FromFile`‑methode leest het bestand in een stream die Aspose kan verwerken.

```csharp
        // Step 5: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/japan_doc.png");
```

> **Tip:** Ondersteunde formaten zijn PNG, JPEG, BMP en TIFF. Als je PDF’s moet verwerken, converteer je elke pagina eerst naar een afbeelding.

## Stap 6 – Voer het herkenningsproces uit  

Nu leest de engine daadwerkelijk de pixels en probeert ze om te zetten in tekst.

```csharp
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Waarom deze stap traag kan zijn:** OCR is CPU‑intensief, vooral voor hoge‑resolutie‑afbeeldingen. Als prestaties een zorg zijn, overweeg dan de afbeelding te verkleinen vóór herkenning.

## Stap 7 – Geef de geëxtraheerde tekst weer  

Tot slot **extraheren we tekst uit afbeelding** en printen we deze naar de console.

```csharp
        // Step 7: Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Het uitvoeren van het programma moet de Japanse tekens weergeven die in `japan_doc.png` stonden. Als alles correct is ingesteld, zie je een nette blok Unicode‑tekst in je console.

### Verwachte uitvoer

```
これはサンプルの日本語テキストです。
```

(De daadwerkelijke uitvoer hangt af van de inhoud van de afbeelding.)

## Veelvoorkomende valkuilen & hoe ze te vermijden  

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Ontbrekend taalbestand** | `AutoDownloadResources` is false, dus kan de engine het niet ophalen. | Controleer of `ResourcesPath` naar de map wijst die `jpn.traineddata` bevat. |
| **Onjuist afbeeldingspad** | `ImageStream.FromFile` werpt een `FileNotFoundException`. | Gebruik absolute paden of zorg dat de werkmap correct is ingesteld. |
| **Niet‑ondersteund afbeeldingsformaat** | Aspose leest alleen bepaalde formaten. | Converteer je afbeelding naar PNG of JPEG voordat je `FromFile` aanroept. |
| **Onvoldoende geheugen bij grote afbeeldingen** | OCR laadt de volledige afbeelding in het geheugen. | Verklein of deel de afbeelding op, of vergroot de geheugengrens van het proces. |

## Voorbeeld uitbreiden  

- **Batchverwerking:** Loop over een map met afbeeldingen, roep dezelfde herkenningscode aan, en schrijf elk resultaat naar een apart `.txt`‑bestand.  
- **Verschillende talen:** Vervang `Language.Japanese` door `Language.English` (of een andere) nadat je de bijbehorende resource‑bestanden hebt geplaatst.  
- **Aangepaste preprocessing:** Gebruik Aspose.Imaging om te deskewen of het contrast te verbeteren vóór OCR voor betere nauwkeurigheid.

## Conclusie  

Je weet nu **hoe je OCR kunt uitschakelen** in Aspose OCR voor C# en het volledig offline kunt uitvoeren. Door `AutoDownloadResources` op `false` te zetten, de engine naar een lokale resources‑map te wijzen, en correct **afbeelding voor OCR laden**, kun je betrouwbaar **tekst uit afbeelding extraheren** zonder ooit het internet aan te raken. Deze aanpak is ideaal voor beveiligde omgevingen, CI‑pipelines, of elke situatie waarin netwerktoegang beperkt is.

Klaar voor de volgende stap? Probeer een volledige map met gescande PDF’s te verwerken, experimenteer met verschillende taalpakketten, of integreer het OCR‑resultaat in een doorzoekbare database. De offline configuratie die je vandaag hebt gebouwd, vormt een solide basis voor elke on‑premises document‑verwerkingsworkflow.

Veel plezier met coderen, en voel je vrij om een reactie achter te laten als je ergens tegenaan loopt!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}