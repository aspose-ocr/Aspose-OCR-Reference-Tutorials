---
category: general
date: 2026-03-26
description: Créer un PDF consultable avec Aspose.OCR Java – apprenez à charger une
  image OCR, définir la langue principale, extraire le texte de l'image et enregistrer
  le PDF OCR.
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: fr
og_description: Créez un PDF consultable avec Aspose.OCR Java. Guide étape par étape
  pour charger l'image OCR, définir la langue principale, extraire le texte de l'image
  et enregistrer le PDF OCR.
og_title: Créer un PDF interrogeable avec Aspose.OCR – Guide Java
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: Créer un PDF recherchable avec Aspose.OCR – Guide Java
url: /fr/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF consultable avec Aspose.OCR – Guide Java

Vous avez déjà eu besoin de **create searchable pdf** à partir d'un document numérisé mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul—de nombreux développeurs rencontrent ce problème lorsqu'ils abordent pour la première fois l'OCR en Java. La bonne nouvelle, c'est qu'Aspose.OCR rend toute la chaîne—du chargement d'une image à la définition de la langue principale et enfin l'enregistrement d'un PDF avec OCR—assez simple. Dans ce tutoriel, nous allons parcourir un exemple complet et exécutable qui **extracts text from image**, vous permet de **set primary language**, et se termine par un **save OCR pdf** que vous pouvez ouvrir avec n'importe quel lecteur.

Nous couvrirons également quelques astuces pratiques, comme l'activation de l'accélération GPU pour un traitement plus rapide et la gestion de documents multilingues (Tamil + English dans notre cas). À la fin, vous disposerez d'un extrait solide, prêt pour la production, que vous pourrez intégrer à votre projet.

## Ce dont vous avez besoin

