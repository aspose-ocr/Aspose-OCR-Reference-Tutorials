---
category: general
date: 2026-02-20
description: Prétraiter l'OCR d'image avec Aspose.OCR en C#. Apprenez comment appliquer
  un filtre médian, réduire le bruit de l'image et extraire le texte de l'image efficacement.
draft: false
keywords:
- preprocess image OCR
- apply median filter
- extract text image
- reduce image noise
- c# ocr example
language: fr
og_description: Prétraiter l’OCR d’image avec Aspose.OCR. Ce tutoriel montre comment
  appliquer un filtre médian, réduire le bruit de l’image et extraire le texte de
  l’image en utilisant C#.
og_title: Prétraitement d'image OCR en C# – Guide complet
tags:
- OCR
- C#
- Image Processing
title: Prétraiter l'OCR d'image en C# – Guide complet étape par étape
url: /fr/net/ocr-optimization/preprocess-image-ocr-in-c-complete-step-by-step-guide/
---

triple backticks? Actually they are placeholders for code blocks. In original they are placed as separate lines, not inside triple backticks. We must keep them as is.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Prétraitement de l'OCR d'image en C# – Guide complet étape par étape

Vous avez déjà eu besoin de **prétraiter l'OCR d'image** parce que vos photos numérisées renvoient du texte illisible ? Vous n'êtes pas seul. Dans de nombreux projets réels—pensez aux reçus, cartes d'identité ou notes manuscrites—l'image brute n'est jamais prête pour une reconnaissance immédiate. Bonne nouvelle : quelques étapes simples de prétraitement peuvent augmenter la précision de façon spectaculaire, et vous pouvez tout faire en C# avec Aspose.OCR.

Dans ce tutoriel, nous allons parcourir un exemple pratique qui montre comment **appliquer un filtre médian**, **réduire le bruit de l'image**, puis **extraire le texte de l'image** avec un résultat propre et lisible. À la fin, vous disposerez d’une application console C# entièrement fonctionnelle que vous pourrez intégrer à n’importe quelle solution .NET. Pas de références vagues, juste le code dont vous avez besoin et le « pourquoi » derrière chaque ligne.

---

## Ce dont vous aurez besoin

- **Aspose.OCR for .NET** (dernière version au moment de la rédaction, 23.12). Vous pouvez l’obtenir via NuGet : `Install-Package Aspose.OCR`.
- .NET 6.0 ou supérieur (l’exemple utilise une application console, mais la même logique fonctionne en ASP.NET, WPF, etc.).
- Une image d’exemple à nettoyer—par ex. `skewed_photo.jpg`.  
- Un minimum d’expérience en C# ; les concepts restent simples même pour des développeurs junior.

> **Astuce :** Si vous travaillez sur une machine d’entreprise, assurez‑vous que votre flux NuGet est configuré pour autoriser les packages externes, sinon l’installation échouera.

---

## Étape 1 – Créer l’instance du moteur OCR  

La première chose à faire est d’instancier un `OcrEngine`. Cet objet contient les paramètres de reconnaissance et traitera plus tard le bitmap pré‑traité.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image handling
using System;

class PreprocessExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is the core component that will read text.
        OcrEngine ocrEngine = new OcrEngine();

        // ... we’ll continue with loading and preprocessing the image below.
```

**Pourquoi ?**  
Créer le moteur une seule fois et le réutiliser pour plusieurs images réduit la surcharge. Cela vous permet également d’ajuster la langue ou les modes de reconnaissance plus tard sans reconstruire toute la chaîne de traitement.

---

## Étape 2 – Charger l’image source  

Vous avez besoin d’un objet `System.Drawing.Image` qui pointe vers votre fichier brut. Dans un vrai projet vous accepterez peut‑être un flux, mais pour plus de clarté nous lisons depuis le disque.

```csharp
        // Load the image that requires preprocessing.
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");
```

> **Remarque :** Remplacez `YOUR_DIRECTORY` par le chemin réel du dossier. Si le fichier n’est pas trouvé, une `FileNotFoundException` sera levée—attrapez‑la si vous voulez gérer l’erreur de façon élégante.

---

## Étape 3 – Redresser et faire pivoter l’image  

La plupart des documents numérisés sont légèrement inclinés. Le filtre `DeskewAndRotate` détecte automatiquement l’angle de rotation et oriente l’image correctement.

```csharp
        // Correct orientation – crucial for accurate OCR.
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());
```

**Pourquoi est‑ce important ?**  
Les moteurs OCR supposent que les lignes de texte sont horizontales. Même une inclinaison de 2 ° peut faire chuter la précision de reconnaissance de 15‑20 %. Redresser l’image est le moyen le plus économique d’obtenir un gros gain.

---

## Étape 4 – Appliquer un filtre médian pour réduire le bruit de l’image  

Le bruit apparaît sous forme de taches ou de pixels aléatoires, surtout dans les photos en faible lumière. Un filtre médian lisse ces artefacts tout en préservant les contours, exactement ce qu’il faut avant l’OCR.

```csharp
        // Reduce noise – radius of 2 is a good balance for most photos.
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));
```

**Pourquoi un filtre médian ?**  
Contrairement à un filtre moyen (average), le filtre médian remplace chaque pixel par la valeur médiane de son voisinage. Ainsi, le bruit isolé est éliminé sans flouter les traits du texte—une technique classique pour **réduire le bruit de l'image**.

---

## Étape 5 – Améliorer le contraste avec un étirement  

Après la suppression du bruit, l’étape suivante consiste à augmenter la différence entre le texte et l’arrière‑plan. L’étirement du contraste répartit les intensités de pixels sur toute la plage 0‑255.

```csharp
        // Stretch contrast to make dark text pop against a light background.
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());
```

**Pourquoi étirer ?**  
Les moteurs OCR dépendent d’une nette séparation premier‑plan/arrière‑plan. Si l’image est délavée, le moteur peut considérer le texte comme faisant partie de l’arrière‑plan. L’étirement du contraste corrige cela sans nécessiter de seuillage manuel.

---

## Étape 6 – Effectuer l’OCR sur l’image pré‑traitée  

Maintenant que l’image est droite, propre et à fort contraste, nous la transmettons au moteur OCR.

```csharp
        // Recognize the text from the cleaned image.
        string extractedText = ocrEngine.Recognize(processedImage);
