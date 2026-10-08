---
category: general
date: 2026-01-13
description: Tutoriel C# OCR qui montre comment extraire du texte d’une image, charger
  l’image pour l’OCR et formater la sortie JSON à l’aide d’Aspose OCR. Apprenez à
  sérialiser un objet en JSON.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- format json output
- serialize object to json
- load image for ocr
language: fr
og_description: Tutoriel C# OCR qui vous guide à travers l'extraction de texte à partir
  d'une image, le chargement de l'image pour l'OCR et le formatage de la sortie JSON
  avec Aspose OCR.
og_title: Tutoriel OCR en C# – Extraire le texte et formater le JSON
tags:
- OCR
- C#
- JSON
title: Tutoriel OCR en C# – Extraire du texte à partir d’une image et obtenir du JSON
  formaté
url: /fr/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-get-formatted-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutoriel c# ocr – Extraire du texte d’une image et formater la sortie JSON

Vous êtes-vous déjà demandé comment **extraire du texte d’une image** dans un projet C# sans vous battre avec le traitement pixel par pixel ? C’est le problème que résout ce *tutoriel c# ocr*. En quelques minutes, vous verrez comment **charger une image pour l’ocr**, exécuter Aspose OCR, et **formater la sortie json** afin de pouvoir injecter les données directement dans votre API ou votre base de données.

Nous passerons en revue chaque ligne de code, expliquerons pourquoi chaque élément est important, et vous montrerons même le JSON exact que vous devez attendre. À la fin, vous disposerez d’une application console prête à l’emploi qui transforme un PNG de facture en JSON propre et indenté. Pas de blabla, juste une solution pratique que vous pouvez intégrer à n’importe quel projet .NET 6+.

## Ce que couvre ce tutoriel c# ocr

- Installation du package NuGet Aspose.OCR  
- Chargement d’un fichier image pour le traitement OCR  
- Reconnaissance du texte anglais (ou de toute langue prise en charge)  
- **Sérialisation du résultat OCR en JSON** avec mise en forme lisible  
- Affichage du JSON dans la console et sauvegarde éventuelle  

Vous n’avez besoin que d’une compréhension basique de C# et d’un SDK .NET récent. Rien d’autre. Si vous êtes curieux de savoir comment **extraire du texte d’une image** pour des factures, des reçus ou des formulaires numérisés, continuez votre lecture.

---

## Étape 1 : Configurer l’environnement du tutoriel c# ocr

Avant d’écrire du code, assurez‑vous de disposer des bons outils :

1. **.NET 6 SDK ou version ultérieure** – téléchargez‑le depuis le site de Microsoft.  
2. **Visual Studio 2022** (la version Community convient) ou tout autre éditeur de votre choix.  
3. **Package NuGet Aspose.OCR** – exécutez `dotnet add package Aspose.OCR` dans le dossier de votre projet.

> **Astuce pro :** Si vous utilisez une pipeline CI, ajoutez la référence du package à votre `.csproj` afin que la restauration s’effectue automatiquement lors du build.

---

## Étape 2 : Charger l’image pour l’OCR

La première vraie étape de notre tutoriel consiste à récupérer l’image que vous souhaitez traiter. Aspose OCR fonctionne avec les formats courants comme PNG, JPEG et TIFF.

```csharp
using Aspose.OCR;
using System.Text.Json;

// Replace this with the actual path to your invoice image
string imagePath = @"C:\Invoices\invoice.png";

// Create an OcrImage instance from the file system
OcrImage inputImage = OcrImage.FromFile(imagePath);
```

> **Pourquoi c’est important :** Charger l’image en tant qu’`OcrImage` donne au moteur accès aux données bitmap et aux informations DPI, ce qui améliore la précision de la reconnaissance. Ignorer cette étape ou fournir un fichier corrompu entraînera une exception d’exécution.

---

## Étape 3 : Extraire le texte de l’image

Nous exécutons maintenant le moteur OCR. La méthode `Recognize` renvoie un objet riche `OcrResult` contenant le texte brut, les scores de confiance et les détails de mise en page.

```csharp
// Initialize the OCR engine – no license needed for a trial run
OcrEngine ocrEngine = new OcrEngine();

// Recognize English text (you can change the language enum if needed)
OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);
```

> **Cas limite :** Si vous devez traiter un document multilingue, appelez `Recognize` deux fois avec des valeurs différentes de `OcrLanguage` et concaténez les résultats. Le moteur est thread‑safe, vous pouvez donc paralléliser de gros lots.

---

## Étape 4 : Sérialiser l’objet en JSON – Formater la sortie JSON

