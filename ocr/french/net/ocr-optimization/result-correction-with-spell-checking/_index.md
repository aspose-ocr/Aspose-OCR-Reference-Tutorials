---
date: 2025-12-25
description: Améliorez la précision de l’OCR avec Aspose OCR pour .NET, en tirant
  parti de la vérification orthographique et du support linguistique pour corriger
  les fautes d’orthographe et personnaliser les dictionnaires afin d’obtenir une reconnaissance
  de texte sans erreurs.
linktitle: Improve OCR Accuracy with Spell Checking in Images
second_title: Aspose.OCR .NET API
title: Améliorer la précision de l'OCR grâce à la vérification orthographique dans
  les images
url: /fr/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Améliorer la précision de l'OCR avec la vérification orthographique dans les images

## Introduction

Lorsque vous travaillez avec la Reconnaissance Optique de Caractères (OCR), l'objectif ultime est d'**améliorer la précision de l'OCR** ​​afin que le texte extrait corresponde parfaitement à l'image d'origine. Les mots mal orthographiés sont une source fréquente d'erreurs, surtout lorsque l'image source est bruitée ou contient des polices inhabituelles. Aspose.OCR for .NET propose des fonctionnalités de vérification orthographique intégrées qui non seulement corrigent ces erreurs mais vous permettent également d'étendre le moteur avec des dictionnaires personnalisés. Dans ce tutoriel, vous apprendrez comment utiliser la vérification orthographique pour améliorer les résultats de l'OCR, voir le résultat avant‑et‑après, et découvrir comment adapter le processus de correction à vos besoins linguistiques spécifiques.

## Réponses rapides
- **Que fait la vérification orthographique pour l'OCR ?** Elle détecte automatiquement les mots mal orthographiés dans la sortie OCR et les remplace par les alternatives les plus probables.
- **Quelle bibliothèque fournit cette fonctionnalité ?** Aspose.OCR for .NET inclut une API de vérification orthographique prête à l'emploi.
- **Ai‑je besoin d'une connexion Internet ?** Non, le moteur de vérification orthographique fonctionne entièrement hors ligne.
- **Puis‑je ajouter ma propre terminologie ?** Oui, vous pouvez fournir un dictionnaire utilisateur personnalisé pour gérer les mots spécifiques à un domaine.
- **Quelles langues sont prises en charge ?** Voir la section « aspose ocr language support » pour plus de détails.

## Qu'est-ce que la vérification orthographique dans l'OCR ?

La vérification orthographique examine le texte brut renvoyé par le moteur OCR, identifie les jetons qui ne correspondent pas aux mots connus du dictionnaire de la langue sélectionnée, et suggère ou applique des corrections. Cette étape est essentielle pour **améliorer la précision de l'OCR**, en particulier lors du traitement des documents numérisés, de reçus ou de formulaires où l'OCR peut mal interpréter les caractères.

## Pourquoi utiliser la prise en charge du langage Aspose OCR ?

Aspose.OCR est fourni avec des packs de langues étendues et vous permet d'ajouter des dictionnaires supplémentaires. Exploiter **aspose ocr language support** signifie que vous pouvez gérer des documents multilingues sans écrire de parseurs personnalisés, et vous bénéficiez de règles spécifiques à chaque langue qui améliorent davantage la qualité de reconnaissance.

## Prérequis

Avant de Sous-marin dans la magie de la vérification orthographique, assurez-vous que les prérequis suivants sont en place :

- Bibliothèque Aspose.OCR pour .NET : Téléchargez et installez la bibliothèque Aspose.OCR depuis la [page de diffusion](https://releases.aspose.com/ocr/net/).
- Répertoire de documents : Assurez-vous de disposer d'un répertoire désigné pour vos documents. Remplacez `"Your Document Directory"` dans les extraits de code par le chemin réel.

## Importer des espaces de noms

Commençons par importer les espaces de noms nécessaires dans votre projet .NET :

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Étape 1 : Initialiser Aspose.OCR

Initialisez une instance d'Aspose.OCR pour lancer le processus OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Étape 2 : Reconnaître l'image

Ensuite, reconnaissez le texte d'une image à l'aide d'Aspose.OCR. Voici un extrait illustrant ce processus :

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Étape 3 : Avant la correction

Récupérez le résultat OCR avant correction afin de le comparer avec la version corrigée.

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Étape 4 : Après correction

Appliquez la vérification orthographique pour obtenir le résultat corrigé. L'extrait de code suivant illustre cette étape :

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Étape 5 : Mots mal orthographiés et suggestions

Obtenez une liste de mots mal orthographiés ainsi que les corrections suggérées à l'aide du code suivant :

```csharp
// Get list of misspelled words with suggestions
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## Étape 6 : Corriger le texte de l'utilisateur

Corrigez un texte fourni par l'utilisateur en utilisant la bibliothèque Aspose.OCR :

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Étape 7 : Correction avec le dictionnaire utilisateur

Améliorez davantage la correction en incorporant un dictionnaire utilisateur personnalisé :

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Problèmes courants et solutions

| Problème | Pourquoi cela se produit | Comment résoudre |
|----------|----------------|-------------------|
| Aucune suggestion renvoyée | Le pack de langue n'est pas chargé ou le texte est trop court. | Assurez-vous que `RecognitionSettings(Language.Eng)` correspond à la langue de l'image source et que le résultat OCR contient suffisamment de caractères. |
| Dictionnaire personnalisé non appliqué | Chemin ou format de fichier incorrect. | Vérifiez que `dictionary.txt` existe à l'emplacement spécifié et utilisez un mot par ligne. |
| Le vérificateur orthographique ralentit les gros documents | Le traitement de chaque mot ajoute individuellement une surtaxe. | Traitez les pages par lots ou augmentez l'allocation de mémoire si vous exécutez sur .NET Core. |

## Questions fréquemment posées

### Q1 : Puis‑je utiliser Aspose.OCR pour des langues autres que l'anglais ?

R1 : Oui, Aspose.OCR prend en charge plusieurs langues. Ajustez les paramètres de langue en conséquence.

### Q2 : Comment intégrer Aspose.OCR dans mon projet .NET ?

R2 : Consultez la [documentation](https://reference.aspose.com/ocr/net/) pour les étapes détaillées d'intégration.

### Q3 : Existe‑t‑il une version d'essai disponible pour Aspose.OCR ?

R3 : Oui, vous pouvez explorer les fonctionnalités avec la [version d'essai gratuite](https://releases.aspose.com/).

### Q4 : Puis‑je télécharger un dictionnaire personnalisé pour la vérification orthographique ?

R4 : Absolument ! Le tutoriel montre comment améliorer la correction en utilisant un dictionnaire fourni par l'utilisateur.

### Q5 : Où puis‑je obtenir de l'aide pour Aspose.OCR ?

R5 : Visitez le [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) pour le support communautaire et des conseils.

---

**Dernière mise à jour :** 2025-12-25
**Testé avec :** Dernière version d'Aspose.OCR pour .NET
**Auteur :** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
