---
date: 2025-12-19
description: Apprenez à effectuer la reconnaissance optique de caractères sur des
  images d’archives, à convertir des images en texte et à extraire du texte à partir
  de fichiers d’archives en utilisant Aspose.OCR pour .NET.
linktitle: How to Perform OCR on Archive Images with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: Comment effectuer la reconnaissance optique de caractères sur des images d'archives
  avec Aspose.OCR pour .NET
url: /fr/net/ocr-configuration/ocr-operation-with-archive/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer une OCR sur des images d'archives avec Aspose.OCR pour .NET

## Introduction

Dans ce tutoriel complet, vous découvrirez **comment effectuer de l’OCR** ​​sur des fichiers image archivés à l’aide de la bibliothèque Aspose.OCR pour .NET. Que vous ayez besoin de **convertir des images en texte** ou **d’extraire du texte depuis une archive**, le guide étape par étape ci-dessous vous accompagnera depuis la configuration de votre environnement de développement jusqu’à la récupération du texte reconnu pour chaque image contenue dans une archive ZIP.

## Réponses rapides
- **Que couvre le didacticiel ?** Exécution de l'OCR sur des images d'archive (ZIP) avec Aspose.OCR pour .NET.
- **Quel mot-clé principal est ciblé ?** *Comment effectuer l'ocr*.
- **Ai-je besoin d'une licence ?** Un essai gratuit fonctionne pour l'évaluation ; une licence commerciale est requise pour la production.
- **Quelles versions de .NET sont prises en charge ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.
- **Puis-je personnaliser les paramètres de reconnaissance ?** Oui : utilisez « RecognitionSettings » pour régler la précision.

## Qu'est-ce que l'OCR et pourquoi l'utiliser sur les archives ?

La reconnaissance optique de caractères (OCR) transforme les images numérisées ou les PDF en texte consultable et modifiable. Lorsque les images sont regroupées dans une archive (par ex., un fichier ZIP), extraire et reconnaître chaque image en une seule opération fait gagner du temps et réduire la complexité du code. La méthode `RecognizeMultipleImages` d'Aspose.OCR rend ce processus simple.

## Prérequis

- Visual Studio 2019ou version ultérieure (ou tout IDE compatible .NET).
- .NET Framework4.5+ ou .NETCore3.1+ installé.
- Accès à la bibliothèque Aspose.OCR pour .NET (lien de téléchargement ci-dessous).
- Une licence Aspose.OCR valide pour une utilisation en production (essai disponible).

## Importer des espaces de noms

Dans votre projet .NET, assurez-vous d'importer les espaces de noms nécessaires pour accéder aux fonctionnalités fournies par Aspose.OCR :

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Téléchargement et installation d'Aspose.OCR pour .NET