L’objet `OcrResult` est une classe C# simple, ce qui signifie que nous pouvons le transmettre à `System.Text.Json`. En activant `WriteIndented`, la sortie devient lisible par l’homme.

```csharp
// Serialize the OCR result with pretty printing
string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
{
    WriteIndented = true
});
```

> **Ce que vous obtenez :** Une chaîne JSON joliment indentée qui inclut le texte reconnu, la confiance et la mise en page de la page. C’est parfait pour le logging, l’envoi à un service web ou le stockage dans une base NoSQL.

---

## Étape 5 : Afficher et (optionnellement) sauvegarder le JSON formaté

Enfin, nous affichons le JSON dans la console. Vous pouvez également l’écrire dans un fichier avec `File.WriteAllText` si vous le souhaitez.

```csharp
// Show the JSON in the console
Console.WriteLine(json);

// Optional: Save to a .json file next to the image
string jsonPath = Path.ChangeExtension(imagePath, ".json");
File.WriteAllText(jsonPath, json);
Console.WriteLine($"\nJSON saved to: {jsonPath}");
```

**Sortie console attendue (troncature pour la brièveté) :**

```json
{
  "Text": "Invoice #12345\nDate: 2025‑12‑01\nTotal: $250.00",
  "Confidence": 0.97,
  "Pages": [
    {
      "PageNumber": 1,
      "Blocks": [
        {
          "Text": "Invoice #12345",
          "Confidence": 0.99,
          "Rectangle": { "X": 50, "Y": 30, "Width": 200, "Height": 30 }
        }
        // …more blocks…
      ]
    }
  ]
}
```

Si le moteur OCR ne trouve aucun texte, le champ `Text` sera une chaîne vide et `Confidence` sera `0`. C’est un bon indicateur pour revérifier la qualité de l’image.

---

## Étape 6 : Exemple complet fonctionnel

En rassemblant le tout, voici le programme complet que vous pouvez copier‑coller dans une nouvelle application console :

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonResultDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the source image (replace with your own path)
        string imagePath = @"C:\Invoices\invoice.png";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Recognize text – this is the core of our c# ocr tutorial
        OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);

        // 4️⃣ Serialize the result with pretty formatting
        string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
        {
            WriteIndented = true
        });

        // 5️⃣ Output to console and optionally write to a file
        Console.WriteLine(json);
        string jsonPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"\nJSON saved to: {jsonPath}");
    }
}
```

Exécutez le programme (`dotnet run` depuis le dossier du projet) et observez la console afficher une représentation JSON correctement formatée de votre facture numérisée.

---

## Pièges courants & Astuces (Extras du tutoriel c# ocr)

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Champ `Text` vide** | Image à faible contraste ou rotation. | Pré‑traitez l’image (augmenter le contraste, redresser) ou utilisez `OcrEngine.ImagePreprocess`. |
| **`System.DllNotFoundException`** | Binaires natifs Aspose OCR manquants. | Vérifiez que le package NuGet a bien été restauré et que l’architecture d’exécution (x64/x86) correspond à votre OS. |
| **Lenteur sur de gros PDF** | L’OCR traite chaque page séquentiellement. | Parallelisez en créant des instances distinctes de `OcrEngine` par page (le moteur est thread‑safe). |
| **JSON trop volumineux** | Vous sérialisez chaque détail, y compris les boîtes englobantes. | Utilisez un DTO ne contenant que `Text` et `Confidence` avant la sérialisation. |

> **Rappel :** Le but de ce tutoriel est de montrer un flux propre, de bout en bout. Vous pouvez toujours réduire le JSON ou ajouter plus de métadonnées plus tard.

---

## Conclusion

Vous venez de terminer un **tutoriel c# ocr** qui charge une image, **extrait du texte d’une image**, et produit une **sortie json formatée** en **sérialisant l’objet en json**. Les étapes sont simples, le code est prêt à être exécuté, et le JSON est parfaitement indenté pour une consommation en aval.

Et après ? Essayez de remplacer `OcrLanguage.English` par `OcrLanguage.French` ou de parcourir un dossier de reçus dans une boucle. Vous pouvez également explorer la sauvegarde du JSON directement dans Azure Blob Storage ou son injection dans un modèle d’apprentissage automatique.

Si vous rencontrez des problèmes, revérifiez que le chemin de l’image est correct et que la licence Aspose OCR (si vous en avez une) est chargée avant d’appeler `Recognize`. Bon codage, et que vos résultats OCR soient toujours nets !

--- 

*Image illustrant le flux OCR (texte alternatif : "diagramme du tutoriel c# ocr montrant charger l’image, reconnaître le texte, sérialiser en JSON")*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}