---
category: general
date: 2026-05-21
description: Créez un PDF consultable à l'aide d'Aspose OCR tout en améliorant la
  précision de l'OCR et apprenez comment charger une image pour l'OCR en C#. Tutoriel
  étape par étape.
draft: false
keywords:
- create searchable PDF
- improve OCR accuracy
- load image for OCR
- Aspose OCR C#
- PDF output with OCR
language: fr
og_description: Créer un PDF consultable avec Aspose OCR. Apprenez comment améliorer
  la précision de l'OCR et charger une image pour l'OCR dans un exemple unique et
  exécutable.
og_title: Créer un PDF consultable avec Aspose OCR – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Create searchable PDF using Aspose OCR while you improve OCR accuracy
    and learn how to load image for OCR in C#. Step‑by‑step tutorial.
  headline: Create Searchable PDF with Aspose OCR – Complete Programming Guide
  type: TechArticle
tags:
- OCR
- Aspose
- PDF
- C#
title: Créer un PDF interrogeable avec Aspose OCR – Guide complet de programmation
url: /fr/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF consultable avec Aspose OCR – Guide complet de programmation

Vous avez déjà eu besoin de **créer un PDF consultable** à partir d’une image numérisée mais vous ne saviez pas par où commencer ? Vous n’êtes pas seul — de nombreux développeurs rencontrent ce problème lorsqu’ils abordent leurs premiers projets OCR. La bonne nouvelle, c’est qu’Aspose OCR rend toute la chaîne—chargement de l’image, amélioration de la qualité pour de meilleurs résultats, puis sauvegarde d’un PDF consultable—très simple.

Dans ce guide, nous parcourrons un exemple complet, de bout en bout, qui non seulement montre comment **créer un PDF consultable**, mais aussi comment **améliorer la précision OCR** et la bonne façon de **charger l’image pour l’OCR**. À la fin, vous disposerez d’une application console C# prête à l’emploi qui génère un PDF consultable avec l’image originale intégrée.

## Ce que vous allez apprendre

- Installer Aspose OCR (y compris l’accélération GPU optionnelle)  
- Configurer le moteur pour le français (ou toute autre langue) afin d’**améliorer la précision OCR**  
- **Charger correctement l’image pour l’OCR** à l’aide de `ImageStream`  
- Construire une chaîne de filtres pour nettoyer l’image avant la reconnaissance  
- Enregistrer le résultat sous forme de PDF consultable avec l’image source intégrée  

Aucune dépendance externe en dehors d’Aspose OCR n’est requise, et le code fonctionne avec .NET 6+ (ou .NET Framework 4.6+). C’est parti.

---

![Exemple de PDF consultable généré par Aspose OCR – créer un PDF consultable](images/searchable-pdf-sample.png "exemple de création de PDF consultable")

## Étape 1 : Créer un PDF consultable – Activer le GPU & définir le chemin des ressources  

Si vous disposez d’un GPU compatible, l’activer peut accélérer la reconnaissance de façon spectaculaire. Même si vous passez cette étape, le reste du code fonctionnera correctement.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// Enable GPU acceleration (optional)
OcrEngine.EnableGpu(true);

// Tell Aspose where to find language data files (offline mode)
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");
```

**Pourquoi c’est important :** L’accélération GPU réduit la latence sur les gros lots, et la définition du chemin des ressources garantit que le moteur peut fonctionner sans connexion Internet—idéal pour les pipelines CI ou les environnements isolés.

> **Astuce :** Sur un serveur sans interface graphique, assurez‑vous que les pilotes CUDA correspondent à la version fournie avec Aspose OCR ; des versions incompatibles peuvent entraîner des échecs silencieux.

## Étape 2 : Améliorer la précision OCR – Choisir la bonne langue  

Sélectionner le bon modèle de langue est un gain rapide de précision. Ici nous choisissons le français, mais vous pouvez remplacer `OcrLanguage.French` par n’importe quelle langue prise en charge.

```csharp
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.French   // improves OCR accuracy for French documents
};
```

**Pourquoi c’est important :** Les dictionnaires spécifiques à chaque langue aident le moteur à résoudre les caractères ambigus (par ex., « œ » vs « oe »). Si vous ignorez cette étape, le moteur utilise l’anglais par défaut, ce qui peut réduire fortement **l’amélioration de la précision OCR** pour les textes non anglais.

## Étape 3 : Charger l’image pour l’OCR – Utilisation de ImageStream  

Nous **chargeons maintenant l’image pour l’OCR**. L’assistant `ImageStream.FromFile` masque la gestion du bitmap brut et fonctionne avec la plupart des formats courants (JPG, PNG, TIFF).

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

**Pourquoi c’est important :** Charger l’image de cette façon garantit qu’Aspose reçoit le fichier dans un format qu’il peut traiter efficacement. Si vous essayez de fournir directement un `Bitmap` brut, vous risquez de rencontrer des problèmes de gestion de mémoire sur les gros fichiers.

## Étape 4 : Construire une chaîne de filtres d’image pour augmenter la précision  

Une image propre représente la moitié du travail. La chaîne ci‑dessous redresse l’image et élimine le bruit de fond—deux coupables classiques qui sabotent **l’amélioration de la précision OCR**.

```csharp
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());   // corrects rotation
filterPipeline.Add(new DenoiseFilter()); // reduces grainy artifacts

