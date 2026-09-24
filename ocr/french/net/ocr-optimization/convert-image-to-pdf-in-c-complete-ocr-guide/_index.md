---
category: general
date: 2025-12-30
description: Convertir une image en PDF avec Aspose OCR en C#. Apprenez à prétraiter
  l’image pour l’OCR, à reconnaître du texte coréen sur une image et à créer rapidement
  un PDF image consultable.
draft: false
keywords:
- convert image to pdf
- preprocess image for ocr
- recognize korean text image
- create searchable pdf image
language: fr
og_description: Convertir une image en PDF avec Aspose OCR. Ce tutoriel montre comment
  prétraiter une image pour l’OCR, reconnaître une image de texte coréen et créer
  un PDF consultable.
og_title: Convertir une image en PDF en C# – Guide complet d’OCR
tags:
- C#
- OCR
- Aspose
- PDF
title: Convertir une image en PDF en C# – Guide complet d’OCR
url: /fr/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir une image en PDF en C# – Guide complet OCR

Vous avez déjà eu besoin de **convertir une image en PDF** tout en souhaitant que le texte à l'intérieur soit recherchable ? Vous n'êtes pas le seul. De nombreux développeurs rencontrent le même obstacle lorsqu'ils traitent des pages numérisées, notamment celles rédigées en coréen. La bonne nouvelle, c’est qu’avec Aspose OCR vous pouvez **prétraiter l’image pour l’OCR**, **reconnaître une image de texte coréen**, et enfin **créer une image PDF recherchable** en quelques lignes seulement.

Dans ce tutoriel, nous parcourrons l’ensemble du pipeline — du chargement d’un JPEG brut d’une page de livre coréen, au nettoyage, à l’extraction du texte, jusqu’à l’encapsulation du tout dans un PDF recherchable. À la fin, vous disposerez d’une application console C# prête à l’emploi que vous pourrez intégrer à n’importe quel projet .NET.

## Ce dont vous aurez besoin

- **.NET 6.0 ou version ultérieure** (le code fonctionne aussi bien sur .NET Core que sur .NET Framework)  
- **Aspose.OCR for .NET** package NuGet (`Aspose.OCR`) – des clés d’essai gratuites sont disponibles sur le site d’Aspose.  
- Une image d’exemple contenant du texte coréen (par ex. `korean_book_page.jpg`).  
- Un environnement de développement de votre choix (Visual Studio, VS Code, Rider – j’utilise VS 2022).

> **Astuce pro :** Conservez vos fichiers image dans un dossier dédié comme `Resources/` afin que le chemin reste cohérent d’une machine à l’autre.

## Aperçu du processus

1. **Initialiser le moteur OCR** avec le support GPU pour plus de rapidité.  
2. **Ajouter des filtres de prétraitement** (redressement, débruitage) pour améliorer la précision de reconnaissance.  
3. **Télécharger et charger le modèle de langue coréenne** – Aspose le fait automatiquement si nécessaire.  
4. **Exécuter la reconnaissance** sur l’image d’entrée.  
5. **Exporter le résultat sous forme de PDF recherchable** à l’aide de l’exportateur intégré.  
6. **Optionnellement, sérialiser le résultat en JSON** pour des analyses ou des journaux supplémentaires.

Ci‑dessous, nous détaillerons chaque étape, expliquerons *pourquoi* elle est importante, et vous fournirons le code exact à copier‑coller.

---

## ## Convertir une image en PDF – Flux complet

Le fragment suivant est le programme *complet*. N’hésitez pas à créer un nouveau projet console (`dotnet new console -n OcrPdfDemo`) et à remplacer le `Program.cs` généré automatiquement par ce code.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### Pourquoi cela fonctionne

- **L’accélération GPU** réduit le temps de reconnaissance d’environ moitié comparé au mode CPU‑only.  
- **Deskew** et **Denoise** sont des techniques classiques de *prétraiter l’image pour l’OCR* ; elles corrigent les défauts de numérisation courants qui, autrement, feraient manquer des caractères au moteur.  
- **Le chargement du modèle de langue** est essentiel pour **reconnaître une image de texte coréen** – sans le modèle coréen, le moteur reviendrait à un alphabet latin générique et produirait du bruit.  
- Le **SearchablePdfExporter** regroupe le bitmap original et une couche de texte invisible, vous offrant ainsi un résultat **créer une image PDF recherchable** que vous pouvez indexer dans n’importe quel lecteur PDF.

