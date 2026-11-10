---
category: general
date: 2026-05-25
description: Apprenez à extraire du texte d’une image avec une API ASP.NET Core minimale.
  Téléversez l’image via POST, lisez les données de formulaire multipart et effectuez
  la reconnaissance optique de caractères (OCR) sur l’image.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: fr
og_description: Extraire du texte d’une image à l’aide d’une API ASP.NET Core minimale.
  Ce guide montre comment télécharger une image via POST, lire les données de formulaire
  multipart et effectuer la reconnaissance optique de caractères (OCR) sur l’image.
og_title: Extraire du texte d’une image dans ASP.NET Core – Étape par étape
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  headline: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  type: TechArticle
- description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  name: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  steps:
  - name: Breaking Down the Logic
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **ReadFormAsync** | Parses the incoming *multipart/form-data* request. | Without
      this, you can’t access the uploaded files. | | **form.Files["image"]** | Retrieves
      the file whose form‑field name is `image`. | Guarant'
  - name: 1. Large Files
    text: 'The default request body limit is 30 MB. For larger scans you might need
      to adjust:'
  - name: 2. Asynchronous OCR
    text: Some OCR libraries expose async methods (`RecognizeAsync`). If yours does,
      replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the
      lambda as `async`.
  - name: 3. Security Considerations
    text: '- **Validate file size** before loading it into memory. - **Sanitize the
      filename** if you ever write it to disk. - **Rate‑limit** the endpoint to avoid
      denial‑of‑service attacks.'
  - name: 4. GPU Acceleration
    text: If you uncomment the `engine.GpuDevice = new GpuDevice(0);` line and your
      hardware supports CUDA or DirectML, you’ll see a noticeable speed boost, especially
      on high‑resolution images.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Minimal API
title: Extraire du texte d’une image dans une API minimale ASP.NET Core – Guide complet
url: /fr/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image avec ASP.NET Core Minimal API – Guide complet

Vous êtes‑vous déjà demandé comment **extraire du texte d'une image** sans vous battre avec des frameworks lourds ? Vous n'êtes pas seul. De nombreux développeurs ont besoin d'une méthode rapide pour permettre aux utilisateurs de déposer une image et de récupérer les caractères bruts, que ce soit pour scanner des reçus, numériser des notes manuscrites ou alimenter un index de recherche.

Dans ce tutoriel, nous créerons une petite ASP.NET Core Minimal API qui **télécharge une image via POST**, analyse la charge *multipart/form‑data*, puis **effectue une OCR sur l'image** à l'aide d'un singleton `OcrEngine`. À la fin, vous disposerez d'une application entièrement fonctionnelle que vous pourrez intégrer à n'importe quel projet .NET 8 et commencer à extraire du texte d'une image immédiatement.

## Ce que vous allez construire

- Une application web minimale qui écoute sur `/ocr`.
- Un point de terminaison qui accepte un fichier image envoyé avec une requête POST `multipart/form-data`.
- Une logique qui lit le fichier téléchargé, le transmet au moteur OCR et renvoie les résultats en texte brut.
- Extrait de code optionnel d'accélération GPU (commenté) pour ceux disposant d'une carte compatible.

