---
category: general
date: 2026-01-12
description: Apprenez à reconnaître le texte à partir d'images et à extraire le texte
  des fichiers PNG en utilisant Aspose OCR en Java. Le traitement parallèle le rend
  rapide.
draft: false
keywords:
- recognize text from images
- extract text from png
language: fr
og_description: Découvrez la façon la plus simple de reconnaître du texte à partir
  d'images en Java et d'extraire du texte de fichiers PNG en utilisant Aspose OCR
  avec traitement parallèle.
og_title: reconnaître du texte à partir d'images avec Java – Guide OCR parallèle
tags:
- OCR
- Java
- Aspose
title: Reconnaître du texte à partir d'images avec Java – Tutoriel OCR parallèle
url: /fr/java/advanced-ocr-techniques/recognize-text-from-images-with-java-parallel-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte à partir d'images avec Java – Tutoriel OCR parallèle

Vous avez déjà eu besoin de **reconnaître du texte à partir d'images** mais vous êtes resté bloqué devant le « comment‑faire‑cela ? ». Vous n'êtes pas le seul. Que vous numérisiez des factures, extrayiez des données à partir de captures d'écran ou construisiez une archive consultable, pouvoir *reconnaître du texte à partir d'images* est un véritable atout.  

Dans ce guide, nous parcourrons un exemple complet et prêt à l’emploi en Java qui non seulement **reconnaît du texte à partir d'images**, mais vous montre également comment **extraire du texte d’un png** à l’aide du moteur parallèle intégré d’Aspose OCR. Aucun script externe, aucune pièce manquante — juste du code simple et des explications claires.

## Ce que vous apprendrez

- Configurer Aspose OCR dans un projet Java  
- Activer le traitement parallèle pour accélérer les travaux par lots  
- Charger une collection de fichiers PNG et **extraire du texte d’un png** efficacement  
- Gérer les problèmes courants (fichiers volumineux, résultats vides, limites de threads)  
- Voir le code source complet et exécutable à la fin de l’article  

À la fin, vous disposerez d’une solution copier‑coller que vous pourrez adapter à tout flux de travail d’extraction de texte basé sur des images.

## Prérequis

| Requirement | Why it matters |
|-------------|----------------|
| Java 8 ou plus récent | L’API Java d’Aspose OCR cible Java 8+ |
| Maven ou Gradle (pour la gestion des dépendances) | Simplifie l’ajout de la bibliothèque Aspose OCR |
| Quelques images PNG que vous souhaitez traiter | Le tutoriel utilise `doc1.png`‑`doc4.png` comme exemples |
| Connaissances de base de la syntaxe Java | Le code est simple, mais vous devrez le compiler et l’exécuter |

Si l’un de ces éléments vous manque, téléchargez le dernier JDK depuis Oracle ou AdoptOpenJDK et configurez un projet Maven simple — rien de compliqué.

![recognize text from images diagram](image.png){alt="diagramme de reconnaissance de texte à partir d'images"}

## Étape 1 – Ajouter Aspose OCR à votre projet

