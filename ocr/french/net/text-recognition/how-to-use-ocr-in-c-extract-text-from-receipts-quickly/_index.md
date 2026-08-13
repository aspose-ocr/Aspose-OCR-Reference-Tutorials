---
category: general
date: 2026-03-05
description: Comment utiliser l'OCR en C# pour extraire le texte des images de reçus.
  Apprenez à charger une image pour l'OCR et à reconnaître une image de reçu en quelques
  minutes.
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: fr
og_description: Comment utiliser l'OCR en C# pour extraire le texte des reçus. Suivez
  ce guide étape par étape pour charger une image pour l'OCR et reconnaître efficacement
  l'image du reçu.
og_title: Comment utiliser l'OCR en C# – Extraction rapide du texte d'un reçu
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: Comment utiliser l'OCR en C# – Extraire rapidement le texte des reçus
url: /fr/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# comment utiliser l'OCR en C# – Extraire rapidement le texte des reçus

Vous vous êtes déjà demandé **comment utiliser l'OCR** pour extraire des données directement d’une photo d’un ticket de supermarché ? Vous n’êtes pas seul. Dans de nombreuses applications pour petites entreprises, le goulot d’étranglement consiste à transformer un PNG flou en texte structuré exploitable.  

La bonne nouvelle ? En quelques lignes de C# et avec Aspose.OCR, vous pouvez **load image for OCR**, lancer le moteur et **recognize receipt image** en moins d’une minute. Vous verrez ci‑dessous un exemple complet, prêt à l’emploi, ainsi que des astuces pour les parties complexes que la plupart des tutoriels négligent.

## Ce que couvre ce guide

Nous passerons en revue tout ce que vous devez savoir :

* Installation du package NuGet Aspose.OCR.  
* Configuration du moteur OCR – le cœur de **comment utiliser l'OCR** correctement.  
* Chargement d’un fichier de ticket (c’est l’étape **load image for OCR**).  
* Exécution du processus de reconnaissance et extraction des données de mise en page au format JSON et XML.  
* Gestion des problèmes courants comme les licences manquantes ou les formats d’image non pris en charge.  

À la fin, vous disposerez d’un programme autonome qui extrait le texte de n’importe quel ticket que vous déposerez dans un dossier. Aucun service externe, aucune magie cachée.

## Prérequis

* SDK .NET 6 ou version ultérieure (le code se compile également avec .NET Core).  
* Un fichier de licence Aspose.OCR valide (`Aspose.OCR.lic`). Vous pouvez obtenir une version d’essai gratuite sur le site d’Aspose si vous n’en avez pas encore.  
* Une image de ticket d’exemple – `receipt.png` convient parfaitement, mais tout format raster courant fonctionnera.  

Si vous avez déjà tout cela, c’est parti.

![exemple d'utilisation d'OCR](https://example.com/ocr-receipt.png "exemple d'utilisation d'OCR")

## Étape 1 : Installer Aspose.OCR et créer un nouveau projet

Première chose à faire : vous avez besoin de la bibliothèque qui fait réellement le travail lourd. Ouvrez un terminal dans le dossier de votre projet et exécutez :

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Cette commande crée une application console et ajoute le dernier package Aspose.OCR. D’après mon expérience, garder un nom de projet court rend les chemins générés plus lisibles, surtout lorsque vous commencez à jongler avec plusieurs démos.

## Étape 2 : Initialiser le moteur OCR – le cœur de **comment utiliser l'OCR**

Nous allons maintenant écrire le code qui répond à la question « **comment utiliser l'OCR** en C# ». Ouvrez `Program.cs` et remplacez son contenu par l’extrait ci‑dessous. Notez les commentaires : ils expliquent le *pourquoi* de chaque ligne, pas seulement le *quoi*.

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Pourquoi cela fonctionne

* **`OcrEngine`** est le point d’entrée ; il contient toutes les configurations que vous pourrez ajuster plus tard (langue, DPI, etc.).  
* **`SetLicense`** supprime le filigrane d’évaluation – une étape cruciale si vous prévoyez de livrer le code.  
* **`ImageStream.FromFile`** réalise le travail de **load image for OCR**, en gérant PNG, JPEG, BMP, TIFF, et plus encore.  
* **`Recognize()`** est la méthode qui **recognize receipt image** réellement. En interne, elle effectue la binarisation, la segmentation et la classification des caractères.  
* L’exportation en JSON et XML vous fournit à la fois un dump lisible par l’homme et une structure adaptée aux machines que vous pouvez transmettre à des analyseurs en aval.

## Étape 3 : Exécuter la démo et vérifier la sortie

Compilez et lancez :

```bash
dotnet run
```

Si tout est correctement configuré, vous verrez quelque chose comme :

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

La console affiche le texte brut, tandis que `receipt.json` et `receipt.xml` contiennent des informations détaillées de mise en page (coordonnées, scores de confiance, etc.). Ces fichiers sont pratiques si vous devez plus tard mapper chaque ligne à un champ de base de données.

## Cas limites & astuces pro

### 1️⃣ Licence manquante ou invalide
Si `SetLicense` échoue, le moteur repasse en mode essai et vous obtiendrez un filigrane dans la sortie. Enveloppez l’appel dans un try/catch et consignez un message convivial :

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ Formats d’image non pris en charge
Aspose.OCR accepte la plupart des formats raster, mais si vous lui fournissez un PDF ou un TIFF multi‑pages, vous devrez d’abord convertir la page qui vous intéresse en image. La bibliothèque `Aspose.PDF` peut gérer cette conversion.

### 3️⃣ Gros tickets & performances
Traiter une image de 10 Mo peut être lent. Réduisez la résolution avant de la transmettre au moteur :

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

La méthode `Resize` conserve le ratio d’aspect (`0` pour la hauteur) et diminue considérablement la taille du fichier sans sacrifier la précision de l’OCR pour des tickets classiques.

### 4️⃣ Problèmes de langue & de police
Les tickets peuvent contenir des caractères spéciaux (€, ¥, etc.). Définissez explicitement la langue si vous connaissez la locale :

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

Pour les tickets multilingues, vous pouvez activer le mode multilingue :

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ Extraction de données structurées
Le texte brut est utile, mais la plupart des applications ont besoin de champs structurés (date, total, articles). La mise en page JSON inclut les coordonnées `BoundingBox` de chaque mot. Vous pouvez le post‑traiter ainsi :

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

Cet extrait montre l’idée ; en production vous utiliserez probablement une expression régulière ou un petit moteur de règles.

## Questions fréquentes

**Q : Puis‑je exécuter cela sous Linux ?**  
R : Absolument. Aspose.OCR est multiplateforme ; il suffit d’installer le runtime .NET sur votre machine Linux et le même code fonctionnera.

**Q : Et si je dois traiter des dizaines de tickets par minute ?**  
R : Lancez une boucle `Parallel.ForEach` et réutilisez une seule instance de `OcrEngine` – elle est thread‑safe pour les opérations en lecture seule. N’oubliez pas de gérer les limites de concurrence de la licence.

**Q : Cela fonctionne‑t‑il avec des photos mobiles prises sous un angle ?**  
R : Le moteur inclut une correction de base de l’inclinaison, mais pour des images fortement penchées vous pouvez pré‑traiter avec une bibliothèque de traitement d’image (par ex., OpenCV) afin de redresser le ticket au préalable.

## Exemple complet (Copier‑Coller)

Voici le *programme entier* que vous pouvez coller dans `Program.cs`. Aucun autre fichier n’est requis en dehors de la licence et d’une image de ticket.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}