---
category: general
date: 2026-03-05
description: Comment utiliser l'OCR en C# pour extraire du texte d’une image. Apprenez
  à convertir une image en texte, à lire les caractères coréens et à charger rapidement
  une image pour l’OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert image to text
- read korean characters
- load image for OCR
language: fr
og_description: Comment utiliser l'OCR en C# et extraire instantanément du texte à
  partir d'une image. Ce guide montre comment convertir une image en texte, lire les
  caractères coréens et charger une image pour l'OCR.
og_title: Comment utiliser l'OCR en C# – Extraire du texte d'une image
tags:
- OCR
- C#
- Aspose
title: Comment utiliser l'OCR en C# – Extraire du texte à partir d’une image
url: /fr/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l'OCR en C# – Extraire du texte d'une image

Vous vous êtes déjà demandé **comment utiliser l'OCR** lorsque vous avez une capture d'écran remplie de texte coréen et que vous avez besoin de la chaîne brute ? Vous n'êtes pas le seul à vous creuser la tête à ce sujet. Dans ce tutoriel, nous parcourrons un exemple complet, prêt à l'exécution, qui **extrait du texte d'une image**, **convertit une image en texte**, et montre même comment **lire les caractères coréens** avec Aspose.OCR.

Nous couvrirons également l'étape souvent négligée de **chargement d'image pour l'OCR** afin que vous ne rencontriez pas de surprise « fichier introuvable » plus tard. À la fin, vous disposerez d'un programme autonome que vous pourrez intégrer à n'importe quel projet .NET.

## Ce dont vous aurez besoin

- .NET 6+ (ou .NET Framework 4.7.2 et versions ultérieures) – le code fonctionne sur les deux.
- Aspose.OCR pour .NET – vous pouvez obtenir un essai gratuit depuis le site web d'Aspose.
- Une image d'exemple (`korean_doc.png`) contenant du texte coréen.
- Votre IDE préféré (Visual Studio, Rider, VS Code – ce qui vous convient).

Aucune autre bibliothèque tierce n'est requise.

## Étape 1 : Configurer le projet et ajouter Aspose.OCR

First, create a new console app:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Then add the Aspose.OCR NuGet package:

```bash
dotnet add package Aspose.OCR
```

> **Astuce pro :** Si vous avez un fichier de licence, placez‑le à la racine du projet ; sinon l'essai gratuit fonctionnera mais ajoutera un filigrane à la sortie.

## Étape 2 : Comment utiliser l'OCR – Initialiser le moteur

Nous allons maintenant écrire le code C#. La première chose à faire lorsqu’on **comment utiliser l'OCR** est d'instancier le `OcrEngine`. Cet objet est le cœur de la bibliothèque ; il contient tous les paramètres dont vous aurez besoin plus tard.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: apply your license to remove trial limitations
            // Replace the path with the actual location of your .lic file
            ocrEngine.SetLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Pourquoi c’est important :** Sans une instance d’engin appropriée, vous ne pouvez pas définir la langue, charger des images ou récupérer les résultats. Le moteur gère également les ressources internes, ainsi le créer une fois et le réutiliser est plus efficace que de créer de nouveaux objets à chaque fois.

## Étape 3 : Choisir la langue – Lire les caractères coréens

La ligne suivante indique au moteur quelle langue rechercher. Puisque notre objectif est de **lire les caractères coréens**, nous définissons `OcrLanguage.Korean`. Vous pouvez la remplacer par l'arabe, le thaï, le gujarati, etc., selon votre cas d'utilisation.

```csharp
            // Step 3: Tell the engine which language to recognize
            ocrEngine.Language = OcrLanguage.Korean; // alternatives: Arabic, Thai, Gujarati, etc.
```

**Pourquoi c’est important :** Le choix de la langue améliore considérablement la précision. Le moteur OCR utilise des dictionnaires et des modèles de caractères spécifiques à chaque langue ; lui fournir la mauvaise langue peut produire une sortie illisible.

## Étape 4 : Charger l'image pour l'OCR – Convertir l'image en texte

Avant que le moteur ne puisse faire quoi que ce soit, vous devez **charger l'image pour l'OCR**. La méthode `ImageStream.FromFile` lit le fichier dans un format que le moteur comprend.

```csharp
            // Step 4: Load the image that contains the text
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/korean_doc.png");
```

Si l'image se trouve dans un autre dossier, ajustez simplement le chemin. N'oubliez pas de définir l'*Action de génération* du fichier sur « Copy if newer » afin que l'exécutable puisse le trouver à l'exécution.

