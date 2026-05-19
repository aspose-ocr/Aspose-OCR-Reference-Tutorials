---
category: general
date: 2026-03-07
description: Exemple Aspose OCR montrant comment activer la correction orthographique,
  ajouter un dictionnaire personnalisé, charger l'OCR d'image et corriger rapidement
  les erreurs d'OCR.
draft: false
keywords:
- aspose ocr example
- how to enable spellcheck
- how to add dictionary
- load image ocr
- how to fix ocr errors
language: fr
og_description: Exemple Aspose OCR qui vous guide à travers l’activation de la correction
  orthographique, l’ajout d’un dictionnaire personnalisé, le chargement d’une image
  pour l’OCR et la correction des erreurs OCR courantes.
og_title: Exemple Aspose OCR – Activer la correction orthographique et corriger les
  erreurs
tags:
- Aspose
- OCR
- C#
- SpellCheck
title: Exemple Aspose OCR – Activer la vérification orthographique et corriger les
  erreurs en C#
url: /fr/net/ocr-optimization/aspose-ocr-example-enable-spellcheck-and-fix-errors-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exemple Aspose OCR – Activer la vérification orthographique et corriger les erreurs en C#

Vous avez déjà eu besoin d’un **exemple Aspose OCR** qui non seulement lit le texte d’une image mais qui nettoie aussi ces fautes d’orthographe agaçantes ? Vous n’êtes pas seul. Dans de nombreux projets réels, la sortie brute de l’OCR est truffée de coquilles, surtout lorsque l’image source contient des polices à faible contraste ou des notes manuscrites.  

Bonne nouvelle : avec Aspose.OCR vous pouvez **activer la vérification orthographique**, brancher votre propre dictionnaire, et obtenir une chaîne épurée en quelques lignes de code seulement. Vous verrez ci‑dessous **comment activer la vérification orthographique**, **comment ajouter un dictionnaire**, et **comment charger l’OCR d’une image** afin de **corriger les erreurs d’OCR** sans perdre patience.

Dans ce tutoriel nous couvrirons tout ce dont vous avez besoin — de l’installation via NuGet à un programme complet, exécutable, qui affiche le texte corrigé. À la fin, vous disposerez d’un **exemple Aspose OCR** solide que vous pourrez insérer directement dans n’importe quel projet .NET.

## Prérequis

- SDK .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Core et .NET Framework)
- Visual Studio 2022 ou tout IDE compatible C#
- Un fichier image (`typed_text.png`) contenant du texte anglais clair et dactylographié
- Accès Internet pour télécharger le package NuGet Aspose.OCR

Aucune autre bibliothèque tierce n’est requise.

---

## Étape 1 – Installer le package NuGet Aspose.OCR (Load Image OCR)

Avant d’écrire du code, nous avons besoin de la bibliothèque qui alimente le moteur OCR.

```bash
dotnet add package Aspose.OCR
```

> **Astuce :** Si vous utilisez Visual Studio, faites un clic droit sur le projet → *Manage NuGet Packages* → recherchez **Aspose.OCR** et cliquez sur *Install*.  

L’installation du package vous donne accès à `OcrEngine`, `ImageStream` et aux utilitaires de vérification orthographique intégrés que nous utiliserons plus tard. Une fois le package en place, vous êtes prêt à **charger l’OCR d’une image**.

## Étape 2 – Créer l’instance du moteur OCR

Créer le moteur est la première étape concrète dans tout **exemple Aspose OCR**. Pensez à `OcrEngine` comme le cerveau qui analysera le bitmap et produira du texte.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

Le constructeur de `OcrEngine` ne nécessite aucun paramètre, ce qui le rend simple et pratique pour les prototypes rapides.

## Étape 3 – Comment activer la vérification orthographique (et pourquoi c’est important)

La sortie brute de l’OCR contient souvent des mots mal reconnus comme « teh » au lieu de « the ». Activer le correcteur orthographique intégré permet à Aspose de remplacer automatiquement ces erreurs par l’orthographe la plus probable.

```csharp
// Step 3: Turn on spell checking and set the language to English
ocrEngine.Settings.SpellCheck.Enabled = true;
ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;
```

> **Pourquoi activer la vérification orthographique ?**  
> - **Précision :** Un correcteur orthographique en post‑traitement peut augmenter la précision globale du texte de 10‑15 % pour les documents imprimés.  
> - **Expérience utilisateur :** Un texte propre signifie moins de nettoyage en aval lorsque vous injectez le résultat dans des index de recherche ou des pipelines d’analyse.

## Étape 4 – Comment ajouter un dictionnaire (mots personnalisés)

Parfois, le dictionnaire par défaut ne connaît pas vos noms de marque, codes produit ou jargon spécifique à votre domaine. C’est là qu’intervient **comment ajouter un dictionnaire**.

```csharp
// Step 4: Add custom words that the spell checker should accept
ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
{
    "AsposeOCR",   // our library name
    "OCRify",      // a fictional product
    "CSharpify"    // another custom term
});
```

