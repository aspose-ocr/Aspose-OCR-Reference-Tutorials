---
category: general
date: 2026-08-09
description: Extraire du texte d’une image avec Aspose OCR en C#. Apprenez comment
  charger une image pour l’OCR, définir la langue de l’OCR, traiter l’image avec l’OCR
  et convertir l’image en texte de manière efficace.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for ocr
- process image ocr
- set ocr language
language: fr
lastmod: 2026-08-09
og_description: Extraire du texte d’une image à l’aide d’Aspose OCR en C#. Ce tutoriel
  montre comment charger une image pour l’OCR, définir la langue de l’OCR, traiter
  l’image avec l’OCR et convertir l’image en texte en quelques lignes de code.
og_image_alt: Screenshot of C# console output showing extracted text from an image
  using Aspose OCR
og_title: Extraire du texte d’une image avec Aspose OCR – Guide C#
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  headline: Extract text from image using Aspose OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  name: Extract text from image using Aspose OCR in C#
  steps:
  - name: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
    text: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
  - name: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
    text: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
  - name: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
    text: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
  - name: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
    text: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
  - name: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
    text: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
  - name: Instantiates `OcrEngine`.
    text: Instantiates `OcrEngine`.
  - name: '**Sets OCR language** to Cyrillic (or any language you choose).'
    text: '**Sets OCR language** to Cyrillic (or any language you choose).'
  - name: '**Loads image for OCR** from disk.'
    text: '**Loads image for OCR** from disk.'
  - name: '**Processes image OCR** to obtain the textual result.'
    text: '**Processes image OCR** to obtain the textual result.'
  - name: '**Converts image to text** and prints it.'
    text: '**Converts image to text** and prints it.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Extraire du texte d’une image à l’aide d’Aspose OCR en C#
url: /fr/net/text-recognition/extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image avec Aspose OCR en C#

Si vous devez **extraire du texte d'une image** dans une application .NET, ce guide vous accompagne pas à pas à travers une solution complète, prête à l'emploi. Vous verrez comment **charger une image pour l'OCR**, choisir le module de langue approprié, exécuter le moteur OCR, et enfin **convertir l'image en texte** en quelques lignes de C#.

Le tutoriel couvre tout ce qui est nécessaire pour obtenir des résultats fiables avec Aspose.OCR, y compris les pièges courants tels que les formats d'image non pris en charge et les nuances propres à chaque langue. À la fin, vous disposerez d'un programme autonome qui affiche le texte reconnu dans la console.

## Ce que vous allez réaliser