// Apply the pipeline and replace the original image
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);
```

**Pourquoi c’est important :** Le redressement (deskew) assure que les lignes de texte sont horizontales, tandis que le débruitage (denoise) réduit les taches de caractères erronées. Vous pouvez ajouter d’autres filtres (par ex., `ContrastFilter`) si vos scans sources sont particulièrement mauvais.

## Étape 5 : Effectuer la reconnaissance OCR  

Après le pré‑traitement, nous laissons enfin le moteur faire sa magie.

```csharp
ocrEngine.Recognize();
```

Cette unique ligne déclenche le modèle d’apprentissage profond derrière Aspose OCR. Elle remplit `ocrEngine.Text` avec le texte brut et prépare également la sortie PDF.

> **Et si le texte apparaît illisible ?** Vérifiez à nouveau le paramètre de langue de l’Étape 2 et envisagez d’ajouter un `BinarizeFilter` à la chaîne.

## Étape 6 : Enregistrer le résultat sous forme de PDF consultable  

L’étape finale consiste à sauvegarder un **PDF consultable** où le texte extrait se trouve derrière l’image originale—exactement ce qu’il faut pour les documents juridiques ou d’archivage.

```csharp
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });
```

**Pourquoi c’est important :** `EmbedOriginalImage = true` conserve la fidélité visuelle du scan tout en permettant la recherche de texte. Si vous le définissez à `false`, le PDF ne contiendra que le texte extrait, ce qui peut être utile pour des archives légères.

### Optionnel : Afficher le texte reconnu & le JSON  

Si vous souhaitez inspecter la sortie brute, ces lignes affichent le texte simple et un payload JSON structuré.

```csharp
Console.WriteLine(ocrEngine.Text);               // plain text
Console.WriteLine(ocrEngine.GetResultAsJson());  // JSON with layout info
```

**Sortie attendue :** Après l’exécution du programme, vous verrez la ou les phrases françaises affichées dans la console, suivies d’un objet JSON contenant les boîtes englobantes, les scores de confiance et les métadonnées de langue.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// 1️⃣ Enable GPU (optional) and set resources path
OcrEngine.EnableGpu(true);
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");

// 2️⃣ Create and configure the OCR engine (improve OCR accuracy)
var ocrEngine = new OcrEngine { Language = OcrLanguage.French };

// 3️⃣ Load the source image (load image for OCR)
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");

// 4️⃣ Build filter pipeline (deskew + denoise)
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());
filterPipeline.Add(new DenoiseFilter());
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);

// 5️⃣ Recognize text
ocrEngine.Recognize();

// 6️⃣ Save as searchable PDF (create searchable PDF)
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });

// Optional: output text and JSON
Console.WriteLine(ocrEngine.Text);
Console.WriteLine(ocrEngine.GetResultAsJson());
```

Exécutez le programme, pointez `YOUR_DIRECTORY` vers un dossier contenant `input.jpg` et les ressources Aspose OCR, et vous obtiendrez `output.pdf` juste à côté.

---

## Conclusion

Vous disposez maintenant d’une recette solide, prête pour la production, pour **créer des PDF consultables** avec Aspose OCR, tout en apprenant comment **améliorer la précision OCR** et **charger correctement l’image pour l’OCR**. La chaîne—GPU (optionnel) → sélection de la langue → chargement de l’image → chaîne de filtres → reconnaissance → sauvegarde PDF—couvre chaque étape cruciale, vous permettant de l’adapter à d’autres langues, à des lots plus importants ou à d’autres formats de sortie.

Et après ? Essayez de remplacer `PdfSaveOptions` par `DocxSaveOptions` pour générer des documents Word consultables, expérimentez des filtres supplémentaires comme `ContrastFilter`, ou intégrez ce code dans une API ASP.NET Core pour générer des PDF à la volée. Les possibilités sont infinies, et avec les bases posées ici, vous êtes bien équipé pour relever tout défi lié à l’OCR.

Des questions ou un problème ? Laissez un commentaire, et bon codage !

## Tutoriels associés

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}