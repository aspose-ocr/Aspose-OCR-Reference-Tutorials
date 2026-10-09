---
category: general
date: 2026-03-07
description: Apprenez à utiliser l’OCR en C# pour extraire du texte à partir de fichiers
  image. Ce guide montre l’OCR hors ligne, la conversion d’image en texte et le chargement
  d’image pour l’OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- convert image to text
- load image for ocr
language: fr
og_description: Comment utiliser l'OCR en C# pour extraire du texte d'images hors
  ligne. Code étape par étape, astuces et explication complète pour convertir une
  image en texte.
og_title: Comment utiliser l'OCR en C# – Guide complet hors ligne
tags:
- OCR
- C#
- Aspose
title: Comment utiliser l'OCR en C# – Extraire du texte d'images hors ligne
url: /fr/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-offline/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l'OCR en C# – Extraire du texte d'images hors ligne

Vous vous êtes déjà demandé **comment utiliser l'OCR** dans un projet .NET sans envoyer les données vers le cloud ? Vous n'êtes pas seul. De nombreux développeurs doivent *extraire du texte d'images* sur une station de travail sécurisée, et ils craignent que le trafic réseau n'expose des informations sensibles.  

Bonne nouvelle ? Avec Aspose.OCR, vous pouvez reconnaître du texte à partir de PNG, JPEG ou PDF entièrement hors ligne. Dans ce tutoriel, nous allons parcourir le chargement d'une image pour l'OCR, la configuration du moteur en mode hors ligne, et enfin **convertir une image en texte** avec seulement quelques lignes de C#.

À la fin de ce guide, vous serez capable de :

* Installer le package NuGet Aspose.OCR.  
* Configurer le moteur OCR pour le traitement hors ligne.  
* Charger une image pour l'OCR et extraire son contenu textuel.  

Aucun service externe, aucune clé API — juste du code C# pur qui s'exécute sur n'importe quelle machine Windows ou Linux.

---

## Prérequis

Avant de plonger, assurez‑vous d'avoir :

* .NET 6.0 SDK ou ultérieur (le code fonctionne également avec .NET Framework 4.7+).  
* Visual Studio 2022, VS Code, ou tout éditeur supportant C#.  
* Une copie de la bibliothèque **Aspose.OCR** – vous pouvez la récupérer depuis NuGet (`Aspose.OCR`).  
* Un dossier de ressources OCR (`Resources`) fourni avec la bibliothèque (contient les fichiers de données linguistiques).  
* Une image d'exemple (par ex. `offline_test.png`) placée dans un répertoire connu.

> **Astuce :** Conservez le dossier de ressources à côté de votre exécutable ; cela simplifie la configuration de `ResourcesPath`.

---

## Étape 1 : Installer le package NuGet Aspose.OCR

Tout d'abord, ajoutez la bibliothèque à votre projet. Ouvrez un terminal dans le dossier du projet et exécutez :

```bash
dotnet add package Aspose.OCR
```

Ou, si vous préférez l'interface Visual Studio, faites un clic droit sur **Dependencies → Manage NuGet Packages**, recherchez *Aspose.OCR*, et cliquez sur **Install**.

> L'installation du package récupère toutes les binaires nécessaires, vous n'aurez donc besoin d'aucune DLL supplémentaire.

---

## Étape 2 : Créer et configurer le moteur OCR (Comment utiliser l'OCR – Mode hors ligne)

Nous allons maintenant instancier le moteur OCR et lui indiquer de fonctionner **hors ligne**. Cela garantit qu'aucun trafic réseau ne se produit pendant la reconnaissance.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Switch the engine to offline mode – crucial for privacy‑first apps
ocrEngine.Settings.EngineMode = EngineMode.Offline;
```

**Pourquoi hors ligne ?**  
Lorsque `EngineMode` est réglé sur `Online`, le moteur contacte le cloud d'Aspose pour télécharger les packs de langues à la volée. Dans les environnements réglementés (finance, santé), ce trafic est souvent interdit. En imposant le mode hors ligne, vous garantissez que tout reste sur la machine locale.

---

## Étape 3 : Pointer le moteur vers le dossier de ressources OCR

Le moteur OCR a besoin de données linguistiques (modèles entraînés) pour reconnaître les caractères. Indiquez‑lui où ces fichiers se trouvent :

```csharp
// Replace with the absolute or relative path to your Resources folder
ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";
```

Si vous ne savez pas où se trouve le dossier, cherchez‑le dans le répertoire du package NuGet (`%USERPROFILE%\.nuget\packages\aspose.ocr\*\resources`). Copiez le dossier complet dans votre projet pour faciliter le déploiement.

---

## Étape 4 : Charger l'image pour l'OCR (Load Image for OCR)

Vous pouvez fournir au moteur n'importe quel bitmap supporté. Ici, nous chargerons un PNG stocké sur le disque :

```csharp
// Load the image you want to recognize – this is the “load image for OCR” step
ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");
```

**Astuce :** Si vous devez traiter des images depuis un flux (par ex. téléchargées via une API), utilisez `ImageStream.FromStream(yourStream)` à la place.

---

## Étape 5 : Exécuter le processus de reconnaissance et convertir l'image en texte

Une fois tout en place, déclenchez l'OCR. La méthode `Recognize()` effectue le travail lourd, et le texte extrait devient disponible via la propriété `Text`.

```csharp
// Perform OCR – this is where the engine reads the pixels and produces text
ocrEngine.Recognize();

