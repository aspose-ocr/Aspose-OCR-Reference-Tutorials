---
category: general
date: 2026-09-18
description: Apprenez comment extraire du texte d'images en Java en utilisant Aspose
  OCR. Traitez par lots les fichiers PNG, JPG et TIFF efficacement en un seul appel.
keywords:
- extract text from images
- convert images to text
- how to batch ocr
- extract text from png
- extract text from jpg
- extract text from tiff
lastmod: 2026-09-18
og_description: Maîtrisez l'extraction de texte d'images en Java avec l'OCR par lots.
  Utilisez Aspose OCR pour convertir les fichiers PNG, JPG et TIFF en un seul appel.
og_image_alt: Diagram showing multiple image files processed together for batch OCR
og_title: Extraire du texte d'images en Java – guide OCR par lots
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to extract text from images in Java using Aspose OCR. Batch
    process PNG, JPG, and TIFF files efficiently in a single call.
  headline: How to extract text from images in Java by batch OCR
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR is pure Java and requires no UI components, so it works
      perfectly on headless environments.
    question: Can I run this on a headless server?
  - answer: A commercial license is needed for production deployments; a free trial
      is available for evaluation.
    question: Is a license required for production use?
  - answer: Any OS that can run Java 17+, including Windows, Linux, and macOS.
    question: Which operating systems are supported?
  - answer: Over 60 languages are supported out of the box, ranging from English and
      Spanish to Arabic and Chinese.
    question: How many languages can Aspose OCR recognise?
  - answer: Individual image files up to 200 MB are supported; larger files should
      be split before processing.
    question: What is the maximum file size Aspose OCR can handle?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Comment extraire du texte d'images en Java avec OCR par lots
url: /fr/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment extraire du texte à partir d'images en Java avec la reconnaissance optique de caractères par lots

Si vous devez **extraire du texte à partir d'images** rapidement et sans écrire une boucle pour chaque fichier, le OCR par lots est la solution. Dans de nombreux projets réels, vous recevez un dossier rempli de numérisations — reçus PNG, captures d'écran JPG ou TIFF multi‑pages — et vous devez les transformer en texte consultable. Aspose OCR vous permet de faire exactement cela avec un seul appel de méthode qui traite les fichiers PNG, JPG et TIFF ensemble, économisant à la fois du temps de développement et des cycles CPU.

## Réponses rapides
- **Que fait le OCR par lots ?** Il traite plusieurs fichiers image en une seule requête, renvoyant le texte pour chaque fichier.
- **Quels formats sont pris en charge ?** PNG, JPG/JPEG, et TIFF multi‑pages sont gérés nativement.
- **Ai-je besoin d'une bibliothèque native séparée ?** Non, le JAR Aspose OCR contient tout ce dont vous avez besoin.
- **Puis-je contrôler le nombre de threads exécutés ?** Oui, utilisez `setMaxParallelism` sur le processeur par lots.
- **Quelle version de Java est requise ?** Java 17 ou plus récent.

## Qu'est-ce qu'Aspose OCR ?
Aspose OCR est une bibliothèque Java qui reconnaît le texte imprimé et manuscrit dans les fichiers image sans dépendances externes. Elle prend en charge plus de 60 langues et peut traiter jusqu'à 100 images par lot, ce qui la rend idéale pour la numérisation de documents à grande échelle.

## Ce que couvre ce tutoriel
Chargez une liste de chemins d'image, créez un `OcrBatchProcessor`, ajustez le parallélisme, exécutez un seul appel `recognize` et affichez les chaînes extraites. À la fin, vous disposerez d'un programme Java prêt à l'emploi qui extrait le texte des fichiers PNG, JPG et TIFF en masse.

- **Comment faire du OCR par lots** en utilisant le `OcrBatchProcessor` d'Aspose.
- Manières d'**extraire du texte à partir d'images** de différents formats (PNG, JPG, TIFF).
- Conseils pour contrôler le parallélisme afin que votre application reste réactive.
- Un programme Java complet et exécutable que vous pouvez copier‑coller et exécuter immédiatement.

Aucune expérience préalable avec Aspose n'est requise — juste une installation Java de base et un IDE de votre choix. À la fin, vous disposerez d'une base solide pour reconnaître le texte des fichiers PNG, JPG et TIFF en masse.

---

![Diagramme illustrant comment faire du OCR par lots sur plusieurs fichiers image](/images/batch-ocr-diagram.png "comment faire du OCR par lots")

