---
category: general
date: 2026-03-13
description: Comment effectuer la reconnaissance optique de caractères (OCR) en C#
  et extraire le texte d’une image à l’aide d’OcrEngine. Apprenez à convertir rapidement
  une image en texte grâce à un guide complet étape par étape.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- read text from picture
- how to extract text
language: fr
og_description: Comment effectuer de l’OCR en C# ? Ce guide vous montre comment extraire
  du texte d’une image, convertir une image en texte et lire le texte d’une photo
  à l’aide d’OcrEngine.
og_title: Comment réaliser l'OCR en C# – Extraire le texte d’une image
tags:
- OCR
- C#
- Image Processing
title: Comment réaliser l'OCR en C# – Extraire le texte d’une image
url: /fr/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer de l'OCR en C# – Extraire du texte d'une image

Comment effectuer de l'OCR en C# est une question fréquente pour les développeurs qui doivent **lire du texte à partir d'images**. Dans ce guide, nous vous montrerons comment extraire du texte d'une image en utilisant la bibliothèque `OcrEngine`, transformant les images en chaînes recherchables en quelques lignes de code.  

Si vous avez déjà contemplé une facture numérisée, une note manuscrite ou une capture d'écran en vous demandant *« comment extraire le texte ? »*, vous êtes au bon endroit. Nous aborderons également la conversion d'image en texte pour le traitement par lots, afin que vous puissiez automatiser l’ensemble du flux de travail.

---

## Ce dont vous avez besoin

