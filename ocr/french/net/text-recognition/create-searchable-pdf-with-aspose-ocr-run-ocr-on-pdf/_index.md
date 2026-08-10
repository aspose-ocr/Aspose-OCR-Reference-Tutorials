---
category: general
date: 2026-05-28
description: Créer un PDF consultable avec Aspose OCR en C#. Apprenez à exécuter l’OCR
  sur un PDF, à reconnaître le texte d’un PDF et à transformer un PDF numérisé par
  OCR en PDF consultable.
draft: false
keywords:
- create searchable pdf
- run ocr on pdf
- recognize text pdf
- ocr scanned pdf
- aspose ocr pdf
language: fr
og_description: Créez un PDF consultable à l'aide d'Aspose OCR en C#. Suivez ce guide
  étape par étape pour exécuter l'OCR sur un PDF, reconnaître le texte d'un PDF et
  gérer les fichiers PDF numérisés avec OCR.
og_title: Créer un PDF consultable avec Aspose OCR – Exécuter l’OCR sur le PDF
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  headline: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  type: TechArticle
- description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  name: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  steps:
  - name: Multiple Languages (OCR Scanned PDF)
    text: 'If your source PDF contains both English and Spanish text, combine languages:'
  - name: Password‑Protected PDFs
    text: 'When dealing with secured PDFs, supply the password before calling `Recognize`:'
  - name: Controlling Image Quality
    text: 'Higher DPI yields better OCR results but consumes more memory. Adjust the
      DPI if you notice garbled characters:'
  - name: License vs. Evaluation Mode
    text: 'In evaluation mode a watermark appears on each page. To remove it, apply
      your license before any OCR call:'
  - name: What’s Next?
    text: '- Explore the **aspose ocr pdf** API further: extract plain text, export
      to DOCX, or generate searchable PDFs in bulk. - Combine the searchable PDF output
      with Aspose.PDF to add bookmarks or watermarks. - Experiment with different
      DPI settings or custom OCR dictionaries for niche fonts.'
  type: HowTo
tags:
- Aspose
- OCR
- PDF
- C#
title: Créer un PDF interrogeable avec Aspose OCR – Effectuer l’OCR sur un PDF
url: /fr/net/text-recognition/create-searchable-pdf-with-aspose-ocr-run-ocr-on-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF recherchable avec Aspose OCR – Exécuter l’OCR sur PDF

Vous avez déjà eu besoin de **créer des fichiers PDF recherchables** à partir d’une pile de documents numérisés ? Vous n’êtes pas seul. Dans de nombreux flux de travail de bureau, la seule chose qui vous sépare d’une archive entièrement recherchable est quelques lignes de code qui exécutent l’OCR sur les pages PDF.  

Dans ce tutoriel, nous passerons en revue un exemple complet, prêt à l’emploi, qui vous montre exactement comment **créer des fichiers PDF recherchables** en utilisant la bibliothèque Aspose OCR pour .NET. À la fin, vous saurez *exécuter l’OCR sur PDF*, *reconnaître le texte PDF* et transformer un *PDF numérisé avec OCR* en une version recherchable sans aucun service tiers.

> **Prérequis** – Un SDK .NET récent (6.0+ recommandé), une licence valide d’Aspose.OCR pour .NET (ou une clé d’évaluation temporaire), et un PDF que vous souhaitez traiter.

![Diagramme de création de PDF recherchable](alt="Diagramme illustrant le flux de travail de création de PDF recherchable avec Aspose OCR")  

---

## Ce que couvre ce guide

- Installation de la bibliothèque Aspose OCR dans un projet C#.  
- Chargement d’un PDF source (quel que soit le nombre de pages).  
- Configuration du moteur pour produire un **PDF recherchable**.  
- Exécution du processus OCR et sauvegarde du résultat.  
- Astuces pour gérer les documents multi‑pages, la sélection de langue et les pièges courants.  