*Texte alternatif de l'image : diagramme montrant comment faire du OCR par lots avec plusieurs fichiers image traités ensemble.*

## Prérequis

| Exigence | Pourquoi c'est important |
|----------|---------------------------|
| Java 17 ou plus récent | Aspose OCR cible les JVM modernes. |
| Maven ou Gradle | Simplifie l'ajout de la bibliothèque Aspose OCR. |
| Connaissances Java de base | Nécessaire pour comprendre le flux du code. |
| Un ensemble d'images d'exemple (`.png`, `.jpg`, `.tif`) | Pour voir l'extraction en action. |

Si vous avez déjà tout cela, super — plongeons‑nous dedans.

## Étape 1 : ajouter Aspose OCR à votre projet

La première chose dont vous avez besoin est le JAR Aspose OCR. Avec Maven, ajoutez ceci à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

Si vous préférez Gradle, l'équivalent est :

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

Ajouter la dépendance récupère tout ce qui est nécessaire pour **extraire du texte à partir de png**, **extraire du texte à partir de jpg**, et **extraire du texte à partir de tiff**. Aucune bibliothèque native supplémentaire n'est requise.

## Étape 2 : définir les fichiers image à traiter

Nous allons maintenant indiquer au moteur OCR quels fichiers gérer. C'est ici que **comment faire du OCR par lots** brille vraiment — il suffit de fournir une liste de chemins et laisser la bibliothèque faire le travail lourd.

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **Astuce pro :** Gardez vos chemins de fichiers absolus ou utilisez `Paths.get(...)` pour éviter les surprises sur différents systèmes d'exploitation.

## Étape 3 : créer le processeur par lots et ajuster le parallélisme

Aspose OCR est fourni avec `OcrBatchProcessor`, qui peut exécuter plusieurs reconnaissances en parallèle. Contrôler le nombre de threads empêche votre application de monopoliser le CPU lorsque vous avez des dizaines d'images.

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

Pourquoi limiter le parallélisme ? Si vous lancez trop de threads sur un ordinateur portable modeste, vous pourriez constater un ralentissement plutôt qu'une accélération. Configurer `setMaxParallelism` vous permet d'équilibrer vitesse et stabilité.

## Étape 4 : exécuter l'appel OCR par lots

Voici le cœur de **comment faire du OCR par lots** : un seul appel `recognize` qui renvoie une liste d'objets `RecognitionResult`, un par image.  
`recognize` traite les images fournies et renvoie une liste d'objets `RecognitionResult`, chacun contenant le texte extrait.

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

La méthode bloque jusqu'à ce que chaque image soit traitée, puis vous fournit le texte. Si vous avez besoin d'un comportement non bloquant, vous pouvez envelopper cela dans un `CompletableFuture`, mais pour la plupart des scripts l'appel synchrone garde le code propre.

## Étape 5 : afficher le texte extrait

Enfin, parcourez les résultats et affichez les chaînes reconnues. Cela montre que nous avons réussi à **extraire du texte à partir d'images** de divers formats.  
`RecognitionResult` contient la sortie OCR pour une seule image, incluant le texte extrait et le score de confiance.

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### Sortie attendue

```
File: YOUR_DIRECTORY/img1.png
The quick brown fox jumps over the lazy dog.
---
File: YOUR_DIRECTORY/img2.jpg
Invoice #12345
Total: $567.89
---
File: YOUR_DIRECTORY/img3.tif
Page 1 of 3
Report generated on 2026-02-09
---
```

Si le moteur OCR ne peut pas lire un fichier, la méthode `getText()` renvoie une chaîne vide, vous pouvez donc ajouter une vérification simple pour consigner des avertissements.

## Exemple complet fonctionnel

En rassemblant tout, voici la classe Java complète et prête à l'exécution. Copiez‑la dans un fichier nommé `BatchOcrTutorial.java`, ajustez les chemins d'image, et exécutez `javac && java`.