---

## ## Prétraiter l’image pour l’OCR – Astuces & Trucs

Bien que les deux filtres ajoutés soient généralement suffisants, vous pourriez rencontrer des images récalcitrantes. Voici quelques étapes supplémentaires que vous pouvez essayer :

| Problème | Filtre supplémentaire | Comment ajouter |
|----------|-----------------------|-----------------|
| Faible contraste | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Bruitage de fond important | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Orientation mixte (portrait et paysage) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Note :** Ajouter trop de filtres peut ralentir le traitement. Testez chaque modification sur une seule page avant de passer à l’échelle.

---

## ## Reconnaître une image de texte coréen – Pièges courants

Les scripts coréens contiennent des syllabes Hangul très denses visuellement. Si vous remarquez une sortie illisible :

1. **Assurez‑vous que le modèle de langue est entièrement téléchargé** – vérifiez la console pour un message du type « Downloading Korean model… ».  
2. **Augmentez le `MaxAngle`** dans `DeskewFilter` si vos numérisations sont tournées de plus de 12°.  
3. **Boostez la mémoire GPU** en définissant `ocrEngine.GpuMemoryLimit = 2048;` (valeur en Mo).  

Ces ajustements influencent directement le succès de **reconnaître une image de texte coréen**.

---

## ## Créer une image PDF recherchable – Vérification du résultat

Après l’exécution du programme, ouvrez `korean_page.pdf` dans n’importe quel lecteur PDF (Adobe Acrobat Reader, Foxit, même Chrome). Vous devriez pouvoir :

- **Sélectionner le texte** avec votre souris comme s’il s’agissait d’un PDF natif.  
- **Rechercher** des mots coréens à l’aide de la boîte de recherche intégrée.  

Si la couche de texte apparaît vide, revérifiez que la méthode `Export` a reçu le bon chemin d’image et que le résultat OCR contient un `RecognitionResult.Text` non vide.

---

## ## Sortie JSON complète – À quoi s’attendre

La console affiche une charge JSON joliment formatée. Un exemple tronqué ressemble à ceci :

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

Vous pouvez transmettre ce JSON à des services en aval (p. ex. pipelines d’indexation, API de traduction) sans devoir relancer l’OCR.

---

## ## Dépannage & FAQ

**Q : Mon PDF est énorme comparé à l’image originale.**  
R : L’exportateur intègre le bitmap original à sa résolution native. Si la taille pose problème, réduisez l’image *avant* la reconnaissance :

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q : L’OCR renvoie des chaînes vides.**  
R : Vérifiez que le chemin de l’image est correct et que le fichier n’est pas corrompu. Assurez‑vous également que le pilote GPU est à jour ; les pilotes anciens peuvent provoquer des échecs silencieux.

**Q : Puis‑je traiter plusieurs pages dans une boucle ?**  
R : Bien sûr. Enveloppez les étapes 4‑6 dans une boucle `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` et adaptez le chemin de sortie PDF en conséquence.

---

## ## Conclusion

Nous venons **de convertir une image en PDF** tout en conservant le texte recherchable, grâce à la puissante chaîne de traitement d’Aspose OCR. En **prétraitant l’image pour l’OCR**, vous améliorez la précision ; en **reconnaissant une image de texte coréen**, vous gérez les scripts complexes ; et en **créant une image PDF recherchable**, vous obtenez un document portable et indexable.

Prenez le code, pointez‑le sur vos propres numérisations, et expérimentez avec des filtres ou modèles de langue supplémentaires. Le même schéma fonctionne pour le chinois, le japonais ou toute langue à base latine — il suffit de remplacer `LanguageModel.Korean` par l’énumération appropriée.

Des questions supplémentaires ? Laissez un commentaire, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}