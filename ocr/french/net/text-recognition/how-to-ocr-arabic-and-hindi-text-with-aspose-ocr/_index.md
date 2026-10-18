---
category: general
date: 2026-01-15
description: Apprenez à OCR le texte arabe et à reconnaître le texte hindi à l'aide
  d'Aspose OCR. Ce guide étape par étape vous montre comment extraire le texte d’une
  image et convertir une image en texte efficacement.
draft: false
keywords:
- how to ocr arabic
- recognize arabic text
- extract text from image
- convert image to text
- recognize hindi text
language: fr
og_description: Comment effectuer la reconnaissance OCR du texte arabe et reconnaître
  le texte hindi dans un seul programme C#. Suivez ce guide complet pour extraire
  le texte d’une image et convertir l’image en texte.
og_title: Comment effectuer l'OCR du texte arabe et hindi avec Aspose OCR
tags:
- Aspose OCR
- C#
- Multilingual OCR
title: Comment OCR le texte arabe et hindi avec Aspose OCR
url: /fr/net/text-recognition/how-to-ocr-arabic-and-hindi-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# comment faire de l'ocr arabe et hindi avec Aspose OCR

Vous vous êtes déjà demandé **comment faire de l'ocr arabe** sur des caractères qui s'écrivent de droite à gauche, tout en extrayant les glyphes hindi d'un reçu ? Vous n'êtes pas seul. De nombreux développeurs rencontrent le même problème lorsqu'ils doivent **reconnaître du texte arabe** et **reconnaître du texte hindi** dans le même flux de travail.  

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable en C# qui vous montre comment **extraire du texte d'une image**, **convertir une image en texte**, et gérer à la fois les scripts arabe et hindi avec Aspose OCR. Pas de références vagues — uniquement le code que vous pouvez copier‑coller, ainsi que le raisonnement derrière chaque ligne.

> **Astuce :** Si vous n’avez jamais utilisé Aspose OCR auparavant, installez d’abord le package NuGet `Aspose.OCR`. C’est une opération en un clic dans Visual Studio, et cela récupère toutes les bibliothèques natives dont vous avez besoin pour la reconnaissance basée sur le CPU.

---

