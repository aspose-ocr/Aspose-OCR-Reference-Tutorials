---
category: general
date: 2026-03-28
description: Prétraitez l'image pour l'OCR et reconnaissez le texte à partir de l'image
  avec Aspose OCR. Apprenez à extraire le texte d'une photo et à améliorer la précision
  de l'OCR grâce à un prétraitement étape par étape.
draft: false
keywords:
- preprocess image for OCR
- recognize text from image
- extract text from photo
- improve OCR accuracy preprocessing
- Aspose OCR Java
- image preprocessing pipeline
language: fr
og_description: Prétraitez l'image pour l'OCR et extrayez le texte d'une photo avec
  Aspose OCR Java. Suivez ce tutoriel pour améliorer la précision de l'OCR grâce au
  prétraitement en quelques étapes seulement.
og_title: Prétraiter l'image pour l'OCR – Guide complet Java
tags:
- OCR
- Java
- Image Processing
title: Prétraiter l'image pour l'OCR – Améliorer la précision de l'extraction de texte
  en Java
url: /fr/java/advanced-ocr-techniques/preprocess-image-for-ocr-boost-text-extraction-accuracy-in-j/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Prétraiter l'image pour l'OCR – Un guide complet Java

Vous avez déjà essayé de **prétraiter l'image pour l'OCR** et vous êtes toujours retrouvé avec une sortie illisible ? Vous n'êtes pas seul. Dans de nombreux projets réels, un scan brut ou une photo prise avec un smartphone contient des inclinaisons, du bruit ou un faible contraste qui perturbent même le moteur de reconnaissance le plus performant. La bonne nouvelle ? Un court pipeline de prétraitement—dé‑inclinaison, débruitage, binarisation—peut améliorer considérablement **la précision de l'OCR grâce au prétraitement**.

Dans ce tutoriel, nous parcourrons un exemple pratique qui vous montre exactement comment **reconnaître du texte à partir d'une image** en utilisant Aspose OCR pour Java. À la fin, vous pourrez **extraire du texte à partir de fichiers photo** avec beaucoup moins d’erreurs, et vous comprendrez pourquoi chaque étape de prétraitement est importante.

> **Ce que vous en retirerez**  
> * Un programme Java entièrement exécutable qui charge une photo inclinée, applique trois filtres classiques et affiche du texte propre.  
> * Une compréhension du « pourquoi » derrière la dé‑inclinaison, le débruitage et la binarisation.  
> * Des astuces pour gérer les cas limites—fichiers volumineux, différents formats d'image et ordre personnalisé des filtres.

## Prérequis

- Java 8 ou version plus récente installé (le code compile également avec JDK 11).  
- Maven ou Gradle pour récupérer la bibliothèque Aspose OCR.  
- Une image d'exemple (par ex. `angled-photo.jpg`) légèrement inclinée et contenant du bruit visuel.  
- Une connaissance de base de la méthode `main` de Java—aucune expertise approfondie en OCR requise.

Si l'un de ces éléments vous manque, téléchargez simplement le dernier JDK depuis Oracle ou OpenJDK et ajoutez la dépendance Maven suivante à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check Maven Central for the newest version -->
</dependency>
```

Passons maintenant au code.

## Étape 1 – Créer l'instance du moteur OCR

La première chose dont vous avez besoin est un objet `OcrEngine`. Considérez-le comme le cerveau qui lira plus tard l'image traitée.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pourquoi c'est important :** Le moteur encapsule les paramètres de reconnaissance, les packs de langues et—le plus important pour nous—les options de prétraitement. Sans lui, vous devriez enchaîner manuellement des bibliothèques de traitement d'image, ce qui va à l'encontre de l'objectif d'un pipeline propre.

## Étape 2 – Construire un pipeline de prétraitement (dé‑inclinaison → débruitage → binarisation)

Aspose OCR fournit une classe intégrée `PreprocessingOptions` qui vous permet d'empiler les filtres dans l'ordre exact dont vous avez besoin. Ici, nous ajoutons trois filtres :

1. **DE_SKEW** – redresse le texte incliné.  
2. **DENOISE** – lisse les pixels granuleux qui pourraient être confondus avec des caractères.  
3. **BINARIZE** – convertit l'image en noir et blanc pur, facilitant le travail du moteur OCR.

```java
        // Step 2: Assemble the preprocessing pipeline
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);   // correct rotation
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);  // remove grain
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE); // high‑contrast B&W

        // Attach the pipeline to the OCR engine
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);
```

> **Astuce :** L'ordre des filtres est crucial. Si vous binarisez *avant* le débruitage, le bruit peut devenir des taches noires aux bords durs qui perturbent le reconnaisseur. La dé‑inclinaison en premier assure que la ligne de base du texte est horizontale, ce qui améliore les résultats du débruitage et de la binarisation.

## Étape 3 – Fournir l'image au moteur

Nous indiquons maintenant au moteur le fichier que nous voulons lire. Le chemin peut être absolu ou relatif à la racine de votre projet.

```java
        // Step 3: Run OCR on the target image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

