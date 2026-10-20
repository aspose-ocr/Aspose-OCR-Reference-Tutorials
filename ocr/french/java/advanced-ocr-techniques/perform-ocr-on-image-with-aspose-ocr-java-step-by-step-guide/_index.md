---
category: general
date: 2026-09-23
description: Apprenez comment effectuer l'OCR sur des images en Java avec Aspose OCR,
  extraire le texte d'une image et activer la correction orthographique avec un dictionnaire
  personnalisé.
draft: false
keywords:
- how to perform ocr
- how to extract text from image
- java ocr maven dependency
- java image to text conversion
- aspose ocr java
lastmod: 2026-09-23
og_description: Comment effectuer l'OCR sur des images en Java avec Aspose OCR. Ce
  guide montre comment charger une image, extraire le texte d'une image et ajouter
  la correction orthographique pour des résultats précis.
og_image_alt: 'Aspose OCR Java tutorial: extracting text from images with spell correction'
og_title: Comment effectuer l'OCR sur des images avec Aspose OCR en Java
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  headline: How to perform OCR on images with Aspose OCR in Java
  type: TechArticle
- description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  name: How to perform OCR on images with Aspose OCR in Java
  steps:
  - name: set up the project and import dependencies
    text: Add the Aspose OCR Maven dependency to your `pom.xml`. This single line
      pulls in the core OCR engine and all required transitive libraries. > **Pro
      tip:** Verify the version number on Maven Central; newer releases add language
      packs and performance improvements.
  - name: load the image for OCR
    text: '`OcrEngine` works with any `InputStream`. Use `ImageStream` to wrap a file
      path, byte array, or URL. **Definition anchor:** `ImageStream` is Aspose OCR’s
      lightweight wrapper that reads image data from various sources without converting
      it to a `BufferedImage` first.'
  - name: enable spell‑correction (optional but powerful)
    text: Turn on the built‑in spell‑correction flag to automatically fix common OCR
      mis‑recognitions such as “l” vs “1”. Spell‑correction can improve accuracy by
      up to **80 %** on low‑contrast scans, turning “Inv0ice” into “Invoice” without
      extra code.
  - name: provide a custom dictionary (tailor the engine)
    text: Supply a plain‑text dictionary for industry‑specific terminology—medical
      codes, legal terms, product SKUs, etc. **Definition anchor:** `CustomDictionary`
      loads a UTF‑8 word list that the OCR engine consults during post‑processing
      to prefer your domain vocabulary.
  - name: run the OCR process
    text: Invoke `process()` to get an `OcrResult` containing the recognized text,
      confidence scores, and optional layout data. If an error occurs, `ocrResult.getErrorMessage()`
      returns a detailed description you can log or display.
  - name: output the recognized (and corrected) text
    text: 'Print the extracted string to the console or write it to a file. For quick
      testing, a simple `System.out.println` is sufficient. Running the program should
      produce clean, searchable text similar to: If you notice stray characters, revisit
      your custom dictionary and consider pre‑processing the image '
  type: HowTo
- questions:
  - answer: No. The library runs entirely offline; all recognition happens locally
      on your JVM.
    question: Does Aspose OCR require an internet connection?
  - answer: Aspose OCR supports Java 8 through Java 21, including both standard and
      OpenJDK distributions.
    question: Which Java versions are supported?
  - answer: Yes. The engine streams data and can handle images up to 500 MB, limited
      only by available heap memory.
    question: Can I process images larger than 10 MB?
  - answer: Purchase a commercial license from the Aspose store and set the license
      file with `License license = new License(); license.setLicense("Aspose.OCR.lic");`.
    question: How do I license Aspose OCR for production?
  - answer: Aspose OCR includes a handwriting mode that can be enabled via `ocrEngine.getEngineOptions().setHandwriting(true);`,
      improving accuracy on cursive scripts.
    question: Is there built‑in support for handwritten text?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- image to text
- OCR Maven dependency
title: Comment effectuer l'OCR sur des images avec Aspose OCR en Java
url: /fr/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer la reconnaissance optique de caractères (OCR) sur une image – tutoriel complet Java

