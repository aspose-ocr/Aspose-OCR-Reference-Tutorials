---
category: general
date: 2026-03-21
description: 'Tutoriel C# OCR : Apprenez à extraire du texte ourdou d’une image PNG
  à l’aide de l’OCR en C#. Code pas à pas, configuration de la langue et conseils
  pratiques inclus.'
draft: false
keywords:
- c# ocr tutorial
- extract urdu text
- recognize text image
- how to extract urdu
- ocr from png file
language: fr
og_description: 'Tutoriel C# OCR : Apprenez à extraire du texte Urdu d’une image PNG
  à l’aide de l’OCR en C#. Guide complet avec code et astuces.'
og_title: Tutoriel OCR C# – Extraire le texte en ourdou à partir d’images PNG
tags:
- OCR
- C#
- Urdu
- Image Processing
title: Tutoriel OCR C# – Extraire du texte ourdou à partir d'images PNG
url: /fr/net/text-recognition/c-ocr-tutorial-extract-urdu-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutoriel c# ocr – Extraire du texte Urdu à partir d'images PNG

Vous avez déjà eu besoin d'un **c# ocr tutorial** qui extrait réellement du texte Urdu d'un fichier PNG ? Vous n'êtes pas seul. Dans de nombreux projets—traitement de factures, archivage de documents, ou même un outil de traduction rapide—vous arriverez à un moment où vous devez reconnaître des données d'image texte, et la langue importe.  

Dans ce guide, nous parcourrons une solution complète, prête à l'exécution, qui extrait du texte Urdu d'un PNG à l'aide d'un moteur OCR. Vous verrez pourquoi chaque ligne existe, comment gérer les packs de langue manquants, et quoi faire si l'image n'est pas parfaite. À la fin, vous serez suffisamment confiant pour adapter le code à d'autres langues ou types de fichiers.

## Ce que vous apprendrez

- Comment installer une bibliothèque OCR C# (sans magie cachée)  
- Les étapes exactes pour **extract urdu text** d'un fichier PNG  
- Pourquoi la configuration de la langue en Urdu est importante et comment le moteur télécharge automatiquement les données manquantes  
- Méthodes pour vérifier la sortie et dépanner les problèmes courants  

Aucun lien vers une documentation externe n'est requis — tout ce dont vous avez besoin se trouve ici.

## Prérequis (Ce qu'il faut avant de commencer)

