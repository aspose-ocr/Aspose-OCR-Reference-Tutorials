---
category: general
date: 2026-03-29
description: Extraire du texte d’une image avec Aspose OCR en C#. Apprenez la rotation
  automatique OCR et comment redresser une image numérisée pour des résultats parfaits.
draft: false
keywords:
- extract text from image
- auto rotate ocr
- how to deskew scanned image
- Aspose OCR C#
- image preprocessing OCR
language: fr
og_description: Extraire du texte d’une image à l’aide d’Aspose OCR. Ce guide montre
  la reconnaissance optique de caractères avec rotation automatique et comment redresser
  une image numérisée en C#.
og_title: Extraire du texte d’une image en C# – OCR à rotation automatique et redressement
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Extraire du texte d’une image en C# – Guide de rotation automatique OCR et
  redressement
url: /fr/net/ocr-optimization/extract-text-from-image-in-c-auto-rotate-ocr-deskew-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d’une image en C# – Guide de l’OCR à rotation automatique et redressement

Vous avez déjà eu besoin d'**extraire du texte d'une image** mais le fichier était à un angle étrange ? C’est un problème fréquent—surtout lorsque vous traitez des factures numérisées, des reçus photographiés ou des PDF de travers. La bonne nouvelle, c’est que vous n’avez pas besoin d’écrire votre propre algorithme de rotation. En utilisant la fonction intégrée *auto rotate OCR* d’Aspose OCR, vous pouvez laisser le moteur redresser l’image puis **extraire du texte d’une image** en une seule étape fluide.  

Dans ce tutoriel, nous allons parcourir un programme C# complet, prêt à l’emploi, qui :

* Initialise le moteur OCR avec orientation automatique et redressement,
* Reconnaît une image tournée ou inclinée,
* Retourne à la fois l’angle de rotation détecté et le texte extrait.

Pas de services externes, pas de mathématiques compliquées—juste quelques lignes de code et une explication claire de *how to deskew scanned image* lorsque c’est nécessaire.

## Ce dont vous avez besoin

| Pré‑requis | Pourquoi c’est important |
|------------|---------------------------|
| .NET 6.0 ou version ultérieure (ou .NET Framework 4.6+) | Aspose OCR est fourni sous forme de package NuGet ciblant ces environnements d’exécution. |
| Visual Studio 2022 (ou tout éditeur C#) | Facilite l’ajout de packages NuGet et l’exécution de l’application console. |
| Une image d’exemple (`rotated_document.jpg`) | Le fichier doit être un JPEG, PNG, BMP ou TIFF qui n’est pas parfaitement vertical. |
| Package NuGet Aspose.OCR (`Install-Package Aspose.OCR`) | Fournit les classes `OcrEngine`, `PreprocessingFilters` et les types associés. |

Si vous avez coché ces cases, vous êtes prêt à partir. Sinon, récupérez la dernière version d’Aspose OCR sur NuGet—c’est une installation en un clic.

---

## Étape 1 – Initialiser le moteur OCR (Mot‑clé principal en action)

La première chose que nous faisons est de créer une instance `OcrEngine` et de lui indiquer de **auto rotate OCR** et **deskew** toute image entrante. Ces deux indicateurs sont combinés avec un OU binaire (`|`) car `PreprocessingFilters` est une énumération avec l’attribut `[Flags]`.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine with English language and preprocessing options
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Enable both auto‑rotate and auto‑deskew
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };
```

> **Pourquoi c’est important :**  
> *Auto‑rotate OCR* examine la ligne de base du texte de l’image, devine l’orientation correcte et la fait pivoter en interne avant la reconnaissance. *Auto‑deskew* fait de même pour les légères inclinaisons qui apparaissent souvent dans les documents numérisés. En activant les deux, vous garantissez les meilleurs résultats possibles d’**extraction de texte d’une image** sans retouche manuelle de l’image.

---

## Étape 2 – Reconnaître l’image et récupérer le résultat

Nous transmettons maintenant au moteur un chemin de fichier. La méthode `RecognizeImage` renvoie un objet `OcrResult` contenant l’angle de rotation détecté, les scores de confiance et le texte brut.

```csharp
        // Recognise the image file and obtain the OCR result
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/rotated_document.jpg");
```

> **Astuce :** Si vous travaillez avec un flux (par ex., un fichier téléchargé), utilisez `ocrEngine.RecognizeImage(Stream)` à la place. Les mêmes indicateurs de prétraitement s’appliquent, vous bénéficiez donc toujours des avantages du **auto rotate OCR**.

---

## Étape 3 – Afficher l’angle de rotation et le texte extrait

Enfin, nous affichons deux informations dans la console : l’angle que le moteur estime que l’image devait être tournée, et le texte réel qu’il a extrait.

```csharp
        // Show the detected rotation and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Sortie attendue** (vos chiffres différeront selon l’image d’entrée ) :

