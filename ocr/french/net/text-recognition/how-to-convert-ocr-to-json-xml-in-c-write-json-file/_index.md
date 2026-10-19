---
category: general
date: 2026-04-01
description: Comment convertir la sortie OCR en JSON et XML en C# – apprenez à extraire
  du texte d’une image et à écrire un fichier JSON en C# avec Aspose.OCR.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: fr
og_description: Comment convertir les résultats OCR en fichiers JSON et XML structurés
  avec C#. Guide étape par étape pour extraire le texte d’une image et écrire un fichier
  JSON en C#.
og_title: Comment convertir l'OCR en JSON et XML en C# – Écrire un fichier JSON
tags:
- OCR
- C#
- Aspose
title: Comment convertir l'OCR en JSON et XML en C# – écrire un fichier JSON
url: /fr/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment convertir l'OCR en JSON & XML en C# – Écrire un fichier JSON

**Comment convertir l'OCR** en résultats utilisables est une question que se posent de nombreux développeurs. Dans ce guide, nous vous montrerons comment extraire du texte d’une image, transformer la sortie OCR en JSON et XML correctement formatés, puis écrire ces fichiers sur le disque avec C#.

Si vous avez déjà regardé une chaîne OCR brute et pensé « Il doit bien y avoir une meilleure façon de stocker cela », vous êtes au bon endroit. À la fin, vous disposerez d’un programme complet et exécutable qui non seulement **extrait du texte d’une image**, mais sait aussi **écrire un fichier JSON C#** et **écrire un fichier XML C#** sans effort.

## Ce dont vous avez besoin

- **.NET 6.0** ou version ultérieure (le code fonctionne également avec .NET Framework 4.6+).  
- Package NuGet **Aspose.OCR** – installez‑le avec `dotnet add package Aspose.OCR`.  
- Une image contenant du texte (par ex., `invoice.png`).  
- L’IDE de votre choix – Visual Studio, Rider ou VS Code conviendront.

> **Astuce pro :** Conservez vos fichiers image dans un dossier dédié (par ex., `Resources/`) afin que les chemins restent propres.

## Étape 1 : Configurer le moteur OCR – Comment convertir l'OCR

Tout d’abord, nous créons une instance `OcrEngine` et indiquons la langue à rechercher. Dans la plupart des cas, l’anglais suffit, mais vous pouvez remplacer `Language.English` par n’importe quelle langue prise en charge.

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **Pourquoi c’est important :** Initialiser le moteur avec la bonne langue améliore considérablement la précision, surtout pour les scripts non latins.

## Étape 2 : Reconnaître le texte – Extraire le texte de l’image

Nous transmettons maintenant l’image au moteur. La méthode `Recognize` renvoie un objet `OcrResult` contenant le texte brut ainsi que les données de localisation.

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

Si l’image est introuvable, `Recognize` lève une `FileNotFoundException`. Pour simplifier la démonstration, nous supposons que le chemin est correct, mais en production vous devriez entourer cet appel d’un bloc try‑catch.

## Étape 3 : Convertir le résultat en JSON – Écrire un fichier JSON C#

Aspose.OCR rend la sérialisation très simple. La méthode `ToJson` accepte un paramètre `indent` pour produire une sortie joliment indentée, idéale lorsque vous prévoyez d’ouvrir le fichier dans un éditeur de texte.

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### Exemple de JSON attendu

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **Comment extraire le texte** : La propriété `Text` vous fournit la chaîne brute que vous pouvez transmettre à d’autres services (index de recherche, bases de données, etc.).

## Étape 4 : Persister le JSON – Écrire un fichier JSON C# (suite)

Avec la chaîne JSON prête, il suffit de l’écrire dans un fichier avec `File.WriteAllText`. Cela garantit l’encodage UTF‑8 par défaut.

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

Vous avez maintenant un `invoice.json` à côté de votre image, prêt pour le traitement en aval.

## Étape 5 : Convertir le résultat en XML – Écrire un fichier XML C#

Si vous préférez le XML pour des systèmes hérités, la méthode `ToXml` fait le travail lourd. Comme `ToJson`, elle supporte également le formatage lisible.

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### Exemple de XML attendu

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## Étape 6 : Persister le XML – Écrire un fichier XML C# (suite)

Enregistrer le XML est identique à l’étape JSON ; il suffit de pointer vers une extension `.xml`.

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### Exemple complet fonctionnel

En combinant le tout, voici le programme complet que vous pouvez copier‑coller dans une application console :

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

Exécutez le programme, et vous trouverez deux nouveaux fichiers—`invoice.json` et `invoice.xml`—exactement où vous les avez spécifiés. Ouvrez‑les pour vérifier que la structure correspond aux exemples ci‑dessus.

## Questions fréquentes & Cas particuliers

| Question | Réponse |
|----------|--------|
| **Et si l’image contient plusieurs langues ?** | Créez des instances `OcrEngine` distinctes pour chaque langue ou utilisez `Language.Multi` si elle est prise en charge. |
| **Puis‑je contrôler le format de sortie (par ex., exclure les données de région) ?** | Oui. `ToJson` et `ToXml` acceptent des paramètres optionnels pour filtrer les champs ; consultez la documentation Aspose.OCR pour `ExportOptions`. |
| **Comment gérer de gros PDF avec de nombreuses pages ?** | Traitez chaque page séparément, agrégerez les résultats, puis sérialisez une fois. |
| **Le résultat est‑il sûr en UTF‑8 ?** | Absolument — Aspose.OCR utilise Unicode en interne, et `File.WriteAllText` écrit en UTF‑8 par défaut. |
| **Qu’en est‑il des performances ?** | L’OCR est gourmand en CPU. Pour les traitements par lots, envisagez le parallélisme sur plusieurs cœurs ou l’API cloud d’Aspose. |

## Conclusion

Vous savez maintenant **comment convertir les résultats OCR** en JSON et XML avec C#. En suivant les étapes ci‑dessus, vous pouvez **extraire du texte d’une image**, puis **écrire un fichier JSON C#** et **écrire un fichier XML C#** en quelques lignes seulement. Cette approche est rapide, fiable et fonctionne avec tout type d’image supporté par Aspose.OCR.

Prêt pour le prochain défi ? Essayez d’alimenter le

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}