Tout d'abord, indiquez à Maven (ou Gradle) de récupérer la bibliothèque Aspose OCR. Dans un fichier `pom.xml`, ajoutez :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Si vous préférez Gradle, l’équivalent est :

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Astuce :** Consultez le [dépôt Maven d’Aspose OCR](https://repo.aspose.com/repo) pour la version la plus récente. Garder la bibliothèque à jour vous assure d’obtenir les dernières améliorations OCR et corrections de bugs.

## Étape 2 – Activer le traitement parallèle (la sauce secrète)

Aspose OCR peut répartir la charge de travail sur plusieurs cœurs CPU. C’est ainsi que nous maintenons l’opération **reconnaître du texte à partir d'images** rapide, même lorsque vous avez des dizaines de fichiers PNG.

```java
// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Configure parallel options – up to 4 cores in this demo
ParallelOptions parallelOptions = new ParallelOptions();
parallelOptions.setMaxDegreeOfParallelism(4); // Adjust based on your machine
ocrEngine.setParallelOptions(parallelOptions);
```

Pourquoi définir une limite ? Surcharger les threads peut priver d’autres processus de ressources, surtout sur des serveurs partagés. Quatre cœurs constituent une valeur sûre pour la plupart des ordinateurs de bureau ; augmentez-la si vous savez que votre matériel peut en supporter davantage.

## Étape 3 – Préparer la liste des fichiers PNG

Le tutoriel se concentre sur **extraire du texte d’un png** fichiers, mais le même code fonctionne pour JPEG, BMP, etc. Placez vos images dans un dossier et référez‑vous à elles comme suit :

```java
String[] imageFiles = {
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
};
```

> **Note :** Remplacez `YOUR_DIRECTORY` par le chemin absolu ou relatif où résident les fichiers PNG. Si vous devez traiter un dossier dynamique, vous pouvez utiliser `Files.list(Paths.get("YOUR_DIRECTORY"))` pour construire le tableau automatiquement.

## Étape 4 – Exécuter l’OCR sur chaque image (le moteur fait le gros du travail)

Même si nous avons activé le parallélisme, nous parcourons toujours le tableau de fichiers. Aspose OCR distribue en interne le travail de reconnaissance sur les threads que nous avons configurés.

```java
for (String imagePath : imageFiles) {
    // Load the image into the engine
    ocrEngine.setImage(imagePath);
    
    // Perform recognition
    OcrResult result = ocrEngine.recognize();
    
    // Guard against empty results
    String text = result.getText();
    if (text == null || text.isEmpty()) {
        System.out.println("[" + imagePath + "] => No text found.");
        continue;
    }
    
    // Print a short preview (first 50 characters)
    System.out.println("[" + imagePath + "] => " +
        text.substring(0, Math.min(50, text.length())) + "...");
}
```

### Pourquoi une boucle et non un flux parallèle ?

Aspose OCR divise déjà le traitement des images en interne en fonction de `ParallelOptions`. Envelopper l’appel dans un flux parallèle externe doublerait le travail et pourrait même dégrader les performances. Faites confiance à la bibliothèque pour gérer les threads.

## Étape 5 – Cas limites & conseils pratiques

| Situation | What to do |
|-----------|------------|
| **PNG volumineux ( > 10 Mo )** | Augmenter le tas JVM (`-Xmx2g`) ou redimensionner l’image avant de la transmettre au moteur. |
| **Formats d’image mixtes** | Utiliser `ocrEngine.setImage(new File(imagePath))` – le moteur détecte automatiquement le format. |
| **Besoin du texte complet, pas seulement d’un aperçu** | Stocker `result.getText()` dans un `StringBuilder` ou écrire dans un fichier pour une analyse ultérieure. |
| **Exécution sur un serveur CI sans interface graphique** | Aucune étape supplémentaire — Aspose OCR fonctionne entièrement en mode headless. |
| **Expiration de licence** | Enregistrer une licence temporaire avec `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` pour éviter les filigranes d’évaluation. |

## Exemple complet fonctionnel

Voici la classe Java complète que vous pouvez copier, coller et exécuter. Elle inclut toutes les parties dont nous avons parlé, ainsi que quelques commentaires pour plus de clarté.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.parallel.*;

public class ParallelOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create and initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing (up to 4 CPU cores)
        ParallelOptions parallelOptions = new ParallelOptions();
        parallelOptions.setMaxDegreeOfParallelism(4); // Adjust as needed
        ocrEngine.setParallelOptions(parallelOptions);

        // Step 3: Define the PNG files to be processed
        String[] imageFiles = {
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.png",
            "YOUR_DIRECTORY/doc3.png",
            "YOUR_DIRECTORY/doc4.png"
        };

        // Step 4: Recognize text from each image (engine handles parallelism internally)
        for (String imagePath : imageFiles) {
            // Load the image
            ocrEngine.setImage(imagePath);

            // Perform OCR
            OcrResult result = ocrEngine.recognize();

            // Extract the recognized text
            String text = result.getText();

            // Guard against empty results
            if (text == null || text.isEmpty()) {
                System.out.println("[" + imagePath + "] => No text found.");
                continue;
            }

            // Step 5: Output a short preview (first 50 characters)
            System.out.println("[" + imagePath + "] => " +
                text.substring(0, Math.min(50, text.length())) + "...");
        }
    }
}
```

### Sortie attendue

Si `doc1.png` contient la phrase « Invoice #12345 – Total $250.00 », vous verrez quelque chose comme :

```
[YOUR_DIRECTORY/doc1.png] => Invoice #12345 – Total $250.00...
[YOUR_DIRECTORY/doc2.png] => No text found.
[YOUR_DIRECTORY/doc3.png] => Customer Name: John Doe...
[YOUR_DIRECTORY/doc4.png] => ...
```

L’aperçu est tronqué à 50 caractères, mais la chaîne complète se trouve dans `result.getText()` pour tout traitement en aval dont vous avez besoin.

## Conclusion

Vous disposez maintenant d’un modèle solide, prêt pour la production, pour **reconnaître du texte à partir d'images** avec Aspose OCR en Java, et vous avez vu exactement comment **extraire du texte d’un png** avec des accélérations parallèles. Les étapes principales — configuration du moteur, configuration parallèle, préparation de la liste d’images et gestion des résultats — sont toutes couvertes, ainsi qu’une série de conseils pratiques pour éviter les problèmes courants.

Et ensuite ? Essayez de remplacer la liste PNG par une analyse de répertoire dynamique, canalisez la sortie OCR vers un index de recherche comme Elasticsearch, ou expérimentez les paramètres OCR spécifiques à une langue (`ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH)`). Le ciel est la limite une fois que vous avez maîtrisé le flux de travail de base.

Si vous avez rencontré des problèmes ou avez des idées pour étendre ce tutoriel, laissez un commentaire ci‑dessous. Bon codage, et profitez de transformer ces images récalcitrantes en texte consultable !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}