```
Detected rotation: 12.3°
----- Extracted Text -----
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Si l’image était déjà verticale, l’angle de rotation sera `0°`, et vous obtiendrez toujours un texte propre grâce à l’algorithme *auto‑deskew*.

---

## Étape 4 – Comprendre comment redresser une image numérisée (Analyse approfondie du mot‑clé secondaire)

Vous vous demandez peut‑être *how to deskew scanned image* lorsque le moteur OCR indique une rotation non nulle. En interne, Aspose OCR applique une **transformée de Hough** pour détecter l’orientation dominante des lignes de texte. Il fait ensuite pivoter le bitmap de l’inverse de cet angle, redressant ainsi le texte.

**Quand cela importe‑t‑il ?**  
* Les scanners qui alimentent le papier avec un léger angle (courant en milieu de bureau).  
* Les photos prises avec un smartphone à la main—l’horizon est rarement parfait.  

**Gestion des cas limites :**  
Si le `RotationAngle` du résultat est anormalement élevé (par ex., > 45°), le moteur a peut‑être mal interprété l’image (peut‑être un logo ou un graphique non textuel). Dans ce cas, vous pouvez :

1. Faire pivoter manuellement l’image avec `System.Drawing` avant de la transmettre au moteur, ou  
2. Désactiver `AutoRotate` et ne garder que `AutoDeskew` si vous savez que le document est déjà vertical.

```csharp
// Example: manually rotate 90° clockwise before OCR
using (var img = Aspose.OCR.Image.Load("rotated_document.jpg"))
{
    img.Rotate(90);
    OcrResult result = ocrEngine.RecognizeImage(img);
    Console.WriteLine(result.Text);
}
```

---

## Étape 5 – Pièges courants & Astuces pro (E‑E‑A‑T en action)

| Écueil | Pourquoi cela se produit | Solution |
|--------|--------------------------|----------|
| **Images floues ou basse résolution** | La précision de l’OCR chute drastiquement ; la détection de rotation peut échouer. | Utilisez des scans d’au moins 300 dpi ; appliquez un filtre de netteté avant l’OCR. |
| **Langues mixtes** | Le moteur utilise l’anglais par défaut ; les caractères étrangers deviennent illisibles. | Définissez `Language = Language.English | Language.Spanish` (ou la combinaison appropriée). |
| **Fichiers volumineux (> 10 MB)** | La pression mémoire peut provoquer `OutOfMemoryException`. | Réduisez d’abord l’image, ou traitez en tuiles avec `OcrEngine.RecognizeRegion`. |
| **Chemin de fichier incorrect** | `FileNotFoundException` arrête le programme. | Utilisez `Path.Combine(Environment.CurrentDirectory, "rotated_document.jpg")` pour plus de robustesse. |

> **Astuce pro :** Enregistrez toujours `ocrResult.RotationAngle` et `ocrResult.Confidence` (si disponible). Ces métriques vous aident à décider si une nouvelle tentative avec d’autres paramètres de prétraitement vaut le coup.

---

## Étape 6 – Étendre l’exemple (Et après ?)

Maintenant que vous pouvez **extraire du texte d’une image** avec rotation automatique et redressement, envisagez les étapes suivantes :

* **Traitement par lots** – Parcourez un dossier d’images, stockez chaque résultat dans une base de données, et signalez celles avec `RotationAngle > 5°` pour une révision manuelle.  
* **Conversion PDF** – Combinez le texte extrait avec l’image originale dans un PDF consultable à l’aide d’Aspose.PDF.  
* **Détection de langue** – Utilisez le drapeau `AutoDetectLanguage` d’Aspose.OCR pour laisser le moteur choisir automatiquement la meilleure langue.  

Chacune de ces options repose sur le même principe de base : laissez la bibliothèque gérer l’orientation, et concentrez‑vous sur la logique métier.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine with auto‑rotate and auto‑deskew
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };

        // 2️⃣ Recognise the image – replace the path with your own file
        string imagePath = "YOUR_DIRECTORY/rotated_document.jpg";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 3️⃣ Output the rotation angle and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Enregistrez le fichier sous `Program.cs`, exécutez `dotnet add package Aspose.OCR`, puis `dotnet run`. Vous devriez voir l’angle et le texte propre affichés dans la console.

---

## Conclusion

Nous venons de démontrer comment **extraire du texte d’une image** en C# tout en laissant Aspose OCR gérer *auto rotate OCR* et le problème délicat de *how to deskew scanned image*. En activant les deux indicateurs de prétraitement, le moteur redresse automatiquement les images de travers, détecte l’orientation correcte et fournit un texte précis—sans retouche manuelle de l’image.

N’hésitez pas à expérimenter avec des lots plus importants, différentes langues, ou même à intégrer la sortie dans un PDF consultable. Le ciel est la limite une fois que le moteur OCR s’occupe du gros du travail.

**Prêt à faire passer votre pipeline de documents au niveau supérieur ?** Prenez le code, pointez‑le sur vos propres numérisations, et voyez les angles de rotation disparaître. Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous—bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}