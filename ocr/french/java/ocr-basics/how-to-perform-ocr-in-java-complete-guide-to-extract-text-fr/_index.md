---
category: general
date: 2026-06-06
description: Comment effectuer l'OCR en Java – extraire rapidement du texte d’une
  image, convertir une image en texte et lire le texte d’un JPG à l’aide d’un exemple
  de code simple.
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: fr
og_description: Comment effectuer l’OCR en Java – apprenez à extraire du texte d’une
  image, convertir une image en texte et lire le texte d’un JPG avec un exemple prêt
  à l’emploi.
og_title: Comment réaliser l'OCR en Java – Guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  headline: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  type: TechArticle
- description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  name: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  steps:
  - name: What You’ll Learn
    text: '- Install an OCR library (yes, **ocr in java** is easier than you think).
      - Create and configure an OCR engine instance. - Load a JPG (or any image) and
      set the language. - Process the image and **extract text from image** files.
      - Print the recognized string to the console.'
  - name: Expected Output
    text: 'If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console
      will show:'
  - name: 'Pro Tip: Batch Processing'
    text: 'If you need to **extract text from image** files in bulk, wrap the core
      logic in a loop:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Comment effectuer l’OCR en Java – Guide complet pour extraire le texte des
  images
url: /fr/java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer de l'OCR en Java – Guide complet pour extraire du texte d'images

Vous vous êtes déjà demandé **comment effectuer de l'OCR** sur une photo que vous avez prise avec votre téléphone ? Vous n'êtes pas le seul. Que vous construisiez une application de numérisation de reçus ou que vous ayez simplement besoin d'extraire du texte d'un PDF numérisé, **comment effectuer de l'OCR** en Java est une compétence qui rapporte rapidement. Dans ce tutoriel, nous parcourrons un exemple pratique qui **extrait du texte d'une image** fichiers, **convertit l'image en texte**, et montre même comment **lire le texte d'un jpg** avec seulement quelques lignes de code.

> *Astuce :* La même approche fonctionne pour PNG, BMP ou tout format supporté par le moteur OCR — il suffit d'échanger le nom du fichier.

## Comment effectuer de l'OCR en Java – Vue d'ensemble

La reconnaissance optique de caractères (OCR) est la technologie qui transforme des images de lettres en texte réel et consultable. Dans l'écosystème Java, il existe plusieurs bibliothèques — Tesseract, Asprise et des SDK commerciaux — qui exposent toutes un flux de travail similaire : charger une image, indiquer au moteur la langue attendue, lancer la reconnaissance et récupérer le résultat. Ci-dessous, nous utiliserons une classe générique `OcrEngine` pour garder l'exemple clair, mais vous pouvez la remplacer par n'importe quelle implémentation concrète qui suit le même schéma.

### Ce que vous apprendrez

- Installer une bibliothèque OCR (oui, **OCR en Java** est plus facile que vous ne le pensez).
- Créer et configurer une instance du moteur OCR.
- Charger un JPG (ou toute image) et définir la langue.
- Traiter l'image et **extraire du texte d'une image** fichiers.
- Afficher la chaîne reconnue dans la console.

À la fin, vous disposerez d'un programme Java autonome que vous pourrez intégrer à n'importe quel projet et exécuter immédiatement.

![how to perform OCR example](ocr-example.png "how to perform OCR in Java illustration")

## Étape 1 – Installer et importer une bibliothèque OCR (OCR en Java)

Avant d'écrire une seule ligne de Java, vous avez besoin d'une bibliothèque qui effectue réellement le travail lourd. Si vous utilisez Maven, ajoutez une dépendance comme celle-ci (remplacez `com.example.ocr` par le vrai group ID de votre SDK choisi) :

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

Si vous préférez Gradle :

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

Une fois le JAR sur votre classpath, importez les classes dont vous aurez besoin :

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

> **Pourquoi c'est important :** Importer les bonnes classes évite les erreurs « cannot find symbol » et rend votre IDE heureux — rien de plus frustrant qu'un import manquant lorsque vous essayez de **convertir l'image en texte**.

## Étape 2 – Créer l'instance du moteur OCR (comment effectuer de l'OCR)

Maintenant que la bibliothèque est prête, lancez le moteur. Considérez le moteur comme le cerveau qui regardera les pixels et devinera les lettres.

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Créer le moteur est généralement peu coûteux ; la plupart des SDK allouent les tampons internes de façon paresseuse, vous pouvez donc réutiliser en toute sécurité la même instance sur de nombreuses images si vous traitez un lot.

## Étape 3 – Charger l'image et définir la langue (extraire du texte d'une image)

L'étape suivante consiste à fournir quelque chose à lire au moteur. Ici, nous chargeons un JPEG depuis le disque et indiquons au moteur OCR que le texte est en mongol (code ISO 639‑2 « mon »). Vous pouvez modifier le chemin ou le code de langue pour correspondre à votre cas d'utilisation.

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

