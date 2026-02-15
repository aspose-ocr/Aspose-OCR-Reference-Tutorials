---
category: general
date: 2026-02-14
description: 'OCR d''images par lots simplifié : apprenez comment extraire du texte
  à partir de fichiers PNG en utilisant Aspose OCR avec un traitement parallèle en
  Java.'
draft: false
keywords:
- batch image OCR
- extract text from png
- parallel OCR Java
- Aspose OCR async
- OCR batch processing
language: fr
og_description: Tutoriel OCR par lots d'images montrant comment extraire du texte
  de fichiers PNG à l'aide de l'API asynchrone d'Aspose OCR en Java.
og_title: OCR d'images par lots en Java – Extraction rapide de texte PNG
tags:
- Java
- OCR
- Aspose
- Image Processing
title: OCR d'images par lot en Java – Extraire rapidement le texte des fichiers PNG
url: /fr/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/
---

as is. So keep **batch image OCR**. Also **extract text from PNG** keep as is.

Proceed.

We'll translate each paragraph.

Also code block placeholders remain unchanged.

List items, table, etc.

Make sure to keep markdown syntax.

Let's craft final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR d'images par lots en Java – Extraire rapidement du texte à partir de fichiers PNG

Vous avez déjà eu besoin d'exécuter **batch image OCR** sur un dossier de scans PNG mais vous vous inquiétiez de la vitesse ? Vous n'êtes pas seul. Dans de nombreux projets réels—numérisation de factures, archivage de livres numérisés ou traitement de reçus—les développeurs doivent **extract text from PNG** rapidement et de façon fiable.  

La bonne nouvelle ? Avec l'API asynchrone d'Aspose OCR, vous pouvez lancer un pipeline OCR parallèle en quelques lignes de Java. Dans ce guide, nous parcourrons la solution complète et exécutable, expliquerons pourquoi chaque élément est important et vous montrerons comment vérifier les résultats. À la fin, vous disposerez d'un programme autonome qui traite un lot complet de fichiers PNG en parallèle, vous fournissant une sortie texte propre et corrigée orthographiquement.

## Ce que vous allez apprendre

- Comment lister les fichiers PNG pour un traitement par lots  
- Configurer le `OcrEngine` d'Aspose pour la langue anglaise et la correction orthographique  
- Exécuter l'OCR de façon asynchrone avec `processAsync` et gérer le résultat `Future`  
- Lire et afficher le texte reconnu pour chaque image  
- Astuces pour la mise à l'échelle, la gestion des erreurs et l'optimisation des performances  

### Prérequis

- Java 8 ou supérieur installé (le code utilise le package standard `java.util.concurrent`)  
- Une licence Aspose OCR for Java ou un essai gratuit (téléchargez‑la depuis le site d'Aspose)  
- Un dossier contenant quelques captures d'écran PNG ou pages numérisées que vous souhaitez tester  

Passons maintenant à la pratique.

## Étape 1 – Rassembler vos fichiers PNG pour un lot

Avant que le moteur OCR ne puisse travailler, il doit connaître les images à traiter. La façon la plus simple est de créer une `List<String>` de chemins de fichiers absolus ou relatifs.

```java
// Step 1: Prepare a list of PNG files you want to run OCR on
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png",
        "YOUR_DIRECTORY/page4.png");
```

**Pourquoi c’est important :**  
Créer la liste à l'avance permet au moteur de planifier chaque fichier indépendamment, ce qui constitue la base d'un vrai traitement par lots. Si vous devez plus tard parcourir un répertoire dynamiquement, remplacez simplement le `Arrays.asList` statique par un flux `Files.walk`.

## Étape 2 – Initialiser et régler le moteur Aspose OCR

Le `OcrEngine` d'Aspose est hautement configurable. Ici nous définissons la langue sur l'anglais et activons la correction orthographique — deux options qui améliorent considérablement la qualité du texte extrait, surtout à partir de scans PNG bruyants.

```java
// Step 2: Create and configure the OCR engine
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getEngineOptions()
         .setLanguage(OcrLanguage.ENGLISH)          // English language model
         .setSpellCorrectionEnabled(true);          // Enable spell‑checking
```

**Pourquoi ces paramètres :**  
- **Language selection** indique au moteur quel jeu de caractères et quel dictionnaire utiliser, réduisant les fausses reconnaissances.  
- **Spell correction** corrige les erreurs d’OCR courantes (par ex., “1” vs “l”) sans que vous ayez à post‑traiter la sortie.

> **Astuce pro :** Si vos images contiennent plusieurs langues, vous pouvez passer une liste comme `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.FRENCH)`.

## Étape 3 – Lancer le traitement par lots asynchrone

Le travail lourd se fait dans `processAsync`. Il renvoie un `Future<List<OcrResult>>`, permettant à votre thread principal de continuer d’autres tâches pendant que l’OCR s’exécute en arrière‑plan.

```java
// Step 3: Start asynchronous processing of the image batch
Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

// (Optional) Do something useful while OCR runs, e.g., log progress, load UI, etc.
System.out.println("OCR started – you can perform other tasks now...");
```

**Pourquoi asynchrone :**  
Exécuter l’OCR séquentiellement peut être très lent — chaque PNG peut prendre une seconde ou plus. En déléguant le travail à un pool de threads, vous exploitez plusieurs cœurs CPU et réduisez drastiquement le temps d’exécution total.

## Étape 4 – Récupérer les résultats lorsqu’ils sont prêts

Lorsque vous êtes prêt à consommer la sortie, appelez simplement `get()` sur le `Future`. Cette appel ne bloque que jusqu’à la fin de l’OCR, puis vous renvoie une liste d’objets `OcrResult` dans le même ordre que la liste d’entrée.

```java
// Step 4: Wait for all results and retrieve them
List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion
```

**Gestion des expirations :**  
Si vous voulez éviter un blocage indéfini, utilisez `ocrFuture.get(60, TimeUnit.SECONDS)` et capturez `TimeoutException` pour implémenter un plan de secours.

## Étape 5 – Afficher le texte reconnu pour chaque PNG

Maintenant que vous avez les résultats, parcourez‑les et imprimez le texte extrait à côté du nom de fichier original. C’est ici que vous **extract text from PNG** réellement.

```java
// Step 5: Show the OCR output for each image
for (int i = 0; i < ocrResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(ocrResults.get(i).getText());
    System.out.println("---");
}
```

**Exemple de sortie attendue**

```
File: YOUR_DIRECTORY/page1.png
Invoice #12345
Date: 2024‑03‑01
Total: $1,250.00
---
File: YOUR_DIRECTORY/page2.png
...
```

Si le moteur OCR ne parvient pas à reconnaître une page, le `getText()` correspondant renverra une chaîne vide — c’est toujours bon de vérifier cela dans le code de production.

## Exemple complet fonctionnel

Voici le programme complet, prêt à être exécuté. Copiez‑collez‑le dans un fichier nommé `ParallelOcrDemo.java`, remplacez `YOUR_DIRECTORY` par le chemin de votre dossier PNG, puis lancez `javac ParallelOcrDemo.java && java ParallelOcrDemo`.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Prepare a list of image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png",
                "YOUR_DIRECTORY/page4.png");

        // Step 2: Create and configure the OCR engine (set language and enable spell‑checking)
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineOptions()
                 .setLanguage(OcrLanguage.ENGLISH)
                 .setSpellCorrectionEnabled(true);

        // Step 3: Start asynchronous processing of the image batch
        Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

        // (Optional) Perform other work here while OCR runs in the background...
        System.out.println("OCR processing started in background...");

        // Step 4: Wait for all results and retrieve them
        List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion

        // Step 5: Display the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### Exécuter la démo

