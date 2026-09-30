---
category: general
date: 2026-01-09
description: Extrayez rapidement du texte à partir de PNG avec Aspose OCR. Apprenez
  à lire le texte d’image, à améliorer la précision de l’OCR et à obtenir des résultats
  propres en C#.
draft: false
keywords:
- extract text from png
- read image text
- improve ocr accuracy
- extract text from image
- aspose ocr tutorial
language: fr
og_description: Extrayez rapidement du texte à partir de PNG avec Aspose OCR. Apprenez
  à lire le texte d’une image, à améliorer la précision de l’OCR et à obtenir des
  résultats propres en C#.
og_title: Extraire du texte à partir de PNG – Tutoriel complet Aspose OCR
tags:
- Aspose OCR
- C#
- Image Processing
title: Extraire du texte d’un PNG – Tutoriel complet Aspose OCR
url: /fr/net/text-recognition/extract-text-from-png-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte à partir d'un PNG – Tutoriel complet Aspose OCR

Vous avez déjà eu besoin d'**extraire du texte à partir de fichiers PNG** mais les résultats étaient remplis de charabia ? Vous n'êtes pas seul. Dans de nombreux projets réels – factures, reçus ou formulaires numérisés – la qualité de la sortie OCR peut faire ou défaire les pipelines d'automatisation.  

Dans ce guide, nous vous montrerons une méthode **étape par étape** pour lire le texte d'une image avec Aspose OCR, ajouter un dictionnaire personnalisé afin d'**améliorer la précision de l'OCR**, nettoyer le bruit, puis afficher une chaîne propre. À la fin, vous disposerez d'une application console C# prête à l'emploi qui extrait de façon fiable le texte des images PNG.

> **Ce que vous en retirerez**  
> * Un exemple de code complet et exécutable.  
> * Une compréhension de l'importance d'un dictionnaire personnalisé.  
> * Des astuces pour gérer les cas limites comme les scans à faible contraste.  

## Prérequis

- SDK .NET 6 ou version ultérieure (le code cible .NET 6, mais .NET 5 fonctionne également).  
- Visual Studio 2022 ou tout autre éditeur de votre choix.  
- Une image **PNG** que vous souhaitez traiter – par exemple `invoice.png`.  
- Le package NuGet **Aspose.OCR** (`dotnet add package Aspose.OCR`).  

Aucun fichier de configuration supplémentaire n'est nécessaire ; tout se trouve dans un seul fichier `.cs`.

## Étape 1 – Installer et référencer Aspose OCR

Tout d'abord, ajoutez la bibliothèque à votre projet. Ouvrez un terminal dans le dossier de votre solution et exécutez :

```bash
dotnet add package Aspose.OCR
```

Cette seule ligne récupère la dernière version stable (en janvier 2026, version 23.9). Le package inclut la classe `OcrEngine` que nous utiliserons tout au long du tutoriel.

## Étape 2 – Initialiser le moteur OCR

Créer une instance de `OcrEngine` constitue la base. Pensez-y comme allumer un scanner prêt à interpréter les pixels.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

> **Astuce :** Si vous prévoyez de traiter de nombreuses images dans une boucle, réutilisez la même instance de `OcrEngine`. Elle met en cache des ressources internes et accélère les appels suivants.

## Étape 3 – Améliorer la précision avec un dictionnaire personnalisé

L'OCR « prêt à l'emploi » est bon, mais il peut trébucher sur des mots spécifiques au domaine comme “Aspose”, “OCR” ou “SDK”. Ajouter ces termes à un **dictionnaire personnalisé** indique au moteur que ces chaînes sont valides, réduisant ainsi les mauvaises reconnaissances.

```csharp
// Define domain‑specific terms that the engine should recognize
ocrEngine.CustomDictionary = new HashSet<string>
{
    "Aspose",
    "OCR",
    "SDK",
    "invoice"
};
```

### Pourquoi un dictionnaire personnalisé aide

- Les **modèles statistiques** derrière l'OCR accordent un poids important aux schémas linguistiques courants. Les mots rares obtiennent une faible probabilité et peuvent être remplacés par des caractères similaires.  
- En les listant explicitement, vous surchargez les conjectures du modèle.  
- C’est particulièrement utile pour **read image text** contenant des codes produit, des abréviations ou des noms de marque.

## Étape 4 – Reconnaître le texte du fichier PNG

Nous transmettons maintenant le chemin de l'image au moteur. La méthode `RecognizeImage` renvoie une chaîne brute qui contient encore des jetons inconnus (par ex., “#@!”) que le moteur n’a pas pu mapper.

```csharp
// Path to the PNG you want to process
string imagePath = @"YOUR_DIRECTORY/invoice.png";

// Perform OCR
string rawText = ocrEngine.RecognizeImage(imagePath);
```

> **Cas limite :** Si le fichier est introuvable, `RecognizeImage` lève une `FileNotFoundException`. Enveloppez l’appel dans un bloc try‑catch pour le code de production.

## Étape 5 – Nettoyer le résultat avec `CleanText`