![exemple d'ocr arabe](/images/arabic-ocr-sample.png "ocr arabe – exemple de signe arabe")

*Texte alternatif de l'image :* **ocr arabe – exemple de signe arabe**  

---

## comment faire de l'ocr arabe – configuration de l'environnement

Avant de plonger dans le code, assurons‑nous que l’environnement de développement est prêt.

1. **Target framework** – .NET 6.0 ou ultérieur. Une version plus ancienne compilera encore, mais vous manquerez les dernières fonctionnalités du langage.  
2. **Package** – Exécutez `dotnet add package Aspose.OCR` dans le terminal, ou utilisez l’interface du Gestionnaire de packages NuGet.  
3. **Images** – Placez deux images d’exemple dans un dossier que vous pouvez référencer, par ex. `C:\OCRSamples\arabic_sign.jpg` et `C:\OCRSamples\hindi_receipt.png`. L’image arabe doit contenir des caractères arabes clairs et à fort contraste ; l’image hindi peut être un reçu numérisé ou une photographie d’un panneau.  

C’est tout — pas de fichiers de configuration supplémentaires, pas de pilotes GPU, juste un moteur OCR simple basé sur le CPU.

---

## Reconnaître le texte arabe – chargement et traitement

Nous allons maintenant réellement **reconnaître le texte arabe**. L’essentiel est d’indiquer au moteur la langue attendue ; sinon le moteur utilise par défaut les caractères latins et vous obtiendrez une sortie illisible.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class MultiLangDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine (CPU‑based by default)
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load an image that contains Arabic script
        var arabicImage = OcrImage.FromFile(@"C:\OCRSamples\arabic_sign.jpg");

        // 3️⃣ Recognize the Arabic text – note the Language.Arabic enum
        var arabicResult = ocrEngine.Recognize(arabicImage, Language.Arabic);

        // 4️⃣ Print the result to the console
        System.Console.WriteLine("Arabic: " + arabicResult.Text);
```

**Pourquoi cela fonctionne :**  
* `OcrEngine` gère toute la lourde tâche — pré‑traitement, segmentation et classification des caractères.  
* En passant `Language.Arabic`, nous activons le moteur de mise en page de droite à gauche et le jeu de caractères arabe. Sans cela, le moteur traiterait l’image comme du texte latin de gauche à droite, ce qui entraîne des diacritiques manquantes et des mots tronqués.  

**Sortie attendue** (votre texte réel différera selon l’image) :

```
Arabic: مرحبا بكم في متجرنا
```

Si vous voyez des chaînes vides, vérifiez que l’image n’est pas trop sombre et que le chemin du fichier est correct.  

---

## extraire du texte d'une image – gestion des scripts de droite à gauche

L’arabe n’est pas le seul script nécessitant une prise en charge spéciale. Les langues de droite à gauche (RTL) exigent que le moteur OCR inverse l’ordre visuel après la reconnaissance. Aspose le fait automatiquement lorsque vous spécifiez `Language.Arabic`, mais cela vaut la peine d’être noté pour de futures extensions (par ex., l’hébreu).

*Astuce :* Lorsque vous afficherez plus tard le résultat OCR dans une interface, assurez‑vous que le contrôle prend en charge le rendu RTL ; sinon le texte apparaîtra brouillé.

---

## convertir une image en texte – travailler avec le hindi

Changeons de sujet, et **convertissons une image en texte** pour un reçu en hindi. Le processus reflète le flux arabe, mais nous utilisons `Language.Hindi` à la place.

```csharp
        // 5️⃣ Load the Hindi (Devanagari) image
        var hindiImage = OcrImage.FromFile(@"C:\OCRSamples\hindi_receipt.png");

        // 6️⃣ Recognize Hindi text – Language.Hindi tells the engine to use Devanagari models
        var hindiResult = ocrEngine.Recognize(hindiImage, Language.Hindi);

        // 7️⃣ Output the Hindi OCR result
        System.Console.WriteLine("Hindi: " + hindiResult.Text);
    }
}
```

**Pourquoi nous réutilisons la même instance `ocrEngine` :** Créer un nouveau moteur pour chaque langue gaspillerait de la mémoire et du temps d’initialisation. Le moteur d’Aspose est sûr pour les appels séquentiels, donc le réutiliser est à la fois efficace et propre.

**Exemple de sortie console** (encore une fois, dépend de votre image) :

```
Hindi: कुल राशि: ₹ 1,250.00
```

Si le texte hindi apparaît comme des caractères latins illisibles, vous avez probablement omis l’énumération de langue ou la résolution de l’image est trop basse (<300 dpi). Augmenter la taille de l’image ou appliquer un filtre de binarisation simple peut améliorer considérablement la précision.

---

## reconnaître le texte hindi – pièges courants et cas limites

Même avec le bon indicateur de langue, quelques problèmes peuvent vous surprendre :

| Problème | Symptôme | Solution |
|----------|----------|----------|
| Faible contraste | De nombreux caractères deviennent « ? » ou sont omis | Pré‑traiter avec `OcrImage.AdjustContrast(1.5)` |
| Image inclinée | Le texte apparaît tourné, l’OCR renvoie une chaîne vide | Appeler `ocrEngine.PreprocessImage(arabicImage, ImageProcessingOptions.Rotate)` |
| Langues mixtes | Ligne arabe suivie de nombres anglais | Effectuer deux passes : d’abord avec `Language.Arabic`, puis avec `Language.English` sur la même image et concaténer les résultats |
| Taille de fichier importante | Reconnaissance lente ou erreurs de mémoire insuffisante | Redimensionner à une largeur maximale de 2000 px avec `OcrImage.Resize(2000, 0)` |

Ces astuces vous aident à **extraire du texte d'une image** qui n’est pas parfaitement numérisée, ce qui est courant dans les projets réels.

---

## Assemblage complet – exemple fonctionnel complet

Voici le programme complet que vous pouvez copier directement dans un nouveau projet console. Pas de dépendances cachées, pas de configuration supplémentaire—juste du C# pur.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class MultiLangDemo
{
    static void Main()
    {
        // Initialize the OCR engine (CPU‑based)
        var ocrEngine = new OcrEngine();

        // -------------------- Arabic --------------------
        var arabicPath = @"C:\OCRSamples\arabic_sign.jpg";
        var arabicImage = OcrImage.FromFile(arabicPath);
        var arabicResult = ocrEngine.Recognize(arabicImage, Language.Arabic);
        System.Console.WriteLine("Arabic: " + arabicResult.Text);

        // -------------------- Hindi --------------------
        var hindiPath = @"C:\OCRSamples\hindi_receipt.png";
        var hindiImage = OcrImage.FromFile(hindiPath);
        var hindiResult = ocrEngine.Recognize(hindiImage, Language.Hindi);
        System.Console.WriteLine("Hindi: " + hindiResult.Text);
    }
}
```

**Exécuter le programme** affichera les chaînes arabes et hindi dans la console, confirmant que vous avez réussi à **reconnaître le texte arabe** et **reconnaître le texte hindi** en une seule exécution.  

---

## Conclusion

Vous disposez maintenant d’une réponse solide, de bout en bout, à la question **comment faire de l'ocr arabe** tout en gérant le hindi. En créant une seule instance `OcrEngine`, en chargeant chaque image et en passant l’énumération `Language` appropriée, vous pouvez **extraire du texte d'une image**, **convertir une image en texte**, et **reconnaître le texte arabe** ainsi que **reconnaître le texte hindi** sans bibliothèques supplémentaires.  

À partir d’ici, vous pourriez explorer :

* **Traitement par lots** – parcourir un dossier d’images et stocker les résultats dans une base de données.  
* **Post‑traitement** – utiliser des expressions régulières pour nettoyer les symboles monétaires dans les reçus hindi.  
* **Détection hybride de langue** – fournir le bitmap brut à un modèle d’identification de langue avant de choisir l’énumération.  

Essayez, ajustez les étapes de pré‑traitement, et vous verrez la précision de l’OCR augmenter rapidement. Si vous rencontrez des particularités, déposez

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}