Si vous recherchez une méthode fiable pour **how to perform OCR** sur des fichiers image avec Java, vous êtes au bon endroit. Avec Aspose OCR pour Java, vous pouvez extraire du texte à partir d'images en quelques lignes de code, améliorer la précision avec un dictionnaire personnalisé et activer la correction orthographique pour nettoyer les numérisations bruyantes. Ce tutoriel vous guide à travers chaque étape — du chargement de l'image pour l'OCR à l'affichage du texte corrigé — afin que vous puissiez intégrer la conversion image‑vers‑texte dans vos applications dès aujourd'hui.

## Réponses rapides
- **Quelle est la classe principale pour démarrer l'OCR ?** `OcrEngine` est la classe centrale d'Aspose OCR qui effectue la reconnaissance optique de caractères.
- **Quel artefact Maven ajoute la prise en charge de l'OCR ?** Ajoutez `com.aspose:aspose-ocr` à votre `pom.xml`.
- **Ai-je besoin d'une licence pour le développement ?** Une licence temporaire gratuite suffit pour les tests ; une licence commerciale est requise pour la production.
- **Puis-je améliorer la précision sur des numérisations de mauvaise qualité ?** Oui — activez la correction orthographique et fournissez un dictionnaire personnalisé.
- **Le support multi‑pages est‑il intégré ?** Traitez chaque image de page dans une boucle ; le moteur est thread‑safe pour une exécution concurrente.

## Qu'est-ce que how to perform OCR ?
L'expression **how to perform OCR** désigne le processus de conversion du texte imprimé ou manuscrit présent dans une image en caractères numériques éditables et recherchables à l'aide de la technologie de reconnaissance optique de caractères. Aspose OCR implémente ce processus avec un moteur à passage unique qui prend en charge plus de 20 formats raster et plus de 50 langues.

## Pourquoi utiliser Aspose OCR pour Java ?
Aspose OCR prend en charge **plus de 20 formats d'image** (dont PNG, JPEG, TIFF, BMP et GIF) et peut traiter des **lots de plusieurs centaines de pages** sans charger le document complet en mémoire, offrant jusqu'à **300 pages par minute** sur un serveur 4‑cœurs typique. Ses fonctionnalités intégrées de correction orthographique et de dictionnaire personnalisé réduisent les taux d'erreur OCR typiques de 12 % à moins de 2 % sur des factures bruyantes.

## Prérequis
- **Java Development Kit (JDK) 8+** – environnement d'exécution Java standard.
- **Bibliothèque Aspose OCR pour Java** – obtenez le JAR le plus récent depuis Maven Central ou le portail de téléchargement Aspose.
- Un fichier image (par ex., `invoice.png`) que vous souhaitez traiter.
- (Facultatif) `custom_dict.txt` – un fichier texte UTF‑8 contenant des mots spécifiques au domaine, un par ligne.

C’est tout ce dont vous avez besoin — aucune service externe ni framework lourd.

## Comment effectuer l'OCR sur une image en Java ?
Chargez votre image, activez la correction orthographique, fournissez éventuellement un dictionnaire personnalisé, exécutez le moteur et lisez le résultat. Cette approche fonctionne aussi bien pour les fichiers d'une seule page que pour le traitement par lots, et le moteur gère automatiquement le décodage de l'image, la détection de la langue et le calcul de la confiance, vous offrant une sortie texte fiable prête pour un traitement ultérieur. Les sections suivantes détaillent chaque étape avec des explications claires et le code exact à copier.

### Étape 1 : configurer le projet et importer les dépendances

Ajoutez la dépendance Maven Aspose OCR à votre `pom.xml`. Cette ligne unique importe le moteur OCR central et toutes les bibliothèques transitives requises.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

> **Astuce :** Vérifiez le numéro de version sur Maven Central ; les versions plus récentes ajoutent des packs de langues et des améliorations de performances.

### Étape 2 : charger l'image pour l'OCR

