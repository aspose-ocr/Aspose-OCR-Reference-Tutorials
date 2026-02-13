---
category: general
date: 2026-02-13
description: Comment utiliser l'OCR en C# pour extraire du texte d’une image, reconnaître
  le texte d’une photo ou d’un JPG, et exécuter l’OCR sur une image sans internet.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: fr
og_description: Comment utiliser l'OCR en C# pour extraire du texte d’une image, reconnaître
  le texte d’une photo et exécuter l’OCR sur une image avec un exemple complet et
  exécutable.
og_title: Comment utiliser l'OCR en C# – Extraire du texte d'une image
tags:
- OCR
- C#
- Image Processing
title: Comment utiliser l’OCR en C# – Extraire du texte d’une image et reconnaître
  le texte d’une photo
url: /fr/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l’OCR en C# – Extraire du texte d’une image et reconnaître du texte à partir d’une photo

Vous vous êtes déjà demandé **comment utiliser l’OCR** pour extraire des mots d’une capture d’écran, d’un reçu numérisé ou d’une photo prise avec votre téléphone ? Vous n’êtes pas seul. Dans de nombreuses applications réelles, il faut transformer des images en texte interrogeable, et le faire localement—sans dépendre d’une connexion Internet instable—peut parfois sembler un vrai casse‑tête.

C’est pourquoi ce guide vous montre, étape par étape, comment **extraire du texte d’une image** à l’aide d’un moteur OCR en C#, et il couvre également comment **reconnaître du texte à partir d’une photo**, **reconnaître du texte à partir d’un JPG**, et **exécuter l’OCR sur des images** stockées directement sur votre disque. À la fin, vous disposerez d’un programme complet, prêt à copier‑coller, qui fonctionne immédiatement.

## Ce que vous allez apprendre

- Comment configurer un moteur OCR pour le chinois simplifié (ou toute autre langue que vous ajoutez).  
- Le code exact nécessaire pour **charger des ressources** depuis un dossier local—sans aucun appel réseau.  
- Comment **reconnaître du texte à partir d’une photo** (JPEG, PNG ou BMP).  
- Astuces pour gérer les cas limites courants comme les fichiers de modèle manquants ou les formats d’image non pris en charge.  
- Un exemple complet, exécutable, que vous pouvez placer dans Visual Studio et voir les résultats instantanément.

### Prérequis

- .NET 6.0 ou supérieur (l’API utilisée cible .NET Standard 2.0, donc les versions antérieures fonctionnent aussi).  
- Une connaissance de base du C# et de Visual Studio (ou tout autre IDE de votre choix).  
- La bibliothèque OCR que vous utilisez (l’extrait suppose une classe fictive `OcrEngine` fournie avec des modèles linguistiques).  
- Un dossier contenant les fichiers de modèle linguistique requis—considérez‑le comme le “cerveau” que le moteur utilise pour lire les caractères chinois.

> **Astuce pro :** Si vous n’avez pas encore les fichiers de modèle chinois, téléchargez‑les une fois depuis le site du fournisseur et placez‑les dans un dossier comme `C:\OcrResources`. Le moteur n’aura plus jamais besoin d’aller en ligne.

---

![Diagram showing OCR process on a photo](path/to/ocr-diagram.png "Diagram showing OCR process on a photo")

## Comment utiliser l’OCR : configurer le moteur

La première chose dont vous avez besoin est une instance du moteur OCR, configurée pour la langue qui vous intéresse. Dans ce tutoriel nous ciblons le **chinois simplifié**, mais remplacer `OcrLanguage.ChineseSimplified` par `OcrLanguage.English` (ou toute autre valeur d’énumération) ne nécessite qu’une ligne de code.

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**Pourquoi c’est important :**  
Définir la propriété `Language` indique au moteur quel jeu de caractères il doit attendre. Le `ResourceFolder` indique où le moteur cherche les poids du réseau neuronal et les dictionnaires de langue—c’est la mémoire du cerveau. Si vous pointez vers le mauvais dossier, le moteur lèvera une `FileNotFoundException` et vous serez bloqué.

## Extraire du texte d’une image – charger les ressources