> **Remarque :** Si vous ne définissez pas de langue, le moteur utilise l'anglais par défaut, ce qui peut réduire considérablement la précision lorsque le texte est réellement cyrillique ou dans un autre script. Spécifiez toujours la langue correcte lorsque vous le pouvez.

## Étape 4 – Traiter l'image et obtenir le résultat (convertir l'image en texte)

Avec l'image et la langue en place, demandez au moteur de faire sa magie. L'appel `process()` exécute l'algorithme OCR et renvoie un objet `OcrResult` contenant la chaîne reconnue et les scores de confiance.

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

En coulisses, le moteur peut effectuer un prétraitement — redressement, binarisation, réduction du bruit — afin que vous n'ayez pas à écrire ces étapes vous-même. C’est pourquoi la plupart des bibliothèques OCR modernes sont un plaisir à utiliser pour les tâches de **convertir l'image en texte**.

## Étape 5 – Sortir le texte extrait (lire le texte d'un jpg)

Enfin, extrayez le texte brut du résultat et faites-en quelque chose d'utile. Pour cette démonstration, nous l'imprimons simplement dans la console, mais vous pourriez l'écrire dans un fichier, l'alimenter dans un index de recherche ou le transmettre à un autre service.

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

Cette ligne seule prouve que vous avez réussi à **lire le texte d'un jpg** (ou tout format supporté). Si la sortie apparaît brouillée, revérifiez le code de langue et la qualité de l'image.

## Exemple complet fonctionnel (Toutes les étapes combinées)

Ci-dessous se trouve une classe Java complète, prête à être exécutée, qui assemble toutes les pièces. Copiez‑la dans un fichier nommé `OcrDemo.java`, ajustez le chemin de l'image et la langue, puis exécutez `javac OcrDemo.java && java OcrDemo`.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to perform OCR in Java using a generic OCR SDK.
 * This example loads a JPG, sets the language to Mongolian, and prints
 * the recognized text to the console.
 *
 * Replace the import package with the actual library you are using.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Validate command‑line arguments
        if (args.length < 2) {
            System.err.println("Usage: java OcrDemo <image-path> <language-code>");
            System.exit(1);
        }

        String imagePath = args[0];   // e.g., "input.jpg"
        String language = args[1];    // e.g., "mon" for Mongolian

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image
        ocrEngine.setImage(new OcrInputImage(imagePath));

        // Step 3: Set the language (ISO‑639‑2)
        ocrEngine.getSettings().setLanguage(language);

        // Step 4: Run the recognition
        OcrResult result = ocrEngine.process();

        // Step 5: Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Sortie attendue

Si `input.jpg` contient la phrase mongole « Сайн байна уу ?», la console affichera :

```
=== Recognized Text ===
Сайн байна уу?
```

Si l'image est floue ou que le code de langue est incorrect, vous verrez des caractères brouillés ou une chaîne vide — des pièges courants que nous aborderons ensuite.

## Problèmes courants et comment les résoudre

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| Caractères cyrilliques brouillés | Code de langue incorrect (par défaut anglais) | Définir `ocrEngine.getSettings().setLanguage("mon")` ou le code approprié. |
| Aucune sortie | Chemin de l'image incorrect ou fichier illisible | Vérifiez le chemin, assurez‑vous que le fichier existe et que le processus a les permissions de lecture. |
| Faible précision (<70 %) | L'image a un faible contraste ou est tournée | Pré‑traitez l'image : augmentez le contraste, redressez‑la ou convertissez‑la en niveaux de gris avant de la fournir au moteur. |
| `OutOfMemoryError` sur de gros PDF | Chargement de nombreuses pages haute résolution en même temps | Traitez les pages une à une, ou réduisez la résolution des images avant l'OCR. |

### Astuce : Traitement par lots

Si vous devez **extraire du texte d'une image** fichiers en masse, encapsulez la logique principale dans une boucle :

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

Cet extrait montre à quel point il est facile de passer d'un seul JPG à un dossier entier de numérisations.

## Aller plus loin – Que faut‑il explorer ensuite ?

- **Packs de langues :** La plupart des SDK OCR vous permettent de télécharger des fichiers de données linguistiques supplémentaires. Ajouter un nouveau pack vous permet de **convertir l'image en texte** pour des langues au‑delà de l'anglais et du mongol.
- **PDF OCR:** Combinez ce code avec Apache PDFBox pour

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extraire du texte d'images – Bases de l'OCR avec Aspose.OCR pour Java](/ocr/english/java/ocr-basics/)
- [Convertir l'image en texte en Java avec Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Comment OCR du texte d'image avec langue en utilisant Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}