> **Erreur fréquente :** Fournir un chemin avec des barres obliques inverses (`\`) dans une chaîne littérale sans les échapper provoquera une erreur de compilation. Utilisez soit des doubles barres obliques inverses (`\\`) soit une chaîne verbatim (`@"C:\path\file.png"`).

## Étape 5 : Effectuer l'OCR – Extraire le texte d'une image

C’est maintenant le moment du travail intensif. Appeler `Recognize()` exécute l'algorithme OCR, et la propriété `Text` vous donne la chaîne brute.

```csharp
            // Step 5: Run OCR and get the recognized text
            string recognizedText = ocrEngine.Recognize().Text;
```

À ce stade, vous avez **extrait du texte d'une image** et effectivement **converti l'image en texte**. Le résultat peut contenir des caractères de nouvelle ligne si la mise en page originale comportait des sauts de ligne.

## Étape 6 : Afficher le résultat – Vérifier la sortie

Enfin, affichons le résultat dans la console afin que vous puissiez vérifier que cela a fonctionné.

```csharp
            // Step 6: Output the result to the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

Run the program:

```bash
dotnet run
```

### Sortie attendue

```
=== Recognized Text ===
안녕하세요. 이것은 OCR 테스트 문서입니다.
```

Si vous voyez des caractères coréens similaires à l'image, félicitations — vous avez maîtrisé **comment utiliser l'OCR** avec Aspose.OCR !

![Diagramme d'exemple d'utilisation de l'OCR](image.png)

*Texte alternatif de l'image : diagramme d'exemple d'utilisation de l'OCR montrant le flux du chargement d'une image à l'affichage du texte reconnu.*

## Cas limites et variantes

### 1. Gestion de plusieurs pages

Si vous devez **extraire du texte d'une image** contenant plusieurs pages (par ex., un TIFF multi‑pages), bouclez sur chaque page et appelez `Recognize()` pour chaque instance `ImageStream`.

### 2. Gestion des scans de basse qualité

Les images à basse résolution peuvent nuire à la précision. Avant d'appeler `Recognize()`, vous pouvez améliorer l'image avec les outils de prétraitement d'Aspose :

```csharp
ocrEngine.Image = ImageProcessing.Preprocess(ocrEngine.Image, ImageProcessingOptions.Deskew);
```

### 3. Changer de langue à la volée

Supposons que vous ayez un document multilingue. Vous pouvez changer `ocrEngine.Language` entre les reconnaissances :

```csharp
ocrEngine.Language = OcrLanguage.English;
string english = ocrEngine.Recognize().Text;

ocrEngine.Language = OcrLanguage.Korean;
string korean = ocrEngine.Recognize().Text;
```

### 4. Enregistrer le résultat dans un fichier

Si vous préférez **convertir l'image en texte** et le stocker, écrivez simplement la chaîne dans un fichier `.txt` :

```csharp
System.IO.File.WriteAllText("output.txt", recognizedText);
```

## FAQ

- **Ai-je besoin d'une licence pour exécuter ce code ?**  
  Non. L'essai gratuit fonctionne bien pour l'expérimentation, mais il ajoute un filigrane à la sortie. Une licence achetée supprime le filigrane et débloque les performances complètes.

- **Puis-je l'utiliser sous Linux ?**  
  Absolument. Aspose.OCR est multiplateforme ; assurez‑vous simplement d'avoir les dépendances natives requises (libgdiplus pour .NET Core sous Linux).

- **Et si mon image est dans un flux au lieu d'un fichier ?**  
  Utilisez `ImageStream.FromStream(yourStream)` — l'API accepte n'importe quel `System.IO.Stream`.

## Conclusion

Nous vous avons guidé pas à pas à travers **comment utiliser l'OCR** en C# pour **extraire du texte d'une image**, **convertir une image en texte**, et **lire les caractères coréens** tout en chargeant correctement l'image pour l'OCR. L'exemple complet et exécutable ci‑dessus devrait fonctionner immédiatement, et les conseils supplémentaires vous offrent une feuille de route pour des scénarios plus avancés.

Prêt pour le prochain défi ? Essayez de remplacer la langue par une autre, de traiter les PDF page par page, ou d'intégrer l'appel OCR dans une API web afin que les utilisateurs puissent télécharger des images et obtenir instantanément le texte. Les possibilités sont infinies, et vous disposez maintenant d'une base solide pour construire.

Bon codage!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}