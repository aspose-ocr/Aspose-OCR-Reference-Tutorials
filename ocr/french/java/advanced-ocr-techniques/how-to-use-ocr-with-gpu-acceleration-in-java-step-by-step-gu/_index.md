---
category: general
date: 2026-02-09
description: Comment utiliser rapidement l'OCR avec Aspose OCR, reconnaître le texte
  d’une image et extraire le texte d’un PNG tout en définissant le mode et la limite
  de mémoire GPU.
draft: false
keywords:
- how to use ocr
- recognize text from image
- extract text from png
- how to set mode
- set gpu memory limit
language: fr
og_description: Comment utiliser l'OCR efficacement – apprenez à reconnaître le texte
  à partir d’une image, extraire le texte d’un PNG, définir le mode et contrôler la
  limite de mémoire GPU en Java.
og_title: Comment utiliser l'OCR avec l'accélération GPU en Java
tags:
- OCR
- Java
- GPU
- Aspose
title: Comment utiliser l’OCR avec accélération GPU en Java – Guide étape par étape
url: /fr/java/advanced-ocr-techniques/how-to-use-ocr-with-gpu-acceleration-in-java-step-by-step-gu/
---

.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l’OCR avec accélération GPU en Java – Tutoriel complet de programmation

Vous êtes-vous déjà demandé **comment utiliser l’OCR** pour extraire du texte d’une image sans écrire des millions de lignes de code ? Vous n’êtes pas seul. Dans de nombreux projets—numérisation de factures, traitement de reçus, ou simplement digitalisation de vieux documents—les développeurs ont besoin d’une méthode fiable pour **reconnaître le texte à partir d’un fichier image**, notamment les PNG qui contiennent souvent des graphiques nets et haute résolution.  

Bonne nouvelle : Aspose OCR rend cela très simple, et avec quelques ajustements de configuration vous pouvez même déléguer le travail lourd à votre GPU. Dans ce tutoriel, nous parcourrons l’ensemble du processus : du chargement d’un PNG, au **paramétrage du mode** pour le traitement GPU, au **paramétrage de la limite de mémoire GPU**, jusqu’à l’affichage du texte extrait. À la fin, vous disposerez d’un programme Java exécutable qui fait exactement ce dont vous avez besoin.

## Ce que vous allez apprendre

- Comment installer et importer Aspose OCR pour Java.  
- Comment **reconnaître le texte à partir d’un fichier image** avec la bibliothèque.  
- Comment **extraire le texte d’un PNG** de manière efficace.  
- Comment **définir le mode** sur GPU et contrôler l’empreinte mémoire avec **setGpuMemoryLimit**.  
- Les pièges courants et des astuces pour une utilisation en conditions réelles.

### Prérequis

- Java 8 ou supérieur (le code compile également avec JDK 11).  
- Un GPU NVIDIA avec un pilote compatible CUDA si vous souhaitez l’accélération GPU.  
- Le JAR Aspose OCR pour Java (téléchargez‑le depuis le site Aspose ou ajoutez‑le via Maven/Gradle).  
- Une image PNG d’exemple (par ex., `sample1.png`) placée dans un dossier accessible.

---

## Comment utiliser l’OCR – Activer le mode GPU

La première chose à faire est d’indiquer à Aspose OCR que vous voulez qu’il s’exécute sur le GPU plutôt que sur le CPU. C’est ici que le mot‑clé **how to set mode** entre en jeu.

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Step 2: Grab the configuration object
OcrEngineConfiguration config = ocrEngine.getConfiguration();

// Step 3: Switch processing mode to GPU
config.setProcessingMode(ProcessingMode.GPU);   // requires a CUDA‑compatible driver

// (Optional) Step 4: Limit GPU memory usage to 1024 MB
config.setGpuMemoryLimit(1024);                 // set gpu memory limit (MB)
```

**Pourquoi c’est important :**  
Le traitement GPU peut être nettement plus rapide pour de gros lots ou des images haute résolution, mais il consomme de la mémoire vidéo. En appelant `setGpuMemoryLimit`, vous évitez que votre application monopolise tout le GPU, ce qui est crucial lorsque le même appareil exécute d’autres charges de travail (par ex., une interface utilisateur ou un modèle d’apprentissage automatique).

---

## Reconnaître le texte à partir d’une image avec Aspose OCR

Une fois le moteur configuré, il faut le pointer vers le fichier à lire. C’est le cœur de **recognize text from image**.

```java
// Step 5: Define the image to be processed
ImageRecognitionResult imageInfo = new ImageRecognitionResult();
imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