```java
import com.aspose.ocr.*;
import java.util.Arrays;
import java.util.List;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/img1.png",
                "YOUR_DIRECTORY/img2.jpg",
                "YOUR_DIRECTORY/img3.tif");

        // Step 2: Create the batch OCR processor and optionally limit parallelism
        OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();
        ocrProcessor.setMaxParallelism(4); // limit to 4 concurrent threads

        // Step 3: Perform OCR on all images in a single batch call
        List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);

        // Step 4: Output the recognized text for each file
        for (int i = 0; i < recognitionResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(recognitionResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

Exécutez‑le, et vous verrez la console afficher le texte extrait pour chaque fichier PNG, JPG et TIFF — exactement ce dont vous avez besoin lorsque **comment faire du OCR par lots** est la question qui vous préoccupe.

## Questions fréquentes & cas limites

### Que faire si j'ai plus de trois images ?
Ajoutez simplement plus d'entrées à la liste `imageFiles`. Le processeur par lots répartira automatiquement le travail entre les threads que vous avez configurés avec `setMaxParallelism`.

### Mes images sont dans un sous‑dossier — dois‑je les lister manuellement ?
`Files.list` renvoie un flux de chemins peuplé paresseusement dans un répertoire.

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

Cela garde le code flexible et respecte toujours **comment faire du OCR par lots**.

### Comment gérer les résultats à faible confiance ?
`getConfidence()` renvoie une valeur numérique de confiance indiquant la probabilité que le texte reconnu soit correct.

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Aspose OCR prend‑il en charge d'autres langues ?
Oui — appelez `ocrProcessor.setLanguage(OcrLanguage.Spanish)` (ou tout autre enum supporté) avant l'appel `recognize`. Cela étend l'utilité au‑delà de l'anglais, rendant **extraire du texte à partir d'images** véritablement multilingue.

## Conseils de performance

* **La taille du lot compte** – Des lots plus grands réduisent la surcharge, mais des listes très longues peuvent consommer plus de mémoire. Testez avec 50–200 images par lot.
* **Parallélisme** – Sur un CPU à 4 cœurs, `setMaxParallelism(4)` donne généralement le meilleur débit. Ajustez en fonction de la charge de votre serveur.
* **Prétraitement d'image** – Convertir les images en niveaux de gris ou augmenter le contraste avant l'OCR peut améliorer la précision, surtout pour les numérisations bruyantes.

## Conclusion

Vous savez maintenant **comment faire du OCR par lots** en Java avec Aspose OCR, comment **extraire du texte à partir d'images** de divers formats, et pourquoi contrôler le parallélisme est important. L'exemple complet de code montre la reconnaissance de texte à partir de fichiers PNG, JPG et TIFF en un seul appel efficace.

Prêt pour l'étape suivante ? Alimentez la sortie OCR dans un index de recherche, une base de données ou un résumeur IA. Vous pouvez également expérimenter avec des entrées PDF (Aspose OCR les prend en charge) ou combiner cela avec des bibliothèques de prétraitement d'image comme OpenCV pour une précision encore plus élevée.

Bon codage, et rappelez‑vous — le OCR par lots n'a pas à être un casse‑tête. Avec les bons outils et un schéma clair, vous transformerez des piles d'images en texte consultable en un rien de temps.

## Questions fréquemment posées

**Q : Puis‑je exécuter cela sur un serveur sans interface graphique ?**  
R : Oui, Aspose OCR est purement Java et ne nécessite aucun composant UI, il fonctionne donc parfaitement dans des environnements sans tête.

**Q : Une licence est‑elle requise pour une utilisation en production ?**  
R : Une licence commerciale est nécessaire pour les déploiements en production ; un essai gratuit est disponible pour l'évaluation.

**Q : Quels systèmes d'exploitation sont pris en charge ?**  
R : Tout OS capable d'exécuter Java 17+, y compris Windows, Linux et macOS.

**Q : Combien de langues Aspose OCR peut‑il reconnaître ?**  
R : Plus de 60 langues sont prises en charge nativement, allant de l'anglais et l'espagnol à l'arabe et le chinois.

**Q : Quelle est la taille maximale de fichier qu'Aspose OCR peut gérer ?**  
R : Les fichiers image individuels jusqu'à 200 Mo sont pris en charge ; les fichiers plus volumineux doivent être découpés avant le traitement.

---

**Dernière mise à jour :** 2026-09-18  
**Testé avec :** Aspose OCR 24.9 pour Java  
**Auteur :** Aspose

## Tutoriels associés

- [Extraire du texte à partir d'images – Bases de l'OCR pour Java](/ocr/java/ocr-basics/)
- [Comment faire du OCR par lots en Java Guide complet pour extraire du texte](/ocr/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/)
- [Prétraiter l'image OCR en Java Augmenter la précision d'extraction du texte](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}