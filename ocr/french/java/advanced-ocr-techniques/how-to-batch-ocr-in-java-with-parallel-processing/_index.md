---
category: general
date: 2026-04-26
description: Comment réaliser une OCR par lots avec Java et Aspose OCR – reconnaître
  le texte à partir d’images, extraire le texte d’un PNG et exploiter tous les cœurs
  CPU pour un traitement OCR parallèle.
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from PNG
- use all CPU cores
- parallel OCR processing
language: fr
og_description: Comment réaliser une OCR par lots en Java. Apprenez à reconnaître
  le texte à partir d’images, à extraire le texte des PNG et à exploiter tous les
  cœurs du processeur pour un traitement OCR parallèle rapide.
og_title: Comment réaliser une OCR par lots en Java – Guide du traitement parallèle
tags:
- OCR
- Java
- Aspose
- Performance
title: Comment faire de l’OCR par lots en Java avec traitement parallèle
url: /fr/java/advanced-ocr-techniques/how-to-batch-ocr-in-java-with-parallel-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer une OCR par lots en Java – Guide complet

Vous êtes‑vous déjà demandé **comment faire de l'OCR par lots** lorsque vous avez des dizaines de captures d'écran PNG qui vous regardent ? Vous n'êtes pas seul. La plupart des développeurs se heurtent à un mur une fois que la démonstration avec une seule image fonctionne et que la charge réelle – des centaines de fichiers – commence à saturer le CPU.  

Dans ce tutoriel, nous parcourrons une solution pratique, de bout en bout, qui **reconnaît le texte à partir d'images**, extrait le contenu de chaque PNG, et **utilise tous les cœurs du CPU** pour accélérer le traitement. À la fin, vous disposerez d'une classe Java réutilisable qui traite un dossier d'images en parallèle, vous offrant la rapidité d'un moteur multithread sans la complexité de gérer vous‑même les pools de threads.

> **Ce que vous obtiendrez :** un programme Java entièrement exécutable (Aspose OCR), des explications étape par étape, des astuces pour les cas limites, et un aperçu de la sortie console attendue.

---

## Prérequis

Avant de plonger, assurez‑vous d'avoir :

- **Java 17** (ou tout JDK récent) installé et `JAVA_HOME` configuré.  
- **Aspose OCR for Java** library (version 23.10 ou plus récente). Vous pouvez la récupérer depuis Maven Central :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- Un dossier contenant quelques **images PNG** que vous souhaitez traiter.  
- Une connaissance de base de la syntaxe Java – rien de compliqué requis.

Si l'un de ces éléments vous est inconnu, faites une pause ici et configurez‑les ; le reste du guide suppose qu'ils sont prêts.

---

## Étape 1 – Créer un moteur OCR à thread unique (la référence de base)

Première chose à faire : instancier le `OcrEngine`. Cet objet effectue le travail lourd – chargement de l'image, exécution du réseau neuronal, et renvoie le texte brut.

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pourquoi c’est important :** Réutiliser le même moteur pour de nombreux fichiers évite le surcoût de chargement répété des modèles de langue, ce qui peut être un facteur de ralentissement lors du **traitement par lots**.

---

## Étape 2 – Activer le traitement parallèle avec tous les cœurs disponibles

Nous indiquons maintenant à Aspose OCR de répartir le travail sur chaque processeur logique disponible sur votre machine. L'appel `Runtime.getRuntime().availableProcessors()` renvoie ce nombre, que vous ayez un ordinateur portable à 4 cœurs ou un serveur à 32 cœurs.

```java
        // Step 2: Enable parallel processing by using all available logical processors
        ocrEngine.getRecognitionSettings()
                 .setNumberOfThreads(Runtime.getRuntime().availableProcessors());
```

> **Astuce pro :** Sur un CPU hyper‑threadé, vous verrez le double du nombre de cœurs, mais la bibliothèque limite intelligemment le pool de threads, ainsi vous n’avez pas besoin de l’ajuster manuellement.

---

## Étape 3 – Rassembler les images à traiter

Coder en dur un petit tableau fonctionne pour une démonstration, mais dans un traitement par lots réel vous scannerez probablement un répertoire. Ci‑dessous nous montrons les deux approches.

```java
        // Step 3a: Define a static list (quick demo)
        String[] imageFiles = {
            "YOUR_DIRECTORY/image1.png",
            "YOUR_DIRECTORY/image2.png",
            "YOUR_DIRECTORY/image3.png"
        };

        // Step 3b: Or, dynamically load every PNG in a folder
        // File folder = new File("YOUR_DIRECTORY");
        // String[] imageFiles = folder.list((dir, name) -> name.toLowerCase().endsWith(".png"));
```

> **Pourquoi cela peut être utile :** Si vous devez **extraire du texte de fichiers PNG** arrivant via un pipeline d'upload, la version dynamique récupère automatiquement les nouveaux fichiers sans modification du code.

---

## Étape 4 – Exécuter l'OCR sur chaque image en utilisant le même moteur

La boucle ci‑dessous définit l'image courante, exécute `recognize()` et affiche le résultat. Comme nous avons activé le multithreading précédemment, chaque appel peut s'exécuter sur un thread de travail séparé en arrière‑plan.