Avant que le moteur ne puisse réellement lire quoi que ce soit, vous devez charger ces fichiers de modèle en mémoire. Cette étape est **cruciale** car elle évite un appel réseau à chaque traitement d’image.

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**Que pourrait‑il se passer ?**  
Si le chemin du dossier est incorrect ou si les fichiers sont corrompus, `LoadResources()` lèvera une exception. Le bloc `try/catch` ci‑dessus montre comment gérer les erreurs de façon élégante—une pratique courante en production.

## Reconnaître du texte à partir d’une photo – exécuter l’OCR

Place maintenant la partie amusante : fournir un fichier image au moteur et récupérer le texte reconnu. C’est le cœur des scénarios **exécuter l’OCR sur image**, que l’image soit un JPEG, un PNG ou même un BMP.

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

La méthode `RecognizeImage` renvoie un `RecognitionResult` (ou quel que soit le nom utilisé dans votre SDK) qui contient généralement :

- `Text` – la transcription en texte brut.  
- `Confidence` – un score numérique indiquant le degré de certitude du moteur pour chaque ligne.  
- `BoundingBoxes` – coordonnées optionnelles indiquant où chaque mot se situe sur l’image.

**Pourquoi la confiance peut vous intéresser :**  
Si vous construisez un outil d’automatisation de saisie de données, vous pouvez définir un seuil (par ex. 0,85) et demander à l’utilisateur de confirmer les lignes à faible confiance. Cela améliore considérablement la précision globale.

## Reconnaître du texte à partir d’un JPG – gérer différents formats

Beaucoup de développeurs pensent que l’OCR ne fonctionne qu’avec les PNG, mais les moteurs modernes traitent très bien les fichiers **JPG**. Le seul hic, c’est que la compression JPEG peut introduire des artefacts qui perturbent le modèle.

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

Si vous n’avez pas de fonction d’aide `DenoiseAndDeskew`, de nombreuses bibliothèques (par ex. OpenCvSharp) offrent ces fonctionnalités. L’idée principale : **exécuter l’OCR sur image** après un petit nettoyage si les fichiers proviennent d’un scanner ou d’un appareil photo mobile.

## Exécuter l’OCR sur image – conseils, cas limites et bonnes pratiques

### 1. Gestion de la mémoire
Charger de gros modèles linguistiques peut consommer plusieurs centaines de mégaoctets. Libérez le moteur lorsque vous avez fini :

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. Traitement par lots
Si vous devez traiter des dizaines de photos, chargez les ressources une fois, puis bouclez :

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. Scénarios multilingues
Vous pouvez changer de langue à la volée en réaffectant `ocrEngine.Language` et en rappelant `LoadResources()`. Attention toutefois au temps de chargement supplémentaire.

### 4. Gestion des résultats vides
Parfois le moteur renvoie une chaîne vide. Cela signifie généralement que l’image est trop floue ou que la couleur du texte se fond dans l’arrière‑plan. Un contrôle rapide :

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. Considérations de sécurité
Ne jamais injecter directement des fichiers téléchargés par l’utilisateur dans le moteur OCR sans validation. Au minimum, vérifiez l’extension et la taille du fichier, et envisagez une analyse anti‑malware.

---

## Exemple complet fonctionnel

Voici un programme autonome que vous pouvez copier dans un nouveau projet Console App. Il montre **comment utiliser l’OCR**, **extraire du texte d’une image**, **reconnaître du texte à partir d’une photo**, **reconnaître du texte à partir d’un JPG**, et **exécuter l’OCR sur image**—le tout en une seule fois.

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**Sortie attendue (exemple) :**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

Votre texte réel variera selon le contenu de l’image, mais vous devriez voir un bloc de caractères Unicode affiché dans la console accompagné d’un pourcentage de confiance.

---

## Conclusion

Nous avons parcouru **comment utiliser l’OCR** en C# du début à la fin — configuration du moteur, chargement des ressources linguistiques, puis **reconnaissance du texte à partir d’une photo** ou d’un **JPG** sans jamais toucher à Internet. En suivant les étapes ci‑dessus, vous pouvez **extraire du texte d’une image**, **exécuter l’OCR sur image**, et gérer les pièges les plus courants qui bloquent les débutants.

Prêt pour le prochain défi ? Essayez de faire analyser au moteur une page PDF convertie en image, ou expérimentez avec un autre pack linguistique pour voir comment les scores de confiance évoluent. Vous pourriez

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}