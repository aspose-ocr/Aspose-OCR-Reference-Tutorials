---
category: general
date: 2026-06-22
description: Voer OCR uit op een afbeelding met Aspose.OCR in C#. Leer tekst uit een
  PNG te extraheren, afbeelding naar tekst te converteren en tekst uit een PNG te
  herkennen, inclusief de Russische taal.
draft: false
keywords:
- perform ocr on image
- extract text from png
- convert image to text
- recognize text from png
- read russian text
language: nl
og_description: Voer OCR uit op een afbeelding in C# met Aspose.OCR. Deze gids laat
  zien hoe je tekst uit een PNG kunt extraheren, een afbeelding naar tekst kunt converteren
  en Russische tekst efficiënt kunt lezen.
og_title: Voer OCR uit op afbeelding met Aspose.OCR – C#‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Aspose.OCR in C#. Learn to extract text
    from png, convert image to text, and recognize text from png including Russian
    language.
  headline: Perform OCR on Image with Aspose.OCR – Complete C# Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Voer OCR uit op afbeelding met Aspose.OCR – Complete C#-gids
url: /nl/net/text-recognition/perform-ocr-on-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR op afbeelding uitvoeren met Aspose.OCR – Complete C# gids

Heb je je ooit afgevraagd hoe je **OCR op afbeelding** kunt uitvoeren zonder uren te zoeken naar de juiste bibliotheek? Naar mijn ervaring maakt Aspose.OCR het hele proces een makkie, vooral wanneer je **tekst uit png**‑bestanden in het Cyrillisch moet **extraheren**.  

In deze tutorial lopen we een praktijkvoorbeeld door dat niet alleen **afbeelding naar tekst converteren** laat zien, maar ook hoe je **tekst uit png** kunt **herkennen** en **Russische tekst lezen** betrouwbaar. Aan het einde heb je een kant‑klaar console‑appje dat het OCR‑resultaat direct naar de console print.

---

![OCR op afbeelding workflow diagram](image-placeholder.png "OCR op afbeelding workflow diagram")

## OCR op afbeelding uitvoeren – Stapsgewijze implementatie

Hieronder staat de volledige, uitvoerbare code. Voel je vrij om deze te kopiëren en plakken in een nieuw console‑project, druk op F5, en zie de magie gebeuren.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load your Aspose.OCR license (if you have one)
        var license = new License();
        // license.SetLicense("Aspose.OCR.lic");   // uncomment and provide the path to your license file

        // Step 2: Create an OCR engine (CPU mode is the default)
        var ocrEngine = new OcrEngine();

        // Step 3: Specify the language to recognize – Russian (Cyrillic)
        ocrEngine.Language = OcrLanguage.Russian;

        // Step 4: (Optional) Set a download timeout for language resources, in seconds
        ocrEngine.ResourceDownloadTimeout = 120;

        // Step 5: Perform OCR on the image file
        var ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/sample_russian.png");

        // Step 6: Output the recognized plain‑text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

Het uitvoeren van het programma geeft iets als output:

```
Привет, мир!
Это тестовое изображение.
```

Die output bewijst dat we succesvol **OCR op afbeelding uitvoeren** en **Russische tekst lezen** in één stap.

---

## Tekst uit PNG extraheren – Het bestand laden

Voordat de engine zijn werk kan doen, heeft hij een bitmap nodig om mee te werken. De `RecognizeImage`‑methode accepteert een pad naar elk ondersteund rasterformaat, PNG is het meest gangbaar voor verliesvrije screenshots.  

> **Waarom PNG?** Omdat het elk pixel behoudt, wat betekent dat de OCR‑engine exact dezelfde gegevens ziet als je hebt vastgelegd—geen compressie‑artefacten die de herkenner in de war brengen.

Als je een JPEG of BMP gebruikt, werkt dezelfde aanroep; vervang alleen de bestandsextensie. Het belangrijke is dat het bestand bestaat en dat je app leesrechten heeft.

---

## Afbeelding naar tekst converteren – De inhoud herkennen

Het hart van de tutorial is stap 5, waar we **afbeelding naar tekst converteren**. In de achtergrond laadt Aspose.OCR de afbeelding, voert deze door een neuraal netwerk getraind op Cyrillische glyphs, en retourneert een platte‑tekst‑string.  

* **Tip:** Als je onduidelijke tekens ziet, verhoog dan `ResourceDownloadTimeout` of download het taalpakket vooraf om netwerkonderbrekingen te vermijden.  
* **Tip:** Voor multi‑page PDF's zou je over elke pagina‑afbeelding itereren en de resultaten samenvoegen—nog steeds dezelfde **OCR op afbeelding uitvoeren**‑aanroep per pagina.

---

## Russische tekst lezen – De taal instellen

Je vraagt je misschien af: “Moet ik Russisch handmatig specificeren?” Het korte antwoord: **ja**, als je optimale nauwkeurigheid wilt. Door `ocrEngine.Language = OcrLanguage.Russian;` toe te wijzen, vertellen we de engine het Cyrillische teken‑ en taalmodel te laden.  