Aspose OCR fournit un utilitaire qui supprime les caractères qu’il considère comme “inconnus”. Cette étape est cruciale pour les projets **extract text from image** où les analyseurs en aval attendent uniquement des caractères alphanumériques et une ponctuation de base.

```csharp
// Remove unknown tokens and extra whitespace
string cleanedText = ocrEngine.CleanText(rawText);
```

La méthode `CleanText` normalise également les sauts de ligne, rendant la sortie sûre à stocker dans des bases de données ou à transmettre à d’autres services.

## Étape 6 – Afficher le texte nettoyé

Enfin, affichez ou stockez le résultat. Dans une application console, `Console.WriteLine` fait l’affaire.

```csharp
Console.WriteLine("=== Cleaned OCR Output ===");
Console.WriteLine(cleanedText);
```

Lorsque vous exécuterez le programme, vous devriez voir un bloc de texte propre qui reflète le contenu de `invoice.png`. Si l’image contient le mot “Aspose”, le dictionnaire personnalisé garantit qu’il apparaît correctement plutôt que sous une forme comme “A5p0se”.

## Exemple complet fonctionnel

En rassemblant le tout, voici le fichier complet `Program.cs` que vous pouvez copier‑coller dans un nouveau projet console :

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add domain‑specific terms to improve OCR accuracy
        ocrEngine.CustomDictionary = new HashSet<string>
        {
            "Aspose",
            "OCR",
            "SDK",
            "invoice"
        };

        // 3️⃣ Path to your PNG file (adjust as needed)
        string imagePath = @"YOUR_DIRECTORY/invoice.png";

        try
        {
            // 4️⃣ Recognize raw text from the image
            string rawText = ocrEngine.RecognizeImage(imagePath);

            // 5️⃣ Clean up unknown tokens
            string cleanedText = ocrEngine.CleanText(rawText);

            // 6️⃣ Show the result
            Console.WriteLine("=== Cleaned OCR Output ===");
            Console.WriteLine(cleanedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

**Sortie attendue** (en supposant que le PNG contienne une facture simple) :

```
=== Cleaned OCR Output ===
Invoice #12345
Date: 01/08/2026
Total: $1,250.00
Thank you for your business!
```

Si vous voyez des symboles parasites, revérifiez la qualité de l’image ou enrichissez le dictionnaire personnalisé avec davantage de termes.

## Bonus : Gestion des scans de mauvaise qualité

Parfois les PNG sont numérisés à 72 dpi ou présentent de lourds artefacts de compression. Voici quelques astuces rapides pour **améliorer la précision de l'OCR** sans quitter C# :

1. **Pré‑traiter l'image** avec une bibliothèque comme `SixLabors.ImageSharp` – augmenter le contraste, convertir en niveaux de gris ou appliquer un léger flou pour réduire le bruit.  
2. **Définir la propriété `Resolution`** sur le `OcrEngine` (par ex., `ocrEngine.Resolution = 300;`) pour indiquer au moteur de traiter l’image comme haute résolution.  
3. **Activer les packs de langues** si vous traitez du texte non anglais (`ocrEngine.Language = Language.English;`).

Ces trois approches peuvent être ajoutées avant l’appel à `RecognizeImage`.

## Questions fréquentes

- **Cette méthode fonctionne‑t‑elle avec d’autres formats d’image ?**  
  Oui. `RecognizeImage` accepte JPEG, BMP, TIFF et même PDF (en tant que conteneur d’image). Les mêmes étapes s’appliquent.

- **Puis‑je extraire du texte de plusieurs PNG dans un dossier ?**  
  Absolument. Enveloppez la logique principale dans une boucle `foreach (var file in Directory.GetFiles(folder, "*.png"))` et stockez chaque résultat dans une liste ou écrivez‑les dans des fichiers séparés.

- **Et si j’ai besoin des coordonnées du texte ?**  
  Aspose OCR fournit également des objets `OcrResult` contenant les boîtes englobantes. Utilisez `ocrEngine.RecognizeImageToResult(imagePath)` pour ce scénario avancé.

## Conclusion

Nous avons parcouru une solution **complète, de bout en bout** pour **extraire du texte à partir de PNG** en utilisant Aspose OCR. En initialisant le moteur, en lui fournissant un **dictionnaire personnalisé**, en nettoyant la sortie brute et en gérant quelques pièges courants, vous pouvez lire le texte d’une image de façon fiable et **améliorer la précision de l'OCR** dans vos propres applications C#.

Prêt pour l’étape suivante ? Essayez de remplacer le PNG par un reçu numérisé, ajoutez davantage de mots spécifiques à votre domaine dans le dictionnaire, ou intégrez la sortie à une base de données pour un traitement automatisé des factures. Le ciel est la limite lorsque vous combinez Aspose OCR avec l’écosystème riche de .NET.

Bon codage, et que votre OCR soit toujours précis ! 

![Extract text from png example](/images/extract-text-from-png.png "extract text from png – Aspose OCR demo")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}