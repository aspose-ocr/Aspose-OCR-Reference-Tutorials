---
category: general
date: 2026-02-14
description: Chargez le fichier image et extrayez le texte du reçu à l'aide du moteur
  OCR GPU d'Aspose. Apprenez à définir la mémoire GPU maximale, à configurer la mémoire
  GPU et à exécuter l'OCR sur l'image de manière efficace.
draft: false
keywords:
- load image file
- extract text from receipt
- set max gpu memory
- run OCR on image
- configure gpu memory
language: fr
og_description: Chargez le fichier image et extrayez le texte du reçu à l'aide du
  moteur OCR GPU d'Aspose. Ce guide montre comment définir la mémoire GPU maximale
  et exécuter l'OCR sur une image en C#.
og_title: Charger un fichier image et extraire le texte du reçu avec OCR GPU en C#
tags:
- C#
- OCR
- Aspose
- GPU
title: Charger un fichier image & extraire le texte du reçu avec OCR GPU en C#
url: /fr/net/ocr-configuration/load-image-file-extract-receipt-text-with-gpu-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Charger un fichier image et extraire le texte d'un reçu avec OCR GPU en C#

Vous avez déjà eu besoin de **load image file** et d'extraire le texte exact d'un reçu mais vous êtes resté bloqué à l'étape OCR ? Vous n'êtes pas le seul. Dans de nombreuses applications réelles — suiveurs de dépenses, systèmes d'inventaire, ou même de simples bots de numérisation de reçus — la capacité de lire rapidement une image de reçu peut changer la donne.  

Bonne nouvelle ? Avec le moteur accéléré par GPU d’Aspose.OCR, vous pouvez **load image file**, **set max GPU memory**, et **run OCR on image** en quelques lignes de C#. Ci-dessous, nous parcourrons l’ensemble du processus, de la configuration du GPU à l’affichage du texte brut extrait.

## Ce que vous allez apprendre

* **Load image file** depuis le disque en utilisant `ImageStream` d’Aspose.
* **Configure GPU memory** afin que le moteur ne consomme jamais plus de RAM que vous ne le permettez.
* **Run OCR on image** et extraire chaque caractère d’un reçu.
* Gérer les pièges courants — comme les erreurs out‑of‑memory ou les scans flous.
* Vérifier la sortie et ajuster les paramètres pour une meilleure précision.

Pas de services externes, pas d'astuces obscures — juste du code C# pur que vous pouvez intégrer dans n'importe quel projet .NET 6+.

---

## Prérequis

Avant de plonger, assurez‑vous d’avoir :

