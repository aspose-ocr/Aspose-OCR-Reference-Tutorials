---
category: general
date: 2026-02-27
description: Apprenez à utiliser l’OCR en Java pour extraire le texte d’images à partir
  de fichiers TIFF et PDF en utilisant le traitement parallèle d’Aspose OCR. Guide
  rapide et simple.
draft: false
keywords:
- how to use ocr
- perform ocr on pdf
- extract text from tiff
- extract image text java
language: fr
og_description: Apprenez à utiliser l’OCR en Java pour extraire le texte d’images
  à partir de fichiers TIFF et PDF en utilisant le traitement parallèle d’Aspose OCR.
og_title: Comment utiliser l’OCR en Java – Traitement parallèle avec Aspose
tags:
- OCR
- Java
- Aspose
title: Comment utiliser l’OCR en Java – Traitement parallèle avec Aspose
url: /fr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l'OCR en Java – Traitement parallèle avec Aspose

Vous êtes‑vous déjà demandé **comment utiliser l'OCR** pour extraire du texte d'un document numérisé sans effort ? Vous n'êtes pas le seul. Les développeurs se heurtent constamment à un mur lorsqu'ils doivent lire du texte à partir d'images—en particulier les TIFF et les PDF—tout en maintenant les performances sous contrôle.  

Dans ce tutoriel, nous vous montrerons une solution complète, prête à l'emploi, qui **extrait le texte d'images en Java** à l'aide d'Aspose OCR, active le traitement parallèle, et vous permet même de limiter le nombre de threads. À la fin, vous disposerez d’une classe unique capable de **perform OCR on PDF** et d’**extract text from TIFF** en une fraction du temps qu’une approche mono‑threadée prendrait.

> **Ce que vous en retirerez**  
> * Une explication claire de l'importance de l'OCR parallèle.  
> * Un programme Java complet (sans import manquant).  
> * Des astuces pour ajuster l'utilisation des threads et gérer les pièges courants.  

## Prérequis

- Java 8 ou plus récent (le code compile également avec JDK 11).  
- Bibliothèque Aspose.OCR for Java – vous pouvez récupérer le JAR le plus récent depuis Maven Central (`com.aspose:aspose-ocr`).  
- Un fichier image (`.tif`, `.tiff`) ou un PDF que vous souhaitez traiter.  
- Une quantité modeste de RAM — le traitement parallèle créera quelques threads, mais Aspose est efficace en mémoire.

Si vous avez tout cela, plongeons‑y.

![Diagramme d'exemple d'utilisation de l'OCR – comment utiliser l'OCR en Java avec traitement parallèle](how-to-use-ocr-pipeline.png)

*Image alt text: diagramme d'exemple d'utilisation de l'OCR*

---

## Étape 1 : Configurez votre projet et ajoutez Aspose OCR

### Pourquoi c’est important

Avant de pouvoir **perform OCR on PDF** ou toute image, la bibliothèque doit être sur votre classpath. Sans elle, le compilateur lèvera `ClassNotFoundException` et vous resterez bloqué à l’étape deux.

### Comment faire

Si vous utilisez Maven, ajoutez la dépendance :

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

Pour Gradle :

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Astuce pro** : Gardez le numéro de version synchronisé avec les notes de version d’Aspose ; les versions plus récentes incluent souvent des améliorations de performance pour le traitement parallèle.

---

## Étape 2 : Créez le moteur OCR et activez le traitement parallèle

### Pourquoi c’est important

Par défaut, Aspose OCR s’exécute sur un seul thread. Lorsque vous lui fournissez un PDF multi‑pages ou un lot de TIFF, le moteur traite chaque page l’une après l’autre—lent et inefficace. Activer le traitement parallèle permet au CPU de traiter plusieurs pages simultanément, réduisant drastiquement le temps d’exécution.

### Code

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Path to the input file (TIFF or PDF)
        String inputPath = "YOUR_DIRECTORY/input.tif";

        // 2️⃣ Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Turn on parallel processing – this is the core of how to use OCR efficiently
        ocrEngine.getConfig().setUseParallelProcessing(true);

        // 4️⃣ (Optional) Limit threads – you can cap it to the number of cores you have
        // ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors());

        // 5️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.processImage(inputPath);

        // 6️⃣ Output the recognised text
        System.out.println(ocrResult.getText());
    }
}
```

**Explication des lignes clés**

- `setUseParallelProcessing(true) :` indique à Aspose de répartir la charge de travail sur les cœurs CPU disponibles.  
- `setMaxThreads(...) :` vous pouvez restreindre le pool de threads si vous êtes sur un serveur partagé ou si vous voulez laisser de la marge pour d’autres services.  
- `processImage(inputPath) :` fonctionne à la fois pour les fichiers image et les documents PDF, de sorte que le même appel **perform OCR on PDF** et sur les TIFF.

---

## Étape 3 : Gestion des différents types d’entrée – PDF vs. TIFF

### Pourquoi c’est important

Même si `processImage` accepte une chaîne de chemin, le traitement sous‑jacent diffère. Les PDF contiennent souvent plusieurs pages, chacune devenant un travail OCR distinct. Les TIFF peuvent être à page unique ou multi‑pages ; Aspose traite chaque trame comme une page.

### Points d’attention

| Entrée | Problème typique | Solution recommandée |
|--------|-------------------|----------------------|
| PDF | Les PDF volumineux peuvent épuiser la mémoire si toutes les pages sont chargées simultanément. | Utilisez `ocrEngine.getConfig().setMemoryOptimization(true);` (disponible dans les versions récentes). |
| TIFF multi‑pages | Certains TIFF anciens utilisent une compression non prise en charge. | Convertissez d’abord vers un format supporté, ou utilisez l’assistant `TiffImage` d’Aspose. |

Voici un extrait rapide montrant comment détecter le type de fichier et enregistrer un message convivial :

```java
import java.nio.file.*;