`OcrEngine` fonctionne avec n'importe quel `InputStream`. Utilisez `ImageStream` pour encapsuler un chemin de fichier, un tableau d'octets ou une URL.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Ancre de définition :** `ImageStream` est le wrapper léger d'Aspose OCR qui lit les données d'image provenant de diverses sources sans les convertir d'abord en `BufferedImage`.

### Étape 3 : activer la correction orthographique (optionnel mais puissant)

Activez le drapeau de correction orthographique intégré pour corriger automatiquement les erreurs d'OCR courantes telles que « l » vs « 1 ».

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

La correction orthographique peut améliorer la précision jusqu'à **80 %** sur des numérisations à faible contraste, transformant « Inv0ice » en « Invoice » sans code supplémentaire.

### Étape 4 : fournir un dictionnaire personnalisé (adapter le moteur)

Fournissez un dictionnaire en texte brut pour la terminologie spécifique à un secteur — codes médicaux, termes juridiques, références produit, etc.

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

**Ancre de définition :** `CustomDictionary` charge une liste de mots UTF‑8 que le moteur OCR consulte lors du post‑traitement pour privilégier votre vocabulaire métier.

### Étape 5 : exécuter le processus OCR

Appelez `process()` pour obtenir un `OcrResult` contenant le texte reconnu, les scores de confiance et, éventuellement, les données de mise en page.

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

En cas d'erreur, `ocrResult.getErrorMessage()` renvoie une description détaillée que vous pouvez consigner ou afficher.

### Étape 6 : afficher le texte reconnu (et corrigé)

Affichez la chaîne extraite dans la console ou écrivez‑la dans un fichier. Pour un test rapide, un simple `System.out.println` suffit.

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

L'exécution du programme devrait produire un texte propre et recherché similaire à :

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

Si vous remarquez des caractères parasites, revisitez votre dictionnaire personnalisé et envisagez de pré‑traiter l'image (augmenter le contraste, débruiter ou convertir en niveaux de gris).

## Comment extraire du texte d'une image à l'aide d'un dictionnaire personnalisé ?
Chargez le dictionnaire avant le traitement, puis appelez `ocrEngine.setCustomDictionary(customDict)`. Le moteur privilégiera les mots de la liste, réduisant considérablement les faux positifs pour les vocabulaires spécialisés. En fournissant des termes spécifiques au domaine, vous aidez le post‑processeur OCR à résoudre les caractères ambigus, comme distinguer la lettre « O » du chiffre « 0 », ce qui améliore la précision globale sur les documents techniques.

## Comment ajouter correctement la dépendance Maven OCR Java ?
Ajoutez le fragment suivant à votre `pom.xml` dans la section `<dependencies>`. Cette dépendance importe la bibliothèque centrale Aspose OCR ainsi que tous les composants transitifs requis, garantissant que le moteur OCR peut être instancié sans configuration supplémentaire. Assurez‑vous d'exécuter `mvn clean install` après la mise à jour du fichier afin que Maven résolve la dernière version depuis le dépôt central.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

## Questions fréquentes & cas particuliers

### Que faire si l'image est dans un format différent (PDF, TIFF, etc.) ?
Aspose OCR gère directement les formats raster. Pour les PDF, extrayez chaque page sous forme d'image d'abord — Aspose PDF pour Java fournit `PdfExtractor` pour le faire efficacement. Une fois que vous disposez d'un `BufferedImage` ou d'un flux d'octets, l'appel `setImage` fonctionne de la même manière. Cette approche vous permet de traiter des documents multi‑pages sans convertir l'intégralité du PDF en mémoire, maintenant ainsi un flux de travail rapide et évolutif.

### Comment gérer les documents multi‑pages ?
Itérez sur chaque image de page, créez un nouveau `OcrEngine` (ou réinitialisez celui existant) et concaténez les valeurs de `OcrResult.getText()`. Cette approche maintient les contextes de correction orthographique indépendants par page. En traitant les pages séquentiellement ou en threads parallèles, vous pouvez conserver un débit élevé tout en garantissant que chaque page bénéficie du même dictionnaire et des mêmes paramètres de correction orthographique.