Si vous suivez chaque étape, vous obtiendrez un fichier que vous pourrez ouvrir dans Adobe Reader, appuyer sur **Ctrl + F**, et rechercher instantanément n’importe quel mot présent dans la numérisation d’origine.

---

## Étape 1 : Installer Aspose OCR pour .NET

Avant d’écrire du code, ajoutez le package NuGet à votre projet :

```bash
dotnet add package Aspose.OCR
```

> **Astuce pro** : Utilisez le drapeau `--version` pour verrouiller la dernière version stable (par ex., `Aspose.OCR 23.10`). Cela garantit la compatibilité avec .NET 6 et les versions ultérieures.

---

## Étape 2 : Créer une instance du moteur OCR

Le cœur du processus est le `OcrEngine`. Pensez‑y comme le cerveau qui lit les images et génère du texte. Son initialisation est simple :

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Instantiate the OCR engine
            var ocrEngine = new OcrEngine();
```

L’objet `OcrEngine` contiendra à la fois le flux d’image d’entrée et la configuration qui indique à Aspose comment vous souhaitez le résultat.

---

## Étape 3 : Charger le PDF source (Exécuter l’OCR sur PDF)

Aspose OCR peut ingérer directement un PDF ; il extrait chaque page sous forme d’image en interne. Remplacez le chemin factice par l’emplacement de votre document numérisé :

```csharp
            // Step 3: Load the source PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);
```

> **Pourquoi cela fonctionne** : La méthode `ImageStream.FromFile` détecte automatiquement le format PDF et prépare une représentation raster pour l’OCR. aucune étape de conversion supplémentaire n’est requise.

---

## Étape 4 : Configurer le format de sortie et la langue

Ici nous indiquons à Aspose ce que nous voulons en retour. Définir `OutputFormat` sur `SearchablePdf` indique au moteur d’intégrer le texte reconnu derrière les images originales de chaque page, produisant ainsi un **PDF recherchable**. Vous pouvez également choisir la langue pour améliorer la précision — l’anglais est la valeur par défaut, mais vous pouvez passer au français, à l’allemand, etc.

```csharp
            // Step 4: Choose output format and language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf; // creates searchable PDF
            ocrEngine.Configuration.Language = Language.English;               // *recognize text PDF* in English
```

Si vous devez traiter un document bilingue, vous pouvez combiner les langues à l’aide des drapeaux de l’énumération `Language`.

---

## Étape 5 : Exécuter le processus OCR – Reconnaître le texte PDF

Maintenant le travail lourd commence. La méthode `Recognize` parcourt chaque page, extrait les glyphes et construit un flux PDF interne contenant à la fois l’image originale et une couche de texte invisible. C’est l’étape où nous *reconnaissons le texte PDF*.

```csharp
            // Step 5: Execute OCR – this *recognizes text PDF* and builds the searchable stream
            ocrEngine.Recognize();
```

> **Question fréquente** : *Et si le PDF compte 200 pages ?*  
> Le moteur traite les pages séquentiellement et diffuse les résultats, de sorte que la consommation mémoire reste modeste. Cependant, pour des fichiers extrêmement volumineux, vous pourriez vouloir augmenter le paramètre `MemoryLimit` dans `ocrEngine.Configuration`.

---

## Étape 6 : Enregistrer le PDF recherchable

Enfin, écrivez le résultat sur le disque. La méthode `Save` enregistre le flux interne dans un nouveau fichier que vous pouvez ouvrir avec n’importe quel lecteur PDF.

```csharp
            // Step 6: Save the searchable PDF to disk
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

Exécutez le programme (`dotnet run`) et observez la console confirmer la création du fichier. Ouvrez `handbook_searchable.pdf` et essayez de rechercher un mot que vous savez présent dans la numérisation d’origine — vous devriez voir les correspondances immédiatement.

---

## Gestion des cas particuliers et scénarios avancés

### Plusieurs langues (PDF numérisé avec OCR)

Si votre PDF source contient à la fois du texte anglais et espagnol, combinez les langues :

```csharp
ocrEngine.Configuration.Language = Language.English | Language.Spanish;
```