1. **Compiler** – `javac -cp "aspose-ocr.jar" ParallelOcrDemo.java`  
2. **Exécuter** – `java -cp ".:aspose-ocr.jar" ParallelOcrDemo`  

Vous devriez voir chaque nom de fichier PNG suivi du texte extrait, séparés par des tirets.  

> **Remarque :** Si vous rencontrez une `LicenseException`, assurez‑vous de charger votre licence Aspose avant de créer le moteur :

```java
License lic = new License();
lic.setLicense("Aspose.OCR.Java.lic");
```

## Mise à l’échelle – Conseils pour un OCR par lots en production

| Situation | Recommandation |
|-----------|----------------|
| **Centaines de PNG** | Augmentez la taille du pool de threads via `ocrEngine.setThreadPoolSize(8)` (ou plus, en fonction du nombre de cœurs CPU). |
| **Contraintes de mémoire** | Traitez les fichiers par petits lots (par ex., lots de 50) et libérez la liste `OcrResult` après chaque lot. |
| **Qualité d’image variable** | Activez `setPreprocessingOptions` pour auto‑rotation, redressement ou amélioration du contraste avant la reconnaissance. |
| **Multiples langues** | Appelez `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.SPANISH)` et, éventuellement, définissez un dictionnaire personnalisé. |
| **Gestion des erreurs** | Enveloppez `ocrFuture.get()` dans un bloc try‑catch pour `ExecutionException` afin de consigner les fichiers échoués sans interrompre tout le lot. |

Ces stratégies maintiennent votre pipeline **batch image OCR** robuste, même lorsque le jeu d’entrée s’agrandit.

## Foire aux questions

**Q : Cette méthode fonctionne‑t‑elle avec des fichiers JPEG ou TIFF ?**  
R : Absolument. La méthode `processAsync` accepte tout format supporté par Aspose OCR (PNG, JPEG, TIFF, BMP, etc.). Il suffit de changer les extensions de fichier dans votre liste.

**Q : Et si je dois préserver la mise en page (tables, colonnes) ?**  
R : Aspose OCR fournit une méthode `getLayoutResult()` qui renvoie les données de position. Vous pouvez reconstruire les tables en analysant les boîtes englobantes de chaque mot.

**Q : Puis‑je exécuter cela sur une plateforme serverless ?**  
R : Oui—il suffit d’empaqueter le JAR avec la bibliothèque Aspose et de le déployer sur AWS Lambda, Azure Functions ou Google Cloud Functions. Veillez à allouer suffisamment de mémoire à la fonction pour le pool de threads OCR.

## Conclusion

Vous disposez maintenant d’une solution complète et autonome de **batch image OCR** qui extrait efficacement **text from PNG** grâce à l’API asynchrone d’Aspose OCR en Java. Le tutoriel a couvert tout, de la préparation de la liste de fichiers à la configuration de la langue et de la correction orthographique, en passant par le lancement du traitement parallèle, la gestion des résultats et l’optimisation pour la production.

Prêt pour l’étape suivante ? Essayez de changer la langue en français, expérimentez avec des dictionnaires personnalisés, ou intégrez la sortie dans un index ElasticSearch consultable. Le ciel est la limite lorsque vous combinez un OCR par lots rapide avec la concurrence moderne en Java.

Bon codage, et que votre extraction de texte soit rapide et précise ! 

![Diagram showing parallel OCR workers handling multiple PNG files](/images/batch-ocr-diagram.png){: .center alt="Batch image OCR processing diagram"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}