// Grab the result – now you have “convert image to text” completed
string extractedText = ocrEngine.Text;
```

---

## Étape 6 : Afficher le texte extrait

Enfin, affichez le résultat. Dans une application console, vous pouvez simplement écrire dans la console, mais dans une API web vous renverrez la chaîne en JSON.

```csharp
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(extractedText);
```

L'exécution du programme devrait afficher le contenu textuel de `offline_test.png`. Par exemple, si l'image contient la phrase *« Hello, World! »*, vous verrez :

```
=== OCR Result ===
Hello, World!
```

---

## Exemple complet fonctionnel

Ci-dessous le programme complet, prêt à être exécuté. Copiez‑collez‑le dans un nouveau projet console (`dotnet new console`) et ajustez les chemins pour correspondre à votre environnement.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2: Set offline mode – no network traffic
        // -------------------------------------------------
        ocrEngine.Settings.EngineMode = EngineMode.Offline;

        // -------------------------------------------------
        // Step 3: Provide path to OCR resource files
        // -------------------------------------------------
        ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";

        // -------------------------------------------------
        // Step 4: Load the image you want to recognize
        // -------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");

        // -------------------------------------------------
        // Step 5: Run recognition and extract text
        // -------------------------------------------------
        ocrEngine.Recognize();
        string extractedText = ocrEngine.Text;

        // -------------------------------------------------
        // Step 6: Show the result
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

> **Sortie attendue :** La console imprime le texte exact contenu dans le fichier PNG. Si l'image est floue, le résultat peut contenir des caractères mal reconnus — consultez la section dépannage ci‑dessous.

---

## Pièges courants & astuces (Reconnaître du texte à partir de PNG efficacement)

| Problème | Pourquoi cela se produit | Comment résoudre |
|----------|--------------------------|-------------------|
| **Sortie vide** | `ResourcesPath` pointe vers le mauvais dossier ou les fichiers de langue sont manquants. | Vérifiez que le dossier contient `eng.traineddata` (ou d'autres fichiers de langue) et revérifiez la chaîne du chemin. |
| **Caractères indésirables** | La résolution de l'image est trop basse ou l'image n'est pas binarisée. | Pré‑traitez l'image (augmentez le DPI, appliquez `ImageProcessor` pour affiner). |
| **Ralentissement des performances** | Les grandes images sont traitées à pleine résolution. | Redimensionnez l'image à une largeur maximale de 2000 px avant de la fournir à l'OCR. |
| **Format non pris en charge** | Utilisation d'un BMP avec un format de pixel inhabituel. | Convertissez d'abord l'image en PNG ou JPEG (`System.Drawing.Image.Save`). |

**Astuce :** Si vous devez reconnaître plusieurs langues, définissez `ocrEngine.Settings.Language = Language.English | Language.French;` avant d'appeler `Recognize()`.

---

## Questions fréquentes

**Q : Puis-je utiliser ce code sous Linux ?**  
Absolument. Aspose.OCR est multiplateforme ; assurez‑vous simplement que les bibliothèques natives sont présentes (elles sont incluses dans le package NuGet).

**Q : Et si je n’ai pas de dossier Resources ?**  
Vous pouvez télécharger les packs de langues gratuits depuis le site d'Aspose ou les extraire du package NuGet (`.../aspose.ocr/<version>/resources`).

**Q : Existe‑t‑il un moyen d’obtenir les scores de confiance ?**  
Oui. Après `Recognize()`, inspectez `ocrEngine.RecognizedWords` – chaque mot inclut une propriété `Confidence`.

---

## Conclusion

Nous avons couvert **comment utiliser l'OCR** en C# pour *extraire du texte d'images* entièrement hors ligne. En installant Aspose.OCR, en configurant `EngineMode.Offline`, en pointant vers les ressources, en chargeant une image et en appelant `Recognize()`, vous pouvez de manière fiable **convertir une image en texte** sans jamais toucher à Internet.  

Prenez le code ci‑dessus, remplacez les chemins d’image par les vôtres, et commencez à créer des fonctionnalités comme des PDF recherchables, l’automatisation de la saisie de données ou des outils d’accessibilité. Ensuite, vous pourriez explorer **reconnaître du texte à partir de PNG** en masse, ou intégrer le moteur dans une API ASP.NET Core pour fournir les résultats OCR aux applications front‑end.

Bon codage, et n’hésitez pas à expérimenter — l'OCR est étonnamment indulgent une fois le moteur correctement configuré !

---

![Diagramme montrant le flux de travail OCR hors ligne – comment utiliser l'OCR dans un environnement sécurisé](https://example.com/ocr-workflow.png "diagramme comment utiliser l'OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}