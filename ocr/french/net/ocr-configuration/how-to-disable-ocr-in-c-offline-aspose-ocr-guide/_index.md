---
category: general
date: 2026-04-11
description: Apprenez comment désactiver l'OCR dans Aspose OCR pour C# afin de le
  faire fonctionner hors ligne, extraire du texte d'une image sans connexion Internet
  et charger correctement l'image pour l'OCR.
draft: false
keywords:
- how to disable OCR
- extract text from image
- load image for OCR
- offline OCR C#
- Aspose OCR resources
language: fr
og_description: Comment désactiver l’OCR dans Aspose OCR pour C#, l’exécuter hors
  ligne, extraire le texte d’une image sans connexion Internet et charger facilement
  une image pour l’OCR.
og_title: Comment désactiver l’OCR en C# – Guide hors ligne Aspose OCR
tags:
- C#
- OCR
- Aspose
- Offline Processing
title: Comment désactiver l’OCR en C# – Guide hors ligne d’Aspose OCR
url: /fr/net/ocr-configuration/how-to-disable-ocr-in-c-offline-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment désactiver l'OCR en C# – Guide hors ligne Aspose OCR

Vous vous êtes déjà demandé **comment désactiver l'OCR** lorsque vous avez besoin d'une solution réellement hors ligne ? Peut‑être que vous créez une application de bureau sécurisée qui ne peut pas dépendre d'une connexion réseau, ou que vous voulez simplement éviter les téléchargements inattendus. Quoi qu'il en soit, la bonne nouvelle est qu'Aspose OCR vous permet de désactiver la récupération automatique des ressources, de la pointer vers un dossier local, et de tout garder sur site. Dans ce tutoriel, vous verrez également comment **extraire du texte d'une image** et correctement **charger l'image pour l'OCR** sans aucun problème.

Nous parcourrons un exemple complet, prêt à l'exécution, qui montre chaque étape — de l'initialisation du moteur à l'affichage du texte japonais reconnu. Aucun document externe, aucune magie cachée ; juste du code C# simple que vous pouvez intégrer à votre projet dès aujourd'hui. À la fin, vous comprendrez pourquoi désactiver la fonction de téléchargement automatique est important, comment définir le chemin des ressources, et quels pièges éviter.

## Prérequis

- .NET 6.0 (ou toute version récente de .NET) installé sur votre machine.  
- Package NuGet Aspose.OCR pour .NET (`Install-Package Aspose.OCR`).  
- Un dossier contenant déjà les ressources linguistiques dont vous avez besoin (par ex., le modèle japonais).  
- Un fichier image (`japan_doc.png`) sur lequel vous souhaitez exécuter l'OCR.  

Si vous ne disposez pas des packs de langues, récupérez‑les depuis le portail Aspose une fois, décompressez‑les dans un dossier comme `AsposeOCRResources`, et le tour est joué. Aucun téléchargement supplémentaire ne sera effectué une fois que vous avez désactivé la fonction de téléchargement automatique.