* Charger un fichier image dans le moteur Aspose OCR.  
* **Définir la langue OCR** (cyrillique dans l'exemple, mais toute langue prise en charge fonctionne).  
* **Traiter l'image OCR** et obtenir la représentation textuelle.  
* **Convertir l'image en texte** et l'afficher, prête pour un traitement ou un stockage ultérieur.  

**Prérequis**

* .NET 6.0 ou ultérieur (le code fonctionne également sur .NET Framework 4.6+).  
* Visual Studio 2022 (ou tout IDE supportant C#).  
* Package NuGet Aspose.OCR (`Install-Package Aspose.OCR`).  

---

## Extraire du texte d'une image – guide complet du code

Ci-dessous se trouve le programme complet et exécutable. Copiez-le dans un nouveau projet console et remplacez `YOUR_DIRECTORY/sample_cyrillic.jpg` par le chemin de votre propre image.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create an OCR engine instance.
            // The using block ensures the engine is disposed correctly.
            using (var engine = new OcrEngine())
            {
                // Step 2: Set OCR language.
                // Change OcrLanguage.Cyrillic to any other supported language,
                // e.g., OcrLanguage.English, OcrLanguage.Chinese, OcrLanguage.Hindi.
                engine.Language = OcrLanguage.Cyrillic;

                // Step 3: Load image for OCR.
                // ImageStream.FromFile reads the image from disk.
                // Supported formats: JPEG, PNG, BMP, TIFF, GIF.
                engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.jpg");

                // Step 4: Process image OCR.
                // The Process method runs the recognition engine and returns an OcrResult.
                var result = engine.Process();

                // Step 5: Convert image to text.
                // The recognized text is available via result.Text.
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

### Pourquoi chaque étape est importante

1. **Créer une instance du moteur OCR** – Le `OcrEngine` encapsule toutes les fonctionnalités OCR. Le libérer rapidement libère les ressources natives, ce qui est crucial pour les services de longue durée.  
2. **Définir la langue OCR** – Sélectionner le bon module de langue améliore considérablement la précision. Aspose propose plus de 30 packs de langues ; la langue par défaut est l'anglais. L'exemple utilise le cyrillique pour illustrer un script non latin.  
3. **Charger une image pour l'OCR** – Le moteur travaille avec un `ImageStream`. Fournir une image haute résolution (≥300 dpi) réduit les erreurs de reconnaissance, surtout pour les scripts complexes.  
4. **Traiter l'image OCR** – C'est ici que le travail intensif se déroule. La méthode renvoie un `OcrResult` contenant le texte extrait, les scores de confiance et, éventuellement, les données de mise en page.  
5. **Convertir l'image en texte** – `result.Text` est une simple `string`. Vous pouvez l'écrire dans un fichier, l'alimenter dans un index de recherche, ou le transmettre à des pipelines NLP en aval.  

---

## Charger une image pour l'OCR

La méthode `ImageStream.FromFile` prend en charge les formats raster courants. Si vous recevez des images sous forme de tableaux d'octets (par ex., depuis une API web), utilisez `ImageStream.FromBytes(byte[])` à la place :

```csharp
byte[] imageBytes = File.ReadAllBytes("path/to/image.png");
engine.Image = ImageStream.FromBytes(imageBytes);
```

**Astuce :** Vérifiez toujours que l'image n'est pas corrompue avant de la transmettre au moteur. Une simple protection `try { Image.FromFile(...); } catch { ... }` évite les exceptions d'exécution.

---

## Définir la langue OCR

Aspose.OCR est fourni avec des packs de langues que vous pouvez activer à l'exécution. Pour lister toutes les langues disponibles :

```csharp
foreach (var lang in Enum.GetValues(typeof(OcrLanguage)))
{
    Console.WriteLine(lang);
}
```

Si vous devez reconnaître plusieurs langues dans le même document, combinez-les avec l'opérateur OU bit à bit :

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Russian;
```

**Cas particulier :** Mélanger des langues de droite à gauche (RTL) (par ex., l'arabe) avec des scripts de gauche à droite peut nécessiter une gestion de mise en page supplémentaire. Aspose détecte automatiquement la direction, mais vous pouvez l'ajuster via `engine.PageSegmentationMode`.

---

## Traiter l'image OCR

L'appel `Process` est synchrone et bloque jusqu'à ce que le moteur termine. Pour de gros lots ou des applications UI, envisagez la surcharge asynchrone :

```csharp
var task = engine.ProcessAsync();
OcrResult result = await task;
```

**Erreur fréquente :** Oublier de définir `engine.Image` avant d'appeler `Process` déclenche une `InvalidOperationException`. Assignez toujours l'image d'abord.

---

## Convertir l'image en texte

La chaîne extraite peut être manipulée comme n'importe quelle `string` .NET. Par exemple, pour écrire le résultat dans un fichier :

```csharp
File.WriteAllText("output.txt", result.Text);
```

Si vous devez conserver les sauts de ligne exactement comme ils apparaissent dans l'image, utilisez directement `result.Text`. Pour le post‑traitement (par ex., suppression des espaces superflus), appliquez les méthodes standard de chaîne :

```csharp
string cleaned = result.Text
    .Replace("\r\n", "\n")
    .Trim();
```

---

## Récapitulatif de l'exemple complet

En combinant tous les éléments, le programme :

1. Instancie `OcrEngine`.  
2. **Définit la langue OCR** sur le cyrillique (ou toute langue de votre choix).  
3. **Charge une image pour l'OCR** depuis le disque.  
4. **Traite l'image OCR** pour obtenir le résultat textuel.  
5. **Convertit l'image en texte** et l'affiche.  

Exécuter l'exemple avec une image cyrillique claire produit une sortie similaire à :

```
=== Recognized Text ===
Пример текста на кириллице
```

Si l'image contient du texte anglais, il suffit de changer `engine.Language = OcrLanguage.English;` et le même code **extraira le texte de l'image** correctement.

---

## Conclusion

Vous savez maintenant comment **extraire du texte d'une image** en utilisant Aspose OCR en C#. Le tutoriel a couvert le chargement de l'image, la sélection de la langue appropriée, l'exécution du processus OCR, et **la conversion de l'image en texte** pour une utilisation en aval.  

À partir d'ici, vous pouvez :

* Expérimenter avec d'autres langues (`load image for OCR` → `set OCR language` → `process image OCR`).  
* Intégrer l'étape OCR dans un pipeline plus large (par ex., ingestion de documents, PDF recherchables).  
* Optimiser les performances en traitant les images par lots ou en utilisant l'API asynchrone.  

N'hésitez pas à explorer la documentation Aspose.OCR pour des fonctionnalités avancées telles que les dictionnaires personnalisés, les modes de segmentation de page et le réglage de la précision OCR. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extraire le texte d'une image C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extraire du texte d'une image – Optimisation OCR avec Aspose.OCR pour .NET](/ocr/english/net/ocr-optimization/)
- [Comment effectuer l'extraction de texte d'image depuis un flux en utilisant Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}