### Puis‑je limiter la langue ou l'ensemble de caractères ?
Oui. Appelez `ocrEngine.getEngineOptions().setLanguage(Language.English)` (ou toute langue prise en charge) pour restreindre le champ de reconnaissance, ce qui accélère le traitement jusqu'à **30 %**. Limiter la langue réduit l'ensemble de caractères que le moteur doit considérer, diminuant l'ambiguïté et améliorant à la fois la vitesse et la précision, surtout pour les documents ne contenant que des caractères latins.

### Qu'en est‑il des performances sur de gros lots ?
Le moteur est thread‑safe pour les opérations en lecture seule. Créez un pool de threads et attribuez chaque image à sa propre instance `OcrEngine`. Sur une machine à 4 cœurs, vous pouvez atteindre **≈250 pages/minute** avec une exécution parallèle. Assurez‑vous d’allouer suffisamment de mémoire heap et surveillez l'utilisation du CPU afin d'éviter les goulets d'étranglement lors du traitement de milliers d'images haute résolution.

## Conseils pour une meilleure précision

- **Pré‑traitez l'image** : augmentez le contraste, appliquez un filtre médian ou convertissez en niveaux de gris avant l'OCR.
- **Utilisez des numérisations de 300 dpi ou plus** ; les résolutions inférieures augmentent considérablement les taux d'erreur.
- **Gardez le dictionnaire personnalisé ciblé** : un excès de mots non pertinents peut perturber le correcteur orthographique.
- **Post‑traitez avec des expressions régulières** : validez les dates, nombres ou identifiants après extraction pour détecter les anomalies restantes.

## Prochaines étapes

Maintenant que vous savez **how to perform OCR** sur des images et **how to extract text from image** fichiers, vous pouvez explorer :

- Enregistrer la sortie OCR sous forme de PDF recherchable avec une couche de texte cachée.
- Stocker les données de factures extraites directement dans une base de données relationnelle.
- Appliquer des modèles d'apprentissage automatique pour nettoyer davantage les notes manuscrites.
- Exposer le flux de travail OCR en tant que service web RESTful pour les images téléchargées par les utilisateurs.

Chacune de ces extensions s'appuie sur les étapes principales présentées ci‑dessus, vous trouverez donc la transition fluide.

---

**Dernière mise à jour :** 2026-09-23  
**Testé avec :** Aspose OCR 24.12 pour Java  
**Author:** Aspose  

## Questions fréquemment posées

**Q : Aspose OCR nécessite‑t‑il une connexion Internet ?**  
R : Non. La bibliothèque fonctionne entièrement hors ligne ; toute la reconnaissance se fait localement sur votre JVM.

**Q : Quelles versions de Java sont prises en charge ?**  
R : Aspose OCR prend en charge Java 8 à Java 21, incluant les distributions standard et OpenJDK.

**Q : Puis‑je traiter des images supérieures à 10 Mo ?**  
R : Oui. Le moteur diffuse les données et peut gérer des images jusqu'à 500 Mo, limitées uniquement par la mémoire heap disponible.

**Q : Comment licencier Aspose OCR pour la production ?**  
R : Achetez une licence commerciale sur la boutique Aspose et définissez le fichier de licence avec `License license = new License(); license.setLicense("Aspose.OCR.lic");`.

**Q : Existe‑t‑il une prise en charge intégrée du texte manuscrit ?**  
R : Aspose OCR inclut un mode manuscrit qui peut être activé via `ocrEngine.getEngineOptions().setHandwriting(true);`, améliorant la précision sur les scripts cursifs.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

## Tutoriels associés

- [Effectuer l'OCR sur une image avec Aspose OCR Java – Guide étape par étape](/ocr/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/)
- [Prétraiter l'image OCR en Java pour améliorer la précision et extraire le texte](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [Comment activer le GPU pour l'OCR en Java et reconnaître le texte d'une image](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}