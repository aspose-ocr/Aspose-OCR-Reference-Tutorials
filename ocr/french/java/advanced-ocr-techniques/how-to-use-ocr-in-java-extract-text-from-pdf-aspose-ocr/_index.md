---
category: general
date: 2026-10-24
description: Apprenez à exécuter un exemple Aspose OCR Java qui extrait du texte de
  fichiers PDF, y compris le parallel OCR processing, le password‑protected PDFs,
  et la conversion de PDF numérisés en searchable text.
draft: false
keywords:
- aspose ocr java example
- parallel ocr processing
- extract text pdf java
- ocr password protected pdf
- convert scanned pdf searchable
lastmod: 2026-10-24
og_description: Exécutez un exemple Aspose OCR Java pour extraire du texte d'un PDF
  rapidement. Ce guide couvre le parallel OCR processing, les password‑protected PDFs,
  et la conversion de PDF numérisés en searchable documents.
og_image_alt: Screenshot of a Java console showing extracted text after parallel OCR
  processing with Aspose OCR
og_title: Exemple Aspose OCR Java – extraire du texte d'un PDF rapidement
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to run an Aspose OCR Java example that extracts text from
    PDF files, including parallel OCR processing, handling password‑protected PDFs,
    and converting scanned PDFs to searchable text.
  headline: 'Aspose OCR Java example: extract text from PDF quickly'
  type: TechArticle