// Step 6: Run the OCR operation
RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);
```

**Que se passe‑t‑il en coulisses ?**  
Aspose OCR charge le PNG, le pré‑traite (binarisation, redressement, etc.), puis exécute le réseau neuronal OCR sur le GPU. L’objet résultat contient le texte brut ainsi que les scores de confiance pour chaque ligne.

---

## Extraire le texte d’un PNG avec une limite de mémoire GPU

Après la reconnaissance, extraire la chaîne de caractères est trivial, mais de nombreux développeurs oublient de vérifier la sortie. Voici comment **extract text from PNG** en toute sécurité et l’afficher.

```java
// Step 7: Output the recognized text
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Sortie attendue (exemple) :**

```
Recognized text:
Invoice #12345
Date: 2026-02-09
Total: $1,250.00
Thank you for your business!
```

Si l’image contient du bruit ou des polices inhabituelles, vous pourriez obtenir des caractères illisibles. Dans ce cas, envisagez d’ajuster les options de pré‑traitement (par ex., `config.setLanguage(Language.ENGLISH)` ou `config.setAutoSkewCorrection(true)`).

---

## Exemple complet, exécutable

Voici le programme Java complet qui réunit tous les éléments. Copiez‑collez‑le dans un fichier nommé `GpuExample.java`, ajustez le chemin de l’image, puis exécutez‑le avec `javac`/`java` ou depuis votre IDE.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.configuration.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the image to be processed
        ImageRecognitionResult imageInfo = new ImageRecognitionResult();
        imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

        // Step 2: Create the OCR engine and enable GPU processing
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration config = ocrEngine.getConfiguration();

        // Step 3: Set processing mode to GPU (requires CUDA driver)
        config.setProcessingMode(ProcessingMode.GPU);

        // Step 4 (optional): Limit GPU memory usage to 1024 MB
        config.setGpuMemoryLimit(1024);

        // Step 5: Perform recognition
        RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);

        // Step 6: Print the extracted text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Exécution du programme**

```bash
javac -cp "path/to/aspose-ocr.jar" GpuExample.java
java -cp ".:path/to/aspose-ocr.jar" GpuExample
```

Assurez‑vous que le JAR se trouve dans votre classpath ; sinon vous obtiendrez `ClassNotFoundException`.

---

## Astuces pro & pièges courants

- **Version du pilote GPU :** Le drapeau `ProcessingMode.GPU` lèvera une exception si le pilote CUDA est absent ou incompatible. Vérifiez avec `nvidia-smi`.  
- **Gestion de la mémoire :** Si vous traitez de nombreuses images en parallèle, augmentez la valeur de `setGpuMemoryLimit` ou exécutez les tâches séquentiellement pour éviter les erreurs d’out‑of‑memory.  
- **Format d’image :** Bien que le PNG fonctionne très bien, les JPEG fortement compressés peuvent entraîner des erreurs de reconnaissance. Convertissez-les en PNG sans perte avant l’OCR.  
- **Support linguistique :** Par défaut, Aspose OCR suppose l’anglais. Pour d’autres langues, appelez `config.setLanguage(Language.SPANISH)` (ou l’énumération appropriée) avant `recognize`.  
- **Tests de performance :** Réalisez un petit benchmark (`System.nanoTime()`) avec et sans GPU pour vérifier que le gain de vitesse justifie la complexité supplémentaire.

---

## Questions fréquentes

**Cela fonctionne‑t‑il sous macOS ou Linux ?**  
Oui—Aspose OCR est multiplateforme. Assurez‑vous simplement d’avoir un GPU compatible CUDA et le pilote adéquat installé pour votre OS.

**Et si je n’ai pas de GPU ?**  
Vous pouvez simplement omettre la ligne `setProcessingMode(ProcessingMode.GPU)` ; le moteur repassera automatiquement en mode CPU.

**Puis‑je traiter directement des PDF ?**  
Aspose OCR se concentre sur les images raster. Pour les PDF, extrayez chaque page sous forme d’image d’abord (par ex., avec Aspose PDF) puis alimentez les PNG dans le flux OCR.

---

## Conclusion

En résumé, **comment utiliser l’OCR** avec Aspose en Java se résume à trois étapes claires : configurer le moteur (y compris **how to set mode** et **set GPU memory limit**), le pointer vers votre PNG, et lire la chaîne résultante. Le fragment ci‑dessus constitue une solution fonctionnelle de bout en bout que vous pouvez intégrer à n’importe quel projet Java.

Maintenant que vous maîtrisez **recognize text from image** et **extract text from PNG**, vous pouvez étendre le flux de travail : traitement par lots de dossiers, stockage des résultats dans une base de données, ou même alimentation du texte dans des pipelines NLP en aval. Le ciel est la limite—veillez simplement à surveiller la mémoire GPU et la compatibilité des pilotes.

Vous avez d’autres questions sur l’OCR, l’accélération GPU ou les fonctionnalités d’Aspose ? N’hésitez pas à laisser un commentaire ou à explorer la documentation officielle d’Aspose OCR pour des options de personnalisation avancées. Bon codage ! 🚀

![diagramme comment utiliser l ocr](https://example.com/images/ocr-gpu-diagram.png "diagramme comment utiliser l ocr")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}