---
category: general
date: 2026-04-26
description: Extrayez le texte d’une image en C# avec Aspose.OCR et apprenez à convertir
  l’image aux formats JSON et XML en quelques minutes.
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: fr
og_description: Extraire du texte d’une image en C# avec Aspose.OCR. Apprenez étape
  par étape comment convertir le résultat en JSON et XML instantanément.
og_title: Extraire du texte d’une image en C# – Convertir en JSON et XML
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: Extraire du texte d’une image en C# – Convertir en JSON et XML
url: /fr/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image en C# – Convertir en JSON & XML

Vous avez déjà eu besoin d'**extraire du texte d'une image** dans un projet .NET mais vous êtes resté bloqué sur la question « comment récupérer réellement les données ? ». Vous n'êtes pas seul. Dans de nombreuses applications réelles — pensez au traitement de factures, à la numérisation de reçus ou à la vérification de badges — extraire les caractères bruts d'une image est la première étape cruciale.  

Bonne nouvelle ? Avec Aspose.OCR, vous pouvez le faire en quelques lignes, puis convertir instantanément **l'image en JSON** ou **l'image en XML** pour les systèmes en aval. Dans ce guide, nous parcourrons le code complet, prêt à l'exécution, expliquerons pourquoi chaque partie est importante et vous montrerons quelques astuces pour éviter les pièges courants.

---

## Ce dont vous avez besoin