```java
        // Step 4: Recognize text from each image (reusing the same engine instance)
        for (String imagePath : imageFiles) {
            ocrEngine.setImage(imagePath);
            String recognizedText = ocrEngine.recognize().getText();
            System.out.println("Result for " + imagePath + ":\n" + recognizedText);
        }
    }
}
```

### Sortie console attendue

```
Result for YOUR_DIRECTORY/image1.png:
Welcome to the OCR demo.
Result for YOUR_DIRECTORY/image2.png:
Invoice #12345
Total: $567.89
Result for YOUR_DIRECTORY/image3.png:
© 2026 MyCompany. All rights reserved.
```

Si les images contiennent des scripts non latins ou des captures d'écran basse résolution, vous pourriez voir des caractères illisibles – ajustez les paramètres DPI ou de réduction du bruit du moteur en conséquence (voir la section « Ajustements avancés » ci‑dessous).

---

## Ajustements avancés – Affinage pour les traitements par lots réels

| Situation | Paramètre suggéré | Extrait de code |
|-----------|-------------------|-----------------|
| PNGs basse résolution | Augmenter `setResolution` | `ocrEngine.getRecognitionSettings().setResolution(300);` |
| Documents multilingues | Ajouter des packs de langues | `ocrEngine.getRecognitionSettings().addLanguage(OcrLanguage.Spanish);` |
| Lots de traitements très volumineux (plus de 10 k fichiers) | Diffuser les fichiers au lieu de charger tous les noms d'un coup | Use `Files.walk(Paths.get("YOUR_DIRECTORY"))` with a filter. |
| Contraintes de mémoire | Libérer le moteur après chaque N fichiers | `if (counter % 500 == 0) ocrEngine.dispose();` |

> **Rappel :** Même si nous **utilisons tous les cœurs du CPU**, le système d'exploitation gère toujours la planification des threads. Si vous remarquez que votre machine devient lente, envisagez de limiter les threads à `availableProcessors() - 1`.

---

## Pièges courants & comment les éviter

1. **Épuisement des descripteurs de fichiers** – Java limite le nombre de fichiers ouverts par processus. Fermez chaque image explicitement si vous rencontrez des erreurs `Too many open files` :

   ```java
   ocrEngine.setImage(imagePath);
   String text = ocrEngine.recognize().getText();
   ocrEngine.getImage().close(); // releases the handle
   ```

2. **Séparateurs de chemin incorrects sous Windows** – Utilisez `File.separator` ou `Paths.get()` pour rester indépendant de la plateforme.

3. **Rappels personnalisés non thread‑safe** – Si vous ajoutez un écouteur de progression, assurez‑vous qu’il est thread‑safe (par ex., `AtomicInteger`).

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```java
import com.aspose.ocr.*;
import java.io.File;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable parallelism – use every logical CPU core
        ocrEngine.getRecognitionSettings()
                 .setNumberOfThreads(Runtime.getRuntime().availableProcessors());

        // 3️⃣ Locate PNG files (adjust the folder path)
        File folder = new File("YOUR_DIRECTORY");
        String[] imageFiles = folder.list((dir, name) ->
                name.toLowerCase().endsWith(".png"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG files found in the directory.");
            return;
        }

        // 4️⃣ Process each image – same engine, multi‑threaded under the hood
        for (String imageName : imageFiles) {
            String imagePath = folder.getAbsolutePath() + File.separator + imageName;
            ocrEngine.setImage(imagePath);
            String recognizedText = ocrEngine.recognize().getText();

            System.out.println("Result for " + imagePath + ":\n" + recognizedText);
            // Optional: free the image handle (good for huge batches)
            ocrEngine.getImage().close();
        }

        // Clean up
        ocrEngine.dispose();
    }
}
```

> **Ce que cela fait :** Il parcourt `YOUR_DIRECTORY` à la recherche de chaque `.png`, exécute l'OCR en parallèle, affiche chaque résultat, puis libère les ressources. Vous pouvez intégrer cette classe dans n'importe quel projet Maven, exécuter `mvn exec:java`, et observer le gain de vitesse comparé à une boucle monothread.

---

## Conclusion

Vous disposez maintenant d'un modèle solide, prêt pour la production, pour **effectuer de l'OCR par lots** en Java. En réutilisant un seul `OcrEngine`, en activant le **traitement OCR parallèle**, et en exploitant **tous les cœurs du CPU**, vous pouvez **reconnaître le texte à partir d'images** en une fraction du temps qu'une boucle naïve prendrait.  

À partir d'ici, vous pourriez :

- Brancher la sortie dans un index de recherche (Elasticsearch) pour une recherche rapide.  
- Combiner avec un convertisseur PDF‑vers‑PNG pour **extraire du texte de PNG** intégrés dans des documents numérisés.  
- Ajouter une gestion des erreurs et une logique de réessai pour les lecteurs réseau peu fiables.

Continuez à expérimenter – remplacez par des JPEG, ajustez le DPI, ou même alimentez des images vidéo pour une transcription en temps réel. Les idées principales restent les mêmes, et les gains de performance sont généralement spectaculaires.

Bon codage, et que vos pipelines OCR fonctionnent aussi vite que votre machine à café ! 🚀

![Diagramme montrant le flux de travail OCR parallèle – comment faire de l'OCR par lots sur plusieurs cœurs CPU]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}