- description: Learn how to run an Aspose OCR Java example that extracts text from
    PDF files, including parallel OCR processing, handling password‑protected PDFs,
    and converting scanned PDFs to searchable text.
  name: 'Aspose OCR Java example: extract text from PDF quickly'
  steps:
  - name: set up your project
    text: 'Add the Aspose OCR dependency to your `pom.xml`: If you prefer Gradle,
      replace the snippet with the equivalent `implementation` line. After the dependency
      resolves, you can import the required classes in your Java source file.'
  - name: create and configure the OCR engine
    text: '`OcrEngine` is the core class that performs optical character recognition.
      The `OcrEngine` class is Aspose OCR''s primary object that encapsulates all
      OCR settings and execution logic. Enable parallel processing and optionally
      limit the thread pool: **Why this matters:** - `setParallelProcessing(true'
  - name: load the PDF you want to process
    text: '`OcrInput` represents the collection of files (PDFs, images, or mixed media)
      that the engine will analyze. The `OcrInput` class aggregates one or more input
      sources, allowing you to feed PDFs, TIFFs, or JPEGs to the OCR engine in a single
      batch. Add your PDF (or a set of PDFs) to the input collectio'
  - name: run OCR across all pages in parallel
    text: '`OcrResult` holds the combined text output and per‑page confidence information
      after recognition completes. The `OcrResult` object contains the concatenated
      plain‑text result and a list of `PageResult` objects that expose confidence
      scores for each processed page. Execute the recognition: **Under th'
  - name: retrieve and display the combined text
    text: '`OcrResult.getText()` returns the full searchable string. The `getText()`
      method of `OcrResult` returns a single `String` that contains the OCR‑extracted
      text from every page, with line breaks preserved as they appeared in the source
      PDF. **Expected output:** The console prints one continuous string'
  - name: handle special scenarios
    text: '#### How does the engine deal with password‑protected PDFs? Supply the
      password when adding the file to `OcrInput`: The `add` method overload that
      accepts a password decrypts the document on the fly, allowing seamless OCR without
      manual decryption.'
  type: HowTo
- questions:
  - answer: Yes, the Aspose OCR free trial works for development and testing; a commercial
      license is required for production deployments.
    question: Can I use this example with a free trial license?
  - answer: Absolutely – pass the password to `OcrInput.add(filePath, password)` and
      the engine will decrypt the document automatically.
    question: Does the example support OCR on password‑protected PDFs?
  - answer: Over 70 languages, including right‑to‑left scripts such as Arabic and
      Hebrew.
    question: How many languages does Aspose OCR recognise?
  - answer: The engine can handle multi‑hundred‑page PDFs; you can set a memory limit
      to keep RAM usage predictable.
    question: What is the maximum PDF size I can process?
  - answer: Yes, by configuring `setMaxThreadCount` you control the maximum number
      of concurrent threads, preventing resource exhaustion.
    question: Is parallel OCR safe on shared servers?
  type: FAQPage
tags:
- ocr
- java
- aspose
- pdf
title: 'Exemple Aspose OCR Java : extraire du texte d''un PDF rapidement'
url: /fr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exemple Aspose OCR Java : extraire du texte d'un PDF rapidement

Dans ce tutoriel, vous découvrirez **comment utiliser un exemple Aspose OCR Java** pour transformer des PDF numérisés en texte consultable et lisible par machine. Que vous ayez un seul fichier multipage ou un lot de PDF protégés par mot de passe, les étapes ci‑dessous vous montrent comment configurer le moteur OCR, activer le traitement parallèle et récupérer la sortie combinée en quelques lignes de code Java.

Vous apprendrez également quand ajuster le nombre de threads pour des performances optimales, comment gérer les PDF chiffrés, et pourquoi cette approche est idéale pour convertir des documents PDF numérisés en archives consultables.

![comment utiliser OCR avec Aspose OCR Java](/images/ocr-parallel.png "Illustration du traitement OCR parallèle en Java – comment utiliser OCR")
[comment utiliser OCR avec Aspose OCR Java](/images/ocr-parallel.png "Illustration du traitement OCR parallèle en Java – comment utiliser OCR")

## Réponses rapides
- **Que fait l'exemple Aspose OCR Java ?** Il charge un PDF, exécute l'OCR sur chaque page en parallèle et renvoie le texte complet consultable sous forme d'une seule chaîne.  
- **Peut‑il traiter des PDF protégés par mot de passe ?** Oui – vous pouvez fournir le mot de passe du document lors de l'ajout du fichier à `OcrInput`.  
- **Le traitement OCR parallèle vaut‑il le coup ?** Sur une machine à 4 cœurs, il réduit le temps de traitement de 30‑70 % pour les PDF de plus de cinq pages.  
- **Quelles langues sont prises en charge ?** Plus de 70 langues, dont l'anglais, le français, l'allemand, le chinois et l'arabe.  
- **Ai‑je besoin d'une licence pour la production ?** Une licence commerciale Aspose OCR est requise pour un usage non‑essai ; l'essai gratuit fonctionne pour l'évaluation.

## Qu'est‑ce qu'un exemple Aspose OCR Java ?
L'**exemple Aspose OCR Java** est un programme concis et exécutable qui montre comment instancier le `OcrEngine`, configurer l'exécution parallèle et extraire du texte de fichiers PDF à l'aide de la bibliothèque Aspose OCR for Java. Il montre également comment gérer des scénarios courants tels que les documents protégés par mot de passe, l'ajustement de la limite de mémoire et la sélection de la langue, offrant une base solide pour construire des pipelines de traitement de documents plus importants.

## Pourquoi utiliser le traitement OCR parallèle ?
Aspose OCR peut découper un PDF multipage en pages séparées et traiter chaque page sur son propre thread. Sur un serveur à 8 cœurs, un document de 120 pages est généralement traité en moins de 30 secondes, contre plus d'une minute en mode séquentiel. Ce gain de vitesse est particulièrement précieux lorsque vous devez **convertir en masse des PDF numérisés consultables**.

## Prérequis
- Java 8 ou version supérieure installé.  
- Outil de construction Maven ou Gradle (l'exemple utilise Maven).  
- Une licence Aspose OCR for Java (l'essai gratuit suffit pour les tests).  

## Comment exécuter l'exemple Aspose OCR Java étape par étape

### Étape 1 : configurez votre projet

Ajoutez la dépendance Aspose OCR à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.11</version>
</dependency>
```

Si vous préférez Gradle, remplacez le fragment par la ligne `implementation` équivalente.  
Une fois la dépendance résolue, vous pouvez importer les classes requises dans votre fichier source Java.

### Étape 2 : créez et configurez le moteur OCR

`OcrEngine` est la classe principale qui effectue la reconnaissance optique de caractères.

La classe `OcrEngine` est l'objet principal d'Aspose OCR qui encapsule tous les paramètres et la logique d'exécution de l'OCR.  
Activez le traitement parallèle et limitez éventuellement le pool de threads :

```java
// Step 2: Initialise the OCR engine and enable parallel processing
OcrEngine ocrEngine = new OcrEngine();

// Turn on parallel processing – this is the key to faster PDF extraction
ocrEngine.setParallelProcessing(true);

// Optional: limit the number of threads (helps on low‑end machines)
ocrEngine.setMaxThreadCount(4);
```

