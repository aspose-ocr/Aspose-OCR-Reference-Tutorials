---
category: general
date: 2026-04-06
description: Comment définir la licence dans Aspose OCR avec C# – apprenez comment
  intégrer une ressource, récupérer la ressource intégrée et charger la licence à
  partir d’un fichier ou d’un flux en quelques étapes seulement.
draft: false
keywords:
- how to set license
- how to embed resource
- get embedded resource
- how to load license
- use license stream
language: fr
og_description: Comment configurer la licence dans Aspose OCR est expliqué étape par
  étape. Découvrez comment intégrer la licence, la récupérer et utiliser un flux de
  licence pour une intégration fluide.
og_title: Comment définir la licence dans Aspose OCR – Guide complet C#
tags:
- Aspose OCR
- C#
- .NET licensing
title: Comment définir la licence dans Aspose OCR – Guide complet C#
url: /fr/net/ocr-configuration/how-to-set-license-in-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment définir la licence dans Aspose OCR – Guide complet C#

Définir la licence dans Aspose OCR est un obstacle fréquent pour les développeurs. Dans ce tutoriel, nous passerons en revue les étapes exactes pour définir la licence, l’intégrer en tant que ressource et la charger depuis un flux — afin que vous puissiez commencer à faire de l’OCR sans le filigrane gênant du mode d’évaluation.

Vous avez déjà essayé d’exécuter une tâche d’OCR pour ne voir qu’une bannière « Version d’évaluation » ? C’est le symptôme d’une licence manquante ou mal appliquée. À la fin de ce guide, vous disposerez d’une instance Aspose OCR entièrement licenciée, que vous conserviez le fichier `.lic` à côté de vos binaires ou que vous l’intégriez dans votre assembly.

## Ce dont vous avez besoin

- **Aspose.OCR for .NET** (dernier package NuGet au moment de la rédaction – 23.10)
- Un **fichier de licence Aspose OCR valide** (`Aspose.OCR.lic`)
- Visual Studio 2022 ou tout IDE compatible C#
- Une connaissance de base de l’intégration de ressources .NET (nous couvrirons cela)

Aucune bibliothèque tierce supplémentaire n’est requise ; tout se trouve dans le package Aspose.

![Illustration de la configuration de licence](image.png "Comment définir la licence")

## Étape 1 : Installer le package NuGet Aspose.OCR

Avant de toucher au code de licence, assurez‑vous que la bibliothèque est référencée :

```bash
dotnet add package Aspose.OCR
```

Ou, via le gestionnaire NuGet de Visual Studio, recherchez **Aspose.OCR** et cliquez sur *Installer*. Cela récupère le `Aspose.OCR.dll` et ses dépendances.

> **Astuce :** Ciblez .NET 6 ou une version ultérieure pour profiter de la dernière surface d’API et de meilleures performances.

## Étape 2 : Créer un objet License – Le cœur du « Comment définir la licence »

Aspose utilise une classe simple `License` pour appliquer la clé commerciale. L’instancier est la première ligne de tout flux de travail licencié :

```csharp
using Aspose.OCR;

// Step 2: Create a License object
var ocrLicense = new License();
```

Pourquoi c’est important : l’instance `License` lit le contenu du fichier `.lic` et l’enregistre globalement pour le domaine d’application actuel. Une fois enregistrée, chaque `OcrEngine` que vous créez fonctionnera en mode complet.

## Étape 3 : Appliquer la licence depuis un fichier (Méthode classique « Comment charger la licence »)

Si vous préférez garder le fichier de licence à côté de votre exécutable, appelez `SetLicense` avec le chemin du fichier :

```csharp
// Step 3: Apply the license from a file (replace with your actual path)
ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

### Points d’attention

- **Chemins absolus vs relatifs** : les chemins relatifs sont résolus par rapport au *répertoire de travail* du processus, qui est souvent le dossier `bin`.
- **Permissions de fichier** : le compte qui exécute l’application doit avoir le droit de lecture sur le fichier `.lic`.
- **Gestion des exceptions** : `SetLicense` lève une `FileNotFoundException` si le chemin est incorrect, donc encapsulez‑le dans un `try/catch` si vous avez besoin d’une dégradation gracieuse.

## Étape 4 : Comment intégrer une ressource – Incorporer la licence dans votre assembly

Intégrer la licence élimine le besoin de livrer un fichier séparé. Voici comment **intégrer une ressource** dans un projet .NET :

1. Ajoutez le fichier `.lic` à votre projet (par ex., dans un dossier nommé `Resources`).
2. Clic droit sur le fichier → *Propriétés* → définissez **Build Action** sur **Embedded Resource**.
3. Compilez le projet ; la licence devient partie du DLL compilé.

Vous pouvez maintenant la récupérer avec la logique **obtenir une ressource intégrée**.

## Étape 5 : Obtenir le flux de la ressource intégrée

L’extrait suivant montre **obtenir une ressource intégrée** à l’aide de la réflexion. Ajustez l’espace de noms et le nom de la ressource pour correspondre à la structure de votre projet :

```csharp
using System.Reflection;

// Step 5: Load the embedded license stream
using var licenseStream = Assembly.GetExecutingAssembly()
                                 .GetManifestResourceStream("MyApp.Resources.Aspose.OCR.lic");