- **.NET 6+** (tout SDK récent fonctionne ; l'exemple cible .NET 6)
- **Aspose.OCR for .NET** NuGet package  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Un fichier image (PNG, JPG, etc.) contenant du texte imprimable ; nous utiliserons `invoice.png` comme exemple.
- Un éditeur de code — Visual Studio, VS Code ou Rider — selon votre préférence.

C’est tout. Aucun moteur OCR supplémentaire, aucun service externe, juste un seul package NuGet.

---

## Étape 1 : Configurer le moteur OCR – Comment extraire du texte d'une image

Tout d'abord, nous créons une instance `OcrEngine` et la pointons vers le fichier image. Cette étape est la base ; sans une image correctement chargée, le moteur ne peut rien reconnaître.

```csharp
using Aspose.OCR;
using System.IO;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process
// Replace YOUR_DIRECTORY with the actual folder path
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");

// Optional: verify the image was loaded
if (ocrEngine.Image == null)
{
    throw new FileNotFoundException("Image not found. Check the path and filename.");
}
```

**Pourquoi c’est important :**  
- `OcrEngine` encapsule tout le prétraitement d'image de bas niveau (binarisation, redressement).  
- Le chargement de l'image via `ImageStream.FromFile` garantit que le moteur lit les octets exacts, préservant le DPI et la profondeur de couleur — tous deux pouvant affecter la précision de la reconnaissance.  

> **Astuce :** Si vos images sources sont dans un flux (par ex., téléchargées via une API web), utilisez `ImageStream.FromStream(votreFlux)` au lieu de `FromFile`.

---

## Étape 2 : Indiquer au moteur la langue attendue – extraire du texte d'une image avec précision

Aspose.OCR prend en charge de nombreux alphabets. Spécifier la langue correcte restreint l'ensemble des caractères et améliore la précision.

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**Pourquoi :**  
Lorsque vous définissez `Language.Latin`, le moteur OCR ignore les glyphes cyrilliques ou asiatiques, réduisant les faux positifs. Si vous devez ensuite gérer des documents multilingues, vous pouvez passer à `Language.Multilingual` ou combiner plusieurs langues.

---

## Étape 3 : Exécuter le processus de reconnaissance – extraire du texte d'une image en un seul appel

Nous reconnaissons maintenant réellement le texte. La méthode `Recognize` renvoie un objet `RecognitionResult` qui contient le texte brut, les scores de confiance et même les données de mise en page.

```csharp
// Perform OCR
RecognitionResult recognitionResult = ocrEngine.Recognize();

// Quick sanity check
if (recognitionResult == null || string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text was detected. Verify the image quality.");
    return;
}

// Print the raw extracted text to the console
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(recognitionResult.Text);
```

**Pourquoi :**  
Appeler `Recognize` une seule fois suffit, car le moteur effectue en interne le prétraitement, la segmentation et la classification des caractères. La propriété `Text` vous fournit une représentation sous forme de chaîne simple, idéale pour le journal ou une validation rapide.

---

## Étape 4 : Convertir le résultat en JSON – convertir facilement l'image en JSON

De nombreux services modernes préfèrent les charges utiles JSON. Aspose.OCR fournit une méthode pratique `ToJson` qui sérialise l'intégralité du `RecognitionResult`, y compris les valeurs de confiance et les boîtes englobantes.

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**Pourquoi vous pourriez vouloir du JSON :**  
- **Interopérabilité :** Les applications front‑end (React, Angular) peuvent consommer le JSON directement.  
- **Débogage :** Le JSON inclut la confiance par caractère, vous permettant de signaler les mots à faible confiance pour une révision manuelle.  

> **Cas particulier :** Si votre système en aval ne nécessite que le texte brut, vous pouvez extraire `recognitionResult.Text` et l'envelopper dans un objet JSON personnalisé au lieu du payload complet d'Aspose.

---

## Étape 5 : Convertir le résultat en XML – convertir l'image en XML pour les systèmes hérités

Certaines entreprises s'appuient encore sur des schémas XML pour l'échange de données. La méthode `ToXml` reflète `ToJson` mais produit du XML.

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**Pourquoi XML :**  
- **Validation de schéma :** Vous pouvez définir un XSD correspondant à la structure générée par Aspose, garantissant la conformité au contrat.  
- **Intégration :** Les anciens ERP ou systèmes de gestion de documents analysent souvent le XML nativement.

---

## Exemple complet fonctionnel – Code tout‑en‑un

Voici le programme complet qui assemble tous les éléments. Copiez‑collez‑le dans un nouveau projet console (`dotnet new console`) et exécutez‑le.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Initialize OCR engine and load the image
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();
            // Adjust the path to point at your PNG/JPG file
            string imagePath = "YOUR_DIRECTORY/invoice.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image at {imagePath}");
                return;
            }

            // -------------------------------------------------
            // Step 2: Specify language (Latin for most European scripts)
            // -------------------------------------------------
            ocrEngine.Language = Language.Latin;

            // -------------------------------------------------
            // Step 3: Run OCR and get the result
            // -------------------------------------------------
            RecognitionResult result = ocrEngine.Recognize();

            if (result == null || string.IsNullOrWhiteSpace(result.Text))
            {
                Console.WriteLine("No text detected – check image quality or language setting.");
                return;
            }

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();

            // -------------------------------------------------
            // Step 4: Convert to JSON (convert image to json)
            // -------------------------------------------------
            string json = result.ToJson();
            string jsonPath = "YOUR_DIRECTORY/invoice.json";
            File.WriteAllText(jsonPath, json);
            Console.WriteLine($"JSON output written to {jsonPath}");

            // -------------------------------------------------
            // Step 5: Convert to XML (convert image to xml)
            // -------------------------------------------------
            string xml = result.ToXml();
            string xmlPath = "YOUR_DIRECTORY/invoice.xml";
            File.WriteAllText(xmlPath, xml);
            Console.WriteLine($"XML output written to {xmlPath}");
        }
    }
}
```

**Sortie attendue (console) :**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

Les fichiers JSON et XML contiendront une structure plus riche, par exemple :

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
  "Confidence": 0.96,
  "Blocks": [
    { "Text": "Invoice #12345", "Confidence": 0.98, "Rectangle": { "X": 12, "Y": 30, "Width": 200, "Height": 20 } },
    ...
  ]
}
```

```xml
<RecognitionResult>
  <Text>Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00</Text>
  <Confidence>0.96</Confidence>
  <Blocks>
    <Block>
      <Text>Invoice #12345</Text>
      <Confidence>0.98</Confidence>
      <Rectangle X="12" Y="30" Width="200" Height="20"/>
    </Block>
    ...
  </Blocks>
</RecognitionResult>
```

---

## Questions fréquentes & cas particuliers

### Que faire si l'image est floue ou tournée ?

Aspose.OCR redresse automatiquement la plupart des images, mais pour les cas extrêmes vous pouvez pré‑traiter avec `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)`. Ajouter un léger renforcement du contraste (`ImageProcessor.AdjustContrast`) peut également améliorer le score de confiance.

### Puis‑je extraire du texte de PDF ?

Oui — convertissez d'abord chaque page PDF en image (par ex., avec Aspose.PDF ou une bibliothèque gratuite comme PDFium) puis alimentez ces images dans le même flux OCR.

### Comment gérer plusieurs langues dans un même document ?

Set `ocrEngine.Language = Language.Multilingual;` or combine specific languages:

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

Be aware that broader language sets may

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}