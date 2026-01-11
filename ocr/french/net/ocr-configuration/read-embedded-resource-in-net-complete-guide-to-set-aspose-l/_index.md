---
category: general
date: 2026-01-10
description: Lire une ressource intégrée et définir la licence Aspose en C#. Apprenez
  à utiliser GetManifestResourceStream, à intégrer un fichier de licence et à obtenir
  l'assembly d'exécution .NET dans un seul tutoriel.
draft: false
keywords:
- read embedded resource
- set aspose license
- use getmanifestresourcestream
- how to embed license
- get executing assembly .net
language: fr
og_description: Lisez une ressource intégrée dans .NET et configurez rapidement la
  licence Aspose. Guide étape par étape couvrant GetManifestResourceStream, l’intégration
  de la licence et l’utilisation de l’assembly en cours d’exécution.
og_title: Lire la ressource incorporée – Définir la licence Aspose dans .NET
tags:
- C#
- .NET
- Aspose OCR
- Embedded Resources
title: Lire une ressource intégrée dans .NET – Guide complet pour configurer la licence
  Aspose
url: /fr/net/ocr-configuration/read-embedded-resource-in-net-complete-guide-to-set-aspose-l/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lire une ressource intégrée – Guide complet pour définir la licence Aspose

Vous avez déjà eu besoin de **lire une ressource intégrée** à l’exécution et vous vous êtes demandé comment obtenir votre bibliothèque Aspose OCR sous licence sans coder en dur les chemins ? Vous n’êtes pas seul. Dans de nombreuses applications d’entreprise, le fichier de licence vit à l’intérieur de l’assembly afin de ne pas avoir à déployer de fichiers supplémentaires ou à se soucier de permissions manquantes. Ce tutoriel vous montre exactement comment lire une ressource intégrée et définir la licence Aspose en utilisant la méthode .NET `GetManifestResourceStream`.

Nous passerons en revue tout ce dont vous avez besoin : intégrer le fichier `.lic`, le récupérer avec `GetExecutingAssembly`, puis l’appliquer à la classe `License` d’Aspose OCR. À la fin, vous disposerez d’une solution autonome qui fonctionne sur n’importe quel projet .NET—sans fichiers externes requis.

## Ce que vous allez apprendre

- **Comment intégrer un fichier de licence** dans un projet .NET afin qu’il devienne partie du DLL compilé.
- La bonne façon **d’utiliser GetManifestResourceStream** pour lire cette ressource intégrée.
- Comment **définir la licence Aspose** programmatique sans toucher au système de fichiers.
- Astuces pour gérer les pièges courants comme les noms de ressources mal orthographiés ou les actions de génération manquantes.
- Un exemple de code complet, exécutable, que vous pouvez copier‑coller dans votre propre solution.

### Prérequis

- .NET 6.0 ou supérieur (le code fonctionne également avec .NET Framework 4.x, il suffit d’ajuster le fichier projet en conséquence).
- Package NuGet Aspose.OCR installé (`dotnet add package Aspose.OCR`).
- Familiarité de base avec C# et Visual Studio (ou votre IDE préféré).

Si vous avez déjà ces éléments en place, super—plongeons‑y.

## Étape 1 : Intégrer le fichier de licence Aspose dans votre assembly

La première chose dont vous avez besoin est le vrai fichier de licence (`Aspose.OCR.lic`). Au lieu de le copier à côté de votre exécutable, vous allez l’intégrer comme **ressource**.

1. Ajoutez le fichier `.lic` à votre projet (par ex., créez un dossier `Resources` et déposez le fichier à l’intérieur).
2. Dans les propriétés du fichier, définissez **Build Action** sur `Embedded Resource`.  
   *Astuce :* gardez la structure de dossiers simple ; le nom complet de la ressource sera `YourNamespace.Resources.Aspose.OCR.lic`.