if (licenseStream == null)
{
    throw new InvalidOperationException("Embedded license not found. Check the resource name.");
}
```

> **Pourquoi la réflexion ?** `Assembly.GetExecutingAssembly()` pointe vers l’assembly en cours d’exécution, garantissant que le code fonctionne que vous soyez dans une application console, un site web ou une Azure Function.

## Étape 6 : Utiliser le flux de licence – Le modèle « utiliser le flux de licence »

Une fois que vous avez le flux, **utilisez le flux de licence** pour appliquer la licence sans toucher au système de fichiers :

```csharp
// Step 6: Apply the license using the stream
ocrLicense.SetLicense(licenseStream);
```

Lorsque `SetLicense` reçoit un `Stream`, Aspose lit directement les octets, enregistre la licence et libère le flux à la sortie du bloc `using`. C’est la façon la plus propre de garder votre licence cachée.

### Exemple complet fonctionnel

En rassemblant le tout, voici un programme autonome qui démontre les trois approches (fichier, ressource intégrée et flux). Commentez les sections dont vous n’avez pas besoin.

```csharp
using System;
using System.Reflection;
using Aspose.OCR;

namespace LicenseDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣  Create the License object – core of how to set license
            // -------------------------------------------------
            var ocrLicense = new License();

            // -------------------------------------------------
            // 2️⃣  Option A: Load from external .lic file (how to load license)
            // -------------------------------------------------
            // Replace with your actual path or use a relative path.
            // ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

            // -------------------------------------------------
            // 3️⃣  Option B: Load from an embedded resource (how to embed resource)
            // -------------------------------------------------
            // Ensure the .lic file is added as an Embedded Resource.
            // string resourceName = "LicenseDemo.Resources.Aspose.OCR.lic";
            // using var licenseStream = Assembly.GetExecutingAssembly()
            //                                   .GetManifestResourceStream(resourceName);
            // if (licenseStream == null)
            // {
            //     Console.WriteLine("Embedded license not found.");
            //     return;
            // }
            // ocrLicense.SetLicense(licenseStream); // use license stream

            // -------------------------------------------------
            // 4️⃣  Verify the license – no exception means success
            // -------------------------------------------------
            Console.WriteLine("License applied successfully!");

            // -------------------------------------------------
            // 5️⃣  Run a quick OCR test to prove it works
            // -------------------------------------------------
            var engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample.png"); // replace with your image
            engine.Recognize();

            Console.WriteLine("Recognized text:");
            Console.WriteLine(engine.Text);
        }
    }
}
```

**Sortie attendue**

```
License applied successfully!
Recognized text:
[Your OCR result here]
```

Si la licence n’est pas appliquée, Aspose lève une `LicenseException` ou vous verrez le filigrane d’évaluation dans les résultats d’OCR.

## Pièges courants & comment les éviter

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| La bannière « Version d’évaluation » apparaît toujours | Licence non chargée ou chemin incorrect | Vérifiez le chemin du fichier ou le nom de la ressource intégrée. |
| `NullReferenceException` sur `GetManifestResourceStream` | Nom de ressource erroné ou Build Action non définie sur Embedded Resource | Vérifiez le nom qualifié par l’espace de noms et définissez correctement la Build Action. |
| La licence fonctionne en local mais échoue après déploiement | Permissions de lecture manquantes sur le serveur | Accordez à l’identité du pool d’applications l’accès en lecture au fichier `.lic`, ou intégrez la licence pour éviter les problèmes de système de fichiers. |
| Plusieurs objets `License` n’ont aucun effet | Vous avez appelé `SetLicense` sur une *autre* instance après la première | Conservez une seule instance `License` par AppDomain ; réutilisez‑la ou appelez `SetLicense` une seule fois au démarrage. |

## Quand choisir chaque approche

- **Basée sur fichier** – Prototypage rapide, facile à remplacer sans recompilation.
- **Ressource intégrée** – Idéal pour la distribution de bureau ou de bibliothèque où vous ne voulez pas que la licence soit visible.
- **Basée sur flux** – Parfait pour les environnements cloud (Azure Functions, AWS Lambda) où vous pouvez récupérer la licence depuis un coffre sécurisé et la fournir directement.

## Prochaines étapes – Approfondir votre connaissance de la licence

Maintenant que vous avez maîtrisé **comment définir la licence**, vous pourriez explorer :

- **Comment intégrer une ressource** dans des solutions multi‑projets plus complexes.
- **Obtenir une ressource intégrée** depuis des assemblies satellites pour des scénarios de localisation.
- **Comment charger la licence** dynamiquement depuis Azure Key Vault ou AWS Secrets Manager.
- **Utiliser le flux de licence** avec l’injection de dépendances pour un code de démarrage plus propre.

Chacun de ces sujets s’appuie sur les bases présentées ici et vous aide à garder votre stratégie de licence à la fois sécurisée et maintenable.

---

### TL;DR

Nous vous avons montré **comment définir la licence** dans Aspose OCR en utilisant trois techniques fiables : charger depuis un fichier, intégrer le `.lic` en tant que ressource, et l’appliquer via un flux. Suivez le code, respectez les pièges, et votre moteur OCR fonctionnera à pleine vitesse—sans filigrane d’évaluation, sans surprise.

Bon codage, et que vos résultats d’OCR soient d’une clarté cristalline !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}