Als je deze stap overslaat, valt de engine terug op Engels, en zullen je Russische tekens veranderen in vraagtekens of onzin. Stel daarom altijd **Russische tekst lezen** in door expliciet de taal te zetten.

---

## Tekst uit PNG herkennen – Time‑outs en resources afhandelen

Netwerk‑latentie kan je verrassen wanneer de OCR‑engine voor de eerste keer taalresources moet ophalen. De eigenschap `ResourceDownloadTimeout` (stap 4) biedt een veiligheidsnet.  

* **Wanneer aanpassen:** Als je op een trage bedrijfs‑VPN zit, verhoog de timeout naar 180 seconden.  
* **Wanneer niet aanpassen:** Voor lokale, vooraf geïnstalleerde taalpakketten is de standaard van 120 seconden ruim voldoende.

---

## Tekst uit PNG extraheren – Licentiebeheer (optioneel)

Aspose.OCR werkt direct uit de doos in de proefmodus, maar een licentie verwijdert watermerken en ontgrendelt de volledige API. Om **OCR op afbeelding uitvoeren** zonder beperkingen, verwijder de commentaartekens van de licentielijn en wijs deze naar je `.lic`‑bestand.  

```csharp
var license = new License();
license.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

---

## Afbeelding naar tekst converteren – Volledige projectchecklist

| ✅ | Item |
|---|------|
| 1 | Installeer **Aspose.OCR** via NuGet (`Install-Package Aspose.OCR`) |
| 2 | Voeg `using Aspose.OCR;` en `using Aspose.OCR.Models;` toe |
| 3 | (Optioneel) Pas je licentie toe |
| 4 | Maak een `OcrEngine`‑instance aan |
| 5 | Stel `Language = OcrLanguage.Russian` in om **Russische tekst te lezen** |
| 6 | Pas `ResourceDownloadTimeout` aan indien nodig |
| 7 | Roep `RecognizeImage(@"path\to\file.png")` aan om **OCR op afbeelding uit te voeren** |
| 8 | Print `ocrResult.Text` – je hebt zojuist **tekst uit png geëxtraheerd**! |

---

## Veelgestelde vragen & randgevallen

**Wat als mijn PNG zowel Engels als Russisch bevat?**  
Je kunt `ocrEngine.Language = OcrLanguage.Multilingual;` instellen, waardoor een gecombineerd model wordt geladen. De engine zal nog steeds **tekst uit png herkennen** nauwkeurig, maar de bestandsgrootte van het taalpakket wordt iets groter.

**Kan ik een map met afbeeldingen verwerken?**  
Zeker. Plaats de `RecognizeImage`‑aanroep in een `foreach (var file in Directory.GetFiles(folder, "*.png"))`‑lus. Elke iteratie **voert OCR op afbeelding uit** en je kunt de resultaten naar een `.txt`‑bestand schrijven.

**Wat te doen met lage‑resolutie afbeeldingen?**  
De OCR‑kwaliteit daalt onder 72 dpi. Als je een onscherpe screenshot hebt, overweeg dan om deze op te schalen met een grafische bibliotheek voordat je deze aan Aspose.OCR doorgeeft. De bibliotheek zelf zal de pixelkwaliteit niet magisch verbeteren.

---

## Pro‑tips voor productie‑klare OCR

* **Resultaten cachen:** Sla de platte tekst op in een database om OCR niet opnieuw uit te voeren op ongewijzigde bestanden.  
* **Uitvoer valideren:** Gebruik een eenvoudige regex om te detecteren of het resultaat leeg is—zo ja, probeer opnieuw met een hogere timeout.  
* **Paralleliseren:** Voor bulkverwerking, start meerdere `OcrEngine`‑instances op aparte threads; Aspose.OCR is thread‑veilig zolang elke thread zijn eigen engine heeft.

---

## Conclusie

We hebben zojuist **OCR op afbeelding uitgevoerd** op bestanden met Aspose.OCR, laten zien hoe je **tekst uit png kunt extraheren**, **afbeelding naar tekst kunt converteren**, en **tekst uit png kunt herkennen** terwijl je **Russische tekst leest** zonder fouten. De volledige oplossing past in één `Main`‑methode, maar schaalt naar enterprisescenario's met een paar aanpassingen.

Klaar voor de volgende uitdaging? Probeer beeld‑preprocessing (kantlijncorrectie, ruisverwijdering) toe te voegen met een bibliotheek zoals **ImageSharp**, of experimenteer met het exporteren van het OCR‑resultaat naar JSON voor downstream‑analyse. De mogelijkheden zijn eindeloos als je de basisprincipes van OCR in C# onder de knie hebt.

Veel plezier met coderen, en moge je afbeeldingen altijd leesbaar zijn!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Afbeeldingstekst extraheren C# met taalkeuze met Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [tekst uit afbeelding herkennen met Aspose OCR voor meerdere talen](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Afbeelding naar tekst converteren – OCR op afbeelding uitvoeren vanaf URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}