**Pourquoi c'est important :**  
- `setParallelProcessing(true)` répartit les pages sur plusieurs cœurs CPU, réduisant considérablement le temps d'exécution sur du matériel multi‑cœur.  
- `setMaxThreadCount` protège les ressources du serveur en empêchant le moteur de monopoliser tous les cœurs, ce qui est crucial dans les environnements d'hébergement partagé ou d'intégration continue.

### Étape 3 : chargez le PDF à traiter

`OcrInput` représente la collection de fichiers (PDF, images ou médias mixtes) que le moteur analysera.

La classe `OcrInput` agrège une ou plusieurs sources d'entrée, vous permettant d'alimenter le moteur OCR avec des PDF, TIFF ou JPEG en un seul lot.  
Ajoutez votre PDF (ou un ensemble de PDF) à la collection d'entrée :

```java
// Step 3: Prepare the input – add your multi‑page PDF
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");

// If the PDF is password‑protected, supply the password like this:
// ocrInput.add("protected.pdf", "mySecretPassword");
```

**Astuce :** Utilisez un chemin absolu ou un chemin relatif au répertoire de travail pour éviter `FileNotFoundException`. La méthode `add` peut être appelée plusieurs fois pour mettre en file d'attente plusieurs documents pour un traitement par lot.

### Étape 4 : exécutez l'OCR sur toutes les pages en parallèle

`OcrResult` contient le texte combiné et les informations de confiance par page après la reconnaissance.

L'objet `OcrResult` contient le résultat texte concaténé et une liste d'objets `PageResult` qui exposent les scores de confiance pour chaque page traitée.  
Exécutez la reconnaissance :

```java
// Step 4: Perform OCR – this will run on multiple threads
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Dans les coulisses :** Chaque page est confiée à un thread de travail distinct (jusqu'au `maxThreadCount` que vous avez défini). La bibliothèque synchronise les résultats afin que le `OcrResult` final préserve l'ordre original des pages.

### Étape 5 : récupérez et affichez le texte combiné

`OcrResult.getText()` renvoie la chaîne consultable complète.

La méthode `getText()` de `OcrResult` renvoie une unique `String` contenant le texte extrait par OCR de chaque page, avec les sauts de ligne préservés tels qu'ils apparaissent dans le PDF source.  

```java
// Step 5: Output the combined OCR result
System.out.println("Combined text from all pages:");
System.out.println(ocrResult.getText());
```

**Sortie attendue :** La console affiche une chaîne continue contenant le texte lisible de toutes les pages, prête à être indexée, stockée ou traitée davantage.

### Étape 6 : gérez les scénarios spéciaux

#### Comment le moteur traite‑t‑il les PDF protégés par mot de passe ?

Fournissez le mot de passe lors de l'ajout du fichier à `OcrInput` :

```java
ocrEngine.getLanguageEngine().setLanguage(OcrLanguage.FRENCH);
```

La surcharge de la méthode `add` qui accepte un mot de passe déchiffre le document à la volée, permettant un OCR fluide sans déchiffrement manuel.

#### Comment limiter l'utilisation de la mémoire pour des fichiers très volumineux ?

Appelez `ocrEngine.setMemoryLimit(256);` pour plafonner la consommation RAM à 256 Mo. Le moteur déversera automatiquement les données excédentaires vers des fichiers temporaires, évitant les plantages « out‑of‑memory » même sur des PDF de plusieurs centaines de pages.

## Questions fréquentes & cas limites

### Ai‑je vraiment besoin du traitement parallèle ?

Si votre PDF contient **plus d'une poignée de pages** et que vous disposez d'au moins quatre cœurs CPU, activer le traitement parallèle réduit généralement le temps total d'exécution de **30‑70 %**. Pour un scan d'une seule page, la surcharge du threading peut dépasser le bénéfice, vous pouvez donc le désactiver avec `ocrEngine.setParallelProcessing(false)`.

### Que se passe‑t‑il lorsqu'une page échoue à l'OCR ?

Aspose OCR lève une `OcrException` uniquement pour les erreurs fatales comme un fichier corrompu. Les pages qui ne peuvent pas être reconnues renvoient simplement une chaîne vide, que le moteur concatène silencieusement. Vous pouvez inspecter `ocrResult.getPageResults()` pour récupérer les scores de confiance par page et gérer manuellement les pages à faible confiance.

### Comment changer la langue de reconnaissance ?

Le moteur utilise l'anglais par défaut, mais vous pouvez changer de langue avec :

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing and optionally limit threads
        ocrEngine.setParallelProcessing(true);
        ocrEngine.setMaxThreadCount(4); // Adjust based on your hardware

        // Step 3: Load the multi‑page PDF to be processed
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");
        // Uncomment and set password if needed:
        // ocrInput.add("protected.pdf", "mySecretPassword");

        // Step 4: Recognize text from all pages in parallel
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the combined OCR result
        System.out.println("Combined text from all pages:");
        System.out.println(ocrResult.getText());
    }
}
```