- **.NET 6.0 ou ultérieur** (l'API que nous utilisons fonctionne avec .NET Standard 2.0+)
- Le package NuGet **OcrEngine** (ou toute bibliothèque OCR compatible exposant les propriétés `Language`, `Image`, `Recognize` et `Text`)
- Un fichier image d'exemple, par ex. `hindi_page.jpg`, placé dans un dossier que vous pouvez référencer depuis le code
- Une compréhension de base de la syntaxe C# – aucun tour avancé requis

C’est tout. Aucun service externe, aucune clé d'API, juste une bibliothèque locale qui fait le travail lourd.

---

## Implémentation étape par étape

Ci-dessous, nous découpons le processus en parties logiques. Chaque section possède un titre clair, un court extrait de code et une explication du **pourquoi** de l'étape – pas seulement du **quoi**.

### Comment effectuer de l'OCR – Étapes principales

Le flux global peut être résumé en cinq actions :

1. **Créer** une instance du moteur OCR
2. **Sélectionner** la langue que vous souhaitez reconnaître
3. **Charger** l'image contenant le texte
4. **Exécuter** l'algorithme de reconnaissance
5. **Lire** le texte extrait

C’est le squelette ; les sections suivantes le développent.

---

### Extraire du texte d'une image – Créer le moteur

Tout d'abord, nous avons besoin d'un objet qui sait communiquer avec le moteur OCR.

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

*Pourquoi c’est important :* Instancier `OcrEngine` alloue tous les tampons internes et charge les DLL natives nécessaires à l'analyse d'image. Ignorer cette étape vous laisserait sans reconnaisseur à appeler plus tard.

> **Astuce :** Si vous prévoyez de traiter de nombreuses images consécutivement, conservez la même instance `ocrEngine`. Elle réutilise les modèles de langue et accélère les appels suivants.

---

### Convertir l'image en texte – Choisir la langue

La précision de l'OCR dépend fortement du modèle de langue que vous lui fournissez. Pour le Hindi, le Tamil ou tout autre script, définissez la propriété `Language` en conséquence.

```csharp
// Step 2: Select the language of the text to recognize (e.g., Hindi)
ocrEngine.Language = Language.Hindi;   // You can also use Language.Tamil, Language.English, etc.
```

*Pourquoi c’est important :* Le moteur utilise des jeux de caractères et des modèles statistiques spécifiques à chaque langue. Fournir la mauvaise langue produit souvent un résultat illisible, surtout pour les scripts non latins.

> **Cas particulier :** Si vous avez besoin d’un support multilingue, certaines bibliothèques vous permettent de définir une liste de secours, par ex. `ocrEngine.Language = Language.Multilingual;`.

---

### Lire le texte d'une image – Charger l'image source

Nous indiquons maintenant au moteur le fichier contenant le texte visuel.

```csharp
// Step 3: Load the image that contains the text
ocrEngine.Image = ImageStream.FromFile(@"C:\OCR\Samples\hindi_page.jpg");
```

*Pourquoi c’est important :* `ImageStream.FromFile` convertit le fichier brut en un format bitmap que le cœur de l'OCR peut comprendre. Fournir un format corrompu ou non supporté (comme SVG) déclenchera une exception.

> **Attention :** Les grandes images peuvent consommer beaucoup de mémoire. Si vous traitez des numérisations haute résolution, envisagez de les réduire avec `Image.Resize` avant de les transmettre au moteur.

---

### Convertir l'image en texte – Exécuter la reconnaissance

Avec le moteur prêt et l'image chargée, nous invoquons enfin le processus OCR.

```csharp
// Step 4: Perform the OCR operation
ocrEngine.Recognize();
```

*Pourquoi c’est important :* `Recognize` déclenche une série d’étapes internes — pré‑traitement, segmentation, classification des caractères et post‑traitement. L’appel est bloquant, ce qui signifie que le thread attend que le texte soit prêt.

> **Note de performance :** Sur un ordinateur de bureau typique, la reconnaissance d’une page à 300 dpi prend < 1 seconde. Sur un serveur, vous pouvez exécuter cela dans une tâche en arrière‑plan pour éviter le gel de l’interface.

---

### Comment extraire le texte – Récupérer le résultat

Une fois la reconnaissance terminée, le moteur stocke le texte brut dans la propriété `Text`.

```csharp
// Step 5: Output the recognized text
Console.WriteLine(ocrEngine.Text);
```

*Pourquoi c’est important :* La propriété `Text` vous fournit une chaîne UTF‑8 propre que vous pouvez écrire dans un fichier, insérer dans une base de données ou transmettre à des pipelines NLP en aval.

> **Sortie attendue :** Pour la page Hindi d’exemple, vous pourriez voir quelque chose comme  
> `यह एक उदाहरण पाठ है जो OCR द्वारा पहचाना गया है।`  
> (La sortie exacte dépend de la qualité de l’image et du modèle de langue.)

---

## Considérations supplémentaires pour les projets réels

Voici quelques scénarios « et si » que vous rencontrerez probablement en essayant de **extraire du texte d'une image** en production.

### Gestion de plusieurs images dans une boucle

Si vous devez **convertir l'image en texte** pour des dizaines de fichiers, encapsulez les étapes dans une boucle `foreach` et réutilisez le même `ocrEngine` :

```csharp
string[] files = Directory.GetFiles(@"C:\OCR\Batch\", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), ocrEngine.Text);
}
```

### Gestion des numérisations de mauvaise qualité

- **Pré‑traiter** avec la binarisation (`Image.Binarize()`), la suppression du bruit ou le redressement.
- **Augmenter le DPI** lors de la numérisation (300 dpi est une base sûre).
- **Choisir un modèle de langue** qui prend en charge les ligatures du script (par ex., Devanagari pour le Hindi).

### Lire le texte d'une image sur le Web

Lorsque l'image provient d'une URL, téléchargez‑la d'abord dans un flux mémoire :

```csharp
using (HttpClient client = new())
{
    byte[] data = await client.GetByteArrayAsync(imageUrl);
    using var ms = new MemoryStream(data);
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
    Console.WriteLine(ocrEngine.Text);
}
```

### Sécurité des threads et parallélisme

La plupart des bibliothèques OCR **ne sont pas** thread‑safe par défaut. Si vous prévoyez de **lire le texte d'une image** simultanément, créez des instances `OcrEngine` séparées par thread, ou utilisez une file d’attente producteur‑consommateur pour sérialiser l’accès.

---

## Exemple complet fonctionnel

En rassemblant tous les éléments, voici une application console prête à l’emploi qui démontre **comment effectuer de l'OCR**, **extraire du texte d'une image** et **lire le texte d'une image** dans un programme cohérent.

```csharp
using System;
using OcrLibrary;               // Adjust to your OCR library's namespace
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Choose the language (Hindi in this case)
        ocrEngine.Language = Language.Hindi;

        // Load the image file
        string imagePath = @"C:\OCR\Samples\hindi_page.jpg";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // Run the recognition process
        ocrEngine.Recognize();

        // Output the extracted text
        string result = ocrEngine.Text;
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(result);

        // Optional: Save to a .txt file
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, result);
        Console.WriteLine($"Text saved to {txtPath}");
    }
}
```

**Ce que vous devriez voir :** La console affiche la phrase Hindi extraite de `hindi_page.jpg`, suivie d’une confirmation que le fichier texte a été créé. Si l’image est nette, la sortie sera pratiquement identique au texte imprimé d’origine.

---

## Conclusion

Vous savez maintenant **comment effectuer de l'OCR** en C# de bout en bout, comment **extraire du texte d'une image**, **convertir l'image en texte** et **lire le texte d'une image** en utilisant un flux de travail `OcrEngine` simple. Le modèle en cinq étapes — créer, définir la langue, charger, reconnaître, lire — couvre la plupart des cas d’utilisation, et les astuces supplémentaires vous aident à gérer les traitements par lots, les numérisations de mauvaise qualité et les sources web.

Prêt pour le prochain défi ? Essayez de changer la langue en anglais, de fournir une page PDF rendue en image, ou d’enchaîner la sortie OCR dans un pipeline d’indexation de recherche. Le ciel est la limite une fois que vous avez maîtrisé les bases de l'OCR en C#.

Des questions ou une image récalcitrante ? Laissez un commentaire ci‑dessous, et résolvons le problème ensemble. Bon codage !  

![exemple de comment effectuer OCR](images/ocr-example.png "exemple de comment effectuer OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}