* .NET 6 SDK ou version ultérieure installé.
* Une licence Aspose.OCR valide (ou vous pouvez utiliser le mode d'évaluation gratuit).
* Les packages NuGet `Aspose.OCR` et `Aspose.OCR.Gpu` ajoutés à votre projet.
* Une image de reçu d'exemple (`receipt.png`) prête sur le disque.

Si l'un de ces éléments vous est inconnu, faites une pause et installez les packages :

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

C’est tout — aucune bibliothèque native supplémentaire n’est requise car le support GPU est intégré directement dans le package NuGet.

---

## Charger le fichier image et préparer le moteur GPU

La première chose à faire est de **load image file** dans un `ImageStream`. Cet objet abstrait les détails du système de fichiers et fournit au moteur OCR une représentation propre, en mémoire.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Step 1️⃣: Initialize the GPU‑accelerated engine.
var gpuEngine = new GpuEngine
{
    // Step 2️⃣: Set a safety net for GPU RAM usage.
    // Here we limit the engine to 1024 MB (1 GB). Adjust as needed.
    MaxDeviceMemory = 1024 // MB
};

// Step 3️⃣: Load the receipt image from disk.
var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

// At this point the image is ready for OCR.
```

**Pourquoi c’est important :**  
*Loading the image file* via `ImageStream.FromFile` garantit que le moteur voit les données de pixels exactes, en préservant le DPI et la profondeur de couleur. Ignorer cette étape ou fournir un flux corrompu entraînera des caractères manquants ou des exceptions dans l’OCR.

> **Astuce :** Si vous traitez des fichiers téléchargés par les utilisateurs, encapsulez l’appel `FromFile` dans un bloc try‑catch et validez d'abord la taille du fichier. Les images volumineuses peuvent saturer la mémoire GPU si vous n’avez pas **configured GPU memory** correctement.

---

## Définir la mémoire GPU maximale pour des performances optimales

Les ressources GPU sont précieuses, surtout sur les serveurs partagés ou les ordinateurs portables avec une VRAM limitée. La propriété `MaxDeviceMemory` indique à Aspose la quantité de mémoire GPU qu’il peut allouer en toute sécurité.

```csharp
// Example: Restrict to 512 MB for low‑end GPUs.
gpuEngine.MaxDeviceMemory = 512; // MB
```

Lorsque vous **set max GPU memory**, le moteur reviendra automatiquement au traitement CPU s’il ne peut pas satisfaire la demande — évitant ainsi les plantages. C’est la façon la plus sûre de **configure GPU memory** sans coder en dur des limites spécifiques à l’appareil.

**Quand ajuster :**  
* Si vous remarquez une `OutOfMemoryException` lors d’un traitement par lots intensif, réduisez la limite.  
* Si vos reçus sont haute résolution (300 DPI+), augmentez‑la à 2 GB pour maintenir une vitesse élevée.

---

## Exécuter l’OCR sur l’image pour extraire le texte du reçu

Passons à la partie amusante — réellement **run OCR on image** et extraire le texte du reçu. La méthode `Recognize` renvoie un objet `OcrResult` qui contient une propriété `Text` avec le texte brut.

```csharp
// Step 4️⃣: Perform OCR.
OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

// Step 5️⃣: Output the extracted text.
Console.WriteLine("=== Receipt Text ===");
Console.WriteLine(ocrResult.Text);
```

La console affichera quelque chose comme :

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

**Pourquoi cela fonctionne :**  
Le moteur GPU exécute un modèle d’apprentissage profond entraîné sur une variété de mises en page de documents. En fournissant une image propre et correctement chargée, vous donnez au modèle les meilleures chances d’**extract text from receipt** avec précision.

---

## Vérifier la sortie et les pièges courants

Même avec un moteur puissant, l’OCR n’est pas magique. Voici quelques points à surveiller :

| Problème | Cause | Solution |
|----------|-------|----------|
| Caractères brouillés | Faible contraste ou image floue | Pré‑traiter avec `ImageProcessor` d’Aspose pour augmenter le contraste |
| Lignes manquantes | Image trop découpée | S’assurer que le reçu tient entièrement dans les limites de l’image |
| Erreurs de mémoire | `MaxDeviceMemory` trop faible pour la taille de l’image | Augmenter `MaxDeviceMemory` ou réduire la taille de l’image d’abord |
| Mauvaise langue | Le reçu contient du texte non anglais | Définir `gpuEngine.Language = OcrLanguage.Spanish;` (ou approprié) |

Si vous rencontrez l’un de ces problèmes, la solution rapide consiste à redimensionner l’image à moins de 2000 px sur le côté le plus long — cela réduit considérablement la charge GPU sans sacrifier la lisibilité pour la plupart des reçus.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet, prêt à être compilé. Remplacez le chemin du fichier par l’emplacement de votre propre reçu.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class ReceiptOcrDemo
{
    static void Main()
    {
        // 1️⃣ Create GPU‑accelerated engine with a safe memory cap.
        var gpuEngine = new GpuEngine
        {
            MaxDeviceMemory = 1024 // MB – adjust for your hardware
        };

        // 2️⃣ Load the receipt image from disk.
        //    Make sure the path points to a valid PNG/JPEG file.
        var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

        // 3️⃣ Run OCR – this will automatically use the GPU if available.
        OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

        // 4️⃣ Print the extracted text.
        Console.WriteLine("=== Receipt Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Sortie console attendue** (votre reçu différera, bien sûr) :

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

Exécutez le programme avec `dotnet run`. Si le texte s’affiche, félicitations — vous avez réussi à **load image file**, **set max GPU memory**, et **run OCR on image** pour **extract text from receipt**.

---

## Questions fréquentes

**Q : Cela fonctionne-t-il sur des machines sans GPU dédié ?**  
R : Oui. Aspose.OCR reviendra élégamment en mode CPU si aucun GPU compatible n’est détecté. Vous pourrez toujours **load image file** et **run OCR on image**, mais un peu plus lentement.

**Q : Puis‑je traiter plusieurs reçus en lot ?**  
R : Absolument. Encapsulez le code de reconnaissance dans une boucle `foreach`, mais n’oubliez pas de réutiliser la même instance `GpuEngine` — cela évite de réinitialiser les ressources GPU pour chaque fichier.

**Q : Et si mon reçu est dans une langue autre que l’anglais ?**  
R : Définissez la langue avant d’appeler `Recognize` :

```csharp
gpuEngine.Language = OcrLanguage.French;
```

---

## Prochaines étapes et sujets connexes

Maintenant que vous avez maîtrisé les bases, envisagez d’explorer :

* **Fine‑tuning OCR accuracy** – expérimentez avec `gpuEngine.RecognitionOptions` comme `EnableDeskew` ou `ContrastEnhancement`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}