- **Java 17** (ou tout JDK récent ; Aspose.OCR prend en charge Java 8+)
- **Aspose.OCR for Java** library (téléchargez depuis le site officiel ou ajoutez via Maven)
- Un **license file** (ou l'essai de 30 jours)
- Un fichier image contenant du texte (la démo utilise `sample-mixed-tamil-eng.jpg`)

Pas de frameworks supplémentaires, pas de dépendances natives—juste du Java pur et les Aspose.JARs.

## Étape 1 : Créer un PDF consultable – Configuration du projet

Avant de plonger dans le code, assurons-nous que le projet est prêt à générer des fichiers **create searchable pdf**.

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **Pro tip :** Gardez le numéro de version à jour ; les versions plus récentes incluent souvent des correctifs de performance pour l'utilisation du GPU.

Créez maintenant une classe Java simple appelée `RecentFeaturesDemo`. Cette classe contiendra toute la logique dont nous avons besoin pour **load image OCR**, configurer les paramètres de langue, et enfin **save OCR pdf**.

## Étape 2 : Charger l'image OCR et initialiser le moteur

La première vraie étape du pipeline consiste à **load image OCR**. Cela indique à Aspose.OCR quel fichier analyser.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **Why this matters :** Activer le GPU (`setUseGpu(true)`) peut réduire le temps de traitement jusqu'à 70 % sur du matériel moderne, tandis que le traitement parallèle garantit que le CPU n'est pas inactif lorsque le GPU est occupé.

## Étape 3 : Définir la langue principale (et une secondaire)

Si vous sautez cette étape, Aspose.OCR essaiera de deviner la langue, ce qui est plus lent et moins précis. Voici comment **set primary language** en Tamil et ajouter l'anglais comme solution de secours.

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **Explanation :** La langue principale influence le jeu de caractères et le dictionnaire utilisés pendant la reconnaissance. Ajouter une langue secondaire est crucial pour les documents à script mixte (pensez à un reçu contenant à la fois du texte Tamil et English).  
> **Edge case :** Si votre document contient plus de deux langues, vous pouvez appeler `addAdditionalLanguage(...)` pour chaque langue supplémentaire.

## Étape 4 : Pré‑traiter l'image – Redressement et débruitage

Les images numérisées souffrent souvent de rotation ou de bruit de fond. Le pré‑traitement aide le moteur OCR à **extract text from image** de manière plus fiable.

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **Tip :** Si vous savez que l'image est déjà propre, vous pouvez ignorer `setDenoise(true)` pour gagner quelques millisecondes.

## Étape 5 : Charger le fichier image

Maintenant que le moteur est prêt, nous le pointons vers le fichier que nous voulons analyser.

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **What if the path is wrong ?** Aspose.OCR lance une `FileNotFoundException` claire. Enveloppez l'appel dans un try‑catch si vous avez besoin d'une gestion d'erreur élégante.

## Étape 6 : Exécuter l'OCR et extraire le texte de l'image

Avec tout configuré, il est temps d'exécuter réellement la reconnaissance. Cette étape **extracts text from image** et prépare les données nécessaires à la création du PDF.

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

La sortie console typique pour l'image de démonstration ressemble à :

```
வணக்கம் World
This is a mixed language sample.
```

Vous remarquerez que la ligne en Tamil est correctement rendue, suivie de l'anglais. C'est le résultat d'un **set primary language** correctement appliqué.

## Étape 7 : Enregistrer le PDF OCR – La pièce finale

La dernière pièce du puzzle est de **save OCR pdf**. Aspose.OCR peut intégrer une couche de texte invisible au-dessus de l'image originale, rendant le PDF consultable.

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Ouvrez `searchable.pdf` dans Adobe Reader, appuyez sur **Ctrl + F**, et vous pouvez rechercher à la fois des mots en Tamil et en English—exactement ce que promet un workflow **create searchable pdf**.

## Exemple complet fonctionnel (Copier‑Coller)

Ci-dessous le programme complet que vous pouvez compiler et exécuter tel quel. Remplacez les chemins de substitution par vos propres répertoires.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Exécutez-le avec :

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

Vous devriez voir le texte extrait affiché dans la console, suivi d'une confirmation que le **searchable pdf** a été écrit sur le disque.

## Questions fréquentes & cas limites

### Que faire si je dois **load image OCR** depuis un tableau d'octets ?

Vous pouvez remplacer `ImageStream.fromFile(imagePath)` par `ImageStream.fromBytes(byteArray)`. Cela est pratique lorsque l'image provient d'une base de données ou d'un service web.

### Comment gérer les PDF qui contiennent déjà des images ?

Aspose.OCR peut travailler directement sur les pages PDF : `ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`. Le moteur rasterisera chaque page en interne avant la reconnaissance.

### Mon GPU n’est pas détecté—devrais-je garder `setUseGpu(true)` ?

Si `setUseGpu(true)` échoue, Aspose.OCR revient automatiquement au CPU. Vous pouvez vérifier `ocrEngine.getEngineSettings().isGpuAvailable()` avant de l'activer.

### Puis-je **save OCR pdf** avec des métadonnées personnalisées ?

Oui. Après la reconnaissance, utilisez `ocrEngine.getPdfSaveOptions().setTitle("My Document")` ou `setAuthor("John Doe")` avant d'appeler `save`.

## Conseils de performance pour les gros lots

- **Batch processing :** Réutilisez la même instance `OcrEngine` pour plusieurs images. Appelez uniquement `ocrEngine.clear()` entre les exécutions.
- **Thread pool :** Enveloppez chaque tâche d'image dans un `Callable` et soumettez‑la à un `ExecutorService`. Comme nous avons activé le traitement parallèle, chaque thread bénéficiera de l'utilisation multi‑cœur.
- **Memory management :** Pour les images gigapixels, envisagez de réduire la résolution avec `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)` afin de garder une utilisation de RAM raisonnable.

## Conclusion

Nous venons de parcourir un workflow complet **create searchable pdf** en utilisant Aspose.OCR pour Java. En partant de **load image OCR**, nous

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}