> **Et si l'image est très grande ?** Aspose OCR réduit automatiquement les images dont le côté le plus long dépasse 2000 px, mais vous pouvez remplacer ce comportement via `ocrEngine.getRecognitionSettings().setMaxImageDimension(1500)` si la mémoire est un problème.

## Étape 4 – Afficher le texte reconnu

Enfin, nous affichons la chaîne extraite dans la console. Dans une application réelle, vous pourriez l'écrire dans une base de données, un fichier, ou la transmettre à un pipeline NLP en aval.

```java
        // Step 4: Print the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Sortie attendue

Si `angled-photo.jpg` contient la phrase *« The quick brown fox jumps over the lazy dog. »* vous devriez voir quelque chose comme :

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

Remarquez que la sortie est propre—pas de symboles errants, pas de lignes cassées. C’est la puissance du **prétraitement d'image pour l'OCR**.

## Étape 5 – Vérifier et ajuster (facultatif)

Même avec un pipeline solide, vous pourriez rencontrer des cas limites :

| Situation | Ajustement suggéré |
|-----------|--------------------|
| **Très faible contraste** (p. ex. documents numérisés fanés) | Insérer un filtre supplémentaire `ContrastAdjustment` avant la binarisation. |
| **Arrière‑plan coloré** (p. ex. reçus avec tampons colorés) | Ajouter le filtre `BackgroundRemoval` ou convertir manuellement en niveaux de gris d'abord. |
| **PDF multi‑pages** | Boucler sur chaque image de page et réutiliser le même `preprocessingOptions`. |

Vous pouvez expérimenter en appelant `preprocessingOptions.addFilter(PreprocessFilter.CONTRAST)` ou tout autre filtre répertorié dans la documentation de l'API Aspose OCR.

## Exemple complet et exécutable

Voici le programme complet, prêt à être copié‑collé dans un fichier nommé `PreprocessExample.java`. Assurez‑vous que la dépendance Maven est résolue avant de compiler.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing: de‑skew → denoise → binarize
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE);
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);

        // 3️⃣ Perform OCR on the chosen image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // 4️⃣ Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Compilez et exécutez :

```bash
mvn compile exec:java -Dexec.mainClass=PreprocessExample
```

Vous devriez voir le texte propre affiché dans la console, confirmant que vous avez réussi le **prétraitement d'image pour l'OCR** et la **reconnaissance de texte à partir d'une image**.

## Questions fréquentes & réponses

**Q1 : Cela fonctionne‑t‑il avec les fichiers PNG ou TIFF ?**  
Oui—Aspose OCR prend en charge JPEG, PNG, BMP, TIFF et plusieurs autres formats. Le même pipeline de prétraitement s'applique ; la bibliothèque détecte automatiquement le format.

**Q2 : Et si je dois extraire du texte d'une photo prise avec un téléphone ?**  
Les photos de téléphone souffrent souvent d'éclairage inégal. Ajouter un filtre `LIGHTING_CORRECTION` avant la binarisation peut aider. Le changement de code se résume à une seule ligne :

```java
preprocessingOptions.addFilter(PreprocessFilter.LIGHTING_CORRECTION);
```

**Q3 : Puis‑je changer la langue de l'OCR ?**  
Absolument. Après avoir créé le moteur, définissez la langue :

```java
ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.SPANISH);
```

**Q4 : Comment cela améliore‑t‑il le prétraitement de la précision de l'OCR ?**  
Chaque filtre réduit un type spécifique de bruit visuel. La dé‑inclinaison aligne les lignes de texte, le débruitage élimine les taches aléatoires, et la binarisation crée une image à fort contraste. Ensemble, ils fournissent à l'algorithme de reconnaissance un signal plus propre, ce qui se traduit par une précision au niveau des caractères plus élevée—souvent une amélioration de 15‑30 % sur des entrées bruyantes.

## Prochaines étapes & sujets associés

- **Traitement par lots :** Encapsulez la logique principale dans une boucle pour gérer des dossiers entiers de photos.  
- **Ordre de filtres personnalisé :** Expérimentez avec `BINARIZE` avant `DENOISE` pour des documents déjà à fort contraste.  
- **Optimisation des performances :** Utilisez `ocrEngine.getRecognitionSettings().setThreadCount(4)` pour paralléliser sur des machines multi‑cœurs.  
- **Bibliothèques alternatives :** Comparez Aspose OCR avec Tesseract‑Java pour les scénarios open‑source.  
- **Post‑traitement :** Appliquez une correction orthographique ou un nettoyage regex à la sortie brute pour des résultats encore plus propres.

En maîtrisant le flux de travail de **prétraitement d'image pour l'OCR**, vous constaterez que l'extraction de texte à partir de sources photo devient une tâche prévisible et répétable plutôt qu'une expérience aléatoire.

---

*Prêt à améliorer votre pipeline OCR ? Prenez le code, ajustez les filtres, et observez la précision grimper. Si vous rencontrez un problème, laissez un commentaire ci‑dessous—bon codage !*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}