Aspose OCR basculera les dictionnaires à la volée, améliorant la précision pour les documents multilingues.

### PDFs protégés par mot de passe

Lorsque vous traitez des PDFs sécurisés, fournissez le mot de passe avant d’appeler `Recognize` :

```csharp
ocrEngine.Image = ImageStream.FromFile(inputPath, "MySecretPassword");
```

Si le mot de passe est incorrect, `Recognize` lève une `InvalidPasswordException` ; la capturer vous permet de demander à l’utilisateur le bon mot de passe.

### Contrôle de la qualité d’image

Un DPI plus élevé donne de meilleurs résultats OCR mais consomme plus de mémoire. Ajustez le DPI si vous remarquez des caractères déformés :

```csharp
ocrEngine.Configuration.Dpi = 300; // default is 200
```

### Licence vs. mode d’évaluation

En mode d’évaluation, un filigrane apparaît sur chaque page. Pour le supprimer, appliquez votre licence avant tout appel OCR :

```csharp
var license = new License();
license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");
```

---

## Astuces pro pour la production

- **Traitement par lots** : Enveloppez la logique principale dans une boucle `foreach` qui itère sur une liste de PDFs. Libérez le `OcrEngine` après chaque fichier pour libérer les ressources natives.
- **Journalisation** : Utilisez `ocrEngine.Configuration.Logger` pour capturer des statistiques détaillées d’OCR (par ex., caractères reconnus par seconde). Cela est inestimable pour dépanner une faible précision.
- **Optimisation des performances** : Pour les serveurs multi‑cœurs, créez des instances distinctes de `OcrEngine` par thread ; la bibliothèque est thread‑safe tant que chaque instance est isolée.
- **Gestion des erreurs** : Entourez toujours `Recognize` et `Save` de blocs `try/catch`. Les exceptions typiques incluent `FileNotFoundException`, `OutOfMemoryException` et `UnsupportedFormatException`.

---

## Exemple complet fonctionnel (Copier‑coller)

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Apply license (optional – removes evaluation watermark)
            // var license = new License();
            // license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");

            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Load PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Configure output as searchable PDF and set language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
            ocrEngine.Configuration.Language = Language.English;

            // 4️⃣ Run OCR – *recognize text PDF*
            ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Sortie attendue** (console) :

```
Searchable PDF created at: C:\Docs\handbook_searchable.pdf
```

Ouvrez le fichier résultant, appuyez sur **Ctrl + F**, et vous pourrez localiser n’importe quel mot présent dans les pages numérisées d’origine. C’est la magie de transformer un *PDF numérisé avec OCR* en un **PDF recherchable**.

---

## Conclusion

Nous venons de démontrer comment **créer des PDF recherchables** avec Aspose OCR pour .NET, en couvrant tout, de l’installation du package à la gestion des PDFs multilingues et protégés par mot de passe. En suivant ces étapes, vous pouvez de façon fiable *exécuter l’OCR sur PDF*, *reconnaître le texte PDF* et convertir n’importe quel *PDF numérisé avec OCR* en un actif entièrement recherchable.

### Et après ?

- Explorez davantage l’API **aspose ocr pdf** : extraction de texte brut, exportation vers DOCX, ou génération de PDF recherchables en masse.  
- Combinez la sortie PDF recherchable avec Aspose.PDF pour ajouter des signets ou des filigranes.  
- Expérimentez avec différents réglages DPI ou des dictionnaires OCR personnalisés pour des polices spécialisées.

N’hésitez pas à ajuster l’exemple, l’intégrer à votre pipeline de gestion documentaire, ou poser des questions dans les commentaires. Bon codage, et profitez de transformer ces scans illisibles en or recherchable !

## Tutoriels associés

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Cómo hacer OCR a PDF en .NET con Aspose.OCR](/ocr/spanish/net/text-recognition/recognize-pdf/)
- [كيفية إجراء OCR لملف PDF في .NET باستخدام Aspose.OCR](/ocr/arabic/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}