Vous pouvez fournir un tableau, une liste, ou même lire depuis un fichier si vous avez un vocabulaire personnalisé volumineux. Le correcteur orthographique traitera alors ces entrées comme valides, évitant les corrections erronées.

## Étape 5 – Charger l’image pour l’OCR (Load Image OCR)

Une fois le moteur configuré, il faut le pointer vers l’image que vous souhaitez lire. L’assistant `ImageStream.FromFile` masque les détails de lecture du fichier.

```csharp
// Step 5: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");
```

> **Conseil :** Si votre image se trouve dans un sous‑dossier du projet, définissez sa propriété *Copy to Output Directory* sur *Copy always* afin que le chemin soit résolu à l’exécution.

## Étape 6 – Effectuer la reconnaissance et corriger les erreurs d’OCR

Avec tout en place, un seul appel à `Recognize()` lance le pipeline OCR, applique la vérification orthographique, et stocke le résultat nettoyé dans `ocrEngine.Text`.

```csharp
// Step 6: Run OCR and let the spell checker clean the output
ocrEngine.Recognize();

// Step 7: Output the corrected text to the console
Console.WriteLine("Corrected text:");
Console.WriteLine(ocrEngine.Text);
```

### Résultat attendu

En supposant que `typed_text.png` contienne la phrase `The quick brown fox jumps over teh lazy dog`, la console affichera :

```
Corrected text:
The quick brown fox jumps over the lazy dog
```

Remarquez comment « teh » a été automatiquement corrigé en « the ». Si vous aviez ajouté « OCRify » au dictionnaire personnalisé et que l’image contenait ce mot, le moteur l’aurait laissé tel quel.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet que vous pouvez placer dans un nouveau projet console. Il regroupe toutes les étapes précédentes, avec quelques commentaires pour plus de clarté.

```csharp
// ---------------------------------------------------------------
// Aspose OCR Example – Enable Spellcheck and Fix Errors
// ---------------------------------------------------------------

using System;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable spell checking (how to enable spellcheck)
            ocrEngine.Settings.SpellCheck.Enabled = true;
            ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;

            // 3️⃣ Add custom words (how to add dictionary)
            ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
            {
                "AsposeOCR",
                "OCRify",
                "CSharpify"
            });

            // 4️⃣ Load the image (load image OCR)
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");

            // 5️⃣ Run OCR – this also fixes common OCR errors (how to fix ocr errors)
            ocrEngine.Recognize();

            // 6️⃣ Show the corrected result
            Console.WriteLine("Corrected text:");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

Enregistrez-le sous le nom `Program.cs`, exécutez `dotnet run`, et vous devriez voir la phrase corrigée s’afficher dans la console.

---

## Questions fréquentes & cas particuliers

| Question | Réponse |
|----------|---------|
| **Et si l’image est un PDF multi‑pages ?** | Aspose.OCR peut gérer les pages PDF comme des images. Utilisez `ocrEngine.Image = ImageStream.FromPdf("file.pdf", pageNumber: 1);` et bouclez sur les pages. |
| **Puis‑je changer la langue pour autre chose que l’anglais ?** | Bien sûr. Définissez `ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.French;` (ou toute langue prise en charge). |
| **Mon dictionnaire personnalisé est énorme — cela affectera‑t‑il les performances ?** | Ajouter des milliers de mots engendre un petit coût initial, mais la recherche est O(1) grâce à un hash‑set en interne. Pour des vocabulaires très volumineux, chargez‑les une fois au démarrage de l’application. |
| **Que faire si le moteur OCR lève une exception sur une image corrompue ?** | Enveloppez `Recognize()` dans un bloc try‑catch et inspectez `ocrEngine.LastError`. Vous pouvez également pré‑valider les dimensions de l’image avec `ocrEngine.Image.Width` et `Height`. |
| **Faut‑il une licence pour la production ?** | L’évaluation gratuite suffit pour les tests, mais une licence commerciale supprime le filigrane d’évaluation et débloque les performances complètes. |

---

## Conclusion

Vous disposez maintenant d’un **exemple complet Aspose OCR** qui montre **comment activer la vérification orthographique**, **comment ajouter un dictionnaire**, **comment charger l’OCR d’une image**, et **comment corriger les erreurs d’OCR** de façon propre et prête pour la production. En configurant le correcteur orthographique et en fournissant une liste de mots personnalisée, vous améliorez considérablement la qualité du texte extrait sans écrire de logique de post‑traitement supplémentaire.

Prêt pour l’étape suivante ? Essayez de changer la langue en espagnol, de traiter un PDF multi‑pages, ou d’intégrer la sortie dans un index Azure Cognitive Search. Le même schéma s’applique — il suffit d’ajuster le drapeau de langue et éventuellement d’étendre le dictionnaire personnalisé.

Si ce guide vous a été utile, donnez‑lui une étoile sur GitHub, partagez‑le avec vos collègues, ou laissez un commentaire ci‑dessous. Bon codage, et que vos résultats OCR soient toujours sans erreur !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}