String ext = Files.probeContentType(Paths.get(inputPath)).toLowerCase();
if (ext.contains("pdf")) {
    System.out.println("Processing a PDF – expect multiple pages.");
} else if (ext.contains("tiff") || ext.contains("tif")) {
    System.out.println("Processing a TIFF image.");
} else {
    System.out.println("Unsupported file type. This demo works with PDF and TIFF.");
}
```

---

## Étape 4 : Vérification de la sortie – Que devez‑vous voir ?

Lorsque le programme se termine, le texte brut extrait s’affiche dans la console. Pour une facture numérisée simple, la sortie pourrait ressembler à :

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

Si l’OCR a du mal avec une page particulière, Aspose insère une ligne de remplacement comme `[Unrecognizable]`. Vous pouvez filtrer ces lignes plus tard si vous avez besoin de données propres.

**Vérification rapide**

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

---

## Étape 5 : Optimiser les performances – Quand ajuster le nombre de threads

### Pourquoi c’est important

Plus de threads ne signifient pas toujours des résultats plus rapides. Sur un ordinateur portable à 4 cœurs, lancer 8 threads peut entraîner un surcoût de commutation de contexte. À l’inverse, sur un serveur à 32 cœurs, vous voudrez exploiter toute la puissance disponible.

### Comment trouver le bon compromis

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

Exécutez le programme avec différents paramètres et chronométrez :

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

Enregistrez les temps, choisissez la configuration qui offre le meilleur débit, et verrouillez‑la pour la production.

---

## Étape 6 : Étendre la démo – Traitement par lots de plusieurs fichiers

Si vous devez **extract image text java** d’un dossier complet, encapsulez la logique principale dans une boucle :

```java
Path folder = Paths.get("YOUR_DIRECTORY");
try (DirectoryStream<Path> stream = Files.newDirectoryStream(folder, "*.{tif,tiff,pdf}")) {
    for (Path file : stream) {
        System.out.println("\n--- Processing: " + file.getFileName() + " ---");
        OcrResult result = ocrEngine.processImage(file.toString());
        // Save or further process result.getText()
    }
}
```

Ce modèle s’adapte bien car le moteur exécute déjà les pages de chaque fichier en parallèle. La boucle externe s’exécute séquentiellement, mais vous pourriez également soumettre chaque fichier à un `ExecutorService` si vous devez saturer un grand parc de CPU.

---

## Pièges courants & Comment les éviter

| Symptom | Cause probable | Solution |
|---------|----------------|----------|
| `OutOfMemoryError` | Trop de pages chargées en même temps (surtout avec de gros PDF). | Activez l’optimisation mémoire (`setMemoryOptimization(true)`) ou traitez les PDF page‑par‑page avec `processPage`. |
| Caractères illisibles | Configuration de langue/jeu de caractères incorrecte. | Appelez `ocrEngine.getConfig().setLanguage(OcrLanguage.English);` ou l’énumération de langue appropriée. |
| Performances lentes malgré le drapeau parallèle | Le système d’exploitation limite la création de threads ou la JVM tourne avec une petite taille de tas. | Augmentez le paramètre `-Xmx` du tas, et vérifiez les limites de threads OS (`ulimit -u`). |
| Sortie vide | Résolution de l’image d’entrée < 300 dpi. | Agrandissez l’image avant l’OCR ou utilisez un scanner qui produit une résolution plus élevée. |

---

## Récapitulatif – Ce que nous avons couvert

- **Comment utiliser l'OCR** en Java avec le `OcrEngine` d’Aspose.  
- Activation du **traitement parallèle** pour accélérer **perform OCR on PDF** et **extract text from TIFF**.  
- Ajustement du nombre de threads pour des performances optimales.  
- Gestion des cas limites comme les PDF volumineux, les TIFF multi‑pages et les paramètres de langue.  
- Extension de la démo mono‑fichier en un processeur par lots adapté aux charges de travail réelles.

---

## Prochaines étapes

Maintenant que vous maîtrisez les bases, explorez ces sujets connexes :

- **Extract image text java** à partir de notes manuscrites (activez `setHandwritingRecognition(true)`).  
- Intégration de la sortie OCR avec Apache Tika pour l’extraction de métadonnées.  
- Stockage des résultats dans Elasticsearch pour des archives de documents recherchables.  
- Utilisation d’Aspose OCR avec d’autres langages comme Python ou .NET—les principes restent les mêmes.

N’hésitez pas à expérimenter avec différentes limites de threads, formats d’image et packs de langues. Plus vous jouerez, mieux vous comprendrez les compromis entre vitesse et précision.

---

### Bon codage !

Si vous rencontrez des problèmes ou avez des idées d’optimisation supplémentaires, laissez un commentaire ci‑dessous. Je suis toujours partant pour discuter des astuces OCR—sans effort, juste du code.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}