Téléchargez le dernier package depuis la page des versions **[ici](https://releases.aspose.com/ocr/net/)** et suivez la procédure d'installation standard via NuGet ou l'installation manuelle.

## Acquisition d'une licence

Obtenez une licence depuis la **[page d'achat](https://purchase.aspose.com/buy)** ou essayez la **[version d'essai gratuite](https://releases.aspose.com/)**. Placez le fichier de licence à la racine de votre projet et chargez-le à l'exécution comme indiqué dans la documentation Aspose.

## Étape 1 : Configuration de votre répertoire de documents

Commencez par initialiser le chemin d'accès à votre répertoire de documents :

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";
// ExEnd:1
```

> **Conseil :** Utilisez `Path.Combine` pour la gestion des chemins d'accès multiplateformes.

## Étape 2 : Initialiser Aspose.OCR

Créez une instance de la classe Aspose.OCR pour démarrer les opérations OCR :

```csharp
// ExStart:3
AsposeOcr api = new AsposeOcr();
// ExEnd:3
```

## Étape 3 : Spécifier le chemin d’accès à l’image

Définissez le chemin d’accès complet à votre image d’archive (fichier ZIP contenant les images à analyser) :

```csharp
// ExStart:4
string fullPath = dataDir + "OCR.zip";
// ExEnd:4
```

## Étape 4 : Reconnaissance d’image

Lancez la reconnaissance OCR sur l’archive spécifiée en utilisant les paramètres par défaut ou personnalisés. Cet appel extrait automatiquement chaque image du fichier ZIP et effectue la reconnaissance optique de caractères (OCR) :

```csharp
// ExStart:5
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
   //default or custom settings
});
// ExEnd:5
```

> Vous pouvez ajuster `RecognitionSettings` pour améliorer la précision pour certaines langues ou qualités d’image.

## Étape 5 : Afficher les résultats

Parcourez les résultats et affichez le texte reconnu pour chaque image de l’archive :

```csharp
// ExStart:6
for (int i = 0; i < result.Length; i++)
{
	 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
// ExEnd:6
```

Le résultat affiche l'index de chaque image suivi de la chaîne extraite, ce qui permet de **convertir les images en texte** et d'**extraire le texte des fichiers d'archive**.

## Problèmes courants et dépannage

| Problème | Cause | Solution |

|-------|-------|----------|

| Aucun texte retourné | Qualité d'image insuffisante | Prétraitez les images (par exemple, binarisation) ou ajustez `RecognitionSettings.Dpi` |

| Exception lors de la lecture du fichier ZIP | Chemin d'accès à l'archive invalide | Vérifiez que `fullPath` pointe vers un fichier `.zip` valide et que l'application dispose des autorisations de lecture |

| Licence non appliquée | Fichier de licence manquant ou non chargé | Appelez `License license = new License(); license.SetLicense("Aspose.OCR.lic");` avant de créer une instance `AsposeOcr` |

## Foire aux questions

**Q : Puis-je utiliser Aspose.OCR pour .NET sans licence ?**

R : Oui, une version d’essai gratuite est disponible pour l’évaluation, mais une version sous licence est requise pour les déploiements en production.

**Q : La bibliothèque prend-elle en charge les archives ZIP protégées par mot de passe ?**

R : Actuellement, `RecognizeMultipleImages` fonctionne avec les fichiers ZIP standard. Pour les archives chiffrées, extrayez d’abord les images à l’aide d’une bibliothèque tierce, puis transmettez le tableau d’images au moteur OCR.

**Q : Comment puis-je améliorer la précision de la reconnaissance de texte manuscrit ?**

R : Activez l’option `RecognitionSettings.EnableHandwritingRecognition` et augmentez la résolution (par exemple, à 300 ppp).

**Q : Est-il possible d’obtenir un score de confiance pour chaque ligne reconnue ?**

R : Chaque `RecognitionResult` contient une propriété `Confidence` que vous pouvez consigner ou utiliser pour filtrer les résultats de faible confiance.

## Conclusion

Vous disposez désormais d’un flux de travail complet et prêt pour la production afin d’**effectuer une reconnaissance optique de caractères (OCR) sur des images d’archives**, de **convertir des images en texte** et d’**extraire du texte à partir de fichiers d’archives** grâce à Aspose.OCR pour .NET. Intégrez-le à vos applications pour créer des référentiels de documents consultables, automatiser la saisie de données ou pour tout scénario nécessitant l’extraction de texte en masse à partir d’images.

## Ressources supplémentaires

- **Forum Aspose.OCR :** Pour obtenir de l’aide de la communauté et découvrir des scénarios avancés, consultez le [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16). - **Licence temporaire :** Pour une évaluation à court terme, demandez une [licence temporaire](https://purchase.aspose.com/temporary-license/).

- **Documentation officielle :** Consultez la [documentation](https://reference.aspose.com/ocr/net/) pour rester informé(e) des dernières modifications apportées à l’API.

---

**Dernière mise à jour :** 19/12/2025
**Testé avec :** Aspose.OCR 24.11 pour .NET
**Auteur :** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