```text
MyApp/
 └─ Resources/
     └─ Aspose.OCR.lic   ← Build Action = Embedded Resource
```

Pourquoi intégrer ? Parce que l’assembly porte maintenant la licence en interne, éliminant le risque d’un fichier manquant sur un serveur de production.

## Étape 2 : Récupérer la ressource intégrée avec GetExecutingAssembly

Maintenant que la licence vit à l’intérieur du DLL, il vous faut un moyen de **lire la ressource intégrée** à l’exécution. La classe .NET `Assembly` vous fournit exactement cela.

```csharp
using System.Reflection;

// Get the assembly that contains the embedded resource
Assembly currentAssembly = Assembly.GetExecutingAssembly();
```

La méthode `GetExecutingAssembly` renvoie l’assembly qui s’exécute actuellement—parfait pour localiser les ressources qui se trouvent à côté de votre code.

## Étape 3 : Ouvrir le flux de licence avec GetManifestResourceStream

Avec la référence à l’assembly en main, vous pouvez appeler `GetManifestResourceStream`. Cette méthode renvoie un `Stream` que vous pouvez transmettre directement à Aspose.

```csharp
// Build the fully qualified resource name
string resourceName = "MyApp.Resources.Aspose.OCR.lic";

// Attempt to open the resource stream
using Stream? licenseStream = currentAssembly.GetManifestResourceStream(resourceName);

if (licenseStream == null)
{
    throw new InvalidOperationException(
        $"Unable to locate embedded resource '{resourceName}'. " +
        "Check the namespace and Build Action settings.");
}
```

Remarquez que nous utilisons une instruction `using` **null‑conditional** (`using Stream?`) afin de garantir que le flux soit automatiquement libéré. Si le nom est incorrect, nous levons une exception claire—cela vous évite des échecs silencieux plus tard.

## Étape 4 : Appliquer la licence à Aspose OCR

La classe `License` d’Aspose attend un `Stream`. Nous en avons déjà un, donc la dernière étape est directe.

```csharp
using Aspose.OCR;

// Create a License instance and set the license from the stream
License ocrLicense = new License();
ocrLicense.SetLicense(licenseStream);
```

C’est tout ! Le moteur Aspose OCR est maintenant entièrement licencié et prêt à traiter des images sans le filigrane d’évaluation.

## Exemple complet fonctionnel

Voici un programme complet, prêt à copier‑coller, qui démontre l’ensemble du processus. Il inclut les directives `using` nécessaires, la gestion des erreurs, et un appel OCR simple pour prouver que la licence est active.