```

**Ce que vous obtenez :**  
`extractedText` contient la chaîne Unicode brute détectée par Aspose.OCR. Vous pouvez la post‑traiter davantage (trim, regex, etc.) si besoin.

---

## Étape 7 – Afficher le texte reconnu  

Enfin, écrivez le résultat dans la console ou dans un fichier—selon ce qui convient à votre flux de travail.

```csharp
        // Show the result in the console.
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

### Résultat attendu

Si `skewed_photo.jpg` contient la phrase « Hello World », vous verrez quelque chose comme :

```
=== Extracted Text ===
Hello World
```

Si l’image reste bruyante, vous remarquerez peut‑être des caractères illisibles—revenez à l’Étape 4 et augmentez le rayon du filtre médian, ou expérimentez avec des filtres supplémentaires comme `GaussianBlur`.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet, prêt à être compilé. Aucun morceau manquant—remplacez simplement le chemin du fichier.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;
using System;

class PreprocessExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image that needs preprocessing
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");

        // Step 3: Deskew and rotate the image to correct orientation
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());

        // Step 4: Reduce noise with a median filter (radius = 2)
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));

        // Step 5: Enhance contrast using contrast stretching
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());

        // Step 6: Perform OCR on the preprocessed image
        string extractedText = ocrEngine.Recognize(processedImage);

        // Step 7: Output the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

> **Astuce cas particulier :** Si votre image contient du texte coloré sur un fond coloré, envisagez de la convertir en niveaux de gris avant d’appliquer `ContrastStretch`. Vous pouvez le faire avec `Preprocess.Grayscale()` dans la chaîne de traitement.

---

## Questions fréquentes & variantes  

### Et si l’image est à l’envers ?  
`DeskewAndRotate` détecte automatiquement les rotations de 180 °, mais vous pouvez forcer une rotation avec `Preprocess.Rotate(angle: 180)` avant le redressement.

### Puis‑je sauter le filtre médian ?  
Oui, mais vous verrez probablement les bénéfices de **réduire le bruit de l'image** diminuer. Sur des scans haute résolution, le filtre peut être superflu ; sur des photos de téléphone en faible lumière, il est généralement indispensable.

### En quoi cela diffère‑t‑il d’un simple `Apply(Preprocess.Binarize())` ?  
La binarisation convertit l’image en noir et blanc purs, ce qui peut être trop agressif pour les polices fines. Notre approche conserve les détails en niveaux de gris, puis étire le contraste—souvent plus efficace pour des polices de tailles mixtes.

### Existe‑t‑il un moyen d’**appliquer un filtre médian** uniquement sur une région d’intérêt ?  
`Apply` d’Aspose.OCR agit sur l’ensemble du bitmap, mais vous pouvez d’abord recadrer l’image (`sourceImage.Clone(new Rectangle(...), sourceImage.PixelFormat)`) puis appliquer le filtre à cette sous‑image.

---

## Prochaines étapes – Aller au‑delà du prétraitement de base  

- **Packs de langues :** Si vous devez extraire des caractères français ou japonais, chargez le modèle de langue approprié via `ocrEngine.Language = Language.French;`.
- **Seuillage personnalisé :** Pour des scans extrêmement à faible contraste, expérimentez `Preprocess.AdaptiveThreshold()` après le filtre médian.
- **Traitement par lots :** Enveloppez les étapes dans une boucle `foreach (string file in Directory.GetFiles(...))` et écrivez chaque résultat dans un fichier `.txt`.  
- **Optimisation des performances :** Réutilisez une seule instance de `OcrEngine` et pré‑allouez un tampon `Bitmap` pour éviter les pics de GC lors du traitement de milliers d’images.

---

## Conclusion  

Nous venons de montrer comment **prétraiter l'OCR d'image** en C# du début à la fin : charger la photo, la redresser, **appliquer un filtre médian**, augmenter le contraste, puis **extraire le texte de l'image** avec Aspose.OCR. Le code complet est prêt à être intégré dans n’importe quel projet, et les explications vous donnent le « pourquoi » derrière chaque transformation—afin que vous puissiez ajuster les paramètres à vos propres cas limites.

Testez-le avec différentes photos, jouez avec le rayon du filtre, et observez la précision de reconnaissance grimper. Une fois à l’aise, explorez les ajustements avancés mentionnés plus haut, et vous deviendrez la référence en pipelines OCR propres au sein de votre équipe.

Bon codage, et que votre OCR lise toujours clairement ! 

![exemple de prétraitement OCR d'image](/images/preprocess-image-ocr.png "prétraitement OCR d'image – avant et après le traitement")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}