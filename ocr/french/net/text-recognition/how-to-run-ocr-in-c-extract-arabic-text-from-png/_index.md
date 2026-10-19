---
category: general
date: 2026-01-10
description: Comment exécuter rapidement l'OCR et extraire du texte arabe d'une image.
  Apprenez à convertir une image en texte, à lire le texte d'un PNG, et découvrez
  comment extraire du texte avec Aspose OCR.
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: fr
og_description: Comment exécuter l'OCR en C# et extraire du texte arabe d'une image
  PNG. Ce guide vous montre comment convertir une image en texte et lire le texte
  d'un PNG étape par étape.
og_title: Comment exécuter l'OCR en C# – Extraire du texte arabe à partir d'un PNG
tags:
- OCR
- C#
- Aspose
title: Comment exécuter l'OCR en C# – Extraire du texte arabe d’un PNG
url: /fr/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exécuter l'OCR en C# – Extraire du texte arabe depuis un PNG

Vous êtes-vous déjà demandé **comment exécuter l'OCR** sur une image contenant des caractères arabes ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu'ils doivent **extraire du texte arabe** d'un PNG sans savoir quelle bibliothèque gère correctement les scripts de droite à gauche sans prise de tête.  

Dans ce tutoriel, nous passerons en revue tout ce que vous devez savoir pour **convertir une image en texte**, **lire du texte depuis un PNG**, et enfin **comment extraire du texte** à l'aide d'Aspose.OCR dans une application console C# propre. À la fin, vous disposerez d’un programme prêt à l’emploi qui affiche la chaîne arabe directement dans votre terminal.

## Ce que vous allez apprendre

- Installer et référencer le package NuGet Aspose.OCR.  
- Configurer le moteur OCR pour la prise en charge de la langue arabe.  
- Charger une image PNG et lancer le processus de reconnaissance.  
- Récupérer et afficher le texte extrait.  
- Ajuster les paramètres pour une meilleure précision et gérer les pièges courants.

Aucune expérience préalable avec l'OCR n'est requise, juste une compréhension de base du C# et un environnement de développement .NET (Visual Studio, Rider ou le CLI `dotnet` suffiront).

---

## Comment exécuter l'OCR – Configuration d'Aspose OCR

### Étape 1 : Ajouter le package NuGet Aspose.OCR

La première chose dont nous avons besoin est la bibliothèque OCR elle‑même. Aspose.OCR est un produit commercial, mais il propose une version d’essai gratuite qui fonctionne parfaitement à des fins d’apprentissage.

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

Vous pouvez également ouvrir le **Gestionnaire de packages NuGet** dans Visual Studio, rechercher **Aspose.OCR**, puis cliquer sur **Installer**.

> **Astuce :** Si vous prévoyez d’utiliser la bibliothèque dans un pipeline CI, ajoutez le drapeau `-v` pour verrouiller la version, par ex., `dotnet add package Aspose.OCR -v 23.10`.

### Étape 2 : Créer un nouveau projet console (si vous n’en avez pas)

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

Vous avez maintenant un fichier `Program.cs` frais, prêt pour notre code.

---

## Extraction du texte arabe – Écriture du code OCR

Voici le programme complet, prêt à l’exécution. Enregistrez‑le sous le nom `Program.cs` (ou remplacez le fichier auto‑généré).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### Pourquoi chaque ligne est importante

- **`OcrEngine`** : La classe centrale qui coordonne le chargement d’image, la sélection de la langue et la reconnaissance.  
- **`Language = OcrLanguage.Arabic`** : L’arabe utilise un script de droite à gauche et des glyphes uniques ; définir la langue indique au moteur d’appliquer les modèles de caractères appropriés.  
- **`ImageStream.FromFile`** : Gère PNG, JPEG, BMP et bien d’autres formats. Si vous devez lire depuis un `MemoryStream` (par ex., un fichier téléchargé), remplacez cet appel en conséquence.  
- **`Recognize()`** : Effectue le travail lourd — analyse des pixels, segmentation et classification des caractères.  
- **`ocrEngine.Text`** : La chaîne Unicode finale, prête pour un traitement ultérieur, un stockage ou un affichage.

### Résultat attendu

Si `arabic_sample.png` contient la phrase « مرحبا بالعالم » (Hello World), la console affichera :

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

Si la sortie apparaît corrompue, vérifiez que l’image est nette, que la langue est bien réglée sur l’arabe, et que la version du moteur OCR correspond à la documentation.

---

## Conversion d’image en texte – Optimiser la précision

Si les paramètres par défaut fonctionnent pour la plupart des scans propres, les images du monde réel nécessitent souvent un petit ajustement supplémentaire.

| Paramètre | Fonction | Quand l’utiliser |
|-----------|----------|-------------------|
| `ocrEngine.Config.Preprocess = true` | Active la binarisation automatique et la suppression du bruit. | Documents scannés avec des ombres. |
| `ocrEngine.Config.Deskew = true` | Fait pivoter l’image pour corriger une légère inclinaison. | Photos prises sous un angle. |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | Traite l’ensemble de l’image comme un seul bloc de texte. | Légendes simples ou étiquettes d’une seule ligne. |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | Limite la reconnaissance aux seuls caractères arabes. | Réduit les faux positifs sur des pages multilingues. |

Vous pouvez ajouter ces lignes juste après la création du moteur :

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## Lecture du texte depuis un PNG – Gestion de différentes sources d’image

Parfois le PNG se trouve dans une base de données ou provient d’une requête web. Voici une variante rapide qui lit depuis un `byte[]` :

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

Le reste du flux reste identique, ce qui signifie que **comment extraire du texte** reste cohérent quel que soit la source.

---

## Comment extraire du texte – Options avancées & cas limites

### 1. PDFs ou TIFFs multi‑pages

Si vous devez OCRiser un document multi‑pages, bouclez sur chaque page :

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **Note :** Vous aurez besoin du package `Aspose.PDF` pour cet extrait.

### 2. Détection automatique de la langue

Aspose.OCR propose également la détection automatique, mais elle est plus lente. Si vous n’êtes pas sûr que l’image contienne de l’arabe ou un autre script, activez‑la :

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

Le moteur testera chaque modèle de langue et choisira le meilleur correspondance.

### 3. Conseils de performance

- **Réutilisez l’objet `OcrEngine`** pour plusieurs images ; créer une nouvelle instance à chaque fois ajoute du surcoût.  
- **Exécutez en parallèle** uniquement si vous avez des instances de moteur distinctes par thread — partager une même instance provoque des conditions de concurrence.

---

## Conclusion

Nous avons couvert **comment exécuter l'OCR** en C# de bout en bout, en vous montrant comment **extraire du texte arabe**, **convertir une image en texte**, **lire du texte depuis un PNG**, et répondre à **comment extraire du texte** dans diverses situations. Le code d’exemple est complet, autonome, et prêt à être collé dans n’importe quel projet console .NET.

Et après ? Essayez de remplacer `OcrLanguage.Arabic` par le coréen ou le serbe cyrillique pour découvrir la puissance multilingue de la bibliothèque. Expérimentez avec les drapeaux de prétraitement pour améliorer la précision sur des scans bruyants, ou intégrez la routine OCR dans une API web afin que les utilisateurs puissent télécharger des images et obtenir instantanément le texte.

Bon codage, et que vos résultats OCR soient toujours d’une clarté cristalline !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}