**Prérequis**  
- .NET 8 SDK (ou ultérieur).  
- Familiarité de base avec C# et la ligne de commande.  
- Une bibliothèque OCR qui expose une classe `OcrEngine` (l'exemple suppose un package NuGet hypothétique).  

Si vous avez tout cela, plongeons‑y.

## Étape 1 : Configurer le projet et ajouter le package OCR

Tout d'abord, créez un nouveau projet web et ajoutez la bibliothèque OCR.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Astuce :** Gardez vos dépendances à jour. Les versions plus récentes offrent souvent des gains de performance, notamment pour l'inférence accélérée par GPU.

## Étape 2 : Enregistrer un moteur OCR singleton (service principal)

Nous voulons une seule instance de `OcrEngine` pour toute l'application — pas besoin de créer un nouveau moteur à chaque requête. Enregistrez‑le dans le conteneur de services du builder.

```csharp
using Awesome.Ocr;               // <-- the OCR library namespace
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using System.Drawing;            // System.Drawing.Common for Image handling

var builder = WebApplication.CreateBuilder(args);

// Register a singleton OCR engine (English language)
// Uncomment the GPU line if you have a compatible GPU and the library supports it.
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU acceleration
    return engine;
});
```

**Pourquoi un singleton ?**  
Créer un moteur OCR peut être coûteux — pensez au chargement des poids du réseau neuronal en mémoire. En réutilisant la même instance, nous économisons à la fois des cycles CPU et de la RAM, ce qui se traduit par des temps de réponse plus rapides pour chaque appel `/ocr`.

## Étape 3 : Construire l'application

Nous matérialisons maintenant l'objet `WebApplication`.

```csharp
var app = builder.Build();
```

Cette ligne semble presque magique, mais en coulisses elle configure le routage, le middleware et le conteneur d’injection de dépendances que nous venons de configurer.

## Étape 4 : Définir le point de terminaison POST – « Télécharger une image via POST »

Voici le cœur du tutoriel : un point de terminaison qui **télécharge une image via POST**, lit la charge multipart et transmet les données au moteur OCR.

```csharp
app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    // Step 5: Read multipart form data and extract the uploaded image
    var form = await request.ReadFormAsync();               // <-- read multipart/form-data
    var file = form.Files["image"];                         // expects a field named "image"

    if (file is null || file.Length == 0)
    {
        return Results.BadRequest("No image file provided.");
    }

    // Guard against unsupported content types
    if (!file.ContentType.StartsWith("image/"))
    {
        return Results.BadRequest("Uploaded file is not an image.");
    }

    // Load the image into a System.Drawing.Image
    using var img = Image.FromStream(file.OpenReadStream());

    // Step 6: Perform OCR on the image
    string text = ocr.Recognize(img);                       // <-- perform OCR on image

    // Step 7: Return the extracted text as plain‑text
    return Results.Text(text);
});
```

### Décomposition de la logique

| Étape | Ce qui se passe | Pourquoi c’est important |
|------|------------------|---------------------------|
| **ReadFormAsync** | Analyse la requête *multipart/form-data* entrante. | Sans cela, vous ne pouvez pas accéder aux fichiers téléchargés. |
| **form.Files["image"]** | Récupère le fichier dont le nom du champ de formulaire est `image`. | Garantit un contrat prévisible pour les appelants. |
| **Content‑type check** | Vérifie que le fichier est une image (par ex., `image/png`). | Empêche le moteur OCR de planter avec des données non‑image. |
| **Image.FromStream** | Convertit le flux brut en un `System.Drawing.Image`. | La bibliothèque OCR attend un objet `Image`, pas un tableau d'octets brut. |
| **ocr.Recognize(img)** | Appelle le moteur OCR pour **reconnaître le texte à partir de l'image**. | C’est l’étape principale pour **effectuer l’OCR sur l’image**. |
| **Results.Text** | Renvoie la réponse en texte brut. | Un format simple et exploitable pour les services en aval. |

## Étape 5 : Exécuter l'API

Enfin, démarrez le serveur web.

```csharp
app.Run();
```

Lorsque vous exécutez `dotnet run`, l'API écoutera sur `http://localhost:5000` (ou le port de votre choix). Vous pouvez la tester avec `curl` :

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Sortie attendue :** La console affichera les caractères reconnus, par ex. :

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

Si l'image est floue ou que la langue n’est pas prise en charge, le moteur OCR renverra une chaîne vide ou un message d’erreur — gérez ces cas dans le code de production.

## Cas limites & bonnes pratiques

### 1. Fichiers volumineux

La limite par défaut du corps de la requête est de 30 Mo. Pour des scans plus grands, vous pourriez devoir l’ajuster :

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. OCR asynchrone

Certaines bibliothèques OCR exposent des méthodes asynchrones (`RecognizeAsync`). Si la vôtre le fait, remplacez `ocr.Recognize(img)` par `await ocr.RecognizeAsync(img)` et marquez le lambda comme `async`.

### 3. Considérations de sécurité

- **Validez la taille du fichier** avant de le charger en mémoire.
- **Sanitisez le nom de fichier** si vous l’écrivez jamais sur le disque.
- **Limitez le taux** du point de terminaison pour éviter les attaques par déni de service.

### 4. Accélération GPU

Si vous décommentez la ligne `engine.GpuDevice = new GpuDevice(0);` et que votre matériel prend en charge CUDA ou DirectML, vous constaterez une amélioration de vitesse notable, surtout sur des images haute résolution.

## Exemple complet fonctionnel

Voici le `Program.cs` complet que vous pouvez copier‑coller dans un nouveau projet Minimal API.

```csharp
using Awesome.Ocr;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Http.Features;
using System.Drawing;

var builder = WebApplication.CreateBuilder(args);

// Optional: increase multipart limit for big images
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});

// Register the OCR engine as a singleton
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU if available
    return engine;
});

var app = builder.Build();

app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    var form = await request.ReadFormAsync();
    var file = form.Files["image"];

    if (file is null || file.Length == 0)
        return Results.BadRequest("No image file provided.");

    if (!file.ContentType.StartsWith("image/"))
        return Results.BadRequest("Uploaded file is not an image.");

    using var img = Image.FromStream(file.OpenReadStream());

    // Core OCR operation
    string text = ocr.Recognize(img);

    return Results.Text(text);
});

app.Run();
```

Enregistrez, exécutez `dotnet run`, et vous êtes prêt à **extraire du texte d'une image** à la demande.

## Conclusion

Nous avons parcouru une **solution complète, de bout en bout** pour extraire du texte d'une image avec ASP.NET Core Minimal API. En partant de la structure du projet, nous **avons enregistré un moteur OCR singleton**, construit un point de terminaison qui **télécharge une image via POST**, **lit les données multipart du formulaire**, et enfin **effectue l’OCR sur l’image** pour renvoyer du texte brut propre.

À partir d'ici, vous pouvez :

- Ajouter des enveloppes JSON pour des réponses plus riches.
- Brancher une base de données pour stocker le texte extrait.
- Étendre le support à plusieurs langues (`OcrLanguage.Spanish`, etc.).

Le modèle s’adapte bien — il suffit d’insérer le même point de terminaison dans un microservice plus grand ou de l’exposer derrière une passerelle API.

Des questions sur la gestion des PDF, le traitement par lots ou l’optimisation GPU ? Laissez un commentaire, et bon codage !

## Tutoriels associés

- [Extraire du texte d'une image avec Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extraire du texte d'une image – Optimisation OCR avec Aspose.OCR pour .NET](/ocr/english/net/ocr-optimization/)
- [Extraire le texte d'une image C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}