![Comment désactiver l'OCR hors ligne](/images/how-to-disable-ocr.png "illustration de la désactivation de l'OCR")

## Étape 1 – Créer l'instance du moteur OCR  

La première chose à faire est d'instancier `OcrEngine`. Considérez cet objet comme le cerveau qui lira votre image.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pourquoi c'est important :** Sans moteur, vous ne pouvez rien configurer. L'objet contient tous les paramètres, y compris le drapeau crucial qui indique à la bibliothèque si elle peut se connecter à Internet.

## Étape 2 – Désactiver le téléchargement automatique des ressources  

Par défaut, Aspose OCR tentera de récupérer les fichiers de langue manquants à la volée. Pour tout garder hors ligne, basculez le commutateur `AutoDownloadResources` sur `false`.

```csharp
        // Step 2: Disable automatic resource download to work offline
        ocrEngine.Settings.AutoDownloadResources = false;
```

> **Astuce :** Désactiver cela garantit non seulement la confidentialité, mais accélère également la première exécution de reconnaissance car le moteur ne perdra pas de temps à vérifier les mises à jour.

## Étape 3 – Pointer vers votre dossier de ressources local  

Indiquez maintenant au moteur où se trouvent les packs de langues pré‑téléchargés. C’est le chemin que vous avez configuré dans les prérequis.

```csharp
        // Step 3: Point the engine to the folder containing pre‑downloaded resources
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";
```

> **Qu'est‑ce qui pourrait mal se passer ?** Si le chemin est incorrect ou que le fichier de langue requis est manquant, le moteur lèvera une `ResourceNotFoundException`. Vérifiez l'orthographe du dossier et que le modèle japonais (`jpn.traineddata`) est présent.

## Étape 4 – Sélectionner le modèle de langue local  

Choisissez la langue que vous avez réellement sur le disque. Dans notre exemple, nous utilisons le japonais, mais vous pouvez remplacer `Language.Japanese` par n'importe quelle autre langue que vous avez téléchargée.

```csharp
        // Step 4: Select the language model that is available locally
        ocrEngine.Settings.Language = Language.Japanese;
```

> **Cas particulier :** Certaines langues nécessitent des dictionnaires supplémentaires (par ex., le chinois). Assurez‑vous que ces fichiers auxiliaires se trouvent également dans le même dossier de ressources.

## Étape 5 – Charger l'image pour l'OCR  

C’est ici que nous **chargeons l'image pour l'OCR**. La méthode `ImageStream.FromFile` lit le fichier dans un flux que Aspose peut traiter.

```csharp
        // Step 5: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/japan_doc.png");
```

> **Conseil :** Les formats pris en charge incluent PNG, JPEG, BMP et TIFF. Si vous devez gérer des PDF, convertissez chaque page en image d'abord.

## Étape 6 – Exécuter le processus de reconnaissance  

Le moteur lit maintenant réellement les pixels et tente de les transformer en texte.

```csharp
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Pourquoi cette étape peut être lente :** L'OCR est gourmand en CPU, surtout pour les images haute résolution. Si les performances sont un problème, envisagez de réduire la taille de l'image avant la reconnaissance.

## Étape 7 – Afficher le texte extrait  

Enfin, nous **extrayons du texte d'une image** et l'affichons dans la console.

```csharp
        // Step 7: Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

L'exécution du programme devrait afficher les caractères japonais présents dans `japan_doc.png`. Si tout est correctement configuré, vous verrez un bloc propre de texte Unicode dans votre console.

### Sortie attendue

```
これはサンプルの日本語テキストです。
```

(Votre sortie réelle dépendra du contenu de l'image.)

## Problèmes courants & comment les éviter  

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Fichier de langue manquant** | `AutoDownloadResources` est false, donc le moteur ne peut pas le récupérer. | Vérifiez que `ResourcesPath` pointe vers le dossier contenant `jpn.traineddata`. |
| **Chemin d'image incorrect** | `ImageStream.FromFile` lève `FileNotFoundException`. | Utilisez des chemins absolus ou assurez‑vous que le répertoire de travail est correctement défini. |
| **Format d'image non pris en charge** | Aspose ne lit que certains formats. | Convertissez votre image en PNG ou JPEG avant d'appeler `FromFile`. |
| **Manque de mémoire sur les grandes images** | L'OCR charge l'image entière en mémoire. | Redimensionnez ou découpez l'image, ou augmentez la limite de mémoire du processus. |

## Étendre l'exemple  

- **Traitement par lots :** Parcourez un répertoire d'images, appelez le même code de reconnaissance, et écrivez chaque résultat dans un fichier `.txt` séparé.  
- **Langues différentes :** Remplacez `Language.Japanese` par `Language.English` (ou toute autre) après avoir placé les fichiers de ressources correspondants.  
- **Prétraitement personnalisé :** Utilisez Aspose.Imaging pour redresser ou améliorer le contraste avant l'OCR afin d'obtenir une meilleure précision.

## Conclusion  

Vous savez maintenant **comment désactiver l'OCR** dans Aspose OCR pour C# et l'exécuter complètement hors ligne. En définissant `AutoDownloadResources` sur `false`, en pointant le moteur vers un dossier de ressources local, et en **chargeant correctement l'image pour l'OCR**, vous pouvez **extraire du texte d'une image** de manière fiable sans jamais toucher à Internet. Cette approche est idéale pour les environnements sécurisés, les pipelines CI, ou tout scénario où l'accès réseau est limité.

Prêt pour l'étape suivante ? Essayez de traiter un dossier complet de PDF numérisés, expérimentez avec différents packs de langues, ou intégrez le résultat OCR dans une base de données consultable. La configuration hors ligne que vous avez créée aujourd'hui constitue une base solide pour tout flux de travail de traitement de documents sur site.

Bon codage, et n'hésitez pas à laisser un commentaire si vous rencontrez des problèmes !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}