---
category: general
date: 2026-06-28
description: reconnaître du texte à partir d'une image dans ASP.NET Core – apprenez
  à télécharger une image pour l'OCR et à traiter efficacement une image OCR depuis
  un flux.
draft: false
keywords:
- recognize text from image
- upload image for ocr
- ocr image from stream
language: fr
og_description: Reconnaître le texte d’une image en utilisant Aspose OCR dans ASP.NET
  Core. Télécharger l’image pour l’OCR, gérer l’image OCR depuis le flux et renvoyer
  le texte nettoyé.
og_title: Reconnaître du texte à partir d'une image dans ASP.NET Core – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: recognize text from image in ASP.NET Core – learn how to upload image
    for OCR and process ocr image from stream efficiently.
  headline: recognize text from image in ASP.NET Core – upload for OCR
  type: TechArticle
- description: recognize text from image in ASP.NET Core – learn how to upload image
    for OCR and process ocr image from stream efficiently.
  name: recognize text from image in ASP.NET Core – upload for OCR
  steps:
  - name: Why This Pattern Works
    text: '- **Single `OcrEngine` instance**: Instantiating the engine once avoids
      the overhead of loading language data on every request. - **Async everything**:
      By using `await` on `FromStreamAsync` and `RecognizeAsync`, the ASP.NET Core
      thread pool stays free to serve other callers. - **`IFormFile` binding*'
  - name: Edge Cases to Watch
    text: '- **Corrupt files**: If the uploaded file isn’t a valid image, `FromStreamAsync`
      throws an exception. Wrap the call in a try/catch if you need graceful error
      messages. - **Unsupported formats**: Aspose supports PNG, JPEG, BMP, TIFF, etc.
      If you need PDF input, you’ll have to convert it to an image f'
  - name: Why Not Use `Recognize` (Sync)?
    text: The synchronous version would block the ASP.NET Core thread pool until the
      CPU‑intensive OCR finishes. On a busy server that quickly becomes a bottleneck,
      leading to 504 timeouts. The async variant keeps the API snappy.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Aspose.OCR
title: Reconnaître le texte d’une image dans ASP.NET Core – téléverser pour OCR
url: /fr/net/ocr-optimization/recognize-text-from-image-in-asp-net-core-upload-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte à partir d'une image dans ASP.NET Core – Tutoriel complet

Vous avez déjà eu besoin de **reconnaître du texte à partir d'une image** dans une API web et vous ne saviez pas par où commencer ? Vous n'êtes pas seul. Dans de nombreux projets—pensez aux scanners de factures, aux traceurs de reçus, ou même à une simple fonction « read‑me »—obtenir des résultats OCR fiables est une compétence indispensable.

Dans ce guide, nous parcourrons un exemple complet, prêt à l’emploi, qui vous montre comment **téléverser une image pour l’OCR**, transformer ce téléversement en une **image OCR à partir d’un flux**, et enfin renvoyer le texte extrait sous forme de JSON propre. Aucun morceau manquant, aucune référence vague—juste une solution autonome que vous pouvez intégrer dans n’importe quel projet ASP.NET Core dès aujourd’hui.

## Ce que vous retirerez de ce tutoriel

- Un `OcrController` entièrement fonctionnel qui accepte les téléversements multipart/form.  
- Explication pas à pas de chaque ligne, afin que vous compreniez *pourquoi* nous faisons ce que nous faisons.  
- Astuces pour gérer les gros fichiers, éviter le blocage des threads, et garder votre API réactive.  
- Un aperçu de la façon d’étendre la solution (plusieurs langues, prétraitement d’image, etc.).  

**Prérequis** : .NET 6 ou ultérieur, Visual Studio 2022 (ou VS Code), et une licence Aspose.OCR (l’essai gratuit suffit pour les tests). Si vous avez tout cela, plongeons‑y.