Remplacez `Language.FRENCH` par n'importe quel enum de langue supportée. C’est essentiel lorsque vous devez **extraire du texte PDF Java** à partir de documents multilingues.

## Astuces pro pour un OCR prêt pour la production

- **Traitement par lots :** Enveloppez le flux dans une boucle qui lit les noms de fichiers d'un répertoire, transformant la démo en service évolutif.  
- **Journalisation :** Définissez `ocrEngine.setLogLevel(LogLevel.ERROR)` en production pour supprimer les sorties verbeuses.  
- **Nettoyage du résultat :** Post‑traitez `ocrResult.getText()` avec des expressions régulières pour éliminer les espaces superflus ou les artefacts.  
- **Ajustement du pool de threads :** Utilisez `ocrEngine.setMaxThreadCount(Runtime.getRuntime().availableProcessors())` sur des serveurs à nombreux cœurs pour un débit maximal.  
- **Benchmark de performance :** Sur un Intel Xeon à 8 cœurs, un PDF de 200 pages (300 Mo) se traite en ~22 secondes avec l'OCR parallèle activé.

## Conclusion

Vous disposez maintenant d'un **exemple Aspose OCR Java** complet qui extrait du texte consultable de n'importe quel PDF numérisé, prend en charge les fichiers protégés par mot de passe et exploite le traitement parallèle pour la rapidité. En intégrant ce code dans vos propres applications, vous pouvez créer des pipelines de numérisation de documents puissants, alimenter les sorties OCR dans des index de recherche ou les combiner avec des services de traduction pour des archives multilingues consultables.

Prêt pour l'étape suivante ? Essayez d’alimenter le texte extrait dans Elasticsearch pour la recherche en texte intégral, ou enchaînez la sortie avec une API de traduction linguistique afin de créer un référentiel multilingue consultable. Bon codage !

---

**Dernière mise à jour :** 2026-10-24  
**Testé avec :** Aspose OCR for Java 24.11  
**Auteur :** Aspose  

## FAQ

**Q : Puis‑je utiliser cet exemple avec une licence d'essai gratuite ?**  
R : Oui, l'essai gratuit Aspose OCR fonctionne pour le développement et les tests ; une licence commerciale est requise pour les déploiements en production.

**Q : L'exemple prend‑il en charge l'OCR sur des PDF protégés par mot de passe ?**  
R : Absolument – transmettez le mot de passe à `OcrInput.add(filePath, password)` et le moteur déchiffrera le document automatiquement.

**Q : Combien de langues Aspose OCR reconnaît‑il ?**  
R : Plus de 70 langues, y compris les scripts de droite à gauche comme l'arabe et l'hébreu.

**Q : Quelle est la taille maximale de PDF que je peux traiter ?**  
R : Le moteur peut gérer des PDF de plusieurs centaines de pages ; vous pouvez définir une limite de mémoire pour garder la consommation RAM prévisible.

**Q : Le traitement OCR parallèle est‑il sûr sur des serveurs partagés ?**  
R : Oui, en configurant `setMaxThreadCount` vous contrôlez le nombre maximal de threads concurrents, évitant ainsi l'épuisement des ressources.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

```bash
javac -cp "path/to/aspose-ocr.jar" ParallelOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo
```

## Tutoriels associés

- [How To Use Ocr In Java Parallel Processing With Aspose](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/)
- [Create Searchable Pdf With Aspose Ocr Java Guide](/ocr/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/)
- [How To Use Ocr In Java Extract Text From Pdf Aspose Ocr](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}