```csharp
// Program.cs
using System;
using System.IO;
using System.Reflection;
using Aspose.OCR;

namespace MyApp
{
    class Program
    {
        static void Main()
        {
            try
            {
                // Step 1: Get the current executing assembly
                Assembly currentAssembly = Assembly.GetExecutingAssembly();

                // Step 2: Build the resource name (adjust namespace/folder as needed)
                const string resourceName = "MyApp.Resources.Aspose.OCR.lic";

                // Step 3: Retrieve the embedded license stream
                using Stream? licenseStream = currentAssembly.GetManifestResourceStream(resourceName);
                if (licenseStream == null)
                {
                    Console.WriteLine($"Failed to locate embedded resource: {resourceName}");
                    return;
                }

                // Step 4: Apply the license
                License ocrLicense = new License();
                ocrLicense.SetLicense(licenseStream);
                Console.WriteLine("Aspose OCR license applied successfully.");

                // Optional: Quick test – recognize text from a sample image
                var ocrEngine = new OcrEngine();
                ocrEngine.Image = ImageStream.FromFile("sample.png"); // replace with your image path
                if (ocrEngine.Process())
                {
                    Console.WriteLine("OCR Result:");
                    Console.WriteLine(ocrEngine.Text);
                }
                else
                {
                    Console.WriteLine("OCR processing failed.");
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

### Sortie attendue

Lorsque vous exécutez le programme sur une machine avec une licence valide intégrée, vous devriez voir :

```
Aspose OCR license applied successfully.
OCR Result:
[Detected text from sample.png]
```

Si le flux de licence est introuvable, la console affichera le nom de la ressource manquante, vous guidant ainsi à revérifier le **Build Action** et l’espace de noms.

## Problèmes courants & comment les éviter

| Problème | Pourquoi cela arrive | Solution |
|----------|----------------------|----------|
| **Nom de ressource incorrect** | .NET construit le nom de la ressource à partir de l’espace de noms par défaut + le chemin du dossier. | Utilisez `Assembly.GetManifestResourceNames()` pour lister les noms disponibles et vérifier la chaîne exacte. |
| **Fichier de licence non défini comme Embedded Resource** | L’action de génération par défaut est `Content`. | Changez‑la en `Embedded Resource` dans les propriétés du fichier. |
| **Exécution depuis un assembly différent** | Si vous appelez le code depuis une bibliothèque de classes, `GetExecutingAssembly()` peut renvoyer la bibliothèque au lieu de l’exe principal. | Utilisez `Assembly.GetEntryAssembly()` ou transmettez explicitement l’assembly correct. |
| **Flux disposé trop tôt** | Utilisation accidentelle d’un bloc `using` qui ferme le flux prématurément. | Gardez le `using` autour de l’appel `SetLicense`, comme montré ci‑dessus. |
| **Incompatibilité de version Aspose.OCR** | Les versions plus récentes peuvent exiger un format de licence différent. | Téléchargez toujours la dernière licence depuis votre compte Aspose et ré‑intégrez‑la. |

## Utiliser la même technique pour d’autres fichiers intégrés

Le schéma—**lire une ressource intégrée**, puis **utiliser GetManifestResourceStream**—fonctionne pour tout type de fichier : configurations JSON, images, même DLL natives. Il suffit d’ajuster le `resourceName` et la façon dont vous consommez le flux.

```csharp
// Example: Load an embedded JSON config
string jsonName = "MyApp.Resources.Config.appsettings.json";
using var jsonStream = Assembly.GetExecutingAssembly()
                               .GetManifestResourceStream(jsonName);
using var reader = new StreamReader(jsonStream);
string json = await reader.ReadToEndAsync();
```

## Vue d’ensemble visuelle

![Diagramme illustrant comment lire une ressource intégrée et définir la licence Aspose](read-embedded-resource-diagram.png)

*Texte alternatif :* lire une ressource intégrée – diagramme montrant l’intégration, la récupération avec GetManifestResourceStream, et l’application de la licence Aspose.

## Récapitulatif

Nous avons couvert comment **lire une ressource intégrée** dans un assembly .NET, les étapes exactes pour **utiliser GetManifestResourceStream**, et la manière propre de **définir la licence Aspose** sans exposer de fichiers sur le disque. En intégrant la licence, vous éliminez les tracas de déploiement et rendez votre application portable.

## Et après ?

- **Automatiser les mises à jour de licence :** écrivez un petit script d’étape de build qui remplace le fichier `.lic` intégré lorsque vous renouvelez votre abonnement Aspose.
- **Sécuriser la ressource :** envisagez de chiffrer la licence avant de l’intégrer et de la déchiffrer à l’exécution pour une protection supplémentaire.
- **Explorer d’autres produits Aspose :** la même approche fonctionne pour Aspose.Words, Aspose.PDF, etc., chacun avec sa propre classe `License`.

N’hésitez pas à expérimenter—peut‑être intégrerez‑vous plusieurs licences pour différents modules, ou utiliserez‑vous un nom de ressource piloté par une configuration. Le ciel est la limite.

---

*Bon codage ! Si vous rencontrez des difficultés, laissez un commentaire ci‑dessous ou consultez les forums Aspose pour plus d’exemples.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}