![diagramme du flux de reconnaissance de texte à partir d'une image](https://example.com/ocr-workflow.png "diagramme du flux de reconnaissance de texte à partir d'une image")

## Comment reconnaître du texte à partir d’une image dans ASP.NET Core

Le cœur de la solution réside dans un seul contrôleur. Ci-dessous se trouve le **code complet et exécutable** ; chaque import, chaque directive `using` et chaque appel asynchrone sont inclus afin que vous puissiez le copier‑coller directement dans un nouveau projet ASP.NET Core Web API.

```csharp
using Aspose.OCR;
using Microsoft.AspNetCore.Mvc;
using System.Threading.Tasks;

[ApiController]
[Route("api/ocr")]
public class OcrController : ControllerBase
{
    // Step 1: Create a reusable OCR engine instance
    // Reusing the same OcrEngine across requests saves memory and speeds up init.
    private readonly OcrEngine _ocrEngine = new OcrEngine();

    // Step 2: Define the endpoint that accepts a file upload
    [HttpPost("recognize")]
    public async Task<IActionResult> Recognize([FromForm] IFormFile uploadedFile)
    {
        // Guard clause – make sure we actually got a file
        if (uploadedFile == null || uploadedFile.Length == 0)
            return BadRequest(new { error = "No file uploaded." });

        // Step 3: Open the uploaded file as a read‑only stream
        // This is the **ocr image from stream** part.
        await using var imageStream = uploadedFile.OpenReadStream();

        // Step 4: Load the image asynchronously for OCR processing
        // Aspose.OCR provides FromStreamAsync which off‑loads the I/O work.
        var ocrImage = await OcrImage.FromStreamAsync(imageStream);

        // Step 5: Run OCR recognition without blocking the request thread
        // RecognizeAsync runs the heavy lifting on a background thread.
        var ocrResult = await _ocrEngine.RecognizeAsync(ocrImage);

        // Step 6: Return the extracted text as a JSON response
        return Ok(new { text = ocrResult.Text });
    }
}
```

### Pourquoi ce modèle fonctionne

- **Instance unique de `OcrEngine`** : Instancier le moteur une seule fois évite le surcoût de chargement des données linguistiques à chaque requête.  
- **Tout en async** : En utilisant `await` sur `FromStreamAsync` et `RecognizeAsync`, le pool de threads d’ASP.NET Core reste libre pour servir d’autres appelants.  
- **Liaison `IFormFile`** : L’attribut `[FromForm]` permet au client d’envoyer simplement une requête POST multipart/form‑data—exactement ce que les navigateurs et outils comme Postman savent déjà faire.  

Maintenant que le code est devant vous, décomposons chaque partie logique.

## Téléverser une image pour l’OCR – Gestion de la requête multipart

Lorsqu’un client envoie un fichier, ASP.NET Core le lie à `IFormFile`. Cet objet nous fournit une poignée sécurisée vers les octets bruts sans charger le fichier entier en mémoire d’un coup.

```csharp
[HttpPost("recognize")]
public async Task<IActionResult> Recognize([FromForm] IFormFile uploadedFile)
{
    if (uploadedFile == null || uploadedFile.Length == 0)
        return BadRequest(new { error = "No file uploaded." });

    // …
}
```

**Astuce** : Si vous prévoyez de très grandes images (pensez >10 Mo), envisagez d’ajouter une vérification de taille ici et de renvoyer un 413 Payload Too Large. Cela protège votre serveur des plantages OOM accidentels.

## Traiter l’image OCR à partir d’un flux de manière asynchrone

La ligne `await OcrImage.FromStreamAsync(imageStream)` effectue le travail lourd de décodage des octets d’image dans un format qu’Aspose.OCR peut comprendre. Comme elle est asynchrone, les I/O sous‑jacents (disque ou réseau) ne bloqueront pas le thread de la requête.

```csharp
await using var imageStream = uploadedFile.OpenReadStream();
var ocrImage = await OcrImage.FromStreamAsync(imageStream);
```

### Cas limites à surveiller

- **Fichiers corrompus** : Si le fichier téléversé n’est pas une image valide, `FromStreamAsync` lève une exception. Enveloppez l’appel dans un try/catch si vous avez besoin de messages d’erreur plus doux.  
- **Formats non pris en charge** : Aspose prend en charge PNG, JPEG, BMP, TIFF, etc. Si vous avez besoin d’un PDF en entrée, vous devrez d’abord le convertir en image (Aspose.PDF peut aider).

## Exécuter le moteur OCR sans blocage

`_ocrEngine.RecognizeAsync(ocrImage)` exécute l’algorithme OCR sur un thread d’arrière‑plan. C’est le moment où l’opération de **reconnaissance de texte à partir d’une image** se produit réellement.

```csharp
var ocrResult = await _ocrEngine.RecognizeAsync(ocrImage);
```

Le `ocrResult` retourné contient une propriété `Text` avec la chaîne brute extraite. Vous pouvez la post‑traiter davantage (supprimer les espaces, corriger les erreurs OCR courantes, etc.) avant de la renvoyer.

### Pourquoi ne pas utiliser `Recognize` (synchrone) ?

La version synchrone bloquerait le pool de threads d’ASP.NET Core jusqu’à ce que l’OCR gourmand en CPU se termine. Sur un serveur chargé, cela devient rapidement un goulot d’étranglement, entraînant des time‑outs 504. La variante asynchrone garde l’API réactive.

## Retourner un JSON propre – La pièce finale

```csharp
return Ok(new { text = ocrResult.Text });
```

Les clients reçoivent une charge JSON bien structurée :

```json
{
  "text": "Sample extracted text from the uploaded image."
}
```

Si vous avez besoin de métadonnées supplémentaires—scores de confiance, détection de langue, boîtes englobantes—élargissez simplement l’objet anonyme ou définissez un DTO approprié.

## Tester le point de terminaison

Vous pouvez vérifier que tout fonctionne avec **cURL**, **Postman**, ou même un simple formulaire HTML.

```bash
curl -X POST https://localhost:5001/api/ocr/recognize \
     -F "uploadedFile=@/path/to/your/image.png"
```

Une réponse réussie ressemble à :

```
{"text":"Hello World"}
```

Si vous oubliez d’envoyer un fichier, vous recevrez :

```
{"error":"No file uploaded."}
```

## Aller plus loin – Améliorations courantes

| Amélioration | Pourquoi cela aide | Astuce de code rapide |
|------------|--------------|-----------------|
| **Sélection de la langue** | La précision de l’OCR s’améliore quand vous indiquez au moteur la langue attendue. | `_ocrEngine.Language = OcrLanguage.English;` |
| **Prétraitement d’image** | Ajuster la luminosité/contraste peut sauver des numérisations de mauvaise qualité. | `ocrImage = OcrImage.FromBitmap(ImageProcessor` |

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment extraire du texte d’image depuis un flux en utilisant Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extraire du texte d’une image – Optimisation OCR avec Aspose.OCR pour .NET](/ocr/english/net/ocr-optimization/)
- [Extraire le texte d’une image en C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}