| Requirement | Why It Matters |
|-------------|----------------|
| .NET 6.0+ (or .NET Core 3.1) | APIs modernes et prise en charge async |
| Visual Studio 2022 (or VS Code with C# extension) | IDE avec IntelliSense rend le code plus clair |
| An OCR library that exposes `OcrEngine` (e.g., **Microsoft.Windows.SDK.Contracts** or a third‑party NuGet) | Fournit les méthodes `Language.Urdu` et `Recognize` |
| A PNG image containing Urdu text (e.g., `urdu_invoice.png`) | La source pour l'opération **recognize text image** |

Si vous n'avez pas encore de package OCR, exécutez cette ligne unique dans la console du gestionnaire de packages :

```powershell
Install-Package Microsoft.Windows.SDK.Contracts
```

> **Astuce :** Le SDK récupère automatiquement les données de langue lors de la première utilisation, vous n'avez donc pas besoin de télécharger manuellement les packs de langue Urdu.

## Étape 1 : Installer et référencer la bibliothèque OCR

Avant de pouvoir créer un moteur, le projet doit référencer le package OCR. Ajoutez les directives `using` suivantes en haut de votre fichier :

```csharp
using System;
using Windows.Media.Ocr;          // Core OCR classes
using Windows.Graphics.Imaging;   // For loading PNG files
using Windows.Storage;            // File handling helpers
```

Ces espaces de noms nous donnent accès à `OcrEngine`, `Language` et aux utilitaires de chargement d'images. Si vous utilisez une bibliothèque différente, recherchez des espaces de noms analogues.

## Étape 2 : Créer une instance du moteur OCR  

Nous allons maintenant lancer le moteur. Considérez le moteur comme le cerveau qui interprétera les motifs de pixels en caractères.

```csharp
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));
if (ocrEngine == null)
{
    Console.WriteLine("Failed to create OCR engine for Urdu. Check your language pack.");
    return;
}
```

**Pourquoi c'est important :** `TryCreateFromLanguage` renvoie `null` si les données de langue ne sont pas présentes, nous donnant ainsi la possibilité d'échouer rapidement au lieu de planter plus tard.

## Étape 3 : Charger l'image PNG  

Le moteur OCR travaille avec des objets `SoftwareBitmap`, pas avec des chemins de fichiers bruts. L'assistant suivant charge un PNG depuis le disque et le convertit au format requis.

```csharp
// Step 3: Load the PNG image into a SoftwareBitmap
async Task<SoftwareBitmap> LoadImageAsync(string path)
{
    StorageFile file = await StorageFile.GetFileFromPathAsync(path);
    using var stream = await file.OpenReadAsync();
    var decoder = await BitmapDecoder.CreateAsync(stream);
    // Convert to Gray8 for best OCR accuracy
    return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
}
```

**Cas particulier :** Si le PNG est en couleur, le convertir en niveaux de gris (`Gray8`) améliore souvent la reconnaissance, surtout pour des scripts comme l'Urdu qui possèdent des diacritiques délicates.

## Étape 4 : Reconnaître le texte de l'image  

Voici le cœur du **c# ocr tutorial** — demander au moteur de lire l'image.

```csharp
// Step 4: Perform OCR on the loaded bitmap
async Task<string> RecognizeUrduAsync(string imagePath)
{
    SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
    OcrResult result = await ocrEngine.RecognizeAsync(bitmap);
    return result.Text;
}
```

La propriété `OcrResult.Text` contient la chaîne Unicode brute. Comme nous avons défini la langue sur Urdu précédemment, le moteur applique les règles d'écriture correctes.

## Étape 5 : Afficher et vérifier le texte extrait  

Enfin, nous affichons le résultat dans la console. Dans une application réelle, vous pourriez le stocker dans une base de données ou le transmettre à un service de traduction.

```csharp
// Step 5: Run the OCR and display the result
static async Task Main(string[] args)
{
    string imageFile = @"C:\Images\urdu_invoice.png"; // adjust path as needed
    string extracted = await RecognizeUrduAsync(imageFile);
    Console.WriteLine("=== Extracted Urdu Text ===");
    Console.WriteLine(extracted);
}
```

**Ce à quoi s'attendre :** Si l'image est claire, vous verrez quelque chose comme :

```
=== Extracted Urdu Text ===
بل نمبر: 12345
تاریخ: 21/03/2026
کل رقم: 5,000 روپے
```

Si la sortie apparaît brouillée, vérifiez la qualité de l'image (contraste, bruit) et envisagez un pré‑traitement (par ex., binarisation).

## Comment extraire du texte Urdu d'un fichier PNG – Pièges courants  

1. **Faible contraste** – L'OCR a du mal lorsque les couleurs du premier plan et de l'arrière‑plan sont similaires. Utilisez des outils d'édition d'image pour augmenter le contraste avant d'exécuter le code.  
2. **DPI incorrect** – Scanner à 300 dpi ou plus donne au moteur plus de détails à exploiter.  
3. **Pack de langue manquant** – Le premier appel à `TryCreateFromLanguage` peut déclencher un téléchargement ; assurez‑vous que votre machine a accès à Internet.  

Résoudre ces problèmes améliore considérablement le taux de réussite du **recognize text image**.

## Recognize Text Image : Extension à d'autres formats  

Bien que ce tutoriel se concentre sur le PNG, le même flux de travail fonctionne pour JPEG, BMP ou TIFF—il suffit de changer l'extension du fichier et de s'assurer que le décodeur le prend en charge. La ligne clé reste `await ocrEngine.RecognizeAsync(bitmap);`.

## Conseils pour l'OCR à partir d'un fichier PNG – Performance et mise à l'échelle  

- **Traitement par lots** : chargez plusieurs images dans une liste et exécutez `Task.WhenAll` pour paralléliser la reconnaissance.  
- **Mise en cache du moteur** : créez une seule instance de `OcrEngine` et réutilisez‑la entre les appels ; la créer à chaque fois ajoute une surcharge.  
- **Gestion de la mémoire** : libérez les objets `SoftwareBitmap` après utilisation (`bitmap.Dispose()`) pour garder le processus léger.

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet que vous pouvez compiler et exécuter. Il inclut toutes les déclarations `using`, la gestion async et les vérifications d'erreurs.

```csharp
// Full C# OCR tutorial – Extract Urdu text from a PNG file
using System;
using System.Threading.Tasks;
using Windows.Media.Ocr;
using Windows.Graphics.Imaging;
using Windows.Storage;

class Program
{
    // Initialize the OCR engine for Urdu
    private static OcrEngine _ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));

    static async Task Main(string[] args)
    {
        if (_ocrEngine == null)
        {
            Console.WriteLine("Urdu language pack not available. Ensure internet connectivity for automatic download.");
            return;
        }

        string imagePath = @"C:\Images\urdu_invoice.png"; // <-- change to your image location
        string text = await RecognizeUrduAsync(imagePath);
        Console.WriteLine("=== Extracted Urdu Text ===");
        Console.WriteLine(text);
    }

    // Load PNG and convert to grayscale bitmap
    private static async Task<SoftwareBitmap> LoadImageAsync(string path)
    {
        StorageFile file = await StorageFile.GetFileFromPathAsync(path);
        using var stream = await file.OpenReadAsync();
        var decoder = await BitmapDecoder.CreateAsync(stream);
        return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
    }

    // Perform OCR and return the recognized text
    private static async Task<string> RecognizeUrduAsync(string imagePath)
    {
        SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
        OcrResult result = await _ocrEngine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

**Sortie attendue** : la console affiche les caractères Urdu exacts trouvés dans l'image, en conservant l'ordre de droite à gauche.

## Conclusion  

Vous venez de terminer un **c# ocr tutorial** qui montre comment **extract urdu text** d'un PNG, configurer la langue et gérer le résultat en toute sécurité. Les étapes—installer la bibliothèque, créer le moteur, charger l'image, reconnaître le texte et l'afficher—forment un modèle réutilisable que vous pouvez appliquer à n'importe quel script ou type de fichier.  

Ensuite, envisagez d'expérimenter le **recognize text image** sur des PDF multi‑pages (convertissez chaque page en PNG d'abord) ou d'intégrer une API de traduction pour transformer l'Urdu extrait en anglais automatiquement. Le ciel est la limite une fois que vous avez maîtrisé ce flux de travail de base.

Bon codage, et que vos